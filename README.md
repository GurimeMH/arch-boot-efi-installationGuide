# Arch Linux Installation with /boot/efi as Boot Point and GRUB Fix

Follow these steps to install Arch Linux and configure GRUB with `/boot/efi` as the boot point and fix grub after installation.

### 1. Boot into Arch Linux Installation Media
Boot your system using the Arch Linux installation media.

### 2. Set Font
```bash
setfont ter-132n
```

### 3. Connect to WiFi (Skip if Using Ethernet)
```bash
iwctl
```
```bash
station wlan0 connect "Wifi name"
```
```bash
"password"
```
```bash
exit
```
```bash
ping google.com
```

### 4. Update Package Database
```bash
pacman -Sy
```

### 5. Install Arch Linux Keyring
```bash
pacman -S archlinux-keyring
```

### 6. See Available Disks
```bash
lsblk
```

### 7. Create Partitions
```bash
cfdisk
```
- Select free space and create 1G EFI System and nG Linux filesystem.
- Write disk and quit.

### 8. Format the Partitions
```bash
mkfs.fat -F32 /dev/nvme0n1pX
```
```bash
mkfs.ext4 /dev/nvme0n1pX
```

### 9. Mount the Partitions
```bash
mount /dev/nvme0n1pX /mnt
```
```bash
mkdir /mnt/boot
```
```bash
mkdir /mnt/boot/efi
```
```bash
mount /dev/nvme0n1pX /mnt/boot/efi
```

### 10. Use Archinstall with Pre-mounted Configuration
```bash
archinstall
```
- When setting up Disk configuration, choose Pre-mounted configuration and type `/mnt`.

### 11. Post-Installation Configuration and Install GRUB
```bash
pacman -Syu
```
```bash
pacman -S grub efibootmgr dosfstools mtools
```
```bash
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=Arch
```
```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

### 12. Shutdown
```bash
shutdown now
```

### 13. Boot to Arch Linux
Enjoy
