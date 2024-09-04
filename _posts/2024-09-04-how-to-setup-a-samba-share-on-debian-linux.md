---
title: How to setup a Samba share on Debian Linux
categories:
  - Docs
tags:
  - Debian
  - Linux
---

Setting up a Samba share on Debian Linux allows you to share files across different operating systems within your local network. This is useful in both homelabs and work environments when you want to move files between machines without using a cloud service or local network attached storage. For example, I use Samba to share useful files and scripts from the Public folder in my Home directory.

Here's a step-by-step guide to get you started:

### 1. Install Samba
First, you need to install Samba. Open a terminal and run:
```bash
sudo apt-get update
sudo apt-get install samba
```

### 2. Configure Samba
Next, you'll need to configure Samba. Open the Samba configuration file:
```bash
sudo nano /etc/samba/smb.conf
```
Add the following lines at the bottom of the file to create a new share called "public":
```ini
[public]
   comment = My Samba Share
   path = /home/username/Public
   read only = no
   browsable = yes
```
Replace `/home/username/Public` with the path to the directory you want to share.

### 3. Create the Shared Directory
Create the directory you specified in the configuration file. On some distributions, this folder may already exist:
```bash
mkdir -p /home/username/Public
```

### 4. Set Permissions
Set the appropriate permissions for the shared directory:
```bash
sudo chown -R $USER:$USER /home/username/Public
sudo chmod -R 755 /home/username/Public
```

### 5. Restart Samba
Restart the Samba service to apply the changes:
```bash
sudo systemctl restart smbd
```

### 6. Set Up Samba User
Create a Samba user and set a password. Note that Samba users are separate from system accounts:
```bash
sudo smbpasswd -a username
```

### 7. Access the Share
You can now access the Samba share from other devices on your network. On Windows, open File Explorer and enter:
```
\\your-ip-addr\Public
```
On GNOME, open the file manager, click "Other Locations," and enter:
```
smb://your-ip-addr/Public
```
You can also use your machine name or even a domain name instead of your IP address.

This should get your Samba share up and running! There are a lot of options if you want to get granular with how you share files and with whom. I recommend taking a look at the [SambaWiki](https://wiki.samba.org/index.php/Setting_up_Samba_as_a_Standalone_Server) for advanced configurations.
