root@msi:~# sudo apt update
Hit:1 https://dl.google.com/linux/chrome/deb stable InRelease
Hit:2 http://archive.ubuntu.com/ubuntu noble InRelease                                              
Hit:3 http://security.ubuntu.com/ubuntu noble-security InRelease                                    
Hit:4 http://archive.ubuntu.com/ubuntu noble-updates InRelease                                      
Hit:5 http://archive.ubuntu.com/ubuntu noble-backports InRelease              
Ign:6 http://packages.linuxmint.com zena InRelease      
Hit:7 http://packages.linuxmint.com zena Release
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
All packages are up to date.
root@msi:~# sudo apt --fix-broken install -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
root@msi:~# sudo apt full-upgrade --fix-missing -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
root@msi:~# sudo apt dist-upgrade -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
root@msi:~# sudo apt autoremove -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
root@msi:~# # Display Timeshift configuration to identify the target UUID
cat /etc/timeshift.json | grep -E "backup_device_uuid|snapshot_device_uuid"

# Correlate UUID to partition name
lsblk -o NAME,UUID,MOUNTPOINT,SIZE
cat: /etc/timeshift.json: No such file or directory
NAME                UUID                                   MOUNTPOIN   SIZE
sda                                                                  978.1G
├─sda1              C535-0B9E                              /boot/efi   512M
├─sda2              a95c5aa2-ff4d-4869-88d0-79a55146c509   /boot       1.7G
└─sda3              9d591bba-e650-4c5b-b6d4-d91db2fa8291             975.9G
  └─sda3_crypt      K01bs6-uS6O-3PZD-rroa-7K3C-8egq-fqlh6D           975.9G
    ├─vgmint-root   b19f9559-7eb3-45aa-9f17-eabcc2b48784   /         929.4G
    └─vgmint-swap_1 3a52dd97-4f39-434d-b0ac-fdb43ac52f69   [SWAP]      1.9G
root@msi:~# # 1. Remove Timeshift and purge configuration files
apt remove --purge timeshift -y

# 2. Clean up any unused dependencies
apt autoremove -y

# 3. Verify removal (Should return empty/not found)
which timeshift
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package 'timeshift' is not installed, so not removed
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
root@msi:~# 


