<div align="center">

# 📚 SSRF — Resources, Writeups & Research

**A curated collection of everything you need to master Server-Side Request Forgery**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
![Last Updated](https://img.shields.io/badge/Last%20Updated-2025-brightgreen)
![Category](https://img.shields.io/badge/Category-Web%20Security-red)
![Type](https://img.shields.io/badge/Type-Bug%20Bounty%20%7C%20Pentesting-orange)
![Contributions](https://img.shields.io/badge/Contributions-Welcome-blue)

> 🎯 From beginner fundamentals to advanced exploitation — all in one place.

</div>

---

## 📋 Table of Contents

| # | Section |
|---|---------|
| 1 | [📖 Core Learning Resources](#-core-learning-resources) |
| 2 | [🔗 HackTricks References](#-hacktricks-references) |
| 3 | [📝 Real-World Writeups](#-real-world-writeups) |
| 4 | [👨‍💻 Researcher Blogs to Follow](#-researcher-blogs-to-follow) |
| 5 | [🎥 Video Resources](#-video-resources) |
| 6 | [🏋️ Practice Platforms](#️-practice-platforms) |
| 7 | [🔍 Google Dorks](#-google-dorks) |
| 8 | [⭐ GitHub Repositories](#-github-repositories) |
| 9 | [💬 Community & Forums](#-community--forums) |

---

## 📖 Core Learning Resources

> Start here. These are the most comprehensive and trusted references for SSRF.

| # | Resource | Description |
|---|----------|-------------|
| 1 | [HackViser — SSRF Pentesting](https://hackviser.com/tactics/pentesting/web/ssrf) | Practical pentesting tactics and techniques |
| 2 | [Snyk Learn — SSRF (JavaScript)](https://learn.snyk.io/lesson/ssrf-server-side-request-forgery/?ecosystem=javascript) | Developer-focused, interactive SSRF lesson |
| 3 | [PortSwigger Web Security Academy](https://portswigger.net/web-security/ssrf) | ⭐ Best free labs — must do |
| 4 | [TCM Security — Understanding SSRF](https://tcm-sec.com/understanding-detecting-and-exploiting-ssrf/) | Detection and exploitation walkthrough |
| 5 | [Intigriti — Advanced SSRF Guide](https://www.intigriti.com/researchers/blog/hacking-tools/ssrf-a-complete-guide-to-exploiting-advanced-ssrf-vulnerabilities) | Advanced techniques from a top bug bounty platform |
| 6 | [OWASP Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html) | Authoritative defense reference |
| 7 | [Imperva — SSRF Overview](https://www.imperva.com/learn/application-security/server-side-request-forgery-ssrf/) | Clear conceptual breakdown |
| 8 | [The Hacker Recipes — SSRF](https://www.thehacker.recipes/web/inputs/ssrf/) | Attacker's cookbook style |
| 9 | [OWASP — SSRF Attack](https://owasp.org/www-community/attacks/Server_Side_Request_Forgery) | Community standard reference |
| 10 | [Invicti — SSRF Deep Dive](https://www.invicti.com/learn/server-side-request-forgery-ssrf) | Technical depth + scanner perspective |
| 11 | [OWASP Top 10 2021 — A10 SSRF](https://owasp.org/Top10/2021/A10_2021-Server-Side_Request_Forgery_(SSRF)/index.html) | Why SSRF made the Top 10 |
| 12 | [SSRF Bible (PDF)](https://cheatsheetseries.owasp.org/assets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet_SSRF_Bible.pdf) | 📄 Comprehensive offline reference |
| 13 | [PayloadsAllTheThings — SSRF](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Request%20Forgery) | The payload bible |
| 14 | [Blind SSRF Chains — Assetnote](https://blog.assetnote.io/2021/01/13/blind-ssrf-chains/) | Advanced blind SSRF exploitation |
| 15 | [EC2 Metadata SSRF — HackingTheCloud](https://hackingthe.cloud/aws/exploitation/ec2-metadata-ssrf/) | AWS-specific exploitation |
| 16 | [hacking.the.cloud](https://hackingthe.cloud) | Full cloud attack reference |

---

## 🔗 HackTricks References

> HackTricks covers SSRF across multiple attack surfaces — cloud, web, and protocol-level.

| Resource | Context |
|----------|---------|
| [DigitalOcean Pentesting — SSRF](https://cloud.hacktricks.wiki/en/pentesting-cloud/digital-ocean-pentesting/index.html#ssrf) | Cloud-specific SSRF angle |
| [MSSQL Injection — SSRF](https://hacktricks.wiki/en/pentesting-web/sql-injection/mssql-injection.html#ssrf) | SSRF via SQL injection |
| [AWS Security — SSRF](https://cloud.hacktricks.wiki/en/pentesting-cloud/aws-security/index.html#ssrf) | AWS metadata exploitation |
| [Server-Side XSS / Dynamic PDF — SSRF](https://hacktricks.wiki/en/pentesting-web/xss-cross-site-scripting/server-side-xss-dynamic-pdf.html#ssrf) | PDF generator attack surface |
| [XXE — Blind SSRF](https://hacktricks.wiki/en/pentesting-web/xxe-xee-xml-external-entity.html#blind-ssrf) | SSRF via XXE |

---

## 📝 Real-World Writeups

> Reading writeups is the fastest way to develop an attacker's mindset. Aim for 2–3 per day.

### 🏆 Must-Read Writeups

| # | Writeup | Why It's Great |
|---|---------|---------------|
| 1 | [HackerOne Report #223203](https://hackerone.com/reports/223203) | Classic real-world SSRF disclosure |
| 2 | [Fixing the Unfixable — Google Cloud SSRF](https://bugs.xdavidhu.me/google/2021/12/31/fixing-the-unfixable-story-of-a-google-cloud-ssrf/) | Deep dive into a Google Cloud SSRF chain |
| 3 | [Orange Tsai — Chaining 4 Vulns](https://blog.orange.tw/posts/2017-07-how-i-chained-4-vulnerabilities-on/) | ⭐ Legendary vuln chaining writeup |
| 4 | [Capital One Breach — SSRF + AWS Keys](https://blog.appsecco.com/an-ssrf-privileged-aws-keys-and-the-capital-one-breach-4c3c2cded3af) | Real breach — SSRF → IAM creds → mass data leak |
| 5 | [ShoreBreak — Real-World SSRFs](https://www.shorebreaksecurity.com/blog/ssrfs-up-real-world-server-side-request-forgery-ssrf/) | Multiple real case studies |

---

### 🔎 Writeup Aggregators & Search

| Platform | Link | Notes |
|----------|------|-------|
| HackerOne Hacktivity | [SSRF Disclosed Reports](https://hackerone.com/hacktivity/overview?queryString=ssrf+AND+disclosed%3Atrue&sortField=latest_disclosable_activity_at&sortDirection=DESC&pageIndex=0) | Live feed of real disclosures |
| HackerOne All Disclosed | [All Disclosed](https://hackerone.com/hacktivity/overview?queryString=disclosed%3Atrue&sortField=latest_disclosable_activity_at&sortDirection=DESC&pageIndex=0) | Broader scope |
| Bugcrowd Crowdstream | [crowdstream](https://bugcrowd.com/crowdstream) | Bugcrowd's equivalent |
| Medium Bug Bounty | [Search SSRF](https://medium.com/search?q=ssrf+writeup) | Community writeups |
| Medium BugBountyWriteup | [SSRF tag](https://medium.com/bugbountywriteup/search?q=SSRF) | Curated bounty pub |
| Pentester Land | [Writeup Library](https://pentester.land/writeups/) | Massive curated list |
| BugBountyHunting | [SSRF Search](https://www.bugbountyhunting.com/?q=ssrf) | Searchable DB |
| Dev.to | [SSRF Posts](https://dev.to/search?q=ssrf) | Developer community writeups |
| Substack | [SSRF Articles](https://substack.com/search/ssrf) | Newsletter-style deep dives |
| Hashnode | [SSRF Writeups](https://hashnode.com/search?q=ssrf+writeup) | Developer blogging platform |
| Detectify Labs | [SSRF](https://labs.detectify.com/search/SSRF/) | Research-grade posts |
| Bug Bounty Reference | [SSRF Section](https://github.com/ngalongc/bug-bounty-reference?tab=readme-ov-file#server-side-request-forgery-ssrf) | GitHub-curated reports |
| Marco Tulio Disclosed Reports | [GitHub Repo](https://github.com/marcotuliocnd/bugbounty-disclosed-reports/tree/main/reports) | Raw disclosed report collection |

---

## 👨‍💻 Researcher Blogs to Follow

> These are the people whose work you should study deeply.

| Researcher | Blog | Known For |
|------------|------|-----------|
| **James Kettle** | [jameskettle.com](https://jameskettle.com/) | HTTP request smuggling, SSRF research, PortSwigger |
| **0xPatrik** | [0xpatrik.com](https://0xpatrik.com/) | Subdomain takeover, recon methodology |
| **0xdf** | [0xdf.gitlab.io](https://0xdf.gitlab.io/) | HackTheBox walkthroughs, deep technical analysis |
| **STÖK** | [YouTube](https://www.youtube.com/@STOKfredrik/search?query=SSRF) | Bug bounty mindset & SSRF content |
| **IppSec** | [ippsec.rocks](https://ippsec.rocks/?) | HTB writeup search engine |
| **Intigriti Blog** | [Bug Bytes](https://www.intigriti.com/researchers/blog/bug-bytes) | Weekly security roundup |
| **Red Team Notes** | [ired.team](https://www.ired.team/) | Offensive techniques reference |

---

## 🎥 Video Resources

| Platform | Link | What to Watch |
|----------|------|---------------|
| YouTube — DEF CON | [SSRF Talks](https://www.youtube.com/results?search_query=defcon+ssrf) | Conference-level research |
| YouTube — Bypass Talks | [SSRF Bypass Protections](https://www.youtube.com/results?search_query=ssrf+bypass+protections+talk) | Filter bypass techniques |
| STÖK on YouTube | [SSRF Videos](https://www.youtube.com/@STOKfredrik/search?query=SSRF) | Bug bounty focused |
| Black Hat 2017 (PDF) | [New Era of SSRF — Orange Tsai](https://blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf) | 📄 Must-read/watch presentation |

---

## 🏋️ Practice Platforms

> Build skills by doing, not just reading.

| Platform | Link | Level |
|----------|------|-------|
| PortSwigger Web Academy | [SSRF Labs](https://portswigger.net/web-security/ssrf) | Beginner → Advanced |
| PWN.college | [pwn.college](https://pwn.college/) | Structured, CTF-style |
| HackTheBox | [hackthebox.com](https://www.hackthebox.com) | Intermediate → Advanced |
| TryHackMe | [tryhackme.com](https://tryhackme.com) | Beginner → Intermediate |

---

## 🔍 Google Dorks

> Use these to find fresh writeups, CTF solutions, and real reports.

### General SSRF Writeups

```
site:medium.com "SSRF" "writeup"
site:hackerone.com/reports ssrf
"ssrf" "writeup" "bug bounty" site:medium.com
"server side request forgery" writeup site:medium.com
"ssrf" "$" "bounty" writeup
site:ghost.io "ssrf writeup"
```

### Blind SSRF

```
"blind SSRF" writeup 2023 OR 2024
"blind ssrf" "out of band" writeup
```

### High-Impact SSRF Chains

```
"SSRF to RCE" writeup
"ssrf" "internal network" writeup
"ssrf" "aws metadata" writeup
"ssrf" "169.254.169.254" writeup
"ssrf" "chained" writeup
```

### Platform-Specific

```
"ssrf" writeup site:hackerone.com/reports
"ssrf" writeup site:bugcrowd.com
"ssrf" writeup site:gitlab.com
"SSRF" "$bounty" site:twitter.com
```

### CTF

```
"ssrf" "ctf" writeup site:github.com
"ssrf" "ctf" writeup site:medium.com
```

### GitHub

```
awesome ssrf writeups
ssrf bug bounty report
ssrf payload list github
```

---

## ⭐ GitHub Repositories

| Repository | Description |
|------------|-------------|
| [paulveillard/cybersecurity-ssrf](https://github.com/paulveillard/cybersecurity-ssrf) | Curated SSRF security resources |
| [swisskyrepo/PayloadsAllTheThings — SSRF](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Request%20Forgery) | The definitive payload list |
| [fardeen-ahmed/Bug-bounty-Writeups](https://github.com/fardeen-ahmed/Bug-bounty-Writeups) | Disclosed bug bounty writeups collection |
| [KingOfBugBountyTips — SSRF](https://github.com/KingOfBugbounty/KingOfBugBountyTips/blob/master/SSRF) | Quick tips and payloads |
| [ngalongc/bug-bounty-reference — SSRF](https://github.com/ngalongc/bug-bounty-reference?tab=readme-ov-file#server-side-request-forgery-ssrf) | Categorized bounty report references |
| [djadmin/awesome-bug-bounty](https://github.com/djadmin/awesome-bug-bounty?tab=readme-ov-file) | Broad bug bounty resource list |
| [0xmaximus/Galaxy-Bugbounty-Checklist](https://github.com/0xmaximus/Galaxy-Bugbounty-Checklist) | Full bug bounty checklist |
| [devanshbatham/Awesome-Bugbounty-Writeups](https://github.com/devanshbatham/Awesome-Bugbounty-Writeups) | Categorized writeup collection |
| [marcotuliocnd/bugbounty-disclosed-reports](https://github.com/marcotuliocnd/bugbounty-disclosed-reports/tree/main/reports) | Raw disclosed reports |

---

## 💬 Community & Forums

| Platform | Link | What's There |
|----------|------|-------------|
| Reddit r/netsec | [reddit.com/r/netsec](https://www.reddit.com/r/netsec/) | News, writeups, discussions |
| Security StackExchange | [SSRF Questions](https://security.stackexchange.com/search?q=ssrf) | Q&A with expert answers ⭐ |
| Intigriti Blog | [Bug Bytes Newsletter](https://www.intigriti.com/researchers/blog/bug-bytes) | Weekly curated security news |

---

## 🗺️ Suggested Learning Path

```
Week 1 — Fundamentals
├── PortSwigger Academy (all SSRF labs)
├── Read OWASP SSRF page
└── Read 5 basic writeups from HackerOne Hacktivity

Week 2 — Intermediate
├── Intigriti Advanced SSRF Guide
├── PayloadsAllTheThings SSRF section
├── Practice blind SSRF with Burp Collaborator
└── Read Orange Tsai's chaining writeup

Week 3 — Advanced
├── Blind SSRF Chains (Assetnote)
├── Black Hat 2017 — Orange Tsai PDF<div align="center">

# 📚 SSRF — Resources, Writeups & Research

**A curated collection of everything you need to master Server-Side Request Forgery**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
![Last Updated](https://img.shields.io/badge/Last%20Updated-2025-brightgreen)
![Category](https://img.shields.io/badge/Category-Web%20Security-red)
![Type](https://img.shields.io/badge/Type-Bug%20Bounty%20%7C%20Pentesting-orange)
![Contributions](https://img.shields.io/badge/Contributions-Welcome-blue)

> 🎯 From beginner fundamentals to advanced exploitation — all in one place.

</div>

---

## 📋 Table of Contents

| # | Section |
|---|---------|
| 1 | [📖 Core Learning Resources](#-core-learning-resources) |
| 2 | [🔗 HackTricks References](#-hacktricks-references) |
| 3 | [📝 Real-World Writeups](#-real-world-writeups) |
| 4 | [👨‍💻 Researcher Blogs to Follow](#-researcher-blogs-to-follow) |
| 5 | [🎥 Video Resources](#-video-resources) |
| 6 | [🏋️ Practice Platforms](#️-practice-platforms) |
| 7 | [🔍 Google Dorks](#-google-dorks) |
| 8 | [⭐ GitHub Repositories](#-github-repositories) |
| 9 | [💬 Community & Forums](#-community--forums) |

---

## 📖 Core Learning Resources

> Start here. These are the most comprehensive and trusted references for SSRF.

| # | Resource | Description |
|---|----------|-------------|
| 1 | [HackViser — SSRF Pentesting](https://hackviser.com/tactics/pentesting/web/ssrf) | Practical pentesting tactics and techniques |
| 2 | [Snyk Learn — SSRF (JavaScript)](https://learn.snyk.io/lesson/ssrf-server-side-request-forgery/?ecosystem=javascript) | Developer-focused, interactive SSRF lesson |
| 3 | [PortSwigger Web Security Academy](https://portswigger.net/web-security/ssrf) | ⭐ Best free labs — must do |
| 4 | [TCM Security — Understanding SSRF](https://tcm-sec.com/understanding-detecting-and-exploiting-ssrf/) | Detection and exploitation walkthrough |
| 5 | [Intigriti — Advanced SSRF Guide](https://www.intigriti.com/researchers/blog/hacking-tools/ssrf-a-complete-guide-to-exploiting-advanced-ssrf-vulnerabilities) | Advanced techniques from a top bug bounty platform |
| 6 | [OWASP Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html) | Authoritative defense reference |
| 7 | [Imperva — SSRF Overview](https://www.imperva.com/learn/application-security/server-side-request-forgery-ssrf/) | Clear conceptual breakdown |
| 8 | [The Hacker Recipes — SSRF](https://www.thehacker.recipes/web/inputs/ssrf/) | Attacker's cookbook style |
| 9 | [OWASP — SSRF Attack](https://owasp.org/www-community/attacks/Server_Side_Request_Forgery) | Community standard reference |
| 10 | [Invicti — SSRF Deep Dive](https://www.invicti.com/learn/server-side-request-forgery-ssrf) | Technical depth + scanner perspective |
| 11 | [OWASP Top 10 2021 — A10 SSRF](https://owasp.org/Top10/2021/A10_2021-Server-Side_Request_Forgery_(SSRF)/index.html) | Why SSRF made the Top 10 |
| 12 | [SSRF Bible (PDF)](https://cheatsheetseries.owasp.org/assets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet_SSRF_Bible.pdf) | 📄 Comprehensive offline reference |
| 13 | [PayloadsAllTheThings — SSRF](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Request%20Forgery) | The payload bible |
| 14 | [Blind SSRF Chains — Assetnote](https://blog.assetnote.io/2021/01/13/blind-ssrf-chains/) | Advanced blind SSRF exploitation |
| 15 | [EC2 Metadata SSRF — HackingTheCloud](https://hackingthe.cloud/aws/exploitation/ec2-metadata-ssrf/) | AWS-specific exploitation |
| 16 | [hacking.the.cloud](https://hackingthe.cloud) | Full cloud attack reference |

---

## 🔗 HackTricks References

> HackTricks covers SSRF across multiple attack surfaces — cloud, web, and protocol-level.

| Resource | Context |
|----------|---------|
| [DigitalOcean Pentesting — SSRF](https://cloud.hacktricks.wiki/en/pentesting-cloud/digital-ocean-pentesting/index.html#ssrf) | Cloud-specific SSRF angle |
| [MSSQL Injection — SSRF](https://hacktricks.wiki/en/pentesting-web/sql-injection/mssql-injection.html#ssrf) | SSRF via SQL injection |
| [AWS Security — SSRF](https://cloud.hacktricks.wiki/en/pentesting-cloud/aws-security/index.html#ssrf) | AWS metadata exploitation |
| [Server-Side XSS / Dynamic PDF — SSRF](https://hacktricks.wiki/en/pentesting-web/xss-cross-site-scripting/server-side-xss-dynamic-pdf.html#ssrf) | PDF generator attack surface |
| [XXE — Blind SSRF](https://hacktricks.wiki/en/pentesting-web/xxe-xee-xml-external-entity.html#blind-ssrf) | SSRF via XXE |

---

## 📝 Real-World Writeups

> Reading writeups is the fastest way to develop an attacker's mindset. Aim for 2–3 per day.

### 🏆 Must-Read Writeups

| # | Writeup | Why It's Great |
|---|---------|---------------|
| 1 | [HackerOne Report #223203](https://hackerone.com/reports/223203) | Classic real-world SSRF disclosure |
| 2 | [Fixing the Unfixable — Google Cloud SSRF](https://bugs.xdavidhu.me/google/2021/12/31/fixing-the-unfixable-story-of-a-google-cloud-ssrf/) | Deep dive into a Google Cloud SSRF chain |
| 3 | [Orange Tsai — Chaining 4 Vulns](https://blog.orange.tw/posts/2017-07-how-i-chained-4-vulnerabilities-on/) | ⭐ Legendary vuln chaining writeup |
| 4 | [Capital One Breach — SSRF + AWS Keys](https://blog.appsecco.com/an-ssrf-privileged-aws-keys-and-the-capital-one-breach-4c3c2cded3af) | Real breach — SSRF → IAM creds → mass data leak |
| 5 | [ShoreBreak — Real-World SSRFs](https://www.shorebreaksecurity.com/blog/ssrfs-up-real-world-server-side-request-forgery-ssrf/) | Multiple real case studies |

---

### 🔎 Writeup Aggregators & Search

| Platform | Link | Notes |
|----------|------|-------|
| HackerOne Hacktivity | [SSRF Disclosed Reports](https://hackerone.com/hacktivity/overview?queryString=ssrf+AND+disclosed%3Atrue&sortField=latest_disclosable_activity_at&sortDirection=DESC&pageIndex=0) | Live feed of real disclosures |
| HackerOne All Disclosed | [All Disclosed](https://hackerone.com/hacktivity/overview?queryString=disclosed%3Atrue&sortField=latest_disclosable_activity_at&sortDirection=DESC&pageIndex=0) | Broader scope |
| Bugcrowd Crowdstream | [crowdstream](https://bugcrowd.com/crowdstream) | Bugcrowd's equivalent |
| Medium Bug Bounty | [Search SSRF](https://medium.com/search?q=ssrf+writeup) | Community writeups |
| Medium BugBountyWriteup | [SSRF tag](https://medium.com/bugbountywriteup/search?q=SSRF) | Curated bounty pub |
| Pentester Land | [Writeup Library](https://pentester.land/writeups/) | Massive curated list |
| BugBountyHunting | [SSRF Search](https://www.bugbountyhunting.com/?q=ssrf) | Searchable DB |
| Dev.to | [SSRF Posts](https://dev.to/search?q=ssrf) | Developer community writeups |
| Substack | [SSRF Articles](https://substack.com/search/ssrf) | Newsletter-style deep dives |
| Hashnode | [SSRF Writeups](https://hashnode.com/search?q=ssrf+writeup) | Developer blogging platform |
| Detectify Labs | [SSRF](https://labs.detectify.com/search/SSRF/) | Research-grade posts |
| Bug Bounty Reference | [SSRF Section](https://github.com/ngalongc/bug-bounty-reference?tab=readme-ov-file#server-side-request-forgery-ssrf) | GitHub-curated reports |
| Marco Tulio Disclosed Reports | [GitHub Repo](https://github.com/marcotuliocnd/bugbounty-disclosed-reports/tree/main/reports) | Raw disclosed report collection |

---

## 👨‍💻 Researcher Blogs to Follow

> These are the people whose work you should study deeply.

| Researcher | Blog | Known For |
|------------|------|-----------|
| **James Kettle** | [jameskettle.com](https://jameskettle.com/) | HTTP request smuggling, SSRF research, PortSwigger |
| **0xPatrik** | [0xpatrik.com](https://0xpatrik.com/) | Subdomain takeover, recon methodology |
| **0xdf** | [0xdf.gitlab.io](https://0xdf.gitlab.io/) | HackTheBox walkthroughs, deep technical analysis |
| **STÖK** | [YouTube](https://www.youtube.com/@STOKfredrik/search?query=SSRF) | Bug bounty mindset & SSRF content |
| **IppSec** | [ippsec.rocks](https://ippsec.rocks/?) | HTB writeup search engine |
| **Intigriti Blog** | [Bug Bytes](https://www.intigriti.com/researchers/blog/bug-bytes) | Weekly security roundup |
| **Red Team Notes** | [ired.team](https://www.ired.team/) | Offensive techniques reference |

---

## 🎥 Video Resources

| Platform | Link | What to Watch |
|----------|------|---------------|
| YouTube — DEF CON | [SSRF Talks](https://www.youtube.com/results?search_query=defcon+ssrf) | Conference-level research |
| YouTube — Bypass Talks | [SSRF Bypass Protections](https://www.youtube.com/results?search_query=ssrf+bypass+protections+talk) | Filter bypass techniques |
| STÖK on YouTube | [SSRF Videos](https://www.youtube.com/@STOKfredrik/search?query=SSRF) | Bug bounty focused |
| Black Hat 2017 (PDF) | [New Era of SSRF — Orange Tsai](https://blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf) | 📄 Must-read/watch presentation |

---

## 🏋️ Practice Platforms

> Build skills by doing, not just reading.

| Platform | Link | Level |
|----------|------|-------|
| PortSwigger Web Academy | [SSRF Labs](https://portswigger.net/web-security/ssrf) | Beginner → Advanced |
| PWN.college | [pwn.college](https://pwn.college/) | Structured, CTF-style |
| HackTheBox | [hackthebox.com](https://www.hackthebox.com) | Intermediate → Advanced |
| TryHackMe | [tryhackme.com](https://tryhackme.com) | Beginner → Intermediate |

---

## 🔍 Google Dorks

> Use these to find fresh writeups, CTF solutions, and real reports.

### General SSRF Writeups

```
site:medium.com "SSRF" "writeup"
site:hackerone.com/reports ssrf
"ssrf" "writeup" "bug bounty" site:medium.com
"server side request forgery" writeup site:medium.com
"ssrf" "$" "bounty" writeup
site:ghost.io "ssrf writeup"
```

### Blind SSRF

```
"blind SSRF" writeup 2023 OR 2024
"blind ssrf" "out of band" writeup
```

### High-Impact SSRF Chains

```
"SSRF to RCE" writeup
"ssrf" "internal network" writeup
"ssrf" "aws metadata" writeup
"ssrf" "169.254.169.254" writeup
"ssrf" "chained" writeup
```

### Platform-Specific

```
"ssrf" writeup site:hackerone.com/reports
"ssrf" writeup site:bugcrowd.com
"ssrf" writeup site:gitlab.com
"SSRF" "$bounty" site:twitter.com
```

### CTF

```
"ssrf" "ctf" writeup site:github.com
"ssrf" "ctf" writeup site:medium.com
```

### GitHub

```
awesome ssrf writeups
ssrf bug bounty report
ssrf payload list github
```

---

## ⭐ GitHub Repositories

| Repository | Description |
|------------|-------------|
| [paulveillard/cybersecurity-ssrf](https://github.com/paulveillard/cybersecurity-ssrf) | Curated SSRF security resources |
| [swisskyrepo/PayloadsAllTheThings — SSRF](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Request%20Forgery) | The definitive payload list |
| [fardeen-ahmed/Bug-bounty-Writeups](https://github.com/fardeen-ahmed/Bug-bounty-Writeups) | Disclosed bug bounty writeups collection |
| [KingOfBugBountyTips — SSRF](https://github.com/KingOfBugbounty/KingOfBugBountyTips/blob/master/SSRF) | Quick tips and payloads |
| [ngalongc/bug-bounty-reference — SSRF](https://github.com/ngalongc/bug-bounty-reference?tab=readme-ov-file#server-side-request-forgery-ssrf) | Categorized bounty report references |
| [djadmin/awesome-bug-bounty](https://github.com/djadmin/awesome-bug-bounty?tab=readme-ov-file) | Broad bug bounty resource list |
| [0xmaximus/Galaxy-Bugbounty-Checklist](https://github.com/0xmaximus/Galaxy-Bugbounty-Checklist) | Full bug bounty checklist |
| [devanshbatham/Awesome-Bugbounty-Writeups](https://github.com/devanshbatham/Awesome-Bugbounty-Writeups) | Categorized writeup collection |
| [marcotuliocnd/bugbounty-disclosed-reports](https://github.com/marcotuliocnd/bugbounty-disclosed-reports/tree/main/reports) | Raw disclosed reports |

---

## 💬 Community & Forums

| Platform | Link | What's There |
|----------|------|-------------|
| Reddit r/netsec | [reddit.com/r/netsec](https://www.reddit.com/r/netsec/) | News, writeups, discussions |
| Security StackExchange | [SSRF Questions](https://security.stackexchange.com/search?q=ssrf) | Q&A with expert answers ⭐ |
| Intigriti Blog | [Bug Bytes Newsletter](https://www.intigriti.com/researchers/blog/bug-bytes) | Weekly curated security news |

---

## 🗺️ Suggested Learning Path

```
Week 1 — Fundamentals
├── PortSwigger Academy (all SSRF labs)
├── Read OWASP SSRF page
└── Read 5 basic writeups from HackerOne Hacktivity

Week 2 — Intermediate
├── Intigriti Advanced SSRF Guide
├── PayloadsAllTheThings SSRF section
├── Practice blind SSRF with Burp Collaborator
└── Read Orange Tsai's chaining writeup

Week 3 — Advanced
├── Blind SSRF Chains (Assetnote)
├── Black Hat 2017 — Orange Tsai PDF
├── DNS rebinding and cloud metadata exploitation
└── Build your own vulnerable lab to test payloads

Ongoing
├── Follow researcher blogs weekly
├── Read 2–3 new writeups daily
└── Try SSRF challenges on HackTheBox / pwn.college
```

---

<div align="center">

---

*Curated for bug bounty hunters, penetration testers, and security researchers.*

**⭐ Star this repo if it helped you. Contributions and PRs welcome.**

*For educational and authorized testing purposes only.*

</div>
├── DNS rebinding and cloud metadata exploitation
└── Build your own vulnerable lab to test payloads

Ongoing
├── Follow researcher blogs weekly
├── Read 2–3 new writeups daily
└── Try SSRF challenges on HackTheBox / pwn.college
```

---

<div align="center">

---

*Curated for bug bounty hunters, penetration testers, and security researchers.*

**⭐ Star this repo if it helped you. Contributions and PRs welcome.**

*For educational and authorized testing purposes only.*

</div>