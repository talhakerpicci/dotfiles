## Setting up the drivers

1) Install nvidia and xorg-xrandr packages
2) Edit /usr/share/X11/xorg.conf.d/10-nvidia-drm-outputclass.conf with following:

```
/etc/X11/xorg.conf.d/10-nvidia-drm-outputclass.conf

Section "OutputClass"
    Identifier "intel"
    MatchDriver "i915"
    Driver "modesetting"
EndSection

Section "OutputClass"
    Identifier "nvidia"
    MatchDriver "nvidia-drm"
    Driver "nvidia"
    Option "AllowEmptyInitialConfiguration"
    Option "PrimaryGPU" "yes"
    ModulePath "/usr/lib/nvidia/xorg"
    ModulePath "/usr/lib/xorg/modules"
EndSection
```

3) If using sddm, edit /usr/share/sddm/scripts/Xsetup with the following:

```
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
```

4) To fix screen tearing, add `nvidia-drm.modeset=1` kernel parameter.

```
cd /etc/default
mc grub
# Change following:
GRUB_CMDLINE_LINUX_DEFAULT="..... nvidia-drm.modeset=1"
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

5) Reboot
