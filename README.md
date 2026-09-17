<p align="center">
  <img src="assets/banner.png" alt="Digital Forensics Lab — Android & iOS Mobile Forensics" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Field-Digital%20Forensics-1f6feb?labelColor=0d1117" alt="Digital Forensics">
  <img src="https://img.shields.io/badge/Android-ADB%20%2F%20ALEAPP-3DDC84?logo=android&logoColor=white&labelColor=0d1117" alt="Android">
  <img src="https://img.shields.io/badge/iOS-iLEAPP%20%2F%20iOSbackup-999999?logo=apple&logoColor=white&labelColor=0d1117" alt="iOS">
  <img src="https://img.shields.io/badge/Cracking-Hashcat%2014800-ff5f56?labelColor=0d1117" alt="Hashcat">
  <img src="https://img.shields.io/badge/Env-Ubuntu%20(WSL)-E95420?logo=ubuntu&logoColor=white&labelColor=0d1117" alt="Ubuntu WSL">
  <img src="https://img.shields.io/badge/License-MIT-blue" alt="MIT License">
</p>

<p align="center">
  <b>Practical mobile-forensics lab</b> — acquire, extract, and analyse Android &amp; iOS artifacts with open-source tools, documented with the real evidence output at each step.
</p>

---

## 👋 About

I'm **Adriano Huttener**, focused on security and digital forensics. This repository is a hands-on walkthrough of mobile-forensics techniques on **public datasets (Digital Corpora)** — acquisition, artifact parsing, encrypted-backup analysis, and password recovery — each step backed by the actual tool output.

> 🇮🇪 Based in Kildare, Ireland · Open to security / forensics roles

---

## 🛠 Environment & tooling

| Area | Stack |
|------|-------|
| **OS** | Ubuntu on WSL (Windows Subsystem for Linux) |
| **Android** | ADB · ALEAPP · `tar` |
| **iOS** | iLEAPP · iOSbackup · iTunes_Backup_Reader |
| **Cracking** | Hashcat (mode 14800) · Perl extractor |
| **Cloud** | pyicloud (proof of concept) |

---

## 🧪 Case walkthrough

### 1 · Android forensic analysis
**Objective:** parse artifacts from an Android 10 image.
- **Tool:** ALEAPP (Android Logs, Events And Protobuf Parser).
- **Outcome:** HTML report with call logs, messages, and app-usage artifacts.

### 2 · Advanced Android extraction (root)
**Objective:** simulate a physical extraction on a rooted device.
- **Method:** shell over `adb`, privilege elevation with `su`, and a manual archive of `/data/data` using `tar`.

### 3 · iOS forensic analysis
**Objective:** parse artifacts from an iPhone (iOS 13.4.1, `iPhone12,8`).
- **Tool:** iLEAPP — parses a `tar` extraction into a browsable case report.
- **Outcome:** device build/OS identification, installed apps, and device-data artifacts (IMEI, carrier, identifiers).

<p align="center">
  <img src="assets/ios-ileapp-case-info.png" alt="iLEAPP case information for the iOS 13.4.1 extraction" width="90%">
  <br><em>iLEAPP — case information for the iOS 13.4.1 <code>tar</code> extraction.</em>
</p>

<p align="center">
  <img src="assets/ios-ileapp-device-data.png" alt="iLEAPP device data report (identifiers, IMEI, carrier)" width="90%">
  <br><em>Device-data report: identifiers, IMEI and carrier artifacts.</em>
</p>

### 4 & 5 · Encrypted iTunes backup analysis
**Objective:** access a password-protected iTunes backup.
- **Method:** decrypted the backup with the `iOSbackup` Python library using the known password.
- **Result:** reached internal app containers (Zoom, Telegram).

<p align="center">
  <img src="assets/itunes-backup-decrypted.png" alt="Decrypted iTunes backup showing Zoom and Telegram app containers" width="90%">
  <br><em>Decrypted backup — Zoom &amp; Telegram application containers enumerated.</em>
</p>

### 6 · Password recovery (brute force)
**Objective:** recover a lost iTunes-backup password.
1. Extracted the hash from `Manifest.plist` with a Perl script → Hashcat **mode 14800**.
2. Ran a dictionary attack against [`tools/wordlist.txt`](tools/wordlist.txt).

<p align="center">
  <img src="assets/hashcat-start.png" alt="Hashcat starting against the iTunes backup hash" width="90%">
  <br><em>Hashcat v6.2.6 initialising against the mode-14800 hash.</em>
</p>

<p align="center">
  <img src="assets/hashcat-cracked.png" alt="Hashcat status Cracked — password recovered" width="90%">
  <br><em>Status <b>Cracked</b> — password recovered: <code>mypassword123</code>.</em>
</p>

### 7 · Cloud forensics (iCloud) — proof of concept
**Objective:** show a methodology for cloud data acquisition.
- **Method:** a Python script using `pyicloud` to authenticate via API and retrieve location/contact data.
- *Note: proof-of-concept only.*

---

## 🧰 Tools in this repo

| File | Purpose |
|------|---------|
| [`tools/itunes_backup2hashcat.pl`](tools/itunes_backup2hashcat.pl) | Extracts the Hashcat mode-14800 hash from an iTunes backup `Manifest.plist`. Credit: **philsmd** (public domain). |
| [`tools/wordlist.txt`](tools/wordlist.txt) | Small demo wordlist used for the dictionary attack. |

---

## ⚖️ Disclaimer

Conducted **for education and research only**, using **public forensic datasets (Digital Corpora)**. Only acquire or analyse devices and data you own or are **explicitly authorized** to examine.

---

<p align="center">🌐 <a href="https://cybersecinfo.com">cybersecinfo.com</a> · 👤 <a href="https://github.com/ahuttener">github.com/ahuttener</a></p>
