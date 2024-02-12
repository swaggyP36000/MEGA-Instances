# MEGA-Instances

**This fork ONLY exists to add a Usage and Troubleshooting sections to the ReadMe (below Installation), and this is mostly done for personal use since I doubt many people will see this fork of it. It is far easier to compile and use this if you are on Arch Linux or an Arch-based distro that supports the AUR, etc. I would highly recommend finding the official package on a GUI application like pamac.**

This script will help you running multiple MEGA (megasync) instances on Linux.
Make sure megasync is installed before your first use of this script.
Dependencies:
  - megasync
  - zenity

## Images
![System tray](img/tray.png?raw=true "System tray")
![File manager](img/file-manager.png?raw=true "File manager")

## Installation
```bash
sudo wget -O /usr/bin/megasync-instances https://raw.githubusercontent.com/NicoVarg99/MEGA-Instances/master/mega_instances.sh
sudo chmod 755 /usr/bin/megasync-instances
megasync-instances
```
Arch Linux users can install the package directly from AUR ([megasync-instances](https://aur.archlinux.org/packages/megasync-instances))

## Usage

**PLEASE MAKE SURE YOU DO NOT HAVE EXISTING SYNCS/BACKUPS BECAUSE ON THE FIRST RUN THIS WILL DELETE THEM.** Also, to prevent errors down the line, it is recommended that you sign out of your existing MEGA instances, and disable them from starting at startup/login. You can do this in the Gnome DE by going to the Tweaks app and removing it from the Startup Applications section. In other DEs, I would recommend removing/disabling MEGA's startup through Stacer.

1. When you run `megasync-instances`, you will be asked how many instances you want (how many accounts do you want to sign into?). *This isn't a set amount, you can add/remove them later*
2. Next, it will ask you to name your instances. For ease of access, use names that make it easy to identify which folders match with which account (for example, don't just name them 1 and 2)
3. Next it will walk you through signing in and syncs/backups. **Don't skip the steps or megasync-instances will assume you're done and try to move forward, and although you can still sign in and finish setting up for an individual account later, it's easier if you just do it on setup**
4. Once you are done, it will relaunch both instances. **If you use Stacer, please go to its Startup Apps section and make sure the "megasync_instances" option is enabled.**
5. **To add more accounts later**, in the same directory where it created folders for your first two accounts (if you are unsure of where, run `megasync-instances` in terminal and see the output directories), make a new folder, name it to whatever you want, same as you did in Step 2. Close out of all MEGA instances and run `megasync-instances` again. If all goes well, you will see a new login prompt because it detected the new folder.
6. For the new account, if it doesn't automatically detect the folder you created as the sync location, you can point it there yourself and it will remember.

*If you have any further comment or findings while using this program, please let me know and I will update this section*

## Troubleshooting

This program seems to be very buggy. Here are some common-ish bugs and how to solve them. *Feel free to create an issue if you've seen more, with the steps to fix, and I will add them here as well*
- **"Unknown drive path" error** - I spent hours trying to find a fix for this without setting up my instances again. If this error occurs with one or more of your instances, re-do your megasync-instances setup. **Rename your `~/MEGA` folder to anything else so the program won't automatically delete it. When megasync-instances makes a new MEGA folder, copy everything out of the old folder and paste it into the new one. Merge all files, skip all duplicates.
- **Crash when clicking settings** - this is an issue with MEGA on all recent versions (at least when using with megasync-instances). Wait until all files are synced, then open settings and make changes as you need to.
- **MEGA app randomly re-added to startup apps** - what I realized is megasync-instances works better if you don't actually have MEGA installed prior to using the tool. If you do, uninstall it. When installing megasync-instances, it will prompt you to choose a provider version of MEGAsync. This is a slightly better way to make sure everything works as intended. Alternatively, you can opt to keep the original MEGA app intalled, *so long as you sign out of the app and remove its startup from both Stacer and the Tweaks app so it has no reason to start on launch* (optionally, check to see if MEGA settings has an option start on launch checked, and un-check that.

## Uninstallation
#### Close all instances
```bash
killall megasync
```
#### Remove script
```bash
rm ~/.config/autostart/mega_instances.desktop
rm ~/.config/megasync-instances/status
sudo rm /usr/bin/megasync-instances
```
#### Remove all instances
```bash
rm -rf ~/MEGA/*
```
