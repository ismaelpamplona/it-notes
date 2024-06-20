# Arch Linux - Installation notes and packages to install

## arch linux install lvm on luks
1. Watch "[1e] | LVM on LUKS Encryption Install" on YouTube: [https://youtu.be/kD3WC-93jEk](https://youtu.be/kD3WC-93jEk)
2. same channel video install most recent
3. ddg search arch Linux install lvm on luks
4. arch wiki luks

### Set the console keyboard layout

```
localectl list-keymaps | grep br
```
- Razer Blade Stealth 2018: `br-latin1-us`

### Partition the disks
- `cfdisk`
- UEFI with GPT
- Mount point Partition type Suggested size
- `/mnt/boot` EFI system partition 500M
- `/mnt Linux x86-64 root` (/) Remainder of the device

```bash
cryptsetup luksFormat /dev/sda2
cryptsetup open /dev/sda2 cryptlvm
pvcreate /dev/mapper/cryptlvm
vgcreate vg /dev/mapper/cryptlvm
lvcreate -l 100%FREE vg -n root
mkfs.fat -F 32 /dev/efi_system_partition
mkfs.ext4 /dev/vg/root
mount /dev/vg/root /mnt
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
```

## Installation

### Select the mirrors

```bash
reflector -c Brazil -c "United States" --verbose --latest 50 --protocol https --sort rate --save
/etc/pacman.d/mirrorlist

/etc/pacman.conf
ParallelDownloads = 6
[multilib]
Include = /etc/pacman.d/mirrorlist
```

### Install essential packages [pacstrap list](#pacstrap-list)

```bash
pacstrap /mnt (packages from pacstrap list)
```

## Configure the system

### Chroot
- after chroot: reflector/paralleldownloads ## Installation ## Select the mirrors

### Time zone
```bash
timedatectl list-timezones | grep Sao_Paulo
```

### Localization

``` bash
/usr/share/kbd/consolefonts/

/etc/vconsole.conf
KEYMAP=br-abnt2
FONT=iso01-12x22
```

### Network configuration

```
/etc/hosts
127.0.0.1   localhost
::1         localhost
127.0.1.1   myhostname
```
### install extra packages [pacman list](#pacman-list-1)
```bash
pacman -Syu (packages from pacman list)
```
### Before [Initramfs](#initramfs)

```bash
/etc/mkinitcpio.conf
HOOKS=(base udev autodetect keyboard keymap consolefont modconf block encrypt lvm2 filesystems fsck)
```

### Initramfs
```bash
mkinitcpio -P
```

### Boot loader

```bash
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB

blkid
copy uuid of /dev/sda2 (encrypted partition)

/etc/default/grub
GRUB_CMDLINE_LINUX="cryptdevice=UUID=device-UUID:cryptlvm root=/dev/MyVolGroup/root"

grub-mkconfig -o /boot/grub/grub.cfg
```
### before [Reboot](#reboot)

```bash
systemctl enable NetworkManager
systemctl enable cups
```

## Reboot

### Users and groups
```bash
list shells /etc/shells
useradd -m user-name -s /bin/zsh
passwd user-name
gpasswd -a user-name wheel
visudo
```

- swapfile arch wiki


- [https://wiki.archlinux.org/title/Zsh](https://wiki.archlinux.org/title/Zsh)
- [https://archlinux.org/packages/extra/any/grml-zsh-config/](https://archlinux.org/packages/extra/any/grml-zsh-config/)

### Install paru [aur list](#aur-packages)

``` bash
pacman -Syu && paru -Syu (packages from aur list)
```

lock screen (sflock)
- [https://wiki.archlinux.org/title/Laptop](https://wiki.archlinux.org/title/Laptop)
- [https://wiki.archlinux.org/title/Power_management#Power_management_with_systemd](https://wiki.archlinux.org/title/Power_management#Power_management_with_systemd)
- [https://wiki.archlinux.org/title/Power_management#Suspend_and_hibernate](https://wiki.archlinux.org/title/Power_management#Suspend_and_hibernate)

- touchpad touch click
- mouse revert scroll
- [https://wiki.archlinux.org/title/List_of_applications](https://wiki.archlinux.org/title/List_of_applications)
- Arch Linux Monthly Install: January 2022 : https://youtu.be/7btEUHjECAo

### Others
- dropbox
- keepassxc
- load backup
- .bashrc install cli programs (zsh)
- vimrc install plugins
- kalu for check updates
- script reflector autoRun daily
- [https://wiki.archlinux.org/title/Uncomplicated_Firewall](https://wiki.archlinux.org/title/Uncomplicated_Firewall)
- [https://github.com/sahib/rmlint](https://github.com/sahib/rmlint)
- [https://github.com/lahwaacz/Scripts/blob/master/rmshit.py](https://github.com/lahwaacz/Scripts/blob/master/rmshit.py)
- [https://borgbackup.readthedocs.org/en/stable/](https://borgbackup.readthedocs.org/en/stable/)
- [https://wiki.archlinux.org/title/List_of_applications](https://wiki.archlinux.org/title/List_of_applications)

### First shred the disk using the shred tool:
```
shred -v -n1 /dev/sdX
```

## Packages

### pacstrap list

- base
- base-devel
- linux
- linux-headers
- linux-firmware
- lvm2
- networkmanager
- network-manager-applet
- vim
- neovim
- nano
- man-db
- man-pages
- texinfo
- intel-ucode
- mtools
- dosfstools
- gvfs
- openssh
- reflector
- rsync
- alacritty
- tmux
- sudo
- zsh
- zsh-completions
- bash-completion
- kbd
- git
- xdg-utils
- xdg-user-dirs

### pacman list 1

- grub
- efibootmgr
- dialog
- os-prober
- sof-firmware
- alsa-utils
- alsa-plugins
- alsa-firmware
- alsa-ucm-conf
- pulseaudio
- pulseaudio-alsa
- pulseaudio-bluetooth
- pulseaudio-equalizer
- pulseaudio-jack
- pulseaudio-lirc
- pulseaudio-zeroconf
- bluez
- bluez-utils
- pulseaudio-bluetooth
- avahi
- nss-mdns
- cups
- mesa
- lib32-mesa
- xf86-video-intel
- vulkan-intel
- mesa-utils
- htop
- wget
- pcmanfm
- fzf
- rg
- maim
- exa
- bat
- xclip
- fd
- rmtrash
- libreoffice-fresh
- libreoffice-extension-texmaths
- libreoffice-extension-writer2latex
- hunspell
- hunspell-en_us
- hyphen
- hyphen-en
- libmythes
- mythes-en
- firefox

### pacman dwm

- xorg
- xorg-xinit
- xorg-xrandr
- xorg-xsetroot
- xorg-xlsfonts
- xorg-xev
- pamixer
- nitrogen
- libinput
- picom
- sxhkd
- brightnessctl
- acpi

### aur packages

- apulse
- brave-bin
- librewolf-bin
- asdf-vm
- mons
- hunspell-pt-br
- hyphen-pt-br
- mythes-pt-br
- libreoffice-extension-languagetool

### fonts pacman

- search for nerd-fonts
```bash
pacman -Ssq nerd-fonts
```

- nerd-fonts-complete
- ttf-caladea
- ttf-carlito
- ttf-dejavu
- ttf-liberation
- ttf-linux-libertine-g
- ttf-inconsolata
- ttf-font-awesome
- noto-fonts
- noto-fonts-emoji
- adobe-source-code-pro-fonts
- adobe-source-sans-fonts
- adobe-source-serif-fonts


### fonts aur

- ttf-gentium-basic
- ttf-ms-fonts
- ttf-twemoji-color

### optional packages (pacman)

- starship
- zathura
- mupdf

## References:

1. [https://unix.stackexchange.com/questions/587630/how-to-install-packages-with-pacman-from-a-list-contained-in-a-text-file#587698](https://unix.stackexchange.com/questions/587630/how-to-install-packages-with-pacman-from-a-list-contained-in-a-text-file#587698)