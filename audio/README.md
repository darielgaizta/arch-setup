# How to Setup Audio

## General

Somehow my audio works fine in all parts after my first install. Maybe I installed `pipewire` or something similar during the Arch installation. I can listen to music or watch movies with my laptop's speaker and my headphone through Bluetooth, except the wired one.

## Troubleshoot

### Wired Device Issue (e.g. Headhone, Earphone, Speaker, etc.)

I encountered an issue where my audio is broken. It sounds smaller, robotic, and any worse sound you can imagine. So, to fix this, I created a `disable-hda-powersave.conf` file with the following content:

```
options snd_hda_intel power_save=0 power_save_controller=N
```

The audio is broken because there is a "power-saving" feature for HDA (High Definition Audio) that prevents your audio to sound well. We just need to disable it so your audio can perform at its best.

The `disable-hda-powersave.conf` file only works after a reboot, not at the first boot. So every time you shut down your PC, the audio will break and you need to reboot to fix it. Weird? Yes. All you need to do is to run this command:

```
mkinitcpio -P
```

It will create a new initramfs image so your PC will boot with the new configuration.

#### NOTE

Just to give you an introduction based on my understanding, there is a process running before your PC is booted and it's called **initramfs** (before, it was "initrd"). It is an image (like Docker image) stored in `/boot` directory and it is used to load a temporary root filesystem to the RAM or system memory. By running the command `mkinitcpio -P`, we basically create a new image of initramfs with our **snd_hda_intel** configuration (remember that we have configured it earlier in disable-hda-powersave.conf). Why? Because we need this configuration loaded at the very first time and the way is to put it inside the initramfs image.