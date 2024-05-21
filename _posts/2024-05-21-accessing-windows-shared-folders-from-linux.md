---
layout: post
title: Accessing Windows Shared Folders From Linux
date: 2023-08-30 15:09:00
description: Accessing Windows shared folders from Linux
tags: how-to
categories: how-to
featured: false
---

Accessing Windows shared folders from Linux involves using the Samba (SMB) protocol, which allows interoperability between Linux/Unix servers and Windows-based clients. Here’s a step-by-step guide to access Windows shared folders from a Linux machine:

### Method 1: Using File Manager

Most modern Linux distributions come with file managers that support browsing SMB shares directly.

1. **Open your File Manager:**
   - For example, if you are using GNOME, open the Nautilus file manager.
   - In KDE, use Dolphin.

2. **Connect to the Server:**
   - In Nautilus, go to `Other Locations` and enter `smb://<windows_ip_address>/<shared_folder_name>`.
   - In Dolphin, use the address bar and enter `smb://<windows_ip_address>/<shared_folder_name>`.

3. **Authentication:**
   - If the shared folder requires authentication, you will be prompted to enter your username and password.

### Method 2: Using the Command Line

You can use the `smbclient` tool or mount the share using `cifs` filesystem.

#### Using `smbclient` (for browsing and accessing files)

1. **Install smbclient:**
   ```bash
   sudo apt-get install smbclient    # Debian/Ubuntu
   sudo yum install samba-client     # CentOS/RHEL
   sudo dnf install samba-client     # Fedora
   ```

2. **Access the Shared Folder:**
   ```bash
   smbclient //windows_ip_address/shared_folder -U username
   ```

   - Replace `windows_ip_address` with the IP address of the Windows machine.
   - Replace `shared_folder` with the name of the shared folder.
   - Replace `username` with your Windows username.

3. **Browse the Share:**
   - After entering your password, you will be in the smbclient interactive shell, where you can use commands like `ls`, `cd`, `get`, and `put` to interact with files.

#### Using `cifs` (for mounting the share)

1. **Install cifs-utils:**
   ```bash
   sudo apt-get install cifs-utils    # Debian/Ubuntu
   sudo yum install cifs-utils        # CentOS/RHEL
   sudo dnf install cifs-utils        # Fedora
   ```

2. **Create a Mount Point:**
   ```bash
   sudo mkdir /mnt/windows_share
   ```

3. **Mount the Share:**
   ```bash
   sudo mount -t cifs //windows_ip_address/shared_folder /mnt/windows_share -o username=windows_username,password=windows_password,workgroup=WORKGROUP
   ```

   - Replace `windows_ip_address` with the IP address of the Windows machine.
   - Replace `shared_folder` with the name of the shared folder.
   - Replace `windows_username` and `windows_password` with your Windows credentials.
   - Replace `WORKGROUP` with your network workgroup name if different.

4. **Access the Mounted Share:**
   - Now you can access the shared folder at `/mnt/windows_share`.

5. **Unmount the Share:**
   ```bash
   sudo umount /mnt/windows_share
   ```

### Method 3: Permanent Mount via fstab

1. **Edit fstab File:**
   ```bash
   sudo nano /etc/fstab
   ```

2. **Add an Entry:**
   ```plaintext
   //windows_ip_address/shared_folder /mnt/windows_share cifs username=windows_username,password=windows_password,workgroup=WORKGROUP,iocharset=utf8,sec=ntlm 0 0
   ```

3. **Mount All Filesystems:**
   ```bash
   sudo mount -a
   ```

   - This ensures the shared folder is mounted automatically at boot.

By following these steps, you should be able to access Windows shared folders from your Linux machine easily.