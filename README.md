# Remote Ubuntu Workstation Setup Guide

Welcome to the setup guide for establishing remote access to an Ubuntu workstation. This configuration allows you to work seamlessly using a macOS or Windows client via TeamViewer.

---

## Prerequisites

Before you begin, ensure you have the following:
* **Host Machine:** An Ubuntu workstation with internet access and `sudo` privileges.
* **Client Machine:** A macOS or Windows computer.
* **Account:** A valid email address to create a TeamViewer account.

---

## Phase 1: Host Setup (Ubuntu)

### 1. Install TeamViewer
Open your terminal and run the following commands to download and install the official package:

```bash
# Download the latest 64-bit TeamViewer package
wget https://download.teamviewer.com/download/linux/teamviewer_amd64.deb

# Install the package and resolve dependencies
sudo apt update
sudo apt install ./teamviewer_amd64.deb
```
## 2. Disable Wayland (Crucial for Remote Control)

Ubuntu uses Wayland by default, which restricts remote mouse and keyboard inputs. You must switch to Xorg:

```bash
# Open the display manager configuration
sudo nano /etc/gdm3/custom.conf
```
Find the line ``#WaylandEnable=false``
Remove the ``#`` to uncomment it (``WaylandEnable=false``)
Save the file (``Ctrl+O``, ``Enter``) and exit (``Ctrl+X``).

```bash
# Restart the display manager to apply changes (Note: This will log you out!)
sudo systemctl restart gdm3
```
## 3. Configure TeamViewer Account & Unattended Access
Launch TeamViewer from your Ubuntu application menu and follow these steps:

1. Accept the EULA and DPA prompts.

2. **Account Selection**: When prompted to select your usage type, strictly choose **Private Account (Personal/Non-Commercial Use)**.

   💡 Note: Selecting the private account option ensures the best, uninterrupted experience for personal GitHub repository development and prevents           commercial usage timeouts.

3. Go to **Settings (Gear Icon) > Security**.

4. Under **Personal password (for unattended access)**, set a strong password.

5. Check **Start TeamViewer with system** to ensure access after reboots.

6. Copy your **TeamViewer ID** (you will need this to connect).
---

## Phase 2: Client Setup (macOS & Windows)
### For macOS Users

1. Download the macOS ``.dmg`` installer from the [TeamViewer Download Page](https://www.teamviewer.com/en/download/macos/).

2. Install the application and launch it.

3. Log in using the **same Private Account** created during the Ubuntu setup.

4. Navigate to the **Control Remote Computer** (or Partner ID) field.

5. Enter your Ubuntu workstation's **TeamViewer ID** and click **Connect**.

6. Enter your unattended access password.

### For Windows Users
1. Download the Windows ``.exe`` installer from the [TeamViewer Download Page](https://www.teamviewer.com/en/download/windows/).

2. Run the installer, select **Default Installation**, and explicitly choose **Personal/Non-commercial use**.

3. Launch TeamViewer and log in with your **Private Account**.

4. Enter the **Partner ID** of your Ubuntu workstation.

5. Click **Connect** and enter your unattended access password.
