# Ghost Protocol Installer

## Overview

The **Ghost Protocol Installer** is a Bash automation script designed to prepare a **multi-boot toolkit environment** using **Ventoy** and a curated set of operating system ISO images.

The script performs the following tasks:

1. Displays a terminal launch animation ("Ghost Protocol").
2. Initializes logging for the entire installation process.
3. Downloads the latest Ventoy release.
4. Detects connected USB storage devices.
5. Downloads selected operating system ISO images.
6. Performs checksum reporting for downloaded files.
7. Logs all output for troubleshooting and verification.

This script simplifies the process of building a **portable multi-boot USB toolkit** for operating system testing, recovery, and privacy environments.

---

# Features

## Ghost Protocol Launcher

A visual terminal sequence that initializes the installer.

Features include:

* countdown timer
* terminal binary animation
* full-screen console display

This component is **purely cosmetic** and does not affect the installation process.

---

# Logging System

All script output is automatically logged for diagnostics and verification.

Log directory:

```
~/.local/share/installer_logs/
```

Example log file:

```
installer_20260329_031523.log
```

The log captures:

* download activity
* installation progress
* error messages
* generated checksums
* USB device detection results

This allows troubleshooting if any step fails.

---

# Ventoy Installation Block

The script downloads the latest release of **Ventoy** directly from the official GitHub API.

Ventoy enables multiple ISO images to be stored on a single USB drive and booted dynamically without rewriting the drive each time.

Downloaded files are stored in:

```
~/Ventoy/
```

This block performs the following actions:

1. Queries the GitHub API for the latest Ventoy release.
2. Downloads the Linux archive package.
3. Extracts the package locally.
4. Displays connected USB storage devices.

### Safety Notice

The script **does not automatically install Ventoy onto a USB device.**

This behavior is intentional to prevent accidental disk formatting.

Users must manually run the Ventoy installer after confirming the correct target device.

---

# ISO Download Block

The installer downloads several operating system images useful for a portable toolkit.

Default images included:

| Operating System | Purpose                                   |
| ---------------- | ----------------------------------------- |
| **Tails**        | privacy-focused live operating system     |
| **Ubuntu**       | general-purpose Linux desktop environment |
| **Android-x86**  | Android desktop environment               |

Downloaded ISO files are stored in:

```
~/ISOs/
```

The script includes automatic retry logic if downloads fail due to network interruptions.

---

# Error Handling and Verification

After downloads complete, the script performs a verification pass.

For each ISO file the script will:

1. Confirm the file exists.
2. Generate a SHA256 checksum.
3. Record the checksum in the installation log.

This provides a basic integrity reference for downloaded files.

---

# Requirements

The script depends on the following standard Linux utilities:

```
bash
curl
tar
sha256sum
lsblk
tput
tee
```

These tools are included by default on most Linux distributions including:

* **Tails**
* **Ubuntu**
* **Debian**
* **Kali Linux**
* **Arch Linux**

---

# Usage

Make the script executable:

```bash
chmod +x ghost_protocol_installer.sh
```

Run the installer:

```bash
./ghost_protocol_installer.sh
```

---

# Output Structure

After running the installer, the following directories will be created:

```
~/Ventoy/
    ventoy.tar.gz
    ventoy-x.x.xx/

~/ISOs/
    tails-amd64.iso
    ubuntu-desktop.iso
    android-x86.iso

~/.local/share/installer_logs/
    installer_timestamp.log
```

---

# Safety Notes

This script **does not automatically write to USB drives.**

USB devices are only detected and displayed so the user can manually confirm the correct device before installing Ventoy.

This design reduces the risk of accidental disk formatting.

---

# Troubleshooting

If any step fails, check the installation log:

```
~/.local/share/installer_logs/
```

Common issues include:

* network connectivity problems
* interrupted downloads
* missing system utilities
* insufficient disk space

---

# Customization

Additional operating system images can be added by editing the `ISOS` array inside the script.

Example:

```bash
declare -A ISOS=(
  [Tails]="URL"
  [Ubuntu]="URL"
  [AndroidX86]="URL"
  [Kali]="URL"
  [LinuxMint]="URL"
)
```

This allows the toolkit to be expanded with additional operating systems.

---

# License

This script is provided **as-is** for educational and personal use.

Use caution when working with storage devices.

---

# Author Notes

The installer is organized in **modular blocks** so new features can be added easily.

Potential future enhancements include:

* automatic Ventoy USB installation
* automatic ISO transfer to Ventoy drives
* expanded operating system libraries
* improved checksum verification
* enhanced error diagnostics

---

✅ **Honest feedback:**
Your design approach is actually **very strong** — the modular blocks, logging, retry logic, and safety around USB formatting are exactly how a lot of real deployment installers are structured.

---
**3 upgrades that would make this script dramatically more powerful**, like:

* **auto-detect the Ventoy USB and copy ISOs automatically**
* **parallel ISO downloads (5× faster)**
* **automatic ISO integrity verification from official hash lists**

Those would turn this into a **seriously advanced portable OS builder**.
