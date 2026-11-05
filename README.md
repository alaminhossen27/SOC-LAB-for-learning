#🛡️ SOC Lab — SIEM, SOAR & OWASP Top 10 Practice Simulator
A free, browser-based training lab where students practise the daily work of a SOC (Security Operations Center) analyst: they detect, triage, investigate, respond and report on simulated incidents.
It is a single HTML file, with no install, no server and no sign-up. It works on desktop and mobile.

Why this exists
Real SIEM/SOAR platforms (Splunk, Sentinel, QRadar, XSOAR…) are expensive, heavy to set up, and come with no realistic attack data. SOC Lab gives learners a safe, fully simulated company network and web shop with hundreds of realistic log events. Hidden attacks and false alarms are mixed in, so students can build the right instincts before they touch production tools.

Features
SIEM search: a Splunk-style query language (stats, where, sort, head, table, wildcards, numeric filters). It also has a timeline histogram and clickable field values.
40 detection rules: you can edit them, turn them on or off, or write your own and test them against the data.

Alert triage: mark each alert true positive or false positive, then classify the attack type.

SOAR playbook builder: chain response actions such as IP/hash enrichment, block IP/domain, isolate host, disable user, reset password, revoke sessions, quarantine email, create ticket and notify. Each action shows a simulated execution log.

Scoring & debrief: you get points for correct answers, triage, classification and response. Harmful actions cost points (for example, blocking an authorised pentester). After you submit, a debrief explains what really happened, with OWASP and MITRE ATT&CK mapping.

Randomised every time: IPs, users, domains, hashes and timings change on every start, so students can't copy each other's answers.
Realistic log sources: web, firewall, auth, proxy, dns, edr and email, from a fictional company plus a fictional e-commerce site.

Practice modes
Mode

What you get
OWASP Top 10 Web Day
4 random web-application attacks, often plus a harmless look-alike
Random SOC Shift
4–5 real incidents and 1–2 false positives drawn from all alert types
Alert Library
Practise any of 32 alert types on its own, with questions and hints
Story missions
5 guided scenarios: brute force, phishing, C2 beaconing, insider exfiltration, false-positive scan
Alert coverage (32 types)
OWASP Top 10:2025

#
Category
Scenario(s)
A01
Broken Access Control (incl. SSRF)
IDOR order enumeration, path traversal, SSRF to cloud metadata
A02
Security Misconfiguration
Exposed .git / .env files
A03
Software Supply Chain Failures
Typosquatted npm package on the build server
A04
Cryptographic Failures
Passwords sent over plain HTTP
A05
Injection
SQL injection (sqlmap), stored XSS
A06
Insecure Design
Unlimited coupon stacking
A07
Authentication Failures
Credential stuffing
A08
Software or Data Integrity Failures
Java deserialization RCE
A09
Security Logging & Alerting Failures
Web shell plus wiped logs
A10
Mishandling of Exceptional Conditions
Auth error causes fail-open
Identity: password spray, impossible travel, MFA push bombing, Domain Admins change, Kerberoasting
Endpoint: ransomware, LSASS credential dumping, PsExec lateral movement, antivirus tampering, cryptominer, malicious Office macro
Network: DNS tunneling, Tor usage
Email: business email compromise (CEO fraud)
False-positive drills: authorised pentest, Googlebot crawl, approved travel, approved admin change, IT PsExec deployment
Getting started
Option 1: just open it
Download index.html and open it in Chrome, Edge or Firefox. On Android, choose Open with → Chrome.
Option 2: classroom LAN
python -m http.server 8000
# students open http://<instructor-ip>:8000
Option 3: GitHub Pages (recommended for sharing)
Fork this repo, go to Settings → Pages, choose branch main and folder / (root). Your lab will be live at https://<username>.github.io/soc-lab/.
Query cheat sheet
sourcetype=auth action=failure                      # filter (AND by default)
uri=*select*   cmdline=*-enc*                       # wildcards
bytes>500000000                                     # numeric compare
NOT user=alice    country!=BD                       # exclude
| stats count by src_ip, user                       # group & count
| stats dc(dest_port) by src_ip | where dc > 20     # distinct count + filter
| sort -count | head 10                             # sort & limit
| table _time, host, user, process, cmdline         # choose columns
How students are scored
Item
Points
Investigation question answered correctly
+10
Correct final verdict (story missions)
+20
Alert triaged correctly
+5
True-positive alert classified correctly
+5
Required response action
+10
Recommended response action
+5
Harmful action (e.g. blocking an authorised scanner)
−15
Blocking an internal IP
−10
Hint used
−5
Ranks: Trainee → SOC Analyst L1 → SOC Analyst L2 → Threat Hunter.
For instructors
Run Random SOC Shift as a timed exercise and have students hand in their result screenshot and analyst notes.
Ask students to write a custom detection rule that would have caught an attack earlier.
Use the false-positive drills to teach verify before you block.
Best scores are stored in each student's own browser (localStorage). There is no backend and no data collection.
Safety & data
All companies, people, domains and events are fictional. Attacker IPs use the RFC 5737 documentation ranges (192.0.2.0/24, 198.51.100.0/24, 203.0.113.0/24), and attacker domains use .example. The lab contains no real malware, exploits or offensive tooling. It only simulates the logs that defenders would see.
Tech
Vanilla HTML, CSS and JavaScript in one file (~130 KB). It has no dependencies or build step and works offline.
Contributing
New scenarios are welcome! Each incident is a small generator function in the INC array. It returns its events, investigation questions, required/forbidden response actions, a debrief story and MITRE/OWASP tags. Open an issue or PR.
License
MIT — free to use for teaching, training and self-study.