# Dell-7285-2-in-1-Mac-OS-Monterrey
Working Mac OS Monterrey Dell Latitude 7285 with OpenCore 0.9.3

![About Mac](https://github.com/DanDoren/Dell-7285-2-in-1-Mac-OS-Monterrey/assets/67220648/f472c66a-98d6-495d-9c12-b5feefc7fdf7)

Specifications:
- CPU: Intel Core i7-7Y75 (4M Cache, up to 3.60 GHz)
- RAM: 16GB LPDDR3 - 1866 MHz
- Video: Intel HD 615
- Audio: Realtek ALC3253 (ALC225)
- WiFi&BT: AC 8265 Wi-Fi + BT 4.2 (2x2)

This guide intended only for educational purposes and I'm not responsible for any damage to your laptop.  

Preparation
Enter to BIOS and load DEFAULT Settings then disable and change:
Settings:
- General -> Advanced Boot Options: Clear all
- UEFI Boot Path Security: Always, Except Internal HDD

System Configuration:
- SATA Operation: AHCI

Secure Boot:
- Secure Boot Enable: Disabled

Intel Software Guard Extensions:
- Intel SGX Enable: Disabled

Virtualization Support:
- VT for Direct I/O: Clara all


STEP 1
I Strongly recommend download Monterrey Olarila RAW Image and copy the USB EFI to your USB Installer. 

Here you going to find 2 EFI Folders:
- USB EFI
- USB Post Install

Prepare your USB installer of macOS Monterrey and add this files inside EFI/OC/Tools (you can use Proper tree, OCAT on Windows or OpenCore Configurator on Mac)


*You must do this every time you load Default Setting in BIOS*

Modified GRUB Shell (https://github.com/datasone/grub-mod-setup_var/releases)
ControlMsrE2 (https://github.com/acidanthera/OpenCorePkg/releases)

STEP 2
To set DVMT run Modified GRUB Shell and write:

setup_var 0x795 0x0 --> setup_var 0x795 0x3
setup_var 0x796 0x0 --> setup_var 0x796 0x3

In this case I set the pre-allocated video to max that's why I use 0x3 instead 0x2 in the 2 variables (usually people just change the first variable)


STEP 3
RUN ControlMsrE2.efi and this should provide you one of the following:

CFG-Lock is enabled:
This firmware has LOCKED MSR 0xE2 register!

CFG-Lock is disabled:
This firmware has UNLOCKED MSR 0xE2 register!

STEP 3.1
If your MSR is LOCKED run Modified GRUB Shell and write:

Setup_var 0x4ed 0x0 <-- to disable MSR/CFG lock

This will activate QE/CI graphic acceleration on iGPU


STEP 4
Proceed to install Mac OS on your Dell 7285.
You can make your own EFI or copy mine and it will work.
You must map your USB ports using Hacktool.
