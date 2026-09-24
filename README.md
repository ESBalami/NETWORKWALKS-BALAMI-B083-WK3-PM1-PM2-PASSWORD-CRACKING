# NetworkWalks Cybersecurity Program – Week 3
## Password Cracking with JTR & NetworkWalks Tools

**Author:** Emmanuel Balami
**Program:** NetworkWalks Cybersecurity Program (Batch B083)
**Week:** 03

## Project Overview

This repository documents the practical activities completed during Week 3 of the NetworkWalks Cybersecurity Program: recovering passwords from encrypted PDF files using two different approaches.

Password cracking is used by security professionals to test how strong a password really is. When a file is password-protected, its password is stored as a hash — a scrambled representation of the password. To recover it, the hash is first extracted from the file, then run through a cracking tool that tries candidate passwords until one produces a matching hash.

Three "locked" PDF files were provided for this exercise (`My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`), each containing a hidden flag revealed once unlocked. The work covered two modules:

- **W3-PM1:** Password Cracking with JTR (John the Ripper)
- **W3-PM2:** Password Cracking with NetworkWalks Tools (Hash Calculator + Password Cracker)

## Learning Objectives

- Understand how password-protected files store their passwords as hashes.
- Extract a crackable hash from an encrypted PDF using `pdf2john`.
- Perform a dictionary attack against a password hash using John the Ripper.
- Perform the same style of attack using NetworkWalks' own browser-based tools.
- Compare a native CLI cracking workflow against a no-install, browser-based workflow.
- Document password-cracking activity professionally, including evidence.

## Module 1 – Password Cracking with JTR (W3-PM1)

The lab task specified using JTR John and the Johnny GUI on Windows. I completed the equivalent workflow using **John the Ripper's native Kali Linux command-line tools** instead (`pdf2john` + `john`), since JTR comes pre-installed on Kali as the task's own "Related Info" note allows. Screenshots of both the cracking process and the resulting captured flag are included in `evidence/pm1-jtr-kali/`.

**Workflow used for each locked PDF:**
1. `pdf2john 'My Locked PDFx.pdf' > Hash.txt` — extract the password hash from the PDF into a hash file.
2. `john Hash.txt` — run John the Ripper's default single-crack + wordlist attack (`/usr/share/john/password.lst`) against the hash.
3. `john --show Hash.txt` — display the cracked password once found.
4. Open the PDF with the recovered password to reveal the flag.

**Results**

| File | Cracked Password | Flag Captured | Evidence |
|---|---|---|---|
| My Locked PDF1.pdf | `good-luck` | `nw{cybersecurity_flag_captured_2608}` | [`1`](evidence/pm1-jtr-kali/1_pdf1_crack_kali_john.png), [`2`](evidence/pm1-jtr-kali/2_pdf1_password_prompt.png), [`3`](evidence/pm1-jtr-kali/3_pdf1_flag_captured.png) |
| My Locked PDF2.pdf | `password1` | `nw{networkwalks_persistence_jtr_270521}` | [`4`](evidence/pm1-jtr-kali/4_pdf2_crack_kali_john.png), [`5`](evidence/pm1-jtr-kali/5_pdf2_flag_captured.png) |
| My Locked PDF3.pdf | `1qaz2wsx` | `nw{networkwalks_flag_260821_1}` | [`6`](evidence/pm1-jtr-kali/6_pdf3_crack_kali_john.png), [`7`](evidence/pm1-jtr-kali/7_pdf3_flag_captured.png) |

The extracted hash for PDF1 is included as evidence in [`hash1_pdf1.txt`](evidence/pm1-jtr-kali/hash1_pdf1.txt) — a PDF MD5/SHA2/RC4/AES hash in `pdf2john` format (`$pdf$4*4*128*...`).

**Skills Practised**
- PDF hash extraction (`pdf2john`)
- Dictionary/wordlist attacks with John the Ripper
- Command-line password recovery
- Verifying a cracked password by unlocking the target file

## Module 2 – Password Cracking with NetworkWalks Tools (W3-PM2)

This module used two free browser-based tools from NetworkWalks instead of an installed cracking tool:

- **Hash Calculator** (`networkwalks.com/hash-calculator/`) — parses an uploaded PDF locally in the browser and extracts its crackable `$pdf$...` hash (pdf2john/hashcat-compatible format). No file is uploaded to a server.
- **Password Cracker** (`networkwalks.com/password-cracker/`) — runs a dictionary attack in the browser, hashing every word in a wordlist and comparing it against the pasted `$pdf$` hash, the same underlying idea as John the Ripper.

I applied this workflow to the two PDFs not already demonstrated with a screenshot walkthrough in Module 1: **Locker 2** (`My Locked PDF2.pdf`) and **Locker 3** (`My Locked PDF3.pdf`).

**Workflow used for each PDF:**
1. Upload the locked PDF to the Hash Calculator → copy the extracted `$pdf$` hash.
2. Paste the hash into the Password Cracker.
3. Run the built-in 100-word list attack and wait for a match.
4. Use the revealed password to unlock the PDF.

**Results**

| File ("Locker") | Cracked Password | Evidence |
|---|---|---|
| Locker 2 — My Locked PDF2.pdf (204.7 KB) | `password1` | [`1`](evidence/pm2-networkwalks-tools/1_pdf2_hash_calculator.png), [`2`](evidence/pm2-networkwalks-tools/2_pdf2_password_cracker_running.png), [`3`](evidence/pm2-networkwalks-tools/3_pdf2_password_cracked.png) |
| Locker 3 — My Locked PDF3.pdf (313.5 KB) | `1qaz2wsx` | [`4`](evidence/pm2-networkwalks-tools/4_pdf3_password_cracked.png), [`5`](evidence/pm2-networkwalks-tools/5_pdf3_hash_calculator.png) |

Both passwords match the results independently obtained with John the Ripper in Module 1, confirming the two methods agree.

**Skills Practised**
- Browser-based hash extraction from an encrypted PDF
- Dictionary attacks via a no-install web tool
- Cross-checking cracked credentials across two independent tools

## Technologies & Tools

| Tool | Purpose |
|---|---|
| Kali Linux | Platform for `pdf2john` and John the Ripper |
| `pdf2john` | Extracts a crackable hash from a password-protected PDF |
| John the Ripper (`john`) | Dictionary/wordlist password cracking |
| NetworkWalks Hash Calculator | Browser-based PDF hash extraction |
| NetworkWalks Password Cracker | Browser-based dictionary attack against a `$pdf$` hash |

## Key Skills Demonstrated

- Password Cracking & Recovery
- Hash Extraction
- Dictionary Attacks
- Command-Line Security Tools
- Browser-Based Security Tools
- Evidence-Based Technical Documentation

## Repository Structure

```
.
├── README.md
└── evidence/
    ├── pm1-jtr-kali/
    │   ├── 1_pdf1_crack_kali_john.png
    │   ├── 2_pdf1_password_prompt.png
    │   ├── 3_pdf1_flag_captured.png
    │   ├── 4_pdf2_crack_kali_john.png
    │   ├── 5_pdf2_flag_captured.png
    │   ├── 6_pdf3_crack_kali_john.png
    │   ├── 7_pdf3_flag_captured.png
    │   └── hash1_pdf1.txt
    └── pm2-networkwalks-tools/
        ├── 1_pdf2_hash_calculator.png
        ├── 2_pdf2_password_cracker_running.png
        ├── 3_pdf2_password_cracked.png
        ├── 4_pdf3_password_cracked.png
        └── 5_pdf3_hash_calculator.png
```

## What I Learned

This project reinforced how password cracking works end-to-end: extracting a hash from a protected file, then testing candidate passwords against it until a match is found. Running the same attack through two different tools — a native command-line tool (John the Ripper) and a browser-based tool (NetworkWalks Hash Calculator/Password Cracker) — showed that the underlying technique (dictionary attacks against an extracted hash) is the same regardless of the interface, and produced consistent, verifiable results across both methods.

It also highlighted why weak, common passwords (`password1`, `1qaz2wsx`) are cracked almost instantly against a small wordlist, underlining the importance of long, unique passwords.

## Disclaimer

All activities were conducted against PDF files provided specifically for this authorised training exercise. No exploitation, unauthorised access, or attacks against third-party systems were performed. This repository is intended solely for educational and portfolio purposes.

## Author

**Emmanuel Balami**

NetworkWalks Cybersecurity Program (Batch B083)

Week 3 – Password Cracking with JTR & NetworkWalks Tools
