# 🕵️‍♂️ Digital Forensics Lab: Android & iOS Analysis

This repository documents a series of practical forensic exercises performed in a Linux environment (WSL). The goal was to acquire, extract, and analyze data from mobile devices using open-source tools.

## 🛠 Tools & Environment
- **OS:** Ubuntu (WSL - Windows Subsystem for Linux)
- **Android Tools:** ADB, ALEAPP, Tar
- **iOS Tools:** iLEAPP, iOSbackup, iTunes_Backup_Reader
- **Cracking:** Hashcat, Perl scripts
- **Cloud:** pyicloud (Concept)

## 📂 Project Structure & Methodologies

### 1. Android Forensic Analysis
**Objective:** Parse artifacts from an Android 10 image.
- **Tool:** ALEAPP (Android Logs Events And Protobuf Parser)
- **Outcome:** Generated HTML report containing call logs, messages, and app usage.

### 2. Advanced Android Extraction (Root)
**Objective:** Simulate a physical extraction on a rooted device.
- **Method:** Accessed the shell via `adb`, elevated privileges with `su`, and manually archived `/data/data` using `tar`.

### 3. iOS Forensic Analysis
**Objective:** Parse artifacts from an iPhone (iOS 13.4.1).
- **Tool:** iLEAPP
- **Outcome:** Identification of Device Build (`iPhone12,8`), iOS version, and installed applications.

### 4 & 5. Encrypted iTunes Backup Analysis
**Objective:** Decrypt a password-protected iTunes backup.
- **Challenge:** The backup was locked with a password.
- **Solution:** Utilized the `iOSbackup` Python library to bypass encryption using the known password.
- **Result:** Successfully accessed internal files (Zoom, Telegram containers).

### 6. Password Recovery (Brute-Force)
**Objective:** Recover a lost iTunes backup password.
- **Method:**
  1. Extracted the hash from `Manifest.plist` using a Perl script.
  2. Performed a dictionary attack using **Hashcat** (Mode 14800).
- **Result:** Password recovered: `mypassword123`.

### 7. Cloud Forensics (iCloud)
**Objective:** Demonstrate methodology for cloud data acquisition.
- **Method:** Developed a Python script using `pyicloud` to authenticate via API and retrieve Location/Contact data.
- *Note: Performed as a proof-of-concept script.*

---
*Disclaimer: This project was conducted for educational purposes using public forensic datasets (Digital Corpora).*
