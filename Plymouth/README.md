# Xfce4 Windows 95 Anti-Rice
> [!NOTE]
> This is a very rough draft of what will eventually be instructions on how to rice your desktop to get it to look as close to Windows 95 as possible. It is still very much a work in progress that I can only pursue in my limited free time, so please be patient.

Previous: <sup>link</sup>Theming LightDM<sup>/link</sup>
### Step 3: Enabling splash screens with Plymouth, and setting the Windows 95 splash screen
Plymouth is a program that can replace the typical wall of scrolling text you see when you boot Linux up with a splash animation. You need to make sure you append `splash` to your kernel parameters in order to see a splash animation. I use `quiet` as well.

First, let's set our kernel build hooks. I use `mkinitcpio`, so I'll deal with that first:

```
sudo nano /etc/mkinitcpio.conf
```
```
...
HOOKS=(... systemd ... plymouth ... crypt ...)
...
```
You may not use the `systemd` and/or `crypt` hooks. If you don't, ignore them. If you do, `plymouth` needs to be placed after `systemd` and before `crypt` if you're using `dm-crypt` for encryption.

If you're using `dracut` for your initramfs generator, it should automatically detect Plymouth and add it to your images. If that fails, you can force inclusion:
```
sudo nano /etc/dracut.conf.d/myflags.conf
```
```
...
add_dracutmodules+=" plymouth "
...
```
Next, we'll have to add the relevant kernel parameters. The procedure for this differs depending on how you boot. For example, I use a Unified Kernel Image. I'm going to link to the Arch (btw) Wiki on how to edit kernel parameters:\
- [Unified Kernel Image](https://wiki.archlinux.org/title/Unified_kernel_image#Kernel_command_line)
- [systemd-boot](https://wiki.archlinux.org/title/Kernel_parameters#systemd-boot)
- [GRUB](https://wiki.archlinux.org/title/Kernel_parameters#GRUB)
- [rEFInd](https://wiki.archlinux.org/title/Kernel_parameters#rEFInd)
- [Syslinux](https://wiki.archlinux.org/title/Kernel_parameters#Syslinux)
- [GRUB Legacy](https://wiki.archlinux.org/title/Kernel_parameters#GRUB_Legacy)
- [LILO](https://wiki.archlinux.org/title/Kernel_parameters#LILO)
- [EFISTUB](https://wiki.archlinux.org/title/EFISTUB#Using_UEFI_directly) *NOTE: you will need `efibootmgr` or UEFI Shell v2. If using `efibootmgr`, [auto-UEFI-entry](https://github.com/de-arl/auto-UEFI-entry) can help.*

Next, we're going to aim for as smooth a transition as possible from Plymouth to LightDM. To do that, we're going to need to use a drop-in snippet for our `display-manager.service`:
```
sudo nano /etc/systemd/system/display-manager.service.d/plymouth.conf
```
```
[Unit]
Conflicts=plymouth-quit.service
After=plymouth-quit.service rc-local.service plymouth-start.service systemd-user-sessions.service
OnFailure=plymouth-quit.service

[Service]
ExecStartPost=-/usr/bin/sleep 30
ExecStartPost=-/usr/bin/plymouth quit --retain-splash
```
Now, we're going to once again refer to [these instructions](https://github.com/grassmunk/Chicago95/tree/master/Plymouth) on the Chicago95 repo that we cloned earler. We're going to ignore `RetroTux`.

If you use `mkinitcpio` to generate your unified kernel images, it will automatically regenerate your images after you set your default Plymouth theme.

End of content for now.
