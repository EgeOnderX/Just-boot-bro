# Just-boot-bro

> **No kernel. No systemd. No bloat. Just boot.**

Welcome to the ultimate exercise in low-level minimalism. This repository contains the absolute smallest bootable artifacts possible in the x86 computing universe. When executed, these images trick the hardware into a hardware-level infinite loop (`jmp $`). Your emulator will boot into a black screen and utilize 100% of a single CPU core.

---

## The Lineup

| Name | File Size | Medium Type | QEMU | VirtualBox | Architectural Method |
| :--- | :--- | :--- | :---: | :---: | :--- |
| **1: mini theoretical** | **32 KB** | CD-ROM (`.iso`) | Yes | No | Exploits the ISO 9660 System Area. Pure hybrid hack. |
| **2: mini vbox theoretical** | **36 KB** | CD-ROM (`.iso`) | Yes | Yes | Satisfies VirtualBox's strict ISO 9660 & El Torito bureaucracy. |
| **3: mini** | **512 Bytes** | Hard Disk (`.img`) | Yes | Yes | Pure hardware baseline. No file system overhead. |

---

## One-Line Generation (Windows PowerShell)

Paste these commands into PowerShell to generate the artifacts directly on your Desktop:

### 1: mini theoretical (32 KB ISO)
```powershell
$b = New-Object byte[] 32768; $b[0] = 0xeb; $b[1] = 0xfe; $b[510] = 0x55; $b[511] = 0xaa; [System.IO.File]::WriteAllBytes("$HOME\Desktop\mini_theoretical.iso", $b)
```
### 2: mini vbox theoretical (36 KB ISO)
```PowerShell
$b = New-Object byte[] 36864; $b[0] = 0xeb; $b[1] = 0xfe; $b[510] = 0x55; $b[511] = 0xaa; $b[32768] = 0x01; $b[32769] = 0x43; $b[32770] = 0x44; $b[32771] = 0x30; $b[32772] = 0x30; $b[32773] = 0x31; $b[32774] = 0x01; $b[34816] = 0x00; $b[34817] = 0x45; $b[34818] = 0x4c; $b[34819] = 0x20; $b[34820] = 0x54; $b[34821] = 0x4f; $b[34822] = 0x52; $b[34823] = 0x49; $b[34824] = 0x54; $b[34825] = 0x4f; $b[34826] = 0x20; $b[34827] = 0x55; $b[34828] = 0x50; $b[34829] = 0x45; $b[34830] = 0x43; $b[34831] = 0x49; $b[34832] = 0x46; $b[34833] = 0x49; $b[34834] = 0x43; $b[34835] = 0x41; $b[34836] = 0x54; $b[34837] = 0x49; $b[34838] = 0x4f; $b[34839] = 0x4e; [System.IO.File]::WriteAllBytes("$HOME\Desktop\mini_vbox_theoretical.iso", $b)
```
### 3: mini (512 Byte IMG)
```PowerShell
$b = New-Object byte[] 512; $b[0] = 0xeb; $b[1] = 0xfe; $b[510] = 0x55; $b[511] = 0xaa; [System.IO.File]::WriteAllBytes("$HOME\Desktop\mini.img", $b)
```
## How to Run

### Via QEMU
```bash
qemu-system-x86_64 -cdrom mini_theoretical.iso
# OR
qemu-system-x86_64 -hda mini.img
```
## LICENSE

Copyright (c) 2026 Ege Önder

This project is completely free, open to the public, and anyone is allowed to use, copy, modify, or distribute it without any restrictions.

## DISCLAIMER

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES, OR OTHER LIABILITY ARISING FROM, OUT OF OR IN CONNECTION WITH THIS SOFTWARE.
