# BYTE Society Recruitment Task - Steganography

## Overview
For this recruitment challenge, the objective was to inspect a corrupted PNG file, repair its file structure, fix corrupted header chunks, and extract/polish a hidden steganography flag.

- **Final Derived Flag:** `flag{g0t 1t in p1ain sight}`
- **GitHub Repository Link:** https://github.com/Raghav-G18/BYTE_Steganography_Task_2.git

---

## Step-by-Step Breakdown & Methodology

### 1. Initial File Analysis & Header Verification
- **The Problem:** The target image file (`repair.png`) was malformed and unreadable by standard image viewers due to structure corruption.
- **Observation:** I inspected the raw file bytes and confirmed the standard 8-byte PNG magic signature (`89 50 4E 47 0D 0A 1A 0A`).
- **Action:** I identified and stripped away extraneous trailing garbage bytes appended to the end of the data stream, allowing decoders to parse the file payload without crashing.

### 2. Repairing the IHDR Chunk and CRC Mismatch
- **The Mismatch:** The image dimensions inside the `IHDR` header chunk were corrupted, throwing off the layout.
- **The Reasoning:** By testing and brute-forcing dimensions against expected aspect ratios, the true image height was isolated to **850 pixels**.
- **Action:** I updated the header height field and recalculated the Cyclic Redundancy Check (CRC) checksum so standard image parsers would accept the integrity of the file.

### 3. Polishing and Hidden Data Extraction
- The hidden flag text was embedded via near-black pixel values and subtle variations near the bottom or across color/alpha layers.
- **Automation Proof:** I wrote a modular Python script (`polish_flag.py`) utilizing the `Pillow` library to automate loading, contrast stretching, and channel analysis.

---

## Repository Contents
- `repair.png` — The successfully repaired base image.
- `polish_flag.py` — The automated Python script used for image processing and extraction.
- `README.md` — Project documentation and write-up.

---

*Raghav Gupta*  
*B.Tech CSE (sec-B)*
