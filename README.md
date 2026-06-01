# Lab: Advanced Recovery and Permanent GRUB Fix in Dual-Boot Environments (Kali Linux / Windows UEFI)

## 📌 Scenario & Challenge
After partition table modifications, the boot manager (GRUB) lost reference to the root filesystem, resulting in the critical boot error: `error: unknown filesystem. grub rescue>`.

**The Extra Challenge:** Initial recovery via the GRUB Rescue CLI restored the boot temporarily, but the error persisted after rebooting. This indicated that the partition table and the firmware boot variables (NVRAM) required a structural, surgical intervention for a 100% permanent consolidation.

## 🎯 Objectives
1. Perform a temporary bypass of the error via the Rescue Prompt.
2. Identify the actual EFI System Partition (ESP).
3. Reinstall GRUB binaries targeted specifically for the UEFI ecosystem.
4. Reprogram the firmware boot order directly via the Linux NVRAM.

## 🚀 Step-by-Step Definitive Troubleshooting

### Phase 1: Temporary Access (Bypass)
Mapping and manual loading of GRUB modules through the Rescue CLI (as documented in the `image_2.png` evidence):

```bash
# Define the partition containing the root filesystem
grub rescue> set root=(hd0,gpt4)

# Set the path to the GRUB configuration directory
grub rescue> set prefix=(hd0,gpt4)/boot/grub

# Load the essential 'normal' boot module
grub rescue> insmod normal

# Trigger the graphical boot menu
grub rescue> normal
