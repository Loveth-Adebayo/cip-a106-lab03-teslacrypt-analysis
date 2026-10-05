# CIP-A106 Lab 03 — TeslaCrypt Ransomware Analysis

**Student:** Loveth Adebayo
**Student ID:** C11_26-EHIT-17323
**Course:** CIP-A106 — Malware Analysis
**Lab:** Lab 03 — TeslaCrypt Ransomware Unpacking and Memory Analysis
**Date:** 5 October 2026

---

## Overview

Static, debugger, and memory analysis of a TeslaCrypt-family ransomware sample (`demo1_ransomware.bin`) inside an isolated Windows 10 VM with no external network connectivity.

Analysis confirmed the sample spawns a randomly-named self-deleting child process, establishes HKCU Run persistence, beacons to six C2 domains via the `/bstr.php` pattern, and drops a ransom note (`RECOVERY.TXT`) with an AES notice, Bitcoin demand, and Tor payment portal.

Family attribution to **TeslaCrypt** is **high confidence**. Sample demonstrated **behavioural polymorphism** — regenerating its persistence key and dropped filename on each execution.

---

## Contents

Lab03/
├── README.md
├── CIP_A106_Lab03_Loveth_Adebayo_C11_26-EHIT-17323.pdf
├── Artifacts/ ← baseline, procmon, fakenet, regshot, memory strings, ransom note
├── Memory/ ← TeslaCrypt_pid.dmp
└── Evidence/ ← annotated screenshots (isolation, PEStudio, debugger, memory, cleanup)

text

---

## Key Findings

| Attribute | Value |
|---|---|
| Source SHA-256 | `5343947829609F69E84FE7E8172C38EE018EDE3C9898D4895275F596AC54320D` |
| Memory dump SHA-256 | `B864303518E9F70A98D5230E2A1B198E6B83B883935B7CB32FB814117E60ABCE` |
| Source entropy | **7.6291** (packed) |
| Memory dump entropy | **5.098** (unpacked ✅) |
| Entry Point | `0x00403C40` |
| PDB path leaked | `E:\Tools\aolfed\release\osc.pdb` |
| Persistence (1st run) | `HKCU\...\Run\gvwfpimqupxl` → `qctmcokxcsuh.exe` |
| Persistence (2nd run) | `HKCU\...\Run\ngctjqrjrvjj` → `jgmuoeuplsyh.exe` |
| Victim ID | `B4A3C8C5E7FFC6DB` |

**C2 domains:** biocarbon.com.ec, imagescroll.com, music.mbsaeger.com, stacon.eu, surrogacyandadoption.com, worldisonefamily.info (all via `/bstr.php`)

**Payment portals:** zatcurr.com, keratadze.at, milerteddy.com, xlowfznrg4wf7dli.onion

---

## Tools Used

PEStudio 9.61 · x32dbg · Process Hacker 2.39.124 · OllyDumpEx · FakeNet-NG · Procmon · Regshot 1.9.0 · Sysinternals strings

---

## Safety Note

All analysis performed inside an isolated Virtual Machine (Host-Only network, clipboard and drag-drop disabled, shared folder removed during execution). No live malware is included; `Memory/TeslaCrypt_pid.dmp` is retained for grading only — do not redistribute.

---

## Academic Integrity

All observations in the report are traceable to evidence artifacts and screenshots. Hypotheses are clearly labelled as such. No fabricated evidence.
