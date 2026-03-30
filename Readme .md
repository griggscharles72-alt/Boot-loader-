Overview:

The Ghost Protocol Installer is a Bash-based automation script designed to prepare a multi-boot environment using Ventoy and a curated set of operating system ISO images.

The script performs the following tasks:
	1.	Displays a terminal launch animation (“Ghost Protocol”).
	2.	Initializes logging for the entire installation process.
	3.	Downloads the latest Ventoy release.
	4.	Detects connected USB devices.
	5.	Downloads selected operating system ISO images.
	6.	Performs checksum reporting for downloaded files.
	7.	Logs all output for troubleshooting and verification.

This script is intended to simplify the process of building a portable multi-boot USB toolkit.

⸻

Features

Ghost Protocol Launcher

A visual terminal sequence that initializes the installer.
	•	Countdown timer
	•	Terminal binary animation
	•	Full screen console display

This component is cosmetic and does not affect installation functionality.

⸻

Logging System

All output from the script is automatically logged.

Log location:

~/.local/share/installer_logs/

Example log file:

installer_20260329_031523.log

The log records:
	•	Download activity
	•	Installation messages
	•	Error messages
	•	Checksums
	•	Device detection results

⸻

Ventoy Installation Block

The script automatically downloads the latest Ventoy release directly from the official GitHub API.

Ventoy allows multiple ISO files to be placed on a USB drive and booted directly without needing to rewrite the USB each time.

Ventoy files are stored in:

~/Ventoy/

This block performs:
	1.	Query GitHub for latest release
	2.	Download the Linux tar archive
	3.	Extract the package
	4.	Display available USB devices

Note:
The script does not automatically install Ventoy to a USB device.
This is intentional to prevent accidental drive formatting.

⸻

ISO Download Block

The installer downloads several operating system images.

Default images included:

OS	Purpose
Tails	Privacy-focused live OS
Ubuntu Touch	Mobile-focused Linux environment
Android x86	Android desktop environment

ISO files are stored in:

~/ISOs/

The script retries downloads automatically if a connection error occurs.

⸻

Error Handling & Verification

After downloads complete, the script performs a verification pass.

For each ISO file it will:
	1.	Confirm the file exists
	2.	Generate a SHA256 checksum
	3.	Print the checksum to the log

This helps verify download integrity.

⸻

Requirements

The script requires the following utilities:

bash
curl
tar
sha256sum
lsblk
tput
tee

These tools are available by default on most Linux systems including:
	•	Tails
	•	Ubuntu
	•	Debian
	•	Kali
	•	Arch

⸻

Usage

Make the script executable:

chmod +x ghost_protocol_installer.sh

Run the installer:

./ghost_protocol_installer.sh


⸻

Output Structure

After running, your system will contain:

~/Ventoy/
    ventoy.tar.gz
    ventoy-x.x.xx/

~/ISOs/
    tails-amd64.iso
    ubuntu-touch-xenial.iso
    android-x86.iso

~/.local/share/installer_logs/
    installer_timestamp.log


⸻

Safety Notes

This script does not automatically write to USB drives.

USB devices are only detected and displayed so the user can manually confirm the correct device before installing Ventoy.

This design helps prevent accidental disk formatting.

⸻

Troubleshooting

Check the log file if any step fails:

~/.local/share/installer_logs/

Common issues include:
	•	network connection problems
	•	interrupted downloads
	•	missing system utilities

⸻

Customization

Additional ISO images can be added by editing the ISOS array in the script.

Example:

declare -A ISOS=(
  [Tails]="URL"
  [UbuntuTouch]="URL"
  [AndroidX86]="URL"
  [Kali]="URL"
)


⸻

License

This script is provided as-is for educational and personal use.

Use carefully when working with storage devices.

⸻

Author Notes

The installer is structured in modular blocks so additional functionality can easily be added, such as:
	•	automatic Ventoy USB installation
	•	automatic ISO transfer to USB
	•	expanded operating system libraries
	•	enhanced error diagnostics
