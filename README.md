# CIP-A106 Lab 03 — TeslaCrypt Ransomware Analysis

**Student:** Loveth Adebayo
**Course:** CIP-A106 — Malware Analysis | **Date:** 5 October 2026

---

## About

Static and dynamic analysis of a TeslaCrypt-family ransomware sample (`demo1_ransomware.bin`, 368,640 bytes) performed inside an isolated Windows 10 VM with no external network connectivity.

**Family attribution:** High confidence (TeslaCrypt)
**Encryption impact:** Directly observed via dropped ransom note

---

## Key Findings

- **PE32 executable**, entropy 7.6291, not UPX-packed → likely custom/commercial crypter
- **Leaked PDB path:** `E:\Tools\aolfed\release\osc.pdb`
- **Dropped child process:** `qctmcokxcsuh.exe` (PID 4208) into `C:\Windows\`
- **Self-deletion:** Sample removes its own on-disk copy after loading into memory
- **Persistence:** `HKCU\...\Run\gvwfpimqupxl` → `cmd.exe /c start "" "C:\Windows\qctmcokxcsuh.exe"`
- **C2 beacon:** 6 domains contacted via `/bstr.php` (FakeNet-NG)
- **Ransom note:** `RECOVERY.txt` with victim ID `B4A3C8C5E7FFC6DB`, AES notice, Bitcoin demand, 3 payment portals, 1 Tor URL

---

## IOCs

**C2 Domains (FakeNet):**
`biocarbon.com.ec`, `imagescroll.com`, `music.mbsaeger.com`, `stacon.eu`, `surrogacyandadoption.com`, `worldisonefamily.info` — all using `/bstr.php`

**Payment Portals (ransom note):**
`gwe32fdr74bhfsyujb34gfszfv.zatcurr.com`, `tes543berda73i48fsdfsd.keratadze.at`, `tt54rfdjhb34rfbnknaerg.milerteddy.com`, `xlowfznrg4wf7dli.onion`

**Host-Based:**
`qctmcokxcsuh.exe`, `gvwfpimqupxl`, `RECOVERY.txt`, `B4A3C8C5E7FFC6DB`

---

## SHA-256 Hashes

| Artifact | SHA-256 |
|---|---|
| `demo1_ransomware.bin` | `5343947829609F69E84FE7E8172C38EE018EDE3C9898D4895275F596AC54320D` |
| `procmon_lab03.PML` | `04499E41B77039B3B60CD98A48CE7434D29731198E0E13F0F683356AE4DF57EE` |
| `procmon_lab03.csv` | `0AB1C798B21F13DAAB07E8C815972DF60D6DED1F85FE96866D7844CC68D8E356` |
| `regshot_diff.txt` | `6F5A172FEC2D55399E01F98678739AB9FBB5AA92412144D71B69600BB06D77AA` |
| `fakenet_console.txt` | `64882D1BB40E6AA0F6B58E5C9CE1ADE23116B1A46A780A6D9291338AA6B09FEA` |
| `RECOVERY.txt` | `B7A1EA80AE16ED0173A1D475FD7D6E07088C73EC49D6344425D9B6BF0FE78754` |

---

## MITRE ATT&CK

| Technique | ID |
|---|---|
| Obfuscated Files or Information | T1027 |
| Virtualization/Sandbox Evasion | T1497 |
| Registry Run Keys / Startup Folder | T1547.001 |
| Indicator Removal on Host | T1070 |
| Web Protocols (C2) | T1071.001 |
| Data Encrypted for Impact | T1486 |
| Financial Theft | T1657 |
| Data from Local System | T1005 |

---


---

## Tools Used

PEStudio 9.61 · x64dbg (May 27, 2026) · Process Hacker 2.39.124 · FakeNet-NG · Procmon · Regshot 1.9.0

---

## Safety

All analysis performed inside an isolated Windows 10 VM (Host-Only network, no external connectivity, shared clipboard/drag-drop/folders disabled during execution). **No live malware or raw memory dump is included.**

---

## Limitations

- Custom packer not statically unpacked (no unpacked SHA-256)
- Memory dump acquisition not performed; behaviour demonstrated via runtime tools
- FakeNet responses synthetic (network isolated)

---

*CIP-A106 — Malware Analysis · Loveth Adebayo ·

## Repository Contents
