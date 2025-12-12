# How to Change Your Computer's Boot Order?

**Last Updated:** 30 Sep, 2025

## Table of Contents
1. [Introduction to Boot Order](#1-introduction-to-boot-order)
   - [1.1 What is Boot Sequence?](#11-what-is-boot-sequence)
   - [1.2 Why Change Boot Order?](#12-why-change-boot-order)
   - [1.3 Common Devices in Boot Sequence](#13-common-devices-in-boot-sequence)

2. [Understanding the Boot Process](#2-understanding-the-boot-process)
   - [2.1 Power-On and POST](#21-power-on-and-post)
   - [2.2 Firmware Initialization](#22-firmware-initialization)
   - [2.3 Boot Device Selection](#23-boot-device-selection)
   - [2.4 Bootloader Execution](#24-bootloader-execution)
   - [2.5 OS Initialization](#25-os-initialization)

3. [Accessing BIOS/UEFI Settings](#3-accessing-biosuefi-settings)
   - [3.1 Common Access Methods](#31-common-access-methods)
   - [3.2 Windows Systems](#32-windows-systems)
   - [3.3 macOS Systems](#33-macos-systems)
   - [3.4 Linux Systems](#34-linux-systems)
   - [3.5 Troubleshooting Access Issues](#35-troubleshooting-access-issues)

4. [Managing Boot Order](#4-managing-boot-order)
   - [4.1 Checking Current Boot Order](#41-checking-current-boot-order)
   - [4.2 Changing Boot Order in UEFI](#42-changing-boot-order-in-uefi)
   - [4.3 Changing Boot Order in Legacy BIOS](#43-changing-boot-order-in-legacy-bios)
   - [4.4 Using Boot Menu](#44-using-boot-menu)
   - [4.5 OS-Level Boot Management](#45-os-level-boot-management)

5. [Troubleshooting](#5-troubleshooting)
   - [5.1 Common Issues and Solutions](#51-common-issues-and-solutions)
   - [5.2 Boot Device Not Found](#52-boot-device-not-found)
   - [5.3 Boot Order Reset Issues](#53-boot-order-reset-issues)
   - [5.4 Secure Boot Problems](#54-secure-boot-problems)
   - [5.5 Advanced Troubleshooting](#55-advanced-troubleshooting)

6. [Best Practices](#6-best-practices)
   - [6.1 Before Making Changes](#61-before-making-changes)
   - [6.2 Security Considerations](#62-security-considerations)
   - [6.3 Performance Optimization](#63-performance-optimization)
   - [6.4 Maintenance and Updates](#64-maintenance-and-updates)

7. [Frequently Asked Questions](#7-frequently-asked-questions)
   - [7.1 General Questions](#71-general-questions)
   - [7.2 Technical Questions](#72-technical-questions)
   - [7.3 Troubleshooting Questions](#73-troubleshooting-questions)
   - [7.4 Advanced Configuration](#74-advanced-configuration)
   - [7.5 Performance Questions](#75-performance-questions)

8. [Appendices](#8-appendices)
   - [8.1 Manufacturer-Specific Information](#81-manufacturer-specific-information)
   - [8.2 Command Reference](#82-command-reference)
   - [8.3 Glossary](#83-glossary)
   - [8.4 Additional Resources](#84-additional-resources)

### 2.1 Power-On and POST

#### Overview
The Power-On Self-Test (POST) is the initial diagnostic testing sequence that runs when a computer is powered on. This critical process verifies that essential hardware components are functioning correctly before the operating system loads.

#### Detailed POST Sequence
1. **Power Supply Check**
   - Verifies stable power delivery
   - Checks voltage levels (3.3V, 5V, 12V rails)
   - Tests power good signal

2. **CPU Initialization**
   - Resets and verifies CPU registers
   - Tests basic instruction set
   - Validates cache memory
   - Verifies clock speed and multiplier

3. **Memory Test**
   - Quick memory check (can be disabled in BIOS)
   - Full memory test (if enabled)
   - Memory module detection
   - Memory mapping and allocation

4. **Hardware Enumeration**
   - Detects and initializes hardware components
   - Assigns system resources (IRQs, DMAs, I/O ports)
   - Creates hardware configuration tables

#### Key Components Tested:
- **CPU**
  - Processor functionality
  - Math coprocessor (if present)
  - Cache memory integrity
  - Clock speed verification

- **Memory (RAM)**
  - Memory module detection
  - Memory integrity check
  - Memory size verification
  - Memory speed configuration

- **Motherboard**
  - Chipset functionality
  - System timer
  - DMA controller
  - Interrupt controller
  - CMOS/RTC battery

- **Storage Devices**
  - Hard drives (SATA, NVMe, M.2)
  - Optical drives
  - USB storage devices
  - RAID controllers

- **Peripherals**
  - Keyboard and mouse
  - Display adapter
  - USB controllers
  - Network interfaces

#### POST Beep Codes (Common)
| Beep Pattern | Possible Issue | Troubleshooting Steps |
|--------------|----------------|-----------------------|
| 1 short beep | Normal POST | System is OK |
| 2 short beeps | POST Error | Check screen for error code |
| Continuous beep | Power supply or system board | Check PSU connections, test with known-good PSU |
| 1 long, 2 short | Display adapter | Reseat graphics card, check monitor connection |
| 1 long, 3 short | Graphics card | Reseat GPU, check power connections |
| Repeating short beeps | Power issue | Check PSU, motherboard power connections |
| 3 long beeps | Keyboard controller | Check keyboard connection, try different port |
| No beep | No power, short circuit | Check power connections, test components individually |

#### Common POST Error Messages
| Error Message | Likely Cause | Solution |
|---------------|--------------|----------|
| CMOS Battery Failure | Dead CMOS battery | Replace CR2032 battery |
| No Boot Device Found | No bootable drive detected | Check drive connections, verify boot order |
| CPU Fan Error | CPU fan not detected or too slow | Check fan connection, clean fan, replace if needed |
| Keyboard Error | Keyboard not detected | Check connection, try different port |
| CMOS Checksum Error | CMOS memory corrupted | Reset BIOS to default settings |
| NVRAM/CMOS Checksum Bad | NVRAM corruption | Reset BIOS, replace CMOS battery |
| System Battery Voltage is Low | CMOS battery voltage low | Replace CR2032 battery |

#### POST Code Indicators
Many motherboards feature a POST code display (2-digit or 4-digit code) that shows the current stage of the boot process. These codes vary by manufacturer but generally follow this pattern:
- **00-0F**: CPU initialization
- **10-1F**: Early chipset initialization
- **20-2F**: Memory detection
- **30-3F**: Memory testing
- **40-4F**: Video initialization
- **50-5F**: I/O device detection
- **60-6F**: Storage device detection
- **70-7F**: Final system initialization

#### Troubleshooting POST Failures
1. **No Power**
   - Verify power cable connection
   - Check PSU switch (if present)
   - Test with known-good power supply
   - Check for short circuits

2. **No Display**
   - Verify monitor is powered on
   - Check video cable connections
   - Try integrated graphics (if available)
   - Test with known-good monitor

3. **Beep Codes**
   - Note the beep pattern
   - Consult motherboard manual
   - Check component connections

4. **Hanging During POST**
   - Remove recently added hardware
   - Reset CMOS settings
   - Check for overheating
   - Test with minimal hardware configuration

### 2.2 Firmware Initialization

#### BIOS vs UEFI: A Detailed Comparison
| Feature | Legacy BIOS | UEFI |
|---------|------------|------|
| **Architecture** | 16-bit Real Mode | 32/64-bit Protected Mode |
| **Boot Process** | MBR-based | GPT-based with UEFI boot manager |
| **Partition Table** | MBR (2.2TB max) | GPT (9.4ZB max) |
| **Secure Boot** | Not available | Supported (prevents unauthorized code execution) |
| **Boot Speed** | Slower (typically 15-30s) | Faster (typically 5-15s) |
| **Drive Support** | Limited to 2.2TB per partition | Virtually unlimited partition size |
| **Network Support** | Limited PXE boot | Advanced network stack with IPv6 |
| **GUI Interface** | Text-based | Graphical with mouse support |
| **CPU Architecture** | x86 only | x86, x86-64, ARM, Itanium |
| **Driver Support** | Option ROMs required | Native driver support (EFI drivers) |

#### Firmware Components

1. **Hardware Detection and Initialization**
   - **Processor Initialization**
     - Detects CPU type and features
     - Sets up CPU microcode updates
     - Configures CPU power management
   
   - **Memory Initialization**
     - Memory controller setup
     - Memory training (DDR4/DDR5)
     - Memory map creation
     - Reserved memory allocation
   
   - **Device Enumeration**
     - PCI/PCIe device discovery
     - USB device detection
     - Storage device initialization
     - Graphics card initialization

2. **Configuration Management**
   - **CMOS/NVRAM**
     - Stores system configuration
     - Maintains real-time clock
     - Preserves settings when powered off
   
   - **UEFI Variables**
     - Boot order settings
     - Secure Boot keys
     - System configuration
     - Boot manager entries

3. **Runtime Services**
   - **Hardware Abstraction**
     - Provides standardized hardware access
     - Abstracts platform-specific details
     - Enables OS independence
   
   - **System Management**
     - Power management
     - Thermal monitoring
     - Fan control
     - Battery management (laptops)

#### UEFI-Specific Features

1. **Secure Boot**
   - Verifies digital signatures of bootloaders
   - Prevents unauthorized code execution
   - Uses PK (Platform Key), KEK (Key Exchange Key), and db/dbx databases

2. **Fast Boot**
   - Skips certain hardware checks
   - Caches hardware information
   - Reduces boot time significantly

3. **CSM (Compatibility Support Module)**
   - Allows UEFI to boot in legacy BIOS mode
   - Required for older operating systems
   - Can be disabled for faster boot times

4. **UEFI Shell**
   - Command-line interface
   - Scripting capabilities
   - System debugging tools
   - Firmware updates

#### Firmware Update Process
1. **Preparation**
   - Backup important data
   - Check current firmware version
   - Download correct update package
   - Verify checksum

2. **Update Methods**
   - **BIOS Flash Utility**
     - Bootable USB/DVD
     - DOS-based utilities
   - **UEFI Update Utility**
     - Built-in firmware update tool
     - Windows/Linux update utilities
   - **Vendor-Specific Tools**
     - Manufacturer update software
     - Windows Update integration

3. **Recovery Options**
   - Dual BIOS (on some motherboards)
   - BIOS recovery jumper
   - USB BIOS Flashback (on supported boards)

#### Common Firmware Settings

| Setting | Typical Options | Description |
|---------|-----------------|-------------|
| **Boot Mode** | UEFI, Legacy, UEFI+Legacy | Controls firmware operation mode |
| **Secure Boot** | Enabled, Disabled | Controls signature verification |
| **Fast Boot** | Enabled, Disabled | Skips certain POST tests |
| **CSM** | Enabled, Disabled | Compatibility Support Module |
| **TPM** | Enabled, Disabled | Trusted Platform Module |
| **Virtualization** | VT-x, AMD-V, Disabled | CPU virtualization support |
| **XMP/DOCP** | Profile 1, Profile 2, Disabled | Memory overclocking profiles |
| **SATA Mode** | AHCI, RAID, IDE | Storage controller mode |

#### Troubleshooting Firmware Issues

1. **Common Problems**
   - Failed firmware updates
   - Corrupted settings
   - Hardware detection failures
   - Boot loops

2. **Recovery Methods**
   - Reset to defaults
   - Clear CMOS (jumper/battery)
   - Use backup BIOS (if available)
   - Flash recovery procedure

### 2.3 Boot Device Selection

#### Boot Priority Levels

1. **Primary Boot Device**
   - **Purpose**: First device checked for bootable media
   - **Typical Choices**:
     - Main OS drive (SSD/HDD)
     - NVMe drive (in modern systems)
     - Hardware RAID array (in servers)
   - **Considerations**:
     - Should be the fastest available storage
     - Must contain a valid bootloader
     - Should be reliable and stable

2. **Secondary Boot Device**
   - **Purpose**: Fallback when primary fails
   - **Common Options**:
     - Secondary internal drive
     - Recovery partition
     - External USB drive
   - **Use Cases**:
     - Primary drive failure
     - Corrupted OS
     - Recovery operations

3. **Tertiary Boot Device**
   - **Purpose**: Additional fallback option
   - **Common Choices**:
     - Optical drive (DVD/Blu-ray)
     - USB flash drive
     - SD/microSD card (on some systems)
   - **Usage Scenarios**:
     - OS installation
     - System recovery
     - Diagnostic tools

4. **Network Boot (PXE)**
   - **Purpose**: Boot from network resources
   - **Requirements**:
     - PXE-capable network card
     - DHCP server with PXE options
     - TFTP server with boot files
   - **Enterprise Uses**:
     - Diskless workstations
     - System imaging
     - Remote OS deployment

#### Boot Device Types and Characteristics

| Device Type | Boot Speed | Common Uses | Notes |
|-------------|------------|-------------|-------|
| **NVMe SSD** | Very Fast | Primary OS, Gaming | UEFI required for boot |
| **SATA SSD** | Fast | Primary/Secondary OS | Widely compatible |
| **HDD** | Slow | Secondary storage, Data | Reliable but slower |
| **USB 3.x** | Medium | OS Install, Recovery | Speed varies by drive |
| **Optical** | Very Slow | Recovery, Legacy OS | Becoming obsolete |
| **Network** | Varies | Enterprise deployment | Requires infrastructure |

#### UEFI Boot Process

1. **Firmware Initialization**
   - Loads UEFI drivers
   - Initializes boot services
   - Sets up runtime services

2. **Boot Manager**
   - Reads NVRAM variables
   - Presents boot menu (if configured)
   - Loads selected bootloader

3. **Boot Device Selection**
   - Checks boot order list
   - Scans for bootable devices
   - Validates boot signatures

#### Legacy BIOS Boot Process

1. **POST Completion**
   - Verifies hardware
   - Builds interrupt vector table
   - Initializes BIOS interrupts

2. **Boot Device Polling**
   - Checks boot order
   - Tests devices sequentially
   - Looks for boot signature (55 AA)

3. **Boot Sector Loading**
   - Loads MBR/VBR
   - Executes boot code
   - Passes control to bootloader

#### Boot Device Detection Methods

1. **Automatic Detection**
   - Scans all available buses
   - Identifies bootable devices
   - Creates temporary boot order

2. **Manual Configuration**
   - User-defined boot order
   - Persistent across reboots
   - Stored in NVRAM/CMOS

3. **One-Time Boot Menu**
   - Accessed via function key (F12, F11, etc.)
   - Overrides default boot order
   - No permanent changes

#### Common Boot Device Issues

1. **Device Not Detected**
   - **Causes**:
     - Loose connections
     - Disabled controller
     - Driver issues
   - **Solutions**:
     - Check connections
     - Enable in BIOS/UEFI
     - Update firmware

2. **Boot Failure**
   - **Common Reasons**:
     - Corrupted bootloader
     - Invalid partition table
     - Secure Boot conflict
   - **Troubleshooting**:
     - Verify boot files
     - Check disk integrity
     - Review Secure Boot settings

3. **Slow Boot Times**
   - **Potential Causes**:
     - Too many boot devices
     - Network boot timeout
     - USB device enumeration
   - **Optimizations**:
     - Disable unused boot devices
     - Adjust boot timeouts
     - Update firmware

#### Boot Security Features

1. **Secure Boot**
   - Verifies bootloader signatures
   - Prevents unauthorized code execution
   - Requires UEFI and compatible OS

2. **TPM Integration**
   - Stores encryption keys
   - Enables measured boot
   - Supports BitLocker/full-disk encryption

3. **Password Protection**
   - BIOS/UEFI passwords
   - Boot device passwords
   - HDD passwords

#### Boot Order Management

1. **UEFI Boot Manager**
   - Manage boot entries
   - Set boot order
   - Configure timeouts

2. **Command Line Tools**
   - Windows: `bcdedit`, `bootrec`
   - Linux: `efibootmgr`, `grub-mkconfig`
   - macOS: `bless`, `nvram`

3. **Third-Party Utilities**
   - Boot repair tools
   - Boot managers
   - Recovery software

### 2.4 Bootloader Execution

#### Overview
Bootloaders are specialized programs responsible for loading the operating system kernel into memory and transferring control to it. They act as the bridge between the system firmware and the operating system.

#### Common Bootloaders

| Bootloader | Primary OS | Key Features |
|------------|------------|--------------|
| **Windows Boot Manager** | Windows | Secure Boot support, BCD store, Recovery tools |
| **GRUB2** | Linux | Scriptable, themeable, filesystem awareness |
| **systemd-boot** | Linux | Minimal, UEFI-only, simple configuration |
| **LILO** | Linux | Legacy, simple, MBR-only |
| **boot.efi** | macOS | Apple's EFI implementation, tightly integrated |
| **rEFInd** | Cross-platform | Beautiful GUI, auto-detects OSes, theme support |
| **Clover** | Hackintosh | Modified rEFIt, macOS compatibility |

#### Bootloader Architecture

1. **First-Stage Loader**
   - Typically resides in MBR or ESP (EFI System Partition)
   - Very small (usually < 512 bytes for MBR)
   - Loads the second-stage bootloader

2. **Second-Stage Loader**
   - More feature-rich
   - Handles configuration files
   - Presents boot menu (if configured)

3. **Kernel Loader**
   - Loads the OS kernel into memory
   - Passes necessary parameters
   - Transfers execution to the kernel

#### Bootloader Tasks in Detail

1. **Hardware Initialization**
   - Sets up basic hardware
   - Initializes memory management
   - Configures CPU mode (real/protected/long)

2. **Filesystem Access**
   - Reads configuration files
   - Loads kernel images
   - Accesses initramfs/initrd

3. **User Interface**
   - Presents boot menu
   - Handles user input
   - Displays boot messages

4. **Kernel Loading**
   - Verifies kernel integrity
   - Loads kernel into memory
   - Sets up boot parameters
   - Jumps to kernel entry point

#### Bootloader Configuration

1. **Windows BCD Store**
   - Binary database of boot configuration
   - Managed via `bcdedit.exe`
   - Stores boot entries, settings, and parameters

2. **GRUB Configuration**
   - `/boot/grub/grub.cfg`
   - Generated by `grub-mkconfig`
   - Supports scripting and theming

3. **systemd-boot**
   - Simple configuration files
   - `/boot/loader/entries/`
   - Automatic detection of installed OSes

#### Common Boot Parameters

| Parameter | Purpose | Example |
|-----------|---------|---------|
| `root=` | Specifies root filesystem | `root=/dev/sda1` |
| `ro`/`rw` | Read-only/Read-write root | `ro` |
| `quiet` | Suppresses boot messages | `quiet splash` |
| `splash` | Shows splash screen | `splash` |
| `init=` | Specifies init process | `init=/bin/bash` |
| `single` | Single-user mode | `single` |
| `resume=` | Resume from hibernation | `resume=UUID=...` |

#### Bootloader Security

1. **Secure Boot**
   - Verifies bootloader signatures
   - Prevents unauthorized code execution
   - Requires signed bootloaders

2. **Password Protection**
   - Password for boot menu
   - Password for editing entries
   - Prevents unauthorized changes

3. **TPM Integration**
   - Measures boot components
   - Validates system integrity
   - Enables secure storage

#### Troubleshooting Bootloader Issues

1. **Common Problems**
   - Missing bootloader
   - Corrupted configuration
   - Failed kernel loading
   - Boot loop

2. **Recovery Methods**
   - Boot from installation media
   - Use recovery console
   - Reinstall bootloader
   - Fix configuration files

3. **Diagnostic Commands**
   - `bootrec /fixmbr` (Windows)
   - `grub-install` (Linux)
   - `bcdedit` (Windows)
   - `efibootmgr` (Linux UEFI)

#### Advanced Features

1. **Chainloading**
   - Boot another bootloader
   - Useful for multi-boot setups
   - Common when mixing OSes

2. **Memory Testing**
   - Built-in memtest86+
   - Hardware diagnostics
   - Memory stress testing

3. **Network Booting**
   - PXE support
   - iSCSI boot
   - Remote installation

4. **Custom Boot Entries**
   - Add custom kernels
   - Boot ISO files directly
   - Create recovery options

### 2.5 OS Initialization

#### Overview
OS Initialization is the final stage of the boot process where the operating system takes control, initializes its components, and prepares the system for user interaction. This stage varies significantly between operating systems.

#### Windows Boot Process

1. **Boot Manager Phase**
   - `bootmgr` loads BCD (Boot Configuration Data)
   - Displays boot menu (if multiple OSes present)
   - Loads `winload.exe` from system partition

2. **Kernel Loading**
   - `winload.exe` loads:
     - `ntoskrnl.exe` (Windows kernel)
     - HAL (Hardware Abstraction Layer)
     - System registry hives
     - Boot drivers
   - Transfers control to the kernel

3. **Kernel Initialization**
   - Initializes executive subsystems
   - Starts the Session Manager (`smss.exe`)
   - Loads remaining drivers
   - Creates system environment

4. **Session Manager**
   - Creates user sessions
   - Runs startup programs
   - Launches `winlogon.exe`

5. **Logon Process**
   - `winlogon.exe` starts:
     - Local Security Authority (`lsass.exe`)
     - Service Control Manager (`services.exe`)
     - Logon UI
   - Handles user authentication

#### Linux Boot Process

1. **Initial RAM Disk (initramfs)**
   - Loads temporary root filesystem
   - Contains essential drivers and tools
   - Mounts the real root filesystem

2. **System Initialization**
   - **systemd** (modern):
     - Parallel service startup
     - Service dependency management
     - Socket activation
   - **SysV init** (legacy):
     - Sequential startup
     - Runlevel-based
     - `/etc/inittab` configuration

3. **Service Management**
   - Starts system services
   - Mounts filesystems
   - Configures network
   - Sets up virtual consoles

4. **Login Process**
   - `getty` starts on virtual consoles
   - Display Manager starts for GUI login
   - User session begins after authentication

#### macOS Boot Process

1. **Firmware Phase**
   - Loads Boot.efi
   - Verifies system integrity
   - Initializes hardware

2. **Boot Manager**
   - Presents boot options
   - Loads kernel and kexts
   - Transitions to kernel space

3. **Kernel Initialization**
   - XNU kernel starts
   - Loads essential drivers
   - Sets up system environment

4. **Launchd**
   - First user-space process (PID 1)
   - Manages system services
   - Starts loginwindow

#### Boot Performance Optimization

1. **Windows**
   - Disable unnecessary startup programs
   - Use Fast Startup (hybrid boot)
   - Optimize service startup
   - Defragment boot volume

2. **Linux**
   - Use systemd-analyze to find bottlenecks
   - Enable parallel startup
   - Use SSD-friendly I/O schedulers
   - Optimize initramfs size

3. **macOS**
   - Reset NVRAM/PRAM
   - Manage login items
   - Repair disk permissions
   - Update system software

#### Common Boot Issues and Solutions

| Issue | Windows | Linux | macOS |
|-------|---------|-------|-------|
| **Kernel Panic** | Check dump files, update drivers | Check logs, test with older kernel | Safe boot, reinstall OS |
| **Boot Loop** | System Restore, Startup Repair | Check logs, fix fstab | Reset NVRAM, Safe Mode |
| **Missing OS** | Fix MBR/BCD | Reinstall GRUB | Internet Recovery |
| **Driver Issues** | Safe Mode, Rollback | Blacklist modules | Boot in Safe Mode |
| **File System Errors** | CHKDSK | fsck | Disk Utility |

#### Boot Logs and Diagnostics

1. **Windows**
   - Event Viewer (eventvwr.msc)
   - `Get-WinEvent` PowerShell cmdlet
   - Boot logging (msconfig)

2. **Linux**
   - `journalctl -b` (systemd)
   - `dmesg`
   - `/var/log/boot.log`

3. **macOS**
   - Console.app
   - `log show --predicate 'eventMessage contains "boot"'`
   - System Information -> Software -> Logs

#### Boot Time Analysis

| Component | Windows | Linux | macOS |
|-----------|---------|-------|-------|
| **Firmware** | 2-10s | 2-10s | 2-8s |
| **Bootloader** | 1-3s | 1-5s | 1-2s |
| **Kernel** | 2-5s | 1-3s | 3-6s |
| **Services** | 5-20s | 2-10s | 4-12s |
| **Login** | 2-10s | 1-5s | 2-8s |
| **Desktop** | 3-15s | 2-10s | 2-10s |

#### Advanced Topics

1. **Secure Boot**
   - UEFI Secure Boot
   - TPM integration
   - Measured boot

2. **Network Boot**
   - PXE booting
   - iSCSI boot
   - Network installers

3. **Container/Virtualization**
   - Container-optimized OS
   - Hypervisor integration
   - Cloud-init

4. **Custom Boot Environments**
   - Live USBs
   - Recovery partitions
   - Factory reset images

## 3. Accessing BIOS/UEFI Settings

### 3.1 Common Access Methods

#### Standard Access Keys
| Manufacturer | Common Keys | Notes |
|--------------|-------------|-------|
| **Acer** | F2, Del | F12 for Boot Menu |
| **ASUS** | F2, Del | F8 for Boot Menu |
| **Dell** | F2, F12 | F12 for Boot Menu |
| **HP** | F10, Esc | F9 for Boot Menu |
| **Lenovo** | F1, F2 | F12 for Boot Menu |
| **MSI** | Del | F11 for Boot Menu |
| **Samsung** | F2, F10 | F4 for Recovery |
| **Sony** | F2, Assist | Assist button on some models |
| **Toshiba** | F2, F12 | F12 for Boot Menu |

#### Alternative Access Methods
1. **Windows Recovery Environment**
   - Hold Shift while clicking Restart
   - Troubleshoot > Advanced Options > UEFI Firmware Settings

2. **System Configuration**
   - `msconfig` > Boot tab > Safe boot (minimal)
   - Restart into UEFI firmware settings

3. **Command Line**
   ```powershell
   shutdown /r /fw
   ```
   ```bash
   systemctl reboot --firmware-setup
   ```

### 3.2 Windows Systems

#### Windows 10/11
1. **Settings Method**
   - Windows Settings > Update & Security > Recovery
   - Under Advanced startup, click "Restart now"
   - Troubleshoot > Advanced options > UEFI Firmware Settings

2. **Shift + Restart**
   - Hold Shift while clicking Restart
   - Navigate to UEFI Firmware Settings

3. **Command Line**
   ```powershell
   # Immediate restart to UEFI
   shutdown /r /fw
   
   # Schedule UEFI access on next boot
   shutdown /r /fw /t 0
   ```

#### Windows 8/8.1
1. **PC Settings**
   - PC Settings > Update and Recovery > Recovery
   - Under Advanced startup, click "Restart now"

2. **Charms Bar**
   - Settings > Change PC Settings > Update and Recovery > Recovery
   - Under Advanced startup, click "Restart now"

### 3.3 macOS Systems

#### Intel-based Macs
1. **Startup Manager**
   - Power on while holding Option (⌥)
   - Select boot volume or recovery

2. **Recovery Mode**
   - Cmd (⌘) + R during startup
   - Access Disk Utility, reinstall macOS, etc.

3. **Boot Picker**
   - Hold Option (⌥) at startup
   - Select between bootable volumes

#### Apple Silicon Macs
1. **Startup Options**
   - Press and hold power button
   - Select Options > Continue

2. **Recovery Mode**
   - Power off completely
   - Press and hold power button until "Loading startup options"
   - Click Options > Continue

### 3.4 Linux Systems

#### GRUB Menu
1. **Access GRUB**
   - Hold Shift (BIOS) or press Esc (UEFI) during boot
   - Select "Advanced options" for recovery

2. **Systemd-boot**
   - Press Spacebar during boot
   - Access boot loader menu

#### Terminal Methods
```bash
# Reboot into UEFI
systemctl reboot --firmware-setup

# Check if UEFI is supported
[ -d /sys/firmware/efi ] && echo "UEFI" || echo "BIOS"
```

### 3.5 Dependency Management

#### Driver Dependencies
- **Common Dependency Chains**
  - Chipset drivers → Storage → Network → Graphics/Audio
  - Base System → Firmware → Hardware Abstraction → Device Drivers
  - Virtualization Extensions → Virtual Device Drivers

- **Documentation Format**
  ```yaml
  driver_name:
    version: "1.0.0"
    dependencies:
      - name: "chipset_driver"
        min_version: "2.1.0"
        type: "hard"  # or "soft" for optional dependencies
      - name: "firmware_update"
        min_version: "1.5.0"
    conflicts:
      - name: "legacy_driver"
        max_version: "0.9.0"
  ```

#### Deployment Sequencing
- **Automatic Resolution**
  ```powershell
  function Install-DriverWithDependencies {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverPath,
          
          [ValidateSet('Install', 'Update', 'Rollback')]
          [string]$Action = 'Install',
          
          [switch]$Force
      )
      
      # Load driver metadata
      $metadata = Get-Content -Path "$DriverPath\metadata.json" | ConvertFrom-Json
      
      # Check for conflicts
      $conflicts = $metadata.conflicts | Where-Object {
          $installed = Get-InstalledDriver -Name $_.name
          $installed -and $installed.Version -le [Version]$_.max_version
      }
      
      if ($conflicts -and -not $Force) {
          throw "Found conflicting drivers: $($conflicts -join ', '). Use -Force to override."
      }
      
      # Install dependencies first
      $metadata.dependencies | ForEach-Object {
          if ($_.type -eq 'hard' -or $Force) {
              $depPath = Find-DriverPackage -Name $_.name -MinVersion $_.min_version
              if (-not $depPath) {
                  throw "Missing required dependency: $($_.name) v$($_.min_version) or higher"
              }
              Install-DriverWithDependencies -DriverPath $depPath -Action $Action -Force:$Force
          }
      }
      
      # Install the actual driver
      switch ($Action) {
          'Install' { Install-Driver -Path $DriverPath }
          'Update' { Update-Driver -Path $DriverPath }
          'Rollback' { Restore-SystemRestorePoint -Description "Before $($metadata.name) $($metadata.version)" }
      }
  }
  ```

- **Dependency Validation**
  ```powershell
  function Test-DriverDependencies {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverPath,
          
          [switch]$ResolveAutomatically
      )
      
      $metadata = Get-Content -Path "$DriverPath\metadata.json" | ConvertFrom-Json
      $report = [PSCustomObject]@{
          Driver = $metadata.name
          Version = $metadata.version
          Dependencies = @()
          Conflicts = @()
          IsValid = $true
      }
      
      # Check dependencies
      foreach ($dep in $metadata.dependencies) {
          $installed = Get-InstalledDriver -Name $dep.name
          $status = @{
              Name = $dep.name
              RequiredVersion = $dep.min_version
              Status = 'Missing'
              InstalledVersion = $null
              IsSatisfied = $false
          }
          
          if ($installed) {
              $status.InstalledVersion = $installed.Version
              if ([Version]$installed.Version -ge [Version]$dep.min_version) {
                  $status.Status = 'OK'
                  $status.IsSatisfied = $true
              } else {
                  $status.Status = 'Outdated'
                  $report.IsValid = $false
              }
          } else {
              $report.IsValid = $false
          }
          
          $report.Dependencies += $status
          
          # Auto-resolve if requested
          if ($ResolveAutomatically -and -not $status.IsSatisfied) {
              Write-Host "Resolving dependency: $($dep.name) >= $($dep.min_version)"
              $depPath = Find-DriverPackage -Name $dep.name -MinVersion $dep.min_version
              if ($depPath) {
                  Install-DriverWithDependencies -DriverPath $depPath -Action 'Install'
                  $report.Dependencies[-1].Status = 'Resolved'
                  $report.Dependencies[-1].IsSatisfied = $true
              } else {
                  $report.Dependencies[-1].Status = 'Unresolvable'
              }
          }
      }
      
      # Check for conflicts
      foreach ($conflict in $metadata.conflicts) {
          $installed = Get-InstalledDriver -Name $conflict.name
          if ($installed -and $installed.Version -le [Version]$conflict.max_version) {
              $report.Conflicts += [PSCustomObject]@{
                  Name = $conflict.name
                  InstalledVersion = $installed.Version
                  MaxAllowedVersion = $conflict.max_version
              }
              $report.IsValid = $false
          }
      }
      
      return $report
  }
  ```

#### Conflict Resolution
- **Common Conflict Scenarios**
  - Multiple network drivers for same hardware
  - Old and new versions of same driver
  - Incompatible chipset and device drivers

- **Resolution Workflow**
  1. **Detection**
     - System event logs
     - Driver installation logs
     - Performance monitoring
  
  2. **Analysis**
     - Check driver signatures
     - Verify version compatibility
     - Review system requirements
  
  3. **Remediation**
     ```powershell
     function Resolve-DriverConflict {
         [CmdletBinding()]
         param (
             [Parameter(Mandatory=$true)]
             [string]$DriverName,
             
             [ValidateSet('Downgrade', 'Upgrade', 'Remove')]
             [string]$Resolution,
             
             [string]$TargetVersion
         )
         
         $driver = Get-InstalledDriver -Name $DriverName
         if (-not $driver) {
             Write-Warning "Driver $DriverName not found"
             return
         }
         
         switch ($Resolution) {
             'Downgrade' {
                 $version = $TargetVersion ?? (Get-StableVersion -Name $DriverName)
                 $package = Get-DriverPackage -Name $DriverName -Version $version
                 Install-Driver -Path $package.Path -ForceDowngrade
             }
             'Upgrade' {
                 $version = $TargetVersion ?? (Get-LatestVersion -Name $DriverName)
                 $package = Get-DriverPackage -Name $DriverName -Version $version
                 Install-Driver -Path $package.Path
             }
             'Remove' {
                 Uninstall-Driver -Name $DriverName -Force
             }
         }
         
         # Verify resolution
         Start-Sleep -Seconds 5
         $status = Get-DriverStatus -Name $DriverName
         if ($status -ne 'Running') {
             Write-Warning "Driver $DriverName is not running after resolution"
             Start-Rollback -Snapshot (Get-CurrentSnapshot)
         }
     }
     ```

- **Prevention Strategies**
  - Maintain a driver compatibility matrix
  - Implement pre-deployment testing
  - Use driver isolation techniques
  - Regular driver audits and updates

### 3.6 Package Testing

#### Test Environment Setup
- **Lab Configuration**
  - Isolated network segment
  - Virtual machines for different OS versions
  - Hardware variations (if applicable)
  - Baseline system snapshots

- **Test Matrix**
  ```yaml
  test_environment:
    os_versions:
      - windows_10_21h2
      - windows_11_22h2
      - server_2022
    hardware_profiles:
      - minimal_ram
      - standard
      - high_performance
    test_cases:
      - clean_install
      - upgrade
      - rollback
  ```

#### Automated Testing Framework
- **Test Execution**
  ```powershell
  function Invoke-DriverTestSuite {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverPackagePath,
          
          [ValidateSet('All', 'Installation', 'Functionality', 'Rollback')]
          [string]$TestType = 'All',
          
          [string]$TestEnvironment = 'Lab01',
          
          [switch]$GenerateReport
      )
      
      $testResults = @()
      $startTime = Get-Date
      $testId = [guid]::NewGuid().ToString()
      
      # Load test configuration
      $config = Get-Content -Path "$PSScriptRoot\test_config.json" | ConvertFrom-Json
      
      # Initialize test environment
      Initialize-TestEnvironment -Environment $TestEnvironment
      
      # Run selected tests
      if ($TestType -in @('All', 'Installation')) {
          $testResults += Test-DriverInstallation -DriverPackagePath $DriverPackagePath -TestId $testId
      }
      
      if ($TestType -in @('All', 'Functionality')) {
          $testResults += Test-DriverFunctionality -DriverPackagePath $DriverPackagePath -TestId $testId
      }
      
      if ($TestType -in @('All', 'Rollback')) {
          $testResults += Test-RollbackProcedure -DriverPackagePath $DriverPackagePath -TestId $testId
      }
      
      # Generate report if requested
      if ($GenerateReport) {
          $report = New-TestReport -TestResults $testResults -TestId $testId
          Save-TestReport -Report $report -Path "$PSScriptRoot\reports\$testId.html"
      }
      
      return $testResults
  }
  ```

#### Test Cases
- **Installation Testing**
  ```powershell
  function Test-DriverInstallation {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverPackagePath,
          
          [string]$TestId
      )
      
      $results = @{
          TestId = $TestId
          TestType = 'Installation'
          StartTime = Get-Date
          TestCases = @()
          Success = $true
      }
      
      try {
          # Test silent installation
          $testCase = @{
              Name = 'Silent Installation'
              Status = 'Running'
              Details = $null
          }
          
          $installResult = Install-Driver -Path $DriverPackagePath -Silent -ErrorAction Stop
          
          $testCase.Status = 'Passed'
          $testCase.Details = $installResult
          $results.TestCases += $testCase
          
          # Verify installation
          $verifyResult = Test-DriverInstallation -DriverPackagePath $DriverPackagePath
          $results.TestCases += @{
              Name = 'Installation Verification'
              Status = if ($verifyResult.Success) { 'Passed' } else { 'Failed' }
              Details = $verifyResult
          }
          
          $results.Success = $results.Success -and $verifyResult.Success
      }
      catch {
          $testCase.Status = 'Failed'
          $testCase.Details = $_.Exception.Message
          $results.Success = $false
      }
      finally {
          $results.EndTime = Get-Date
          $results.Duration = $results.EndTime - $results.StartTime
          
          # Log results
          $results | ConvertTo-Json -Depth 5 | 
              Out-File -FilePath "$env:TEMP\$TestId-installation.json"
              
          return $results
      }
  }
  ```

- **Functionality Testing**
  ```powershell
  function Test-DriverFunctionality {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverPackagePath,
          
          [string]$TestId
      )
      
      $results = @{
          TestId = $TestId
          TestType = 'Functionality'
          StartTime = Get-Date
          TestCases = @()
          Success = $true
      }
      
      try {
          # Load test cases from driver package
          $testCases = Get-Content -Path "$DriverPackagePath\test_cases.json" | 
              ConvertFrom-Json -AsHashtable
          
          foreach ($testCase in $testCases.Functionality) {
              $testResult = @{
                  Name = $testCase.Name
                  Status = 'Running'
                  Details = $null
              }
              
              try {
                  $testScript = [scriptblock]::Create($testCase.Script)
                  $testOutput = & $testScript -ErrorAction Stop
                  
                  $testResult.Status = 'Passed'
                  $testResult.Details = $testOutput
              }
              catch {
                  $testResult.Status = 'Failed'
                  $testResult.Details = $_.Exception.Message
                  $results.Success = $false
              }
              
              $results.TestCases += $testResult
          }
      }
      catch {
          $results.TestCases += @{
              Name = 'Test Setup'
              Status = 'Failed'
              Details = $_.Exception.Message
          }
          $results.Success = $false
      }
      finally {
          $results.EndTime = Get-Date
          $results.Duration = $results.EndTime - $results.StartTime
          
          # Log results
          $results | ConvertTo-Json -Depth 5 | 
              Out-File -FilePath "$env:TEMP\$TestId-functionality.json"
              
          return $results
      }
  }
  ```

- **Rollback Testing**
  ```powershell
  function Test-RollbackProcedure {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverPackagePath,
          
          [string]$TestId
      )
      
      $results = @{
          TestId = $TestId
          TestType = 'Rollback'
          StartTime = Get-Date
          TestCases = @()
          Success = $true
      }
      
      try {
          # Create system restore point
          $restorePoint = New-RestorePoint -Description "Pre-test $TestId"
          
          # Install driver
          $installResult = Install-Driver -Path $DriverPackagePath
          
          # Test rollback
          $rollbackResult = Start-Rollback -RestorePoint $restorePoint -Force
          
          $results.TestCases += @{
              Name = 'Rollback Execution'
              Status = if ($rollbackResult.Success) { 'Passed' } else { 'Failed' }
              Details = $rollbackResult
          }
          
          # Verify system state
          $systemState = Test-SystemHealth
          $results.TestCases += @{
              Name = 'System Health Check'
              Status = if ($systemState.Healthy) { 'Passed' } else { 'Failed' }
              Details = $systemState
          }
          
          $results.Success = $rollbackResult.Success -and $systemState.Healthy
      }
      catch {
          $results.TestCases += @{
              Name = 'Rollback Test'
              Status = 'Failed'
              Details = $_.Exception.Message
          }
          $results.Success = $false
      }
      finally {
          $results.EndTime = Get-Date
          $results.Duration = $results.EndTime - $results.StartTime
          
          # Log results
          $results | ConvertTo-Json -Depth 5 | 
              Out-File -FilePath "$env:TEMP\$TestId-rollback.json"
              
          return $results
      }
  }
  ```

#### Test Reporting
- **Report Generation**
  ```powershell
  function New-TestReport {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [array]$TestResults,
          
          [string]$TestId
      )
      
      $report = @"
      <!DOCTYPE html>
      <html>
      <head>
          <title>Driver Test Report - $TestId</title>
          <style>
              body { font-family: Arial, sans-serif; margin: 20px; }
              .test-section { margin-bottom: 30px; }
              .test-case { margin: 10px 0; padding: 10px; border-left: 4px solid #ccc; }
              .passed { border-color: #4CAF50; background-color: #e8f5e9; }
              .failed { border-color: #f44336; background-color: #ffebee; }
              .summary { 
                  padding: 15px; 
                  margin-bottom: 20px; 
                  border-radius: 4px; 
                  font-weight: bold;
              }
              .summary.passed { background-color: #e8f5e9; color: #2e7d32; }
              .summary.failed { background-color: #ffebee; color: #c62828; }
              pre { 
                  background-color: #f5f5f5; 
                  padding: 10px; 
                  border-radius: 4px; 
                  overflow-x: auto;
              }
          </style>
      </head>
      <body>
          <h1>Driver Test Report</h1>
          <p><strong>Test ID:</strong> $TestId</p>
          <p><strong>Generated:</strong> $(Get-Date -Format 'yyyy-MM-dd HH:mm:ss')</p>
  "@
  
      # Add summary section
      $totalTests = $TestResults.Count
      $passedTests = ($TestResults | Where-Object { $_.Success }).Count
      $successRate = [math]::Round(($passedTests / $totalTests) * 100, 2)
      
      $summaryClass = if ($passedTests -eq $totalTests) { 'passed' } else { 'failed' }
      
      $report += @"
      <div class="summary $summaryClass">
          <h2>Test Summary</h2>
          <p>Total Tests: $totalTests</p>
          <p>Passed: $passedTests</p>
          <p>Success Rate: $successRate%</p>
      </div>
  "@
  
      # Add detailed results
      foreach ($testResult in $TestResults) {
          $testClass = if ($testResult.Success) { 'passed' } else { 'failed' }
          
          $report += @"
          <div class="test-section">
              <h3>$($testResult.TestType) - $(if ($testResult.Success) { '✓' } else { '✗' })</h3>
              <p><strong>Duration:</strong> $($testResult.Duration.ToString('hh\:mm\:ss\.fff'))</p>
              <div class="test-cases">
  "@
  
          foreach ($testCase in $testResult.TestCases) {
              $caseClass = if ($testCase.Status -eq 'Passed') { 'passed' else 'failed' }
              $details = $testCase.Details | ConvertTo-Json -Depth 5 | 
                          ForEach-Object { [System.Text.RegularExpressions.Regex]::Unescape($_) }
              
              $report += @"
              <div class="test-case $caseClass">
                  <h4>$($testCase.Name) - $($testCase.Status)</h4>
                  <pre>$details</pre>
              </div>
  "@
          }
          
          $report += "</div></div>"
      }
      
      $report += "</body></html>"
      return $report
  }
  ```

#### Continuous Improvement
- **Test Result Analysis**
  - Track test metrics over time
  - Identify recurring issues
  - Update test cases based on findings
  - Maintain a knowledge base of common issues

- **Automation Integration**
  - CI/CD pipeline integration
  - Automated test scheduling
  - Alerting for test failures
  - Trend analysis and reporting

### 3.7 Enhanced Best Practices

#### Secure Package Distribution
- **Secure Channels**
  - Use HTTPS/TLS for all package transfers
  - Implement package signing and verification
  - Utilize secure package repositories
  - Enforce access controls and authentication

- **Package Integrity**
  ```powershell
  function Test-PackageIntegrity {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$PackagePath,
          
          [string]$ExpectedHash,
          
          [ValidateSet('SHA256', 'SHA384', 'SHA512')]
          [string]$Algorithm = 'SHA256'
      )
      
      $actualHash = (Get-FileHash -Path $PackagePath -Algorithm $Algorithm).Hash
      
      if ($ExpectedHash -and ($actualHash -ne $ExpectedHash)) {
          throw "Package integrity check failed. Expected: $ExpectedHash, Actual: $actualHash"
      }
      
      # Verify digital signature
      $signature = Get-AuthenticodeSignature -FilePath $PackagePath
      if ($signature.Status -ne 'Valid') {
          throw "Invalid package signature: $($signature.Status)"
      }
      
      return $true
  }
  ```

#### Rollback and Recovery
- **Automated Rollback Procedures**
  - System restore points before installation
  - Versioned package storage
  - Automated rollback on failure
  - Health checks before/after installation

- **Rollback Implementation**
  ```powershell
  function Invoke-SafeDriverUpdate {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverPackagePath,
          
          [string]$BackupPath = "$env:ProgramData\DriverBackups"
      )
      
      $rollbackActions = @()
      $success = $false
      
      try {
          # Create backup of current drivers
          $backupFile = "$BackupPath\driver_backup_$(Get-Date -Format 'yyyyMMdd_HHmmss').zip"
          $rollbackActions += @{ Type = 'Backup'; Path = $backupFile }
          
          Export-WindowsDriver -Online -Destination $BackupPath -Force | Out-Null
          Compress-Archive -Path "$BackupPath\*" -DestinationPath $backupFile
          
          # Create system restore point
          $restorePoint = New-RestorePoint -Description "Pre-driver update $(Get-Date)"
          $rollbackActions += @{ Type = 'RestorePoint'; Id = $restorePoint }
          
          # Install new driver
          Install-Driver -Path $DriverPackagePath
          
          # Verify installation
          $healthCheck = Test-SystemHealth
          if (-not $healthCheck.IsHealthy) {
              throw "System health check failed after installation"
          }
          
          $success = $true
      }
      catch {
          Write-Warning "Driver update failed. Initiating rollback..."
          
          # Execute rollback actions in reverse order
          [array]::Reverse($rollbackActions)
          
          foreach ($action in $rollbackActions) {
              try {
                  switch ($action.Type) {
                      'RestorePoint' { 
                          Restore-RestorePoint -Id $action.Id -Confirm:$false 
                      }
                      'Backup' { 
                          Expand-Archive -Path $action.Path -DestinationPath (Split-Path $action.Path) -Force
                          Import-WindowsDriver -Path (Split-Path $action.Path) -Force
                      }
                  }
              }
              catch {
                  Write-Error "Failed to execute rollback action: $_"
              }
          }
          
          throw "Update failed and was rolled back. Original error: $_"
      }
      finally {
          # Clean up temporary files
          if ($success) {
              Remove-Item -Path $backupFile -Force -ErrorAction SilentlyContinue
          }
      }
  }
  ```

#### Monitoring and Metrics
- **Deployment Monitoring**
  - Track success/failure rates
  - Monitor system stability
  - Collect performance metrics
  - Alert on anomalies

- **Metrics Collection**
  ```powershell
  function Get-DeploymentMetrics {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DeploymentId,
          
          [DateTime]$StartTime = (Get-Date).AddDays(-30),
          
          [DateTime]$EndTime = (Get-Date)
      )
      
      $metrics = @{
          DeploymentId = $DeploymentId
          TimeRange = @{
              Start = $StartTime
              End = $EndTime
          }
          Summary = @{
              TotalDeployments = 0
              Successful = 0
              Failed = 0
              Rollbacks = 0
          }
          Performance = @{
              AvgDeploymentTime = $null
              SystemImpact = @{
                  CPU = @()
                  Memory = @()
                  Disk = @()
              }
          }
          Issues = @()
      }
      
      # Get deployment data
      $deployments = Get-EventLog -LogName 'Application' -Source 'DriverDeployment' -After $StartTime -Before $EndTime |
          Where-Object { $_.Message -match $DeploymentId }
      
      $metrics.Summary.TotalDeployments = $deployments.Count
      $metrics.Summary.Successful = ($deployments | Where-Object { $_.EntryType -eq 'Information' }).Count
      $metrics.Summary.Failed = ($deployments | Where-Object { $_.EntryType -eq 'Error' }).Count
      $metrics.Summary.Rollbacks = ($deployments | Where-Object { $_.Message -match 'rollback' }).Count
      
      # Calculate performance metrics
      $deploymentTimes = $deployments | ForEach-Object { 
          if ($_.Message -match 'Duration: (\d+)ms') { [int]$matches[1] } 
      } | Where-Object { $_ -gt 0 }
      
      if ($deploymentTimes) {
          $metrics.Performance.AvgDeploymentTime = [math]::Round(($deploymentTimes | Measure-Object -Average).Average, 2)
      }
      
      # Collect system impact data
      $perfData = Get-Counter '\Processor(_Total)\% Processor Time', '\Memory\% Committed Bytes In Use', '\PhysicalDisk(_Total)\Avg. Disk sec/Read' -SampleInterval 1 -MaxSamples 10
      $metrics.Performance.SystemImpact.CPU = ($perfData.CounterSamples | Where-Object { $_.Path -match 'Processor' }).CookedValue
      $metrics.Performance.SystemImpact.Memory = ($perfData.CounterSamples | Where-Object { $_.Path -match 'Memory' }).CookedValue
      $metrics.Performance.SystemImpact.Disk = ($perfData.CounterSamples | Where-Object { $_.Path -match 'Disk' }).CookedValue
      
      # Identify common issues
      $errorPatterns = @(
          'Driver not found',
          'Signature verification failed',
          'Dependency missing',
          'Access denied',
          'Insufficient resources'
      )
      
      $metrics.Issues = $deployments | 
          Where-Object { $_.EntryType -eq 'Error' } |
          ForEach-Object {
              $issue = $errorPatterns | Where-Object { $_.Message -match $_ } | Select-Object -First 1
              if ($issue) { $issue } else { 'Unknown' }
          } |
          Group-Object |
          Select-Object @{n='Error';e={$_.Name}}, @{n='Count';e={$_.Count}} |
          Sort-Object Count -Descending
      
      return $metrics
  }
  ```

#### Documentation Standards
- **Required Documentation**
  - Installation/upgrade procedures
  - Known issues and workarounds
  - Rollback procedures
  - Dependencies and requirements
  - Security considerations

- **Documentation Template**
  ```markdown
  # Driver Package Documentation
  
  ## Package Information
  - **Name**: 
  - **Version**: 
  - **Release Date**: 
  - **Target OS**: 
  - **Dependencies**: 
  
  ## Installation
  ### Prerequisites
  - [ ] System requirements
  - [ ] Required permissions
  - [ ] Dependencies
  
  ### Installation Steps
  1. [Step 1]
  2. [Step 2]
  
  ## Configuration
  - [Configuration options]
  - [Recommended settings]
  
  ## Troubleshooting
  ### Common Issues
  - [Issue 1]
    - Symptoms:
    - Resolution:
  
  ## Rollback Procedure
  1. [Step 1]
  2. [Step 2]
  
  ## Security
  - [Security considerations]
  - [Required permissions]
  
  ## Support
  - [Contact information]
  - [Support hours]
  ```

### 3.8 Troubleshooting Access Issues

#### Common Problems
1. **Fast Boot Enabled**
   - Disable in Windows Power Options
   - Disable in BIOS/UEFI settings

2. **Incorrect Key Timing**
   - Start pressing the key immediately after power on
   - Try rapid tapping instead of holding

3. **Secure Boot Interference**
   - May prevent certain key combinations
   - Temporarily disable if needed

#### Advanced Recovery
1. **Clear NVRAM/PRAM**
   - Reset to default settings
   - May restore access to setup

2. **CMOS Reset**
   - Remove CMOS battery
   - Use motherboard jumper
   - Resets all BIOS settings

3. **Manufacturer Tools**
   - HP BIOS Configuration Utility
   - Lenovo System Update
   - Dell Command | Configure

## 4. Deployment Methods

### 4.1 Manual Installation

#### Installation Methods
- **Device Manager**
  1. Open Device Manager (devmgmt.msc)
  2. Right-click the device with missing driver
  3. Select "Update driver"
  4. Choose "Browse my computer for drivers"
  5. Navigate to the driver folder and install

- **Command Line (pnputil)**
  ```powershell
  # Install a single driver
  pnputil /add-driver "C:\Drivers\driver.inf" /install /quiet
  
  # Install all drivers in a directory
  pnputil /add-driver "C:\Drivers\*.inf" /subdirs /install /quiet
  
  # Check installed drivers
  pnputil /enum-drivers
  ```

#### Silent Installation
- **Using pnputil**
  ```powershell
  # Basic silent installation
  pnputil /add-driver "C:\Drivers\driver.inf" /install /quiet
  
  # With logging
  pnputil /add-driver "C:\Drivers\driver.inf" /install /quiet > "$env:TEMP\driver_install.log" 2>&1
  ```

- **Using PowerShell**
  ```powershell
  function Install-DriverSilently {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverPath,
          
          [string]$LogPath = "$env:TEMP\DriverInstall_$(Get-Date -Format 'yyyyMMdd_HHmmss').log"
      )
      
      # Start logging
      Start-Transcript -Path $LogPath -Force
      
      try {
          Write-Host "Starting driver installation from: $DriverPath"
          
          # Verify driver file exists
          if (-not (Test-Path $DriverPath)) {
              throw "Driver file not found: $DriverPath"
          }
          
          # Get driver details
          $driverInfo = Get-Item $DriverPath
          Write-Host "Driver: $($driverInfo.Name)"
          Write-Host "Size: $([math]::Round($driverInfo.Length/1MB, 2)) MB"
          
          # Install driver using pnputil
          Write-Host "Installing driver..."
          $process = Start-Process -FilePath "pnputil.exe" \
              -ArgumentList "/add-driver `"$DriverPath`" /install /quiet" \
              -NoNewWindow -Wait -PassThru -RedirectStandardOutput "$env:TEMP\pnputil_stdout.log" \
              -RedirectStandardError "$env:TEMP\pnputil_stderr.log"
          
          # Check installation result
          if ($process.ExitCode -eq 0) {
              Write-Host "Driver installed successfully"
              $success = $true
          } else {
              $errorMsg = Get-Content "$env:TEMP\pnputil_stderr.log" -ErrorAction SilentlyContinue
              throw "Driver installation failed with exit code $($process.ExitCode). Error: $errorMsg"
          }
          
          # Verify driver installation
          Write-Host "Verifying driver installation..."
          $driverName = [System.IO.Path]::GetFileNameWithoutExtension($DriverPath)
          $installedDriver = Get-WindowsDriver -Online -All | Where-Object { $_.OriginalFileName -like "*$driverName*" }
          
          if ($installedDriver) {
              Write-Host "Driver verification successful"
              Write-Host "Driver version: $($installedDriver.DriverVersion)"
              Write-Host "Provider: $($installedDriver.DriverProviderName)"
              $success = $true
          } else {
              throw "Driver verification failed - driver not found in system"
          }
          
          return $success
      }
      catch {
          Write-Error "Error during driver installation: $_"
          return $false
      }
      finally {
          # Stop logging
          Stop-Transcript
          
          # Clean up temporary files
          Remove-Item "$env:TEMP\pnputil_stdout.log" -ErrorAction SilentlyContinue
          Remove-Item "$env:TEMP\pnputil_stderr.log" -ErrorAction SilentlyContinue
          
          Write-Host "Installation log saved to: $LogPath"
      }
  }
  ```

#### Error Handling and Logging
- **Log File Structure**
  ```powershell
  # Create log directory if it doesn't exist
  $logDir = "$env:ProgramData\DriverInstall\Logs"
  if (-not (Test-Path $logDir)) {
      New-Item -ItemType Directory -Path $logDir -Force | Out-Null
  }
  
  # Standard log file name with timestamp
  $logFile = "$logDir\DriverInstall_$(Get-Date -Format 'yyyyMMdd_HHmmss').log"
  
  # Function to write to log
  function Write-Log {
      param([string]$Message, [string]$Level = "INFO")
      $timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
      "[$timestamp] [$Level] $Message" | Out-File -FilePath $logFile -Append -Encoding utf8
  }
  ```

- **Error Handling Example**
  ```powershell
  try {
      # Attempt driver installation
      $result = pnputil /add-driver "C:\Drivers\driver.inf" /install /quiet
      
      if ($LASTEXITCODE -ne 0) {
          throw "pnputil failed with exit code $LASTEXITCODE"
      }
      
      Write-Log "Driver installed successfully"
  }
  catch {
      $errorMsg = $_.Exception.Message
      Write-Log "Installation failed: $errorMsg" -Level "ERROR"
      
      # Additional error handling
      if ($errorMsg -match "file not found") {
          Write-Log "Driver file is missing or inaccessible" -Level "ERROR"
      }
      elseif ($errorMsg -match "access denied") {
          Write-Log "Insufficient permissions. Run as administrator." -Level "ERROR"
      }
      
      # Exit with error code
      exit 1
  }
  ```

#### Post-Installation Verification
- **Verification Script**
  ```powershell
  function Test-DriverInstallation {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverName,
          
          [string]$ExpectedVersion,
          
          [switch]$CheckDeviceStatus
      )
      
      $results = @{
          DriverFound = $false
          VersionMatch = $false
          DeviceStatus = $null
          IsHealthy = $false
          Details = @()
      }
      
      try {
          # Check if driver is installed
          $driver = Get-WindowsDriver -Online -All | 
              Where-Object { $_.Driver -like "*$DriverName*" } | 
              Select-Object -First 1
          
          if ($driver) {
              $results.DriverFound = $true
              $results.Details += "Driver found: $($driver.Driver)"
              
              # Check version if specified
              if ($ExpectedVersion) {
                  $results.VersionMatch = ($driver.DriverVersion -eq $ExpectedVersion)
                  $results.Details += "Version: $($driver.DriverVersion) (Expected: $ExpectedVersion)"
              }
              
              # Check device status if requested
              if ($CheckDeviceStatus) {
                  $device = Get-PnpDevice | Where-Object { $_.FriendlyName -like "*$DriverName*" }
                  if ($device) {
                      $results.DeviceStatus = $device.Status
                      $results.Details += "Device status: $($device.Status)"
                      
                      # Check for error codes
                      if ($device.Problem) {
                          $results.Details += "Error code: $($device.Problem)"
                      }
                  }
              }
              
              # Overall health check
              $results.IsHealthy = $results.DriverFound -and 
                                 (-not $ExpectedVersion -or $results.VersionMatch) -and
                                 (-not $CheckDeviceStatus -or $results.DeviceStatus -eq 'OK')
          }
          else {
              $results.Details += "Driver not found: $DriverName"
          }
      }
      catch {
          $results.Details += "Error during verification: $($_.Exception.Message)"
      }
      
      # Add results to output
      $results.Details += "Verification complete. Healthy: $($results.IsHealthy)"
      
      # Output results
      return $results
  }
  
  # Example usage
  $verification = Test-DriverInstallation -DriverName "Ethernet" -CheckDeviceStatus
  $verification.Details | ForEach-Object { Write-Host $_ }
  ```

- **Common Verification Checks**
  - Driver file exists in system directories
  - Driver is loaded in memory
  - Associated device is functioning
  - No error events in system logs
  - Performance counters within expected ranges

## 5. Managing Boot Order

### 4.1 Checking Current Boot Order

#### UEFI Systems
1. **Windows**
   ```powershell
   # List all boot entries
   bcdedit /enum firmware
   
   # Check current boot order
   bcdedit /enum {fwbootmgr}
   ```

2. **Linux**
   ```bash
   # List UEFI boot entries
   efibootmgr -v
   
   # View boot order
   efibootmgr -o
   ```

3. **macOS**
   ```bash
   # View boot volume
   bless --getBoot
   
   # List all bootable volumes
   diskutil list | grep "EFI"
   ```

#### Legacy BIOS Systems
- Check during POST (usually F2, Del, or F12)
- Look for "Boot" or "Startup" tab in BIOS
- Note: No standard command-line tools for BIOS boot order

### 4.2 Changing Boot Order in UEFI

#### Windows
1. **Using bcdedit**
   ```powershell
   # Set new boot order (example)
   bcdedit /set {fwbootmgr} displayorder {bootmgr} {current}
   
   # Set default boot entry
   bcdedit /default {current}
   ```

2. **Using Windows GUI**
   - System Configuration (msconfig) > Boot tab
   - Advanced Startup > UEFI Firmware Settings

#### Linux
```bash
# Change boot order (example)
efibootmgr -o 0000,0001,0002

# Set next boot only
efibootmgr -n 0001
```

#### macOS
```bash
# Set startup disk
sudo bless --mount /Volumes/YourVolume --setBoot

# Set next boot only
sudo bless --mount /Volumes/YourVolume --nextonly
```

### 4.3 Changing Boot Order in Legacy BIOS

#### Common BIOS Navigation
- **Arrow Keys**: Navigate menus
- **+/- or Page Up/Down**: Change boot order
- **Enter**: Select/confirm
- **F10**: Save and exit
- **ESC**: Go back/cancel

#### Typical BIOS Boot Options
1. **First Boot Device**
2. **Second Boot Device**
3. **Hard Drive BBS Priorities**
4. **USB Boot** (Enable/Disable)
5. **Network Boot** (Enable/Disable)

### 4.4 Using Boot Menu

#### Common Boot Menu Keys
| Manufacturer | Boot Menu Key | Notes |
|--------------|---------------|-------|
| **ASUS** | F8 | May require Fn key on laptops |
| **Dell** | F12 | Some models use Fn+F12 |
| **HP** | F9 | May require Esc then F9 |
| **Lenovo** | F12 | Some models use Novo button |
| **Acer** | F12 | May require Fn+F12 |

#### Temporary vs Permanent Changes
- **Boot Menu**: One-time boot device selection
- **BIOS/UEFI**: Permanent until changed
- **OS-Level**: Can be persistent or one-time

### 4.5 OS-Level Boot Management

#### Windows
```powershell
# Set default OS (multi-boot)
bcdedit /default {identifier}

# Set boot timeout (in seconds)
bcdedit /timeout 5

# Create new boot entry
bcdedit /create /d "Windows 11 Safe Mode" /application osloader
```

#### Linux (GRUB)
```bash
# Update GRUB config
sudo update-grub

# Edit GRUB defaults
sudo nano /etc/default/grub

# Set default boot entry
GRUB_DEFAULT=0  # 0 is first entry
```

#### macOS
```bash
# Set default startup disk
sudo bless --folder /Volumes/YourVolume/System/Library/CoreServices --bootefi

# Create bootable installer
sudo /Applications/Install\ macOS\ Ventura.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

#### Advanced Boot Options
1. **Safe Mode**
   - Windows: F8 or Shift+Restart
   - macOS: Shift at startup
   - Linux: Add 'single' to kernel params

2. **Recovery Mode**
   - Windows: Recovery Drive
   - macOS: Cmd+R
   - Linux: Recovery option in GRUB

3. **Network Boot**
   - PXE configuration
   - iSCSI targets
   - HTTP/FTP boot

## 5. Troubleshooting

### 5.1 Common Issues and Solutions

#### Boot Failures
| Symptom | Possible Cause | Solution |
|---------|----------------|----------|
| **No Boot Device** | Incorrect boot order, Dead drive | Check connections, Verify boot order |
| **Boot Loop** | Corrupt OS, Bad updates | Boot to recovery, Use System Restore |
| **Black Screen** | GPU issues, Display problems | Check cables, Try integrated graphics |
| **Beep Codes** | Hardware failure | Refer to motherboard manual |
| **CMOS Checksum Error** | Dead CMOS battery | Replace CR2032 battery |

#### Boot Performance Issues
- **Slow Boot**: Disable unnecessary startup programs
- **Hanging at Logo**: Disable Fast Boot, Update BIOS
- **Long POST**: Disable memory check, Update firmware

### 5.2 Boot Device Not Found

#### Hardware Checks
1. **Physical Connections**
   - Verify SATA/USB cables are secure
   - Try different ports
   - Check power cables

2. **BIOS/UEFI Detection**
   - Enter BIOS/UEFI
   - Check if device appears in storage list
   - Enable CSM/Legacy mode if needed

#### Software Solutions
```powershell
# Windows: Check disk status
diskpart
list disk
select disk X
detail disk
```

```bash
# Linux: Check disk detection
sudo fdisk -l
sudo lsblk
```

### 5.3 Boot Order Reset Issues

#### Common Causes
1. **CMOS Battery Failure**
   - Symptoms: Time/date reset, BIOS settings lost
   - Fix: Replace CR2032 battery

2. **BIOS Updates**
   - Some updates reset settings
   - Document settings before updating

3. **Hardware Changes**
   - Adding/removing drives can affect order
   - Check after hardware modifications

### 5.4 Secure Boot Problems

#### Common Issues
1. **OS Not Compatible**
   - Some Linux distros require Secure Boot disable
   - Check OS compatibility

2. **Driver Signature Errors**
   - Windows requires signed drivers
   - Enable Test Signing for development

3. **Dual Boot Conflicts**
   - Windows/Linux dual-boot may need Secure Boot off
   - Use rEFInd as alternative boot manager

#### Secure Boot Management
```powershell
# Check Secure Boot status
Confirm-SecureBootUEFI

# Disable Secure Boot (elevated prompt)
bcdedit /set {current} testsigning on
```

### 5.5 Advanced Troubleshooting

#### Boot Log Analysis
1. **Windows**
   ```
   Event Viewer > Windows Logs > System
   Filter: Event ID 100-110
   ```

2. **Linux**
   ```bash
   journalctl -b -1  # Last boot
   dmesg | grep -i error
   ```

#### Recovery Tools
- **Windows**:
  - Startup Repair
  - BootRec /FixMbr
  - BootRec /RebuildBcd

- **Linux**:
  ```bash
  # Fix GRUB
  sudo grub-install /dev/sdX
  sudo update-grub
  ```

- **macOS**:
  - Recovery Mode (Cmd+R)
  - Disk Utility First Aid
  - Reinstall macOS

#### Bootable Diagnostic Tools
1. **Hardware Diagnostics**
   - MemTest86 (RAM)
   - CrystalDiskInfo (Storage)
   - Prime95 (CPU stress test)

2. **Recovery Environments**
   - Windows PE
   - SystemRescueCD
   - GParted Live

#### Firmware Recovery
1. **BIOS Recovery**
   - USB recovery method
   - Flash recovery jumper
   - Manufacturer tools

2. **UEFI Recovery**
   - Built-in recovery
   - Firmware settings reset
   - Manufacturer-specific procedures

## 6. Driver Management Strategies

### 6.1 Centralized vs. Decentralized Management

#### Centralized Management
Single team or system responsible for all driver updates and maintenance.

**Advantages:**
- Consistent driver versions across the organization
- Easier compliance and audit reporting
- Streamlined troubleshooting and support
- Better control over driver quality and compatibility
- Simplified license management

**Disadvantages:**
- Can create bottlenecks for urgent updates
- Less flexibility for individual departments
- Requires dedicated IT resources
- Slower deployment of critical updates
- Potential single point of failure

#### Decentralized Management
Individual teams or departments manage drivers for their devices.

**Advantages:**
- Faster local updates and response to issues
- Greater flexibility for department-specific hardware
- Reduced IT department workload
- Quick adaptation to local needs
- Distributed responsibility

**Disadvantages:**
- Risk of inconsistent driver versions
- Harder to enforce organizational policies
- Potential security vulnerabilities
- Duplication of efforts across teams
- Difficult to maintain compliance

### 6.2 Key Considerations

#### Device Type Diversity
- **Standardized Hardware**: Easier to manage with centralized approach
- **Diverse Hardware**: May require decentralized management
- **Specialized Equipment**: Department-specific management may be necessary

#### Organizational Size and Structure
- **Small Organizations**: May benefit from centralized management
- **Large Enterprises**: Often require hybrid approaches
- **Distributed Teams**: May need regional management strategies

#### Compliance Requirements
- **Regulated Industries**: May require strict centralized control
- **Audit Trails**: Easier to maintain with centralized systems
- **Documentation**: More consistent under centralized management

#### Resource Availability
- **IT Staffing**: Centralized requires dedicated personnel
- **Budget**: Decentralized may have higher overall costs
- **Infrastructure**: Centralized systems need robust infrastructure

### 6.3 Standardizing Drivers Across Models

#### Hardware Standardization Guidelines
- **Consistent Hardware Models**
  - Reduce driver variability across the organization
  - Simplify testing and validation processes
  - Streamline support and troubleshooting

- **Approved Devices List**
  - Maintain a centralized database of approved hardware
  - Include detailed specifications and requirements
  - Regularly update based on compatibility testing

- **Validation Process**
  - Test drivers on all target hardware configurations
  - Document compatibility issues and workarounds
  - Establish a certification process for new drivers

#### Driver Version Control Practices
- **Centralized Repository**
  - Store all approved drivers in a secure, accessible location
  - Include complete version history and change logs
  - Implement access controls and audit trails

- **Version Management**
  - Use semantic versioning (MAJOR.MINOR.PATCH)
  - Document all changes and dependencies
  - Maintain backward compatibility where possible

- **Deployment Automation**
  - Use package managers (Chocolatey, Ninite, etc.)
  - Implement automated testing in staging environments
  - Schedule deployments during maintenance windows

- **Rollback Procedures**
  - Maintain previous stable versions
  - Document rollback steps for each driver
  - Test rollback procedures regularly

### 6.4 Lifecycle Management Approach

#### Planning Phase
- **Requirements Gathering**
  - Inventory all device models and their drivers
  - Document hardware specifications and dependencies
  - Identify critical vs. optional drivers

- **Policy Development**
  - Define update frequency and procedures
  - Establish testing and approval workflows
  - Create rollback and recovery plans
  - Set compliance and security requirements

#### Implementation Phase
- **Deployment Strategy**
  - Use automated deployment tools (SCCM, Intune, etc.)
  - Implement phased rollouts (pilot groups first)
  - Schedule deployments during maintenance windows

- **Verification Process**
  - Log all installation attempts and results
  - Verify driver versions post-deployment
  - Monitor system stability and performance
  - Document any issues and resolutions

#### Maintenance Phase
- **Ongoing Monitoring**
  - Track driver health and performance metrics
  - Monitor for security vulnerabilities
  - Check for manufacturer updates

- **Update Management**
  - Test updates in staging environment
  - Apply patches following change management
  - Maintain version history and documentation
  - Handle emergency updates when needed

#### Retirement Phase
- **Deprecation Process**
  - Identify obsolete or unsupported drivers
  - Notify affected users/departments
  - Plan migration to supported alternatives

- **Archival**
  - Maintain secure archives of retired drivers
  - Document retirement dates and reasons
  - Keep access logs for compliance
  - Store for required retention period

### 6.5 Implementation Strategies

#### Hybrid Approach
- Centralized policy with decentralized execution
- Core drivers managed centrally, peripheral drivers managed locally
- Automated deployment with local overrides

#### Tools and Technologies
- **MDM Solutions**: For centralized management
- **Scripting and Automation**: For consistent deployments
- **Package Managers**: For simplified driver distribution
- **Virtualization**: For testing driver compatibility

#### Best Practices
- Maintain a driver repository
- Test updates in staging environment
- Document all changes and versions
- Implement rollback procedures
- Regular audits of driver versions

## 7. Driver Inventory and Analysis

### 7.1 Identifying Required Drivers

#### Hardware Inventory
- **Comprehensive Device Catalog**
  - List all hardware models in use
  - Document component specifications
  - Track purchase dates and warranty status
  - Map hardware to organizational units

- **Driver Categorization**
  - **Core System**
    - Chipset drivers
    - System firmware
    - Security processors
  - **Display**
    - Graphics cards
    - Monitor firmware
    - Display adapters
  - **Networking**
    - Network interface cards
    - Wireless adapters
    - Bluetooth modules
  - **Storage**
    - Drive controllers
    - RAID controllers
    - Storage firmware
  - **Peripherals**
    - Printers
    - Scanners
    - Input devices

#### Dependency Mapping
- **Driver Dependencies**
  - Document required driver versions
  - Map hardware-to-driver relationships
  - Identify shared components
  - Note compatibility requirements

- **Priority Classification**
  - **Critical**: Essential for boot/operation
  - **High**: Required for full functionality
  - **Medium**: Enhances performance
  - **Low**: Optional features

### 7.2 Inventory Management Tools

#### 7.2.1 Collecting Hardware IDs

##### Automated Discovery Methods
- **Windows PowerShell**
  ```powershell
  # Get all hardware devices with details
  Get-WmiObject Win32_PnPSignedDriver | Select-Object DeviceName, DeviceID, Manufacturer, DriverVersion | Format-Table -AutoSize
  
  # Export to CSV for analysis
  Get-PnpDevice -PresentOnly | Where-Object { $_.InstanceId -match '^PCI' } | 
    Select-Object Status, Class, FriendlyName, InstanceId | 
    Export-Csv -Path "Hardware_Inventory_$(Get-Date -Format 'yyyyMMdd').csv" -NoTypeInformation
  ```

- **WMI Queries**
  ```powershell
  # Get detailed hardware information
  Get-WmiObject Win32_ComputerSystem | Select-Object Manufacturer, Model, SystemType
  Get-WmiObject Win32_Processor | Select-Object Name, NumberOfCores, MaxClockSpeed
  Get-WmiObject Win32_DiskDrive | Select-Object Model, Size, InterfaceType
  ```

- **SCCM Integration**
  - Hardware inventory classes
  - Custom inventory items
  - Collection queries
  - Reporting services

##### Data Validation
- **Verification Checks**
  - Cross-reference multiple data sources
  - Validate against manufacturer databases
  - Check for known-good configurations
  - Flag anomalies for manual review

- **Error Handling**
  ```powershell
  try {
      $devices = Get-PnpDevice -ErrorAction Stop
      $devices | ForEach-Object {
          if (-not $_.DeviceID) {
              Write-Warning "Device missing ID: $($_.FriendlyName)"
              # Log to central system
              Add-Content -Path "$env:TEMP\MissingIDs_$(Get-Date -Format 'yyyyMMdd').log" -Value "$(Get-Date) - Missing ID: $($_.FriendlyName)"
          }
      }
  }
  catch {
      Write-Error "Failed to retrieve device information: $_"
      # Implement retry logic or alternative method
  }
  ```

##### Information Collection
- **Required Fields**
  - Device ID (Hardware ID, Compatible ID)
  - Vendor and model information
  - Device class and category
  - Current driver version and date
  - Driver provider and signer

- **Inventory Logging**
  - Centralized database storage
  - Historical version tracking
  - Change detection and alerts
  - Automated reporting

##### Implementation Best Practices
1. **Scheduled Scans**
   - Regular inventory updates
   - Differential scanning for changes
   - Off-peak hour execution

2. **Security Considerations**
   - Secure storage of hardware data
   - Access control for sensitive information
   - Audit logging of all access

3. **Maintenance**
   - Regular validation of collection methods
   - Update hardware ID databases
   - Review and clean old entries

#### 7.2.2 Enhanced Automated Discovery

##### Comprehensive Scanning
- **Network Device Discovery**
  ```powershell
  # Network device discovery with NMAP
  nmap -sn 192.168.1.0/24 -oG - | Select-String 'Up$' | ForEach-Object { $_ -replace '^.*?\s(\S+)\s+\(' } | Where-Object { $_ -ne '' }
  
  # Get detailed network device information
  Get-NetAdapter | Select-Object Name, InterfaceDescription, Status, LinkSpeed, MacAddress
  ```

- **Storage Infrastructure**
  ```powershell
  # List all storage controllers
  Get-WmiObject Win32_SCSIController | Select-Object Name, Manufacturer, DeviceID
  
  # Get disk information
  Get-PhysicalDisk | Select-Object FriendlyName, MediaType, Size, HealthStatus, OperationalStatus
  ```

- **Specialized Hardware**
  ```powershell
  # List all PCI devices
  Get-PnpDevice -Class 'System' | Where-Object { $_.InstanceId -match '^PCI' }
  
  # Find GPUs and specialized processors
  Get-WmiObject Win32_VideoController | Select-Object Name, AdapterRAM, DriverVersion
  Get-WmiObject Win32_Processor | Select-Object Name, NumberOfCores, MaxClockSpeed
  ```

##### Scheduled Scanning
- **Task Scheduler Integration**
  ```powershell
  # Create a scheduled task for weekly scans
  $action = New-ScheduledTaskAction -Execute 'PowerShell.exe' -Argument '-File "C:\Scripts\HardwareScan.ps1" -NoProfile -NonInteractive'
  $trigger = New-ScheduledTaskTrigger -Weekly -At '2:00AM' -DaysOfWeek Sunday
  Register-ScheduledTask -Action $action -Trigger $trigger -TaskName "Weekly Hardware Scan" -Description "Scans and updates hardware inventory"
  ```

- **Differential Scanning**
  - Compare current scan with baseline
  - Alert on new/removed devices
  - Track hardware changes over time

##### Integration with Deployment Tools
- **Microsoft Endpoint Configuration Manager**
  - Hardware inventory classes
  - Custom WMI queries
  - Collection evaluation schedules
  - Reporting services

- **Third-Party Integration**
  ```powershell
  # Example: Export to PDQ Inventory
  $devices = Get-PnpDevice -PresentOnly | Select-Object Status, Class, FriendlyName, InstanceId
  $devices | Export-Csv -Path "PDQ_Import_$(Get-Date -Format 'yyyyMMdd').csv" -NoTypeInformation
  
  # Example: Lansweeper API Integration
  $body = @{
      "apiKey" = "your-api-key"
      "devices" = @($devices | ConvertTo-Json)
  }
  Invoke-RestMethod -Uri "https://your-lansweeper/api/import" -Method Post -Body $body -ContentType "application/json"
  ```

##### Advanced Discovery Features
- **Agent-Based Discovery**
  - Lightweight background service
  - Real-time hardware change detection
  - Offline data collection

- **Network Topology Mapping**
  - Device relationships
  - Connection paths
  - Bandwidth monitoring

- **Vulnerability Scanning**
  - CVE database integration
  - Security patch status
  - Configuration compliance

#### Documentation Systems
- **CMDB Integration**
  - ServiceNow
  - BMC Remedy
  - Custom databases
- **Spreadsheet Templates**
  - Hardware ID tracking
  - Driver version history
  - Change logs

### 7.3 Driver Version Comparison

#### Version Analysis Methods
- **Baseline Comparison**
  ```powershell
  # Compare installed drivers against baseline
  $baseline = Import-Csv -Path "C:\Drivers\baseline_versions.csv"
  $current = Get-WmiObject Win32_PnPSignedDriver | Where-Object { $_.DeviceName -ne $null } | 
             Select-Object DeviceName, DeviceID, DriverVersion, DriverDate
  
  $comparison = Compare-Object -ReferenceObject $baseline -DifferenceObject $current -Property DeviceID, DriverVersion -PassThru
  $outdated = $comparison | Where-Object { $_.SideIndicator -eq '=>' }
  $outdated | Export-Csv -Path "C:\Reports\outdated_drivers_$(Get-Date -Format 'yyyyMMdd').csv" -NoTypeInformation
  ```

- **Vendor Database Lookup**
  ```powershell
  # Check for driver updates via vendor API
  $devices = Get-PnpDevice -PresentOnly | Where-Object { $_.InstanceId -match '^PCI' }
  foreach ($device in $devices) {
      $hwid = (Get-PnpDeviceProperty -InstanceId $device.InstanceId -KeyName 'DEVPKEY_Device_HardwareIds').Data[0]
      # Example: Query vendor's update service
      $latestVersion = Invoke-RestMethod -Uri "https://api.vendor.com/drivers/latest?hwid=$hwid"
      [PSCustomObject]@{
          Device = $device.FriendlyName
          CurrentVersion = (Get-PnpDeviceProperty -InstanceId $device.InstanceId -KeyName 'DEVPKEY_Device_DriverVersion').Data
          LatestVersion = $latestVersion.Version
          UpdateAvailable = [version]$latestVersion.Version -gt [version](Get-PnpDeviceProperty -InstanceId $device.InstanceId -KeyName 'DEVPKEY_Device_DriverVersion').Data
      }
  }
  ```

#### Compliance Monitoring
- **Version Tracking**
  - Minimum required versions
  - Approved driver versions
  - Blacklisted/problematic versions
  - Security patch levels

- **Reporting**
  ```powershell
  # Generate compliance report
  $report = Get-PnpDevice | ForEach-Object {
      $driver = Get-WmiObject Win32_PnPSignedDriver | Where-Object { $_.DeviceID -eq $_.DeviceID }
      [PSCustomObject]@{
          DeviceName = $_.FriendlyName
          DeviceID = $_.DeviceID
          DriverVersion = $driver.DriverVersion
          DriverDate = [DateTime]::ParseExact($driver.DriverDate.Split('.')[0], 'yyyyMMdd', $null)
          Status = switch ($driver.IsSigned) {
              $true { 'Signed' }
              default { 'Unsigned' }
          }
      }
  }
  $report | Export-Csv -Path "C:\Reports\driver_compliance_$(Get-Date -Format 'yyyyMMdd').csv" -NoTypeInformation
  ```

#### Historical Tracking
- **Version History**
  - SQL database for version tracking
  - Change logging with timestamps
  - User attribution for manual updates
  - Rollback points

- **Audit Logging**
  ```powershell
  # Log driver changes
  $eventParams = @{
      LogName = 'System'
      Source = 'Driver Management'
      EventId = 1001
      EntryType = 'Information'
      Message = 'Driver version change detected'
      Category = 1
      RawData = $comparison | ConvertTo-Json -Compress
  }
  Write-EventLog @eventParams
  ```

#### Alerting and Remediation
- **Notification System**
  - Email alerts for critical updates
  - Dashboard integration
  - Ticketing system integration
  - Automated remediation workflows

- **Remediation Scripts**
  ```powershell
  # Example: Automated driver update
  $problematicDrivers = Import-Csv -Path "C:\Reports\problematic_drivers.csv"
  foreach ($driver in $problematicDrivers) {
      try {
          $update = Find-DriverUpdate -DeviceID $driver.DeviceID
          if ($update) {
              Install-DriverUpdate -Update $update -Force
              Write-Log "Updated $($driver.DeviceName) to version $($update.Version)"
          }
      }
      catch {
          Write-Error "Failed to update $($driver.DeviceName): $_"
          Send-Notification -Type 'Error' -Message "Driver update failed for $($driver.DeviceName)"
      }
  }
  ```

### 7.4 Driver Dependencies

#### Dependency Mapping
- **Dependency Types**
  ```powershell
  # Example: Check driver dependencies using DISM
  $driverPath = "C:\Drivers\Network\Driver1.inf"
  $dependencies = DISM.exe /Image:C:\ /Get-DriverInfo /Driver:$driverPath
  $dependencies | Where-Object { $_ -match 'Dependent\s+:' } | ForEach-Object {
      $_.Trim() -replace 'Dependent\s+:', ''
  }
  ```

- **Common Dependency Chains**
  - Chipset → Storage → Network/Graphics
  - Base System → Firmware → Device Drivers
  - Framework → Service → Application Drivers

#### Deployment Sequencing
- **Dependency Resolution**
  ```powershell
  function Install-DriverWithDependencies {
      param (
          [string]$DriverPath,
          [string]$LogPath = "$env:TEMP\DriverInstall.log"
      )
      
      # 1. Check for INF file
      if (-not (Test-Path $DriverPath)) {
          throw "Driver path not found: $DriverPath"
      }
      
      # 2. Parse INF for dependencies
      $infContent = Get-Content $DriverPath
      $dependencies = $infContent | 
          Where-Object { $_ -match '^\s*Include\s*=|^\s*Needs\s*=' } |
          ForEach-Object { ($_ -split '=')[1].Trim('"\'', ' ') }
      
      # 3. Install dependencies first
      $dependencies | ForEach-Object {
          $depPath = Join-Path (Split-Path $DriverPath) $_
          if (Test-Path $depPath) {
              Install-DriverWithDependencies -DriverPath $depPath -LogPath $LogPath
          }
      }
      
      # 4. Install the driver
      Add-Content -Path $LogPath -Value "[$(Get-Date)] Installing: $DriverPath"
      pnputil /add-driver $DriverPath /install /subdirs | Out-Null
  }
  ```

- **Deployment Groups**
  | Group | Description | Example Drivers |
  |-------|-------------|-----------------|
  | 1 | Firmware/BIOS | System firmware, TPM updates |
  | 2 | Chipset | Intel/AMD chipset drivers |
  | 3 | Storage | RAID, NVMe, SATA controllers |
  | 4 | Network | NIC, wireless, Bluetooth |
  | 5 | Graphics | GPU, display adapters |
  | 6 | Peripherals | Printers, scanners, input devices |

#### Conflict Resolution
- **Common Conflicts**
  - Multiple versions of same driver
  - Incompatible driver stacks
  - Resource conflicts (IRQ, memory)
  - Security policy restrictions

- **Conflict Detection**
  ```powershell
  # Check for driver conflicts in Event Log
  $conflicts = Get-WinEvent -FilterHashtable @{
      LogName = 'System'
      ProviderName = 'Microsoft-Windows-PnP'
      Level = 3 # Warning
  } | Where-Object { $_.Message -match 'conflict|failed to load' }
  
  if ($conflicts) {
      $conflictReport = $conflicts | Select-Object TimeCreated, 
          @{Name='Device';Expression={ ($_.Properties[1].Value -split ';')[0] }},
          @{Name='Issue';Expression={ $_.Message -split '\r?\n' | Select-Object -First 1 }}
      
      $conflictReport | Export-Csv -Path "C:\Reports\DriverConflicts_$(Get-Date -Format 'yyyyMMdd').csv" -NoTypeInformation
  }
  ```

#### Documentation and Tracking
- **Dependency Database**
  - SQL schema for driver relationships
  - Version compatibility matrix
  - Known issues and workarounds
  - Update history and changelog

- **Automated Documentation**
  ```powershell
  # Generate dependency graph using Graphviz
  $graph = @"
  digraph DriverDependencies {
      node [shape=box];
      $(Get-ChildItem -Path 'C:\Drivers\' -Recurse -Filter '*.inf' | ForEach-Object {
          $deps = Get-Content $_.FullName | 
                  Where-Object { $_ -match '^\s*Include\s*=' } |
                  ForEach-Object { "\"$($_.Name)\" -> \"$($_ -replace '^.*?=' -replace '["\'\s]', '')\";" }
          $deps -join "`n"
      })
  }
  "@
  $graph | Out-File -FilePath 'C:\Docs\driver_dependencies.dot'
  # Use Graphviz to generate visualization: dot -Tpng driver_dependencies.dot -o dependencies.png
  ```

### 7.5 Export/Import Functionality

#### Export Capabilities
- **Full System Export**
  ```powershell
  function Export-HardwareInventory {
      param (
          [string]$OutputPath = "$env:TEMP\HardwareInventory_$(Get-Date -Format 'yyyyMMdd').json",
          [ValidateSet('JSON', 'CSV', 'XML')]
          [string]$Format = 'JSON'
      )
      
      $inventory = [PSCustomObject]@{
          ComputerName = $env:COMPUTERNAME
          Timestamp = Get-Date -Format 'o'
          OS = [PSCustomObject]@{
              Name = (Get-CimInstance Win32_OperatingSystem).Caption
              Version = [System.Environment]::OSVersion.Version
              Architecture = (Get-CimInstance Win32_OperatingSystem).OSArchitecture
          }
          Hardware = Get-CimInstance Win32_ComputerSystem | Select-Object Manufacturer, Model, SystemType, NumberOfProcessors, TotalPhysicalMemory
          Processors = Get-CimInstance Win32_Processor | Select-Object Name, Manufacturer, NumberOfCores, MaxClockSpeed
          Memory = Get-CimInstance Win32_PhysicalMemory | Select-Object Manufacturer, PartNumber, Capacity, Speed, DeviceLocator
          Disks = Get-Disk | Select-Object FriendlyName, Size, BusType, PartitionStyle, HealthStatus
          NetworkAdapters = Get-NetAdapter | Where-Object { $_.Status -eq 'Up' } | Select-Object Name, InterfaceDescription, MacAddress, LinkSpeed
          Drivers = Get-WmiObject Win32_PnPSignedDriver | Where-Object { $_.DeviceName } | Select-Object DeviceName, DeviceID, DriverVersion, DriverDate, IsSigned
      }
      
      switch ($Format) {
          'JSON' { $inventory | ConvertTo-Json -Depth 5 | Out-File -FilePath $OutputPath -Encoding utf8 }
          'CSV' { 
              $csvData = $inventory | ConvertTo-Csv -NoTypeInformation
              $csvData | Out-File -FilePath $OutputPath -Encoding utf8 
          }
          'XML' { $inventory | Export-Clixml -Path $OutputPath -Encoding UTF8 }
      }
      
      Write-Output "Inventory exported to: $OutputPath"
      return $OutputPath
  }
  ```

- **Selective Export**
  ```powershell
  function Export-HardwareComponent {
      param (
          [Parameter(Mandatory=$true)]
          [ValidateSet('CPU', 'Memory', 'Disk', 'Network', 'Drivers')]
          [string]$Component,
          [string]$OutputPath = "$env:TEMP\${Component}_Inventory_$(Get-Date -Format 'yyyyMMdd').csv"
      )
      
      $data = switch ($Component) {
          'CPU' { Get-CimInstance Win32_Processor | Select-Object Name, Manufacturer, NumberOfCores, MaxClockSpeed }
          'Memory' { Get-CimInstance Win32_PhysicalMemory | Select-Object Manufacturer, PartNumber, Capacity, Speed }
          'Disk' { Get-Disk | Select-Object FriendlyName, Size, BusType, HealthStatus, OperationalStatus }
          'Network' { Get-NetAdapter | Select-Object Name, InterfaceDescription, MacAddress, LinkSpeed, Status }
          'Drivers' { Get-WmiObject Win32_PnPSignedDriver | Where-Object { $_.DeviceName } | Select-Object DeviceName, DeviceID, DriverVersion, DriverDate, IsSigned }
      }
      
      $data | Export-Csv -Path $OutputPath -NoTypeInformation -Encoding UTF8
      Write-Output "$Component data exported to: $OutputPath"
      return $OutputPath
  }
  ```

#### Import Capabilities
- **Import to Database**
  ```powershell
  function Import-HardwareInventoryToSQL {
      param (
          [Parameter(Mandatory=$true)]
          [string]$InputFile,
          [string]$Server = 'localhost',
          [string]$Database = 'HardwareInventory',
          [PSCredential]$Credential
      )
      
      $connectionString = "Server=$Server;Database=$Database;Integrated Security=True;"
      if ($Credential) {
          $connectionString = "Server=$Server;Database=$Database;User ID=$($Credential.UserName);Password=$($Credential.GetNetworkCredential().Password);"
      }
      
      $json = Get-Content -Path $InputFile -Raw | ConvertFrom-Json
      $connection = New-Object System.Data.SqlClient.SqlConnection($connectionString)
      $connection.Open()
      
      try {
          # Insert system information
          $command = $connection.CreateCommand()
          $command.CommandText = """
              INSERT INTO Systems (ComputerName, OSName, OSVersion, OSArchitecture, LastUpdated)
              VALUES (@ComputerName, @OSName, @OSVersion, @OSArchitecture, @Timestamp);
              SELECT SCOPE_IDENTITY();
          """
          $command.Parameters.AddWithValue('@ComputerName', $json.ComputerName) | Out-Null
          $command.Parameters.AddWithValue('@OSName', $json.OS.Name) | Out-Null
          $command.Parameters.AddWithValue('@OSVersion', $json.OS.Version) | Out-Null
          $command.Parameters.AddWithValue('@OSArchitecture', $json.OS.Architecture) | Out-Null
          $command.Parameters.AddWithValue('@Timestamp', [DateTime]::Parse($json.Timestamp)) | Out-Null
          $systemId = $command.ExecuteScalar()
          
          # Insert drivers
          $json.Drivers | ForEach-Object {
              $command = $connection.CreateCommand()
              $command.CommandText = """
                  IF NOT EXISTS (SELECT 1 FROM Drivers WHERE DeviceID = @DeviceID AND SystemID = @SystemID)
                  BEGIN
                      INSERT INTO Drivers (SystemID, DeviceName, DeviceID, DriverVersion, DriverDate, IsSigned, LastUpdated)
                      VALUES (@SystemID, @DeviceName, @DeviceID, @DriverVersion, @DriverDate, @IsSigned, @Timestamp);
                  END
                  ELSE
                  BEGIN
                      UPDATE Drivers 
                      SET DeviceName = @DeviceName, 
                          DriverVersion = @DriverVersion,
                          DriverDate = @DriverDate,
                          IsSigned = @IsSigned,
                          LastUpdated = @Timestamp
                      WHERE DeviceID = @DeviceID AND SystemID = @SystemID;
                  END
              """
              $command.Parameters.AddWithValue('@SystemID', $systemId) | Out-Null
              $command.Parameters.AddWithValue('@DeviceName', $_.DeviceName) | Out-Null
              $command.Parameters.AddWithValue('@DeviceID', $_.DeviceID) | Out-Null
              $command.Parameters.AddWithValue('@DriverVersion', $_.DriverVersion) | Out-Null
              $command.Parameters.AddWithValue('@DriverDate', [DateTime]::Parse($_.DriverDate)) | Out-Null
              $command.Parameters.AddWithValue('@IsSigned', $_.IsSigned) | Out-Null
              $command.Parameters.AddWithValue('@Timestamp', [DateTime]::Now) | Out-Null
              $command.ExecuteNonQuery() | Out-Null
          }
          
          Write-Output "Successfully imported inventory to database."
      }
      catch {
          Write-Error "Failed to import inventory: $_"
          throw
      }
      finally {
          $connection.Close()
      }
  }
  ```

#### Security and Version Control
- **Secure Storage**
  ```powershell
  function Protect-InventoryFile {
      param (
          [Parameter(Mandatory=$true)]
          [string]$InputFile,
          [string]$OutputPath = [System.IO.Path]::ChangeExtension($InputFile, '.encrypted'),
          [Parameter(Mandatory=$true)]
          [SecureString]$Key
      )
      
      $keyBytes = [System.Runtime.InteropServices.Marshal]::SecureStringToBSTR($Key)
      $key = [System.Runtime.InteropServices.Marshal]::PtrToStringAuto($keyBytes)
      
      try {
          $content = [System.IO.File]::ReadAllBytes($InputFile)
          $protected = [System.Security.Cryptography.ProtectedData]::Protect(
              $content, 
              [System.Text.Encoding]::UTF8.GetBytes($key), 
              [System.Security.Cryptography.DataProtectionScope]::CurrentUser
          )
          
          [System.IO.File]::WriteAllBytes($OutputPath, $protected)
          Write-Output "File encrypted and saved to: $OutputPath"
      }
      finally {
          [System.Runtime.InteropServices.Marshal]::ZeroFreeBSTR($keyBytes)
      }
  }
  ```

- **Git Integration**
  ```powershell
  function Update-InventoryRepository {
      param (
          [string]$RepoPath = "C:\InventoryRepo",
          [string]$CommitMessage = "Update inventory - $(Get-Date -Format 'yyyy-MM-dd HH:mm:ss')"
      )
      
      if (-not (Test-Path $RepoPath)) {
          New-Item -ItemType Directory -Path $RepoPath -Force | Out-Null
          Set-Location $RepoPath
          git init
          git remote add origin <repository-url>
          git fetch
          git checkout -b main origin/main
      }
      
      Set-Location $RepoPath
      
      # Export and add new inventory
      $exportFile = Export-HardwareInventory -OutputPath "$RepoPath\inventory_$(Get-Date -Format 'yyyyMMdd_HHmmss').json"
      git add $exportFile
      
      # Commit and push changes
      git commit -m $CommitMessage
      git push origin main
  }
  ```

### 7.6 Analysis and Reporting

#### Compliance Checking
- Verify driver signatures
- Check for known vulnerabilities
- Audit against security baselines
- Generate compliance reports

#### Optimization Opportunities
- Identify outdated drivers
- Find redundant drivers
- Spot potential conflicts
- Highlight performance bottlenecks

### 7.7 Driver Inventory Best Practices

## 8. Driver Packaging

### 8.1 Creating Driver Packages

#### Export Methods
- **Using DISM (Deployment Image Servicing and Management)**
  ```powershell
  # Export all drivers from online Windows installation
  $exportPath = "C:\DriverPackages\$((Get-ComputerInfo).CsModel)"
  New-Item -ItemType Directory -Path $exportPath -Force | Out-Null
  Export-WindowsDriver -Online -Destination $exportPath -Verbose
  
  # Verify exported drivers
  $exportedDrivers = Get-ChildItem -Path $exportPath -Recurse -Filter "*.inf"
  Write-Output "Exported $($exportedDrivers.Count) drivers to $exportPath"
  ```

- **Using PowerShell (Manual Extraction)**
  ```powershell
  function Export-DriverPackage {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$OutputPath,
          [string[]]$ComputerName = $env:COMPUTERNAME,
          [switch]$IncludeWindowsNative,
          [switch]$ValidateSignature
      )
      
      begin {
          $script:exportedDrivers = @()
          $script:validationResults = @()
          
          # Create output directory structure
          $templateDirs = @(
              "$OutputPath\Drivers",
              "$OutputPath\Scripts",
              "$OutputPath\Metadata"
          )
          $templateDirs | ForEach-Object { New-Item -ItemType Directory -Path $_ -Force | Out-Null }
          
          # Initialize metadata
          $metadata = @{
              PackageInfo = @{
                  Created = Get-Date -Format 'o'
                  Source = $env:COMPUTERNAME
                  Tools = @("DISM", "PowerShell $($PSVersionTable.PSVersion)")
              }
              Drivers = @()
          }
      }
      
      process {
          foreach ($computer in $ComputerName) {
              try {
                  Write-Verbose "Processing computer: $computer"
                  
                  # Get all PnP devices and their drivers
                  $devices = Get-PnpDevice -PresentOnly -Status OK | 
                      Where-Object { $_.Class -notin @('System', 'Computer') }
                  
                  foreach ($device in $devices) {
                      $driver = Get-PnpDeviceProperty -InstanceId $device.InstanceId -KeyName 'DEVPKEY_Device_DriverDesc'
                      $driverFiles = Get-PnpDeviceProperty -InstanceId $device.InstanceId -KeyName 'DEVPKEY_Device_Driver'
                      
                      if ($driverFiles.Data) {
                          $driverPath = $driverFiles.Data -replace '^.*?([a-z]:\\.*)', '$1' -replace '\\\\\?\\', ''
                          $driverDir = Split-Path -Path $driverPath -Parent
                          
                          # Skip Windows native drivers if not included
                          if (-not $IncludeWindowsNative -and $driverDir -like "$env:SystemRoot\*" ) {
                              continue
                          }
                          
                          # Copy driver files
                          $destPath = "$OutputPath\Drivers\$($device.Class)"
                          New-Item -ItemType Directory -Path $destPath -Force | Out-Null
                          
                          $driverFiles = Get-ChildItem -Path $driverDir -Recurse | 
                              Where-Object { $_.Extension -in @('.inf','.cat','.sys','.dll') }
                          
                          foreach ($file in $driverFiles) {
                              $relativePath = $file.FullName.Substring(3)  # Remove drive letter
                              $destFile = Join-Path $destPath $relativePath
                              $destDir = Split-Path -Parent $destFile
                              
                              if (-not (Test-Path $destDir)) {
                                  New-Item -ItemType Directory -Path $destDir -Force | Out-Null
                              }
                              
                              Copy-Item -Path $file.FullName -Destination $destFile -Force
                              Write-Verbose "Copied: $($file.FullName) -> $destFile"
                          }
                          
                          # Add to metadata
                          $driverInfo = @{
                              Device = $device.FriendlyName
                              Class = $device.Class
                              Manufacturer = $device.Manufacturer
                              DriverVersion = (Get-ItemProperty -Path $driverPath).VersionInfo.FileVersion
                              DriverDate = (Get-Item -Path $driverPath).LastWriteTime
                              SourcePath = $driverDir
                              Files = $driverFiles | ForEach-Object { $_.Name }
                          }
                          
                          # Validate driver signature if requested
                          if ($ValidateSignature) {
                              $sig = Get-AuthenticodeSignature -FilePath $driverPath
                              $driverInfo['SignatureStatus'] = $sig.Status
                              $driverInfo['Signer'] = $sig.SignerCertificate.Subject
                              
                              $script:validationResults += [PSCustomObject]@{
                                  Device = $device.FriendlyName
                                  Driver = $driver.Data
                                  Status = $sig.Status
                                  Signer = $sig.SignerCertificate.Subject
                                  TimeStamper = $sig.TimeStamperCertificate.Subject
                              }
                          }
                          
                          $metadata.Drivers += $driverInfo
                          $script:exportedDrivers += $driverInfo
                      }
                  }
              }
              catch {
                  Write-Warning "Error processing $computer : $_"
              }
          }
      }
      
      end {
          # Save metadata
          $metadata | ConvertTo-Json -Depth 5 | 
              Out-File -FilePath "$OutputPath\Metadata\package.json" -Encoding utf8
          
          # Generate validation report
          if ($script:validationResults) {
              $script:validationResults | 
                  Export-Csv -Path "$OutputPath\Metadata\validation_report.csv" -NoTypeInformation
          }
          
          # Create deployment script
          $deployScript = @"
          # Driver Installation Script
          # Generated: $(Get-Date -Format 'yyyy-MM-dd HH:mm:ss')
          
          `$driverPath = Join-Path `$PSScriptRoot 'Drivers'
          `$logPath = Join-Path `$PSScriptRoot 'deployment_$(Get-Date -Format 'yyyyMMdd_HHmmss').log'
          
          function Write-Log {
              param([string]`$Message)
              `$timestamp = Get-Date -Format 'yyyy-MM-dd HH:mm:ss'
              "[`$timestamp] `$Message" | Tee-Object -FilePath `$logPath -Append
          }
          
          try {
              Write-Log 'Starting driver installation...'
              
              # Import drivers into driver store
              `$driverFiles = Get-ChildItem -Path `$driverPath -Recurse -Filter '*.inf'
              
              foreach (`$driver in `$driverFiles) {
                  try {
                      `$result = pnputil /add-driver "`$(`$driver.FullName)" /install /subdirs
                      Write-Log "Installed `$(`$driver.Name): `$result"
                  }
                  catch {
                      Write-Log "ERROR installing `$(`$driver.Name): `$_"
                  }
              }
              
              Write-Log 'Driver installation completed.'
          }
          catch {
              Write-Log "FATAL ERROR: `$_"
              exit 1
          }
          "@
          
          $deployScript | Out-File -FilePath "$OutputPath\Scripts\Install-Drivers.ps1" -Encoding utf8
          
          # Create readme
          $readme = @"
          # Driver Package
          
          ## Package Information
          - Created: $(Get-Date -Format 'yyyy-MM-dd HH:mm:ss')
          - Source: $env:COMPUTERNAME
          - Total Drivers: $($script:exportedDrivers.Count)
          
          ## Contents
          - `Drivers/`: Driver files organized by device class
          - `Scripts/`: Deployment and verification scripts
          - `Metadata/`: Package information and validation reports
          
          ## Deployment Instructions
          1. Run `Scripts\Install-Drivers.ps1` as Administrator
          2. Review the generated log file for any errors
          3. Reboot if prompted
          
          ## Validation
          $(if ($script:validationResults) {
              "- Signature validation report: `Metadata\validation_report.csv`"
          } else {
              "- Signature validation was not performed"
          })
          
          ## Notes
          - This package was generated automatically
          - Always test in a non-production environment first
          "@
          
          $readme | Out-File -FilePath "$OutputPath\README.md" -Encoding utf8
          
          # Output summary
          [PSCustomObject]@{
              PackagePath = $OutputPath
              DriverCount = $script:exportedDrivers.Count
              ValidationResults = $script:validationResults
              MetadataFile = "$OutputPath\Metadata\package.json"
              DeploymentScript = "$OutputPath\Scripts\Install-Drivers.ps1"
          }
      }
  }
  
  # Example usage:
  # Export-DriverPackage -OutputPath "C:\DriverPackages\Dell_Latitude_5420" -ValidateSignature
  ```

#### Package Organization
- **Directory Structure**
  ```
  DriverPackages/
  ├── Vendor_Model_OS/         # e.g., Dell_Latitude_5420_Win10_22H2
  │   ├── Drivers/
  │   │   ├── Network/        # Network adapters
  │   │   ├── Storage/        # Disk controllers
  │   │   ├── Graphics/       # Display adapters
  │   │   └── Chipset/        # Chipset drivers
  │   ├── Scripts/
  │   │   ├── Install.ps1     # Installation script
  │   │   └── Validate.ps1    # Validation script
  │   └── Metadata/
  │       ├── package.json    # Package metadata
  │       ├── inventory.csv   # Driver inventory
  │       └── checksums.sha256 # File integrity
  └── README.md               # Repository documentation
  ```

- **Metadata Standards**
  ```json
  {
    "package": {
      "name": "Dell_Latitude_5420_Win10_22H2",
      "version": "1.0.0",
      "created": "2023-10-01T12:00:00Z",
      "author": "IT Department",
      "description": "Driver package for Dell Latitude 5420 (Windows 10 22H2)"
    },
    "requirements": {
      "os": "Windows 10 22H2",
      "architecture": "x64",
      "minimumMemory": "4GB",
      "diskSpace": "2GB"
    },
    "components": [
      {
        "name": "Intel Wi-Fi 6 AX201",
        "type": "Network",
        "version": "22.40.0",
        "date": "2023-05-15",
        "inf": "Netwtw10\netwtw10.inf",
        "classGuid": "{4d36e972-e325-11ce-bfc1-08002be10318}",
        "hardwareIds": [
          "PCI\VEN_8086&DEV_43F0&SUBSYS_00748086",
          "PCI\VEN_8086&DEV_43F0&SUBSYS_00748086&REV_11"
        ]
      }
    ],
    "dependencies": [
      "Intel_Chipset_Driver_10.1.18836.8283"
    ],
    "installation": {
      "command": "powershell -ExecutionPolicy Bypass -File .\\Scripts\\Install.ps1",
      "requiresReboot": true,
      "estimatedTime": "10 minutes"
    },
    "validation": {
      "script": ".\\Scripts\\Validate.ps1",
      "expectedDrivers": 42,
      "signatureCheck": true,
      "versionCheck": true
    },
    "maintenance": {
      "createdBy": "Automated Build System",
      "lastUpdated": "2023-10-01T12:30:00Z",
      "changeLog": [
        "2023-10-01: Initial package creation"
      ]
    }
  }
  ```

#### Validation and Testing
- **Pre-Package Validation**
  ```powershell
  # Validate driver signatures
  function Test-DriverSignatures {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverPath
      )
      
      $results = @()
      $driverFiles = Get-ChildItem -Path $DriverPath -Recurse -Include '*.sys','*.dll','*.exe','*.ocx'
      
      foreach ($file in $driverFiles) {
          $sig = Get-AuthenticodeSignature -FilePath $file.FullName
          $status = if ($sig.Status -eq 'Valid') { 'PASS' } else { 'FAIL' }
          
          $results += [PSCustomObject]@{
              File = $file.FullName
              Status = $status
              Signer = $sig.SignerCertificate?.Subject
              TimeStamper = $sig.TimeStamperCertificate?.Subject
              Error = if ($sig.Status -ne 'Valid') { $sig.StatusMessage } else { $null }
          }
      }
      
      $results | Format-Table -AutoSize
      
      # Generate summary
      $summary = $results | Group-Object Status
      $summary | ForEach-Object {
          Write-Host "$($_.Name): $($_.Count) files" -ForegroundColor $(if ($_.Name -eq 'PASS') { 'Green' } else { 'Red' })
      }
      
      # Return $true only if all drivers are properly signed
      return ($summary | Where-Object { $_.Name -ne 'PASS' } | Measure-Object).Count -eq 0
  }
  
  # Test driver compatibility
  function Test-DriverCompatibility {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverPath,
          [string]$OSVersion = (Get-CimInstance Win32_OperatingSystem).Version,
          [string]$Architecture = (Get-CimInstance Win32_ComputerSystem).SystemType
      )
      
      $compatibility = @()
      $infFiles = Get-ChildItem -Path $DriverPath -Recurse -Filter '*.inf'
      
      foreach ($inf in $infFiles) {
          $content = Get-Content -Path $inf.FullName -Raw
          
          # Check OS compatibility
          $osCompatible = $true
          $targetOS = $null
          
          if ($content -match '\[(.*\.(NT|WOW64|amd64|x86|arm64))\]') {
              $targetOS = $matches[1]
              # Add more sophisticated OS version checking logic here
              $osCompatible = $true  # Placeholder
          }
          
          # Check architecture
          $archCompatible = $true
          if ($content -match '^Architecture\s*=\s*(\w+)') {
              $driverArch = $matches[1]
              $archCompatible = $driverArch -eq $Architecture
          }
          
          $compatibility += [PSCustomObject]@{
              Driver = $inf.Name
              OSCompatible = $osCompatible
              ArchitectureCompatible = $archCompatible
              TargetOS = $targetOS
              Status = if ($osCompatible -and $archCompatible) { 'PASS' else 'WARNING' }
          }
      }
      
      $compatibility | Format-Table -AutoSize
      return $compatibility
  }
  ```

#### Repository Management
- **Version Control Integration**
  ```powershell
  # Initialize Git repository for driver packages
  function Initialize-DriverRepository {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$RepositoryPath,
          [string]$RemoteUrl,
          [PSCredential]$Credential
      )
      
      if (-not (Test-Path $RepositoryPath)) {
          New-Item -ItemType Directory -Path $RepositoryPath -Force | Out-Null
      }
      
      Set-Location $RepositoryPath
      
      # Initialize repository if it doesn't exist
      if (-not (Test-Path '.git')) {
          git init
          git config user.name "Automated Driver Packaging"
          git config user.email "driver-packages@example.com"
          
          if ($RemoteUrl) {
              git remote add origin $RemoteUrl
              git fetch
              
              # Check if remote has a main branch
              $hasMain = git ls-remote --heads origin main
              if ($hasMain) {
                  git checkout -b main --track origin/main
              } else {
                  git checkout -b main
              }
          }
          
          # Create .gitignore
          @'
          # Ignore temporary files
          *.tmp
          *.temp
          
          # Ignore logs
          *.log
          
          # Ignore build artifacts
          Build/
          
          # Ignore local settings
          .DS_Store
          Thumbs.db
          
          # Ignore package caches
          **/node_modules/
          **/packages/
          
          # Keep driver files
          !**/Drivers/**
          !**/Scripts/**
          !**/Metadata/**
          '@ | Out-File -FilePath "$RepositoryPath\.gitignore" -Encoding utf8
          
          # Create README
          @"
          # Driver Package Repository
          
          This repository contains driver packages for various hardware models.
          
          ## Structure
          
          - `/Vendor_Model_OS/` - Driver packages organized by vendor, model, and OS
            - `Drivers/` - Actual driver files
            - `Scripts/` - Installation and validation scripts
            - `Metadata/` - Package metadata and documentation
          
          ## Usage
          
          1. Clone this repository
          2. Navigate to the desired driver package
          3. Run the installation script as Administrator
          
          ## Maintenance
          
          - Update packages using the packaging scripts
          - Always validate drivers before committing
          - Follow semantic versioning for package versions
          
          ## License
          
          Proprietary - For internal use only
          "@ | Out-File -FilePath "$RepositoryPath\README.md" -Encoding utf8
          
          # Initial commit
          git add .
          git commit -m "Initial commit"
          
          if ($RemoteUrl) {
              git push -u origin main
          }
      }
      
      Write-Output "Repository initialized at $RepositoryPath"
  }
  
  # Add a new driver package to the repository
  function Add-DriverPackage {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$SourcePath,
          [Parameter(Mandatory=$true)]
          [string]$RepositoryPath,
          [string]$Version = "1.0.0",
          [string]$ChangeLog = "Initial version"
      )
      
      # Validate source package
      if (-not (Test-Path "$SourcePath\Metadata\package.json")) {
          throw "Source path does not contain a valid driver package (missing Metadata/package.json)"
      }
      
      # Read package metadata
      $metadata = Get-Content -Path "$SourcePath\Metadata\package.json" -Raw | ConvertFrom-Json
      $packageName = $metadata.package.name
      
      if (-not $packageName) {
          throw "Package metadata is missing required 'name' field"
      }
      
      # Create destination directory
      $destPath = Join-Path $RepositoryPath $packageName
      if (Test-Path $destPath) {
          throw "Package '$packageName' already exists in the repository"
      }
      
      # Copy package files
      Copy-Item -Path $SourcePath -Destination $destPath -Recurse -Force
      
      # Update version in metadata
      $metadata.package.version = $Version
      $metadata.maintenance.lastUpdated = Get-Date -Format 'o'
      if (-not $metadata.maintenance.changeLog) {
          $metadata.maintenance | Add-Member -NotePropertyName 'changeLog' -NotePropertyValue @()
      }
      $metadata.maintenance.changeLog = @("$($metadata.maintenance.lastUpdated): $ChangeLog") + $metadata.maintenance.changeLog
      
      # Save updated metadata
      $metadata | ConvertTo-Json -Depth 10 | 
          Out-File -FilePath "$destPath\Metadata\package.json" -Encoding utf8 -Force
      
      # Add to version control
      Set-Location $RepositoryPath
      git add $packageName
      git commit -m "Add $packageName v$Version"
      
      Write-Output "Added package '$packageName' v$Version to the repository"
      return $destPath
  }
  ```

### 8.2 Version Control and Naming Conventions

#### Naming Standards
- **Package Naming Format**
  ```
  {Vendor}_{DeviceModel}_{DriverType}_{OSVersion}_{Architecture}_{Version}_{BuildNumber}
  ```

- **Field Definitions**
  | Field | Description | Format | Examples |
  |--------|-------------|---------|----------|
  | Vendor | Manufacturer name | No spaces, alphanumeric | `Dell`, `HP`, `Lenovo`, `Intel` |
  | DeviceModel | Model identifier | No spaces, alphanumeric | `Latitude5420`, `EliteBook840`, `ThinkPadX1` |
  | DriverType | Driver category | PascalCase | `Chipset`, `Network`, `Graphics`, `Audio` |
  | OSVersion | OS version | OS+Version | `Win10_22H2`, `Win11_23H2`, `WinServer2022` |
  | Architecture | CPU architecture | x86, x64, arm64 | `x64`, `arm64` |
  | Version | Driver version | Semantic versioning | `1.0.0`, `22.40.0` |
  | BuildNumber | Build identifier | Optional, numeric | `1234`, `20230315` |

- **Examples**
  ```
  Dell_Latitude5420_Chipset_Win10_22H2_x64_1.0.0_1234
  Intel_WiFi6_AX201_Network_Win11_23H2_arm64_22.40.0_20230315
  NVIDIA_RTX_A5000_Graphics_Win10_22H2_x64_456.71
  ```

#### Version Control Implementation

- **Repository Structure**
  ```
  DriverRepository/
  ├── .git/
  ├── .gitattributes
  ├── .gitignore
  ├── README.md
  ├── CHANGELOG.md
  ├── docs/
  │   ├── naming_conventions.md
  │   ├── versioning_policy.md
  │   └── contribution_guide.md
  ├── packages/
  │   ├── Dell/
  │   │   ├── Latitude5420/
  │   │   │   ├── Chipset_Win10_22H2_x64_1.0.0_1234/
  │   │   │   │   ├── Drivers/
  │   │   │   │   ├── Metadata/
  │   │   │   │   └── package.json
  │   │   │   └── Chipset_Win10_22H2_x64_1.1.0_1245/
  │   │   └── XPS15/
  │   │       └── ...
  │   └── Intel/
  │       └── WiFi6_AX201/
  │           └── Network_Win11_23H2_arm64_22.40.0_20230315/
  └── tools/
      ├── validation_scripts/
      └── deployment_scripts/
  ```

- **Git Configuration (`.gitattributes`)**
  ```gitattributes
  # Line Endings
  * text=auto eol=lf
  *.{cmd,[cC][mM][dD]} text eol=crlf
  *.{ps1,psm1,psd1,ps1xml} text eol=crlf
  
  # Binary Files (treat as is, no diff)
  *.{exe,dll,sys,cat,inf,oem,bin,dat} binary
  
  # Diff/Merge Settings
  *.inf diff=ini
  *.json diff=json
  
  # File Size Limits
  *.exe filter=lfs diff=lfs merge=lfs -text
  *.dll filter=lfs diff=lfs merge=lfs -text
  *.sys filter=lfs diff=lfs merge=lfs -text
  
  # Export Ignore
  /.gitattributes export-ignore
  /.gitignore export-ignore
  /docs/ export-ignore
  ```

- **Version Control Best Practices**
  - **Branching Strategy**
    - `main`: Production-ready driver packages
    - `staging`: Pre-release testing
    - `feature/*`: New driver packages or updates
    - `hotfix/*`: Critical fixes for production

  - **Commit Message Format**
    ```
    [type](scope): description
    
    [optional body]
    
    [optional footer(s)]
    ```
    
    - **Types**: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`
    - **Scope**: Package name or component (e.g., `Dell_Latitude5420`, `Intel_Network`)
    - **Example**:
      ```
      feat(Intel_WiFi6): Add support for Windows 11 23H2
      
      - Updated driver to version 22.40.0
      - Added ARM64 architecture support
      - Fixed connectivity issues with 6GHz band
      
      Closes #123
      ```

  - **Tagging Strategy**
    - Lightweight tags for specific versions: `v1.0.0`
    - Annotated tags for releases: `Dell_Latitude5420_Chipset_1.0.0`
    - Tag format: `{PackageName}_{Version}`

  - **Access Control**
    ```powershell
    # .git/config example
    [core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true
    [remote "origin"]
        url = https://git.example.com/drivers/repo.git
        fetch = +refs/heads/*:refs/remotes/origin/*
    [branch "main"]
        remote = origin
        merge = refs/heads/main
    [receive]
        denyCurrentBranch = updateInstead
    [http]
        sslVerify = true
        sslBackend = schannel
    [credential]
        helper = manager-core
    [filter "lfs"]
        clean = git-lfs clean -- %f
        smudge = git-lfs smudge -- %f
        process = git-lfs filter-process
        required = true
    ```

  - **Git Hooks**
    - Pre-commit: Validate package structure and metadata
    - Pre-push: Run integration tests
    - Post-merge: Update dependencies and run validations

  - **Large File Storage (LFS)**
    - Track large binary files with Git LFS
    - Configure in `.gitattributes`
    - Example LFS configuration:
      ```
      # Track all driver files with LFS
      *.exe filter=lfs diff=lfs merge=lfs -text
      *.dll filter=lfs diff=lfs merge=lfs -text
      *.sys filter=lfs diff=lfs merge=lfs -text
      *.inf filter=lfs diff=lfs merge=lfs -text
      *.cat filter=lfs diff=lfs merge=lfs -text
      ```

- **Automated Version Tracking**
  ```powershell
  function New-DriverPackageVersion {
      [CmdletBinding()]
      param(
          [Parameter(Mandatory=$true)]
          [string]$SourcePath,
          
          [Parameter(Mandatory=$true)]
          [ValidatePattern('^\d+\.\d+\.\d+$')]
          [string]$Version,
          
          [string]$ChangeLog,
          
          [ValidateSet('major', 'minor', 'patch')]
          [string]$Bump = 'patch',
          
          [switch]$SkipValidation
      )
      
      # Get package metadata
      $metadataPath = Join-Path $SourcePath 'Metadata\package.json'
      if (-not (Test-Path $metadataPath)) {
          throw "Package metadata not found at $metadataPath"
      }
      
      $metadata = Get-Content -Path $metadataPath -Raw | ConvertFrom-Json -AsHashtable
      
      # Calculate new version
      if (-not $Version) {
          $currentVersion = [Version]$metadata.package.version
          $major, $minor, $patch = $currentVersion.Major, $currentVersion.Minor, $currentVersion.Build
          
          switch ($Bump) {
              'major' { $major++; $minor = 0; $patch = 0 }
              'minor' { $minor++; $patch = 0 }
              'patch' { $patch++ }
          }
          
          $Version = "$major.$minor.$patch"
      }
      
      # Validate package
      if (-not $SkipValidation) {
          Write-Host "Validating package..." -ForegroundColor Cyan
          $validationResult = Test-DriverPackage -Path $SourcePath
          if (-not $validationResult.IsValid) {
              throw "Package validation failed: $($validationResult.Message)"
          }
      }
      
      # Create new version directory
      $packageName = $metadata.package.name
      $destDir = Join-Path (Split-Path (Split-Path $SourcePath)) "${packageName}_$Version"
      
      if (Test-Path $destDir) {
          throw "Version $Version already exists at $destDir"
      }
      
      # Copy files
      New-Item -ItemType Directory -Path $destDir | Out-Null
      Get-ChildItem -Path $SourcePath -Exclude '.git' | 
          Copy-Item -Destination $destDir -Recurse -Force
      
      # Update metadata
      $metadata.package.version = $Version
      $metadata.package.releaseDate = Get-Date -Format 'o'
      
      if (-not $metadata.ContainsKey('changelog')) {
          $metadata['changelog'] = @()
      }
      
      $changeEntry = @{
          version = $Version
          date = Get-Date -Format 'yyyy-MM-dd'
          changes = if ($ChangeLog) { @($ChangeLog) } else { @('Initial release') }
          author = [System.Environment]::UserName
      }
      
      $metadata.changelog = @($changeEntry) + $metadata.changelog
      
      # Save updated metadata
      $metadata | ConvertTo-Json -Depth 10 | 
          Out-File -FilePath (Join-Path $destDir 'Metadata\package.json') -Encoding utf8
      
      # Create git tag
      $tagName = "$packageName/v$Version"
      git -C $SourcePath tag -a $tagName -m "Release $Version"
      
      Write-Host "Created new version $Version at $destDir" -ForegroundColor Green
      return $destDir
  }
  ```

#### Access Control and Security

- **Repository Permissions**
  ```yaml
  # .github/workflows/permissions.yml
  name: 'Repository Permissions'
  
  permissions:
    contents: read
    pull-requests: write
    statuses: write
    
    # Branch protection rules
    required_pull_request_reviews:
      required_approving_review_count: 1
      require_code_owner_reviews: true
      dismiss_stale_reviews: true
      
    # Required status checks
    required_status_checks:
      strict: true
      contexts:
        - 'validate-package'
        - 'test-deployment'
  ```

- **Pre-commit Hooks**
  ```powershell
  # .git/hooks/pre-commit
  #!/usr/bin/env pwsh
  
  # Validate package structure
  $packageRoot = git rev-parse --show-toplevel
  $changedFiles = git diff --cached --name-only --diff-filter=ACMRTUXB
  
  # Check for modified driver packages
  $modifiedPackages = $changedFiles | 
      Where-Object { $_ -match 'packages/([^/]+/[^/]+/[^/]+)' } | 
      ForEach-Object { $matches[1] } | 
      Select-Object -Unique
  
  foreach ($pkg in $modifiedPackages) {
      $pkgPath = Join-Path $packageRoot "packages/$pkg"
      
      # Run validation
      $result = & "$packageRoot/tools/validate-package.ps1" -Path $pkgPath
      
      if ($result.ExitCode -ne 0) {
          Write-Host "::error::Package validation failed for $pkg"
          Write-Host $result.Output
          exit 1
      }
  }
  
  # Check for proper version updates
  $versionChanges = $changedFiles | 
      Where-Object { $_ -match 'packages/[^/]+/[^/]+/[^/]+/Metadata/package\.json$' }
  
  foreach ($file in $versionChanges) {
      $oldContent = git show ":0:$file" | ConvertFrom-Json
      $newContent = Get-Content $file -Raw | ConvertFrom-Json
      
      if ($oldContent.package.version -eq $newContent.package.version) {
          Write-Host "::error::Version not updated in $file"
          Write-Host "Please update the version number before committing changes."
          exit 1
      }
  }
  
  exit 0
  ```

#### Change Tracking and Auditing

- **Changelog Format**
  ```markdown
  # Changelog
  
  ## [Unreleased]
  ### Added
  - New feature A
  - New feature B
  
  ### Changed
  - Improved performance of X
  - Updated dependencies
  
  ### Fixed
  - Bug in Y component
  - Security vulnerability in Z
  
  ## [1.1.0] - 2023-10-01
  ### Added
  - Initial release
  ```

- **Audit Logging**
  ```powershell
  function Add-DriverAuditEntry {
      [CmdletBinding()]
      param(
          [Parameter(Mandatory=$true)]
          [string]$Action,
          
          [string]$Package,
          
          [string]$Version,
          
          [string]$User = [System.Environment]::UserName,
          
          [hashtable]$Details = @{}
      )
      
      $logEntry = [PSCustomObject]@{
          Timestamp = Get-Date -Format 'o'
          Action = $Action
          Package = $Package
          Version = $Version
          User = $User
          Details = $Details
      }
      
      $logPath = Join-Path $PSScriptRoot 'audit.log'
      $logEntry | ConvertTo-Json -Compress | Out-File -FilePath $logPath -Append -Encoding utf8
      
      # Also log to Windows Event Log for system auditing
      $eventSource = 'Driver Management'
      if (-not [System.Diagnostics.EventLog]::SourceExists($eventSource)) {
          New-EventLog -LogName 'Application' -Source $eventSource
      }
      
      $eventMessage = @"
      Action: $Action
      Package: $Package
      Version: $Version
      User: $User
      Details: $($Details | ConvertTo-Json -Compress)
      "@
      
      Write-EventLog -LogName 'Application' -Source $eventSource `
          -EntryType 'Information' -EventId 1000 -Message $eventMessage
  }
  ```

### 8.3 Driver Package Deployment

#### Deployment Methods
- **Manual Installation**
  - Device Manager update
  - INF file right-click install
  - Command line utilities (pnputil, drvload)

- **Automated Deployment**
  - Group Policy Preferences
  - Configuration Manager (SCCM)
  - Microsoft Intune
  - Third-party tools (PDQ Deploy, etc.)
  - Custom PowerShell scripts

- **OS Deployment Integration**
  - Windows Setup (autounattend.xml)
  - Microsoft Deployment Toolkit (MDT)
  - Configuration Manager OSD
  - Windows Deployment Services (WDS)

#### Verification and Rollback
- **Post-Installation Verification**
  ```powershell
  function Test-DriverInstallation {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$PackagePath,
          [string[]]$ComputerName = $env:COMPUTERNAME
      )
      
      # Load package metadata
      $metadataPath = Join-Path $PackagePath 'Metadata\package.json'
      if (-not (Test-Path $metadataPath)) {
          throw "Package metadata not found at $metadataPath"
      }
      
      $metadata = Get-Content -Path $metadataPath -Raw | ConvertFrom-Json
      $results = @()
      
      foreach ($computer in $ComputerName) {
          try {
              $session = New-PSSession -ComputerName $computer -ErrorAction Stop
              
              # Check each expected driver
              foreach ($driver in $metadata.components) {
                  $driverCheck = Invoke-Command -Session $session -ScriptBlock {
                      param($driver)
                      
                      # Check if device exists and is working
                      $device = Get-PnpDevice | Where-Object { 
                          $_.FriendlyName -eq $driver.name -or 
                          $_.DeviceID -in $driver.hardwareIds
                      } | Select-Object -First 1
                      
                      if (-not $device) {
                          return [PSCustomObject]@{
                              Device = $driver.name
                              Status = 'MISSING'
                              Details = 'Device not found'
                          }
                      }
                      
                      # Check driver status
                      if ($device.Status -ne 'OK') {
                          return [PSCustomObject]@{
                              Device = $device.FriendlyName
                              Status = 'ERROR'
                              Details = "Device status: $($device.Status)"
                          }
                      }
                      
                      # Verify driver version if specified
                      $driverVersion = (Get-PnpDeviceProperty -InstanceId $device.InstanceId -KeyName 'DEVPKEY_Device_DriverVersion').Data
                      if ($driver.version -and ($driverVersion -ne $driver.version)) {
                          return [PSCustomObject]@{
                              Device = $device.FriendlyName
                              Status = 'VERSION_MISMATCH'
                              Details = "Expected: $($driver.version), Found: $driverVersion"
                          }
                      }
                      
                      # Check if device is working properly
                      $problemCode = (Get-PnpDeviceProperty -InstanceId $device.InstanceId -KeyName 'DEVPKEY_Device_ProblemCode').Data
                      if ($problemCode -ne 0) {
                          $problemStatus = switch ($problemCode) {
                              1 { 'Device not configured correctly' }
                              10 { 'Device cannot start' }
                              22 { 'Device is disabled' }
                              28 { 'Drivers not installed' }
                              default { "Problem code: $problemCode" }
                          }
                          
                          return [PSCustomObject]@{
                              Device = $device.FriendlyName
                              Status = 'PROBLEM_DETECTED'
                              Details = $problemStatus
                          }
                      }
                      
                      # If we got here, everything is good
                      return [PSCustomObject]@{
                          Device = $device.FriendlyName
                          Status = 'OK'
                          Details = "Version: $driverVersion"
                      }
                  } -ArgumentList $driver
                  
                  $results += $driverCheck | Select-Object @{
                      Name = 'ComputerName'; Expression = { $computer }
                  }, *
              }
              
              Remove-PSSession -Session $session -ErrorAction SilentlyContinue
          }
          catch {
              Write-Warning "Failed to verify drivers on $computer : $_"
              $results += [PSCustomObject]@{
                  ComputerName = $computer
                  Device = 'SYSTEM'
                  Status = 'CONNECTION_ERROR'
                  Details = $_
              }
          }
      }
      
      # Generate summary
      $summary = $results | Group-Object Status
      $summary | ForEach-Object {
          $status = $_.Name
          $count = $_.Count
          $color = switch ($status) {
              'OK' { 'Green' }
              'VERSION_MISMATCH' { 'Yellow' }
              default { 'Red' }
          }
          
          Write-Host "$status`: $count devices" -ForegroundColor $color
      }
      
      # Return detailed results
      return $results | Sort-Object Status, ComputerName, Device
  }
  ```

- **Rollback Procedure**
  ```powershell
  function Start-DriverRollback {
      [CmdletBinding(SupportsShouldProcess=$true, ConfirmImpact='High')]
      param (
          [Parameter(Mandatory=$true)]
          [string]$BackupPath,
          [string[]]$ComputerName = $env:COMPUTERNAME,
          [switch]$Force
      )
      
      # Verify backup exists
      if (-not (Test-Path $BackupPath)) {
          throw "Backup path not found: $BackupPath"
      }
      
      $backupInfo = Get-ChildItem -Path $BackupPath -File 'rollback_info.json' -Recurse | 
          Select-Object -First 1
      
      if (-not $backupInfo) {
          throw "No rollback information found in backup"
      }
      
      $rollbackData = Get-Content -Path $backupInfo.FullName -Raw | ConvertFrom-Json
      
      if (-not $Force -and -not $PSCmdlet.ShouldContinue(
          "This will roll back drivers to the state from $($rollbackData.BackupTime). Continue?",
          "Driver Rollback Confirmation"
      )) {
          return
      }
      
      $results = @()
      
      foreach ($computer in $ComputerName) {
          try {
              $session = New-PSSession -ComputerName $computer -ErrorAction Stop
              
              # Restore each driver from backup
              foreach ($driver in $rollbackData.Drivers) {
                  $result = Invoke-Command -Session $session -ScriptBlock {
                      param($driver, $backupPath)
                      
                      $rollbackFile = Join-Path $backupPath $driver.BackupFile
                      if (-not (Test-Path $rollbackFile)) {
                          return [PSCustomObject]@{
                              Device = $driver.DeviceName
                              Status = 'BACKUP_NOT_FOUND'
                              Details = "Backup file not found: $($driver.BackupFile)"
                          }
                      }
                      
                      try {
                          # Stop the device if it's running
                          $device = Get-PnpDevice -InstanceId $driver.DeviceID -ErrorAction SilentlyContinue
                          if ($device) {
                              $device | Disable-PnpDevice -Confirm:$false -ErrorAction SilentlyContinue
                          }
                          
                          # Restore the driver
                          $result = pnputil /restore-driver "$rollbackFile" /subdirs
                          
                          # Re-enable the device
                          if ($device) {
                              $device | Enable-PnpDevice -Confirm:$false -ErrorAction SilentlyContinue
                          }
                          
                          # Verify the rollback
                          $currentDriver = Get-PnpDevice -InstanceId $driver.DeviceID -ErrorAction SilentlyContinue |
                              Get-PnpDeviceProperty -KeyName 'DEVPKEY_Device_DriverVersion' -ErrorAction SilentlyContinue
                          
                          $status = if ($currentDriver.Data -eq $driver.DriverVersion) {
                              'ROLLBACK_SUCCESS'
                          } else {
                              'VERSION_MISMATCH'
                          }
                          
                          return [PSCustomObject]@{
                              Device = $driver.DeviceName
                              Status = $status
                              Details = "Restored version: $($driver.DriverVersion)"
                          }
                      }
                      catch {
                          return [PSCustomObject]@{
                              Device = $driver.DeviceName
                              Status = 'ROLLBACK_FAILED'
                              Details = $_.Exception.Message
                          }
                      }
                  } -ArgumentList $driver, $BackupPath
                  
                  $results += $result | Select-Object @{
                      Name = 'ComputerName'; Expression = { $computer }
                  }, *
              }
              
              Remove-PSSession -Session $session -ErrorAction SilentlyContinue
          }
          catch {
              Write-Warning "Failed to roll back drivers on $computer : $_"
              $results += [PSCustomObject]@{
                  ComputerName = $computer
                  Device = 'SYSTEM'
                  Status = 'CONNECTION_ERROR'
                  Details = $_
              }
          }
      }
      
      # Generate summary
      $summary = $results | Group-Object Status
      $summary | ForEach-Object {
          $status = $_.Name
          $count = $_.Count
          $color = if ($status -eq 'ROLLBACK_SUCCESS') { 'Green' } else { 'Red' }
          
          Write-Host "$status`: $count devices" -ForegroundColor $color
      }
      
      # Return detailed results
      return $results | Sort-Object Status, ComputerName, Device
  }
  ```

### 8.3 Handling Legacy vs. Modern Drivers

#### Legacy Drivers
- **Packaging**
  - Package separately from modern drivers to prevent conflicts
  - Use dedicated legacy driver repositories
  - Include compatibility notes in package metadata

- **Compatibility Testing**
  ```powershell
  function Test-LegacyDriverCompatibility {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverPath,
          
          [ValidateSet('Win7', 'Win8', 'Win8.1', 'Win10', 'Win11')]
          [string]$TargetOS = 'Win10',
          
          [ValidateSet('x86', 'x64', 'arm64')]
          [string]$Architecture = 'x64'
      )
      
      $results = @{
          DriverPath = $DriverPath
          Compatibility = @()
          Warnings = @()
      }
      
      # Check driver signature
      $signature = Get-AuthenticodeSignature -FilePath $DriverPath
      if ($signature.Status -ne 'Valid') {
          $results.Warnings += "Driver signature is not valid: $($signature.Status)"
      }
      
      # Check OS compatibility from INF file
      $infContent = Get-Content -Path $DriverPath -Raw
      
      # Extract OS compatibility
      if ($infContent -match '\[Manufacturer\]([\s\S]*?)\[') {
          $manufacturerSection = $matches[1]
          $osCompat = @()
          
          # Check for NTx86, NTAMD64, NTARM64 sections
          if ($infContent -match 'NT$Architecture' -and $infContent -notmatch "NT$Architecture") {
              $results.Warnings += "Driver does not support $Architecture architecture"
          }
          
          # Check for specific OS versions
          $osVersions = @{
              'NTx86' = @{ Version = '5.0'; Name = 'Windows 2000' }
              'NTx86.6.0' = @{ Version = '6.0'; Name = 'Windows Vista' }
              'NTx86.6.1' = @{ Version = '6.1'; Name = 'Windows 7' }
              'NTx86.6.2' = @{ Version = '6.2'; Name = 'Windows 8' }
              'NTx86.6.3' = @{ Version = '6.3'; Name = 'Windows 8.1' }
              'NTx86.10.0' = @{ Version = '10.0'; Name = 'Windows 10/11' }
          }
          
          foreach ($os in $osVersions.Keys) {
              if ($infContent -match $os) {
                  $results.Compatibility += $osVersions[$os].Name
              }
          }
      }
      
      # Check for deprecated APIs
      $deprecatedApis = @(
          'NtCreateFile', 'ZwCreateFile', 'IoCreateDevice',
          'ExAllocatePool', 'ObReferenceObjectByHandle', 'IoGetDeviceObjectPointer'
      )
      
      foreach ($api in $deprecatedApis) {
          if ($infContent -match $api) {
              $results.Warnings += "Uses deprecated API: $api"
          }
      }
      
      return $results
  }
  ```

- **Deployment Considerations**
  - Use compatibility modes when installing
  - Disable driver signature enforcement if required
  - Document required system modifications
  - Create system restore points before installation

#### Modern Drivers
- **Packaging**
  - Use Windows Driver Package (.inf) format
  - Include digital signatures
  - Support DCH (Declarative Componentized Hardware) model

- **Deployment Automation**
  ```powershell
  function Install-ModernDriver {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$DriverPackagePath,
          
          [ValidateSet('Install', 'Update', 'Rollback')]
          [string]$Action = 'Install',
          
          [switch]$Force,
          [switch]$RebootIfNeeded
      )
      
      $logPath = "$env:ProgramData\DriverInstall\$(Get-Date -Format 'yyyyMMdd_HHmmss').log"
      $null = New-Item -ItemType Directory -Path (Split-Path $logPath) -Force
      
      try {
          # Initialize log
          Start-Transcript -Path $logPath -Append -Force
          
          # Import the DriverPackage module
          Import-Module "$PSScriptRoot\DriverPackage.psm1" -Force
          
          # Validate driver package
          $validation = Test-DriverPackage -Path $DriverPackagePath
          if (-not $validation.IsValid) {
              throw "Driver package validation failed: $($validation.Errors -join ', ')"
          }
          
          # Check for existing driver
          $existingDriver = Get-InstalledDriver -DeviceId $validation.DeviceId
          
          switch ($Action) {
              'Install' {
                  if ($existingDriver -and -not $Force) {
                      Write-Warning "Driver already installed. Use -Force to reinstall."
                      return
                  }
                  
                  Write-Host "Installing driver package..."
                  pnputil /add-driver "$DriverPackagePath\*.inf" /install /subdirs
              }
              
              'Update' {
                  if (-not $existingDriver) {
                      Write-Warning "No existing driver found. Use 'Install' instead."
                      return
                  }
                  
                  if ($validation.Version -le $existingDriver.Version -and -not $Force) {
                      Write-Host "Newer or same version already installed. Use -Force to reinstall."
                      return
                  }
                  
                  Write-Host "Updating driver package..."
                  pnputil /add-driver "$DriverPackagePath\*.inf" /install /subdirs /force
              }
              
              'Rollback' {
                  if (-not $existingDriver) {
                      throw "No existing driver found to rollback"
                  }
                  
                  $rollbackDriver = Get-RollbackDriver -DeviceId $validation.DeviceId
                  if (-not $rollbackDriver) {
                      throw "No rollback driver found"
                  }
                  
                  Write-Host "Rolling back driver to version $($rollbackDriver.Version)..."
                  pnputil /rollback "$($rollbackDriver.InfPath)" /subdirs
              }
          }
          
          # Check if reboot is required
          $rebootNeeded = $false
          $devices = Get-PnpDevice | Where-Object { $_.Status -eq 'Error' }
          
          if ($devices) {
              Write-Warning "The following devices require attention:"
              $devices | Format-Table -Property Status, FriendlyName, DeviceID
              $rebootNeeded = $true
          }
          
          if ($RebootIfNeeded -and $rebootNeeded) {
              Write-Host "Rebooting system to complete driver installation..."
              Restart-Computer -Force
          }
          
          return @{
              Success = $true
              RebootRequired = $rebootNeeded
              LogPath = $logPath
          }
      }
      catch {
          Write-Error "Driver installation failed: $_"
          return @{
              Success = $false
              Error = $_.Exception.Message
              LogPath = $logPath
          }
      }
      finally {
          Stop-Transcript
      }
  }
  ```

- **Maintenance**
  - Subscribe to vendor security bulletins
  - Test updates in staging environment
  - Use Windows Update for Business for enterprise management
  - Maintain version history and changelog

#### Maintenance Strategies
- **Regular Review Process**
  1. **Quarterly Audit**
     - Review all driver packages for updates
     - Check for security advisories
     - Remove deprecated drivers
     ```powershell
     function Start-DriverAudit {
         [CmdletBinding()]
         param (
             [string]$RepositoryPath = "C:\DriverRepository",
             [switch]$CheckForUpdates,
             [switch]$CheckVulnerabilities
         )
         
         $report = @()
         $packages = Get-ChildItem -Path "$RepositoryPath\packages" -Recurse -Filter "package.json" | 
             Where-Object { $_.FullName -notlike '*\node_modules\*' }
         
         foreach ($pkg in $packages) {
             $pkgData = Get-Content $pkg.FullName | ConvertFrom-Json
             $pkgDir = $pkg.DirectoryName
             
             $pkgInfo = [PSCustomObject]@{
                 PackageName = $pkgData.Name
                 Version = $pkgData.Version
                 Path = $pkgDir
                 LastUpdated = (Get-Item $pkg.FullName).LastWriteTime
                 Issues = @()
             }
             
             # Check for updates
             if ($CheckForUpdates -and $pkgData.UpdateUrl) {
                 try {
                     $latestVersion = Invoke-RestMethod -Uri $pkgData.UpdateUrl -ErrorAction Stop
                     if ([version]$latestVersion -gt [version]$pkgData.Version) {
                         $pkgInfo | Add-Member -NotePropertyName 'UpdateAvailable' -NotePropertyValue $true
                         $pkgInfo | Add-Member -NotePropertyName 'LatestVersion' -NotePropertyValue $latestVersion
                     }
                 }
                 catch {
                     $pkgInfo.Issues += "Failed to check for updates: $($_.Exception.Message)"
                 }
             }
             
             # Check for vulnerabilities
             if ($CheckVulnerabilities -and $pkgData.CVEs) {
                 $vulnerable = $pkgData.CVEs | Where-Object { 
                     $_.Status -eq 'Vulnerable' -and $_.Severity -in @('Critical', 'High')
                 }
                 
                 if ($vulnerable) {
                     $pkgInfo.Issues += "Vulnerable to: $($vulnerable.CVE -join ', ')"
                 }
             }
             
             # Check package health
             $driverFiles = Get-ChildItem -Path $pkgDir -Recurse -Include @('*.sys', '*.dll', '*.inf')
             if (-not $driverFiles) {
                 $pkgInfo.Issues += "No driver files found in package"
             }
             
             $report += $pkgInfo
         }
         
         # Generate summary report
         $summary = [PSCustomObject]@{
             TotalPackages = $report.Count
             NeedsUpdate = ($report | Where-Object { $_.UpdateAvailable }).Count
             HasIssues = ($report | Where-Object { $_.Issues }).Count
             LastAudit = Get-Date
         }
         
         return @{
             Summary = $summary
             Details = $report | Sort-Object { $_.Issues.Count } -Descending
         }
     }
     ```

  2. **Archival Process**
     - Move deprecated drivers to archive repository
     - Update documentation with deprecation notice
     - Notify dependent teams

  3. **Security Patching**
     - Monitor security bulletins
     - Create patch management workflow
     - Document mitigation strategies

### 8.5 Driver Signing

#### Digital Signing Requirements
- **Code Signing Certificates**
  - Obtain from trusted Certificate Authority (CA)
  - Use Extended Validation (EV) certificates for kernel-mode drivers
  - Maintain proper certificate chain validation

- **Signing Process**
  ```powershell
  # Sign a driver package using signtool.exe
  function Sign-DriverPackage {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$PackagePath,
          
          [Parameter(Mandatory=$true)]
          [string]$CertPath,
          
          [string]$CertPassword,
          
          [string]$TimestampServer = 'http://timestamp.digicert.com',
          
          [ValidateSet('SHA1', 'SHA256', 'SHA384', 'SHA512')]
          [string]$Algorithm = 'SHA256'
      )
      
      $signtool = "C:\\Program Files (x86)\\Windows Kits\\10\\bin\\10.0.22621.0\\x64\\signtool.exe"
      
      if (-not (Test-Path $signtool)) {
          throw "SignTool not found at $signtool. Install Windows SDK with Signing Tools."
      }
      
      $files = @(
          (Get-ChildItem -Path $PackagePath -Recurse -Include '*.sys', '*.dll', '*.exe', '*.cat' -File).FullName
      )
      
      $signArgs = @(
          'sign',
          '/fd', $Algorithm,
          '/td', $Algorithm,
          '/tr', $TimestampServer,
          '/a'  # Automatically select the best certificate
      )
      
      if ($CertPath) {
          $signArgs += '/f', $CertPath
          if ($CertPassword) {
              $signArgs += '/p', $CertPassword
          }
      }
      
      $results = @()
      
      foreach ($file in $files) {
          Write-Verbose "Signing $file..."
          $fileArgs = $signArgs + @($file)
          $process = Start-Process -FilePath $signtool -ArgumentList $fileArgs -NoNewWindow -PassThru -Wait
          
          $result = [PSCustomObject]@{
              File = $file
              ExitCode = $process.ExitCode
              Success = ($process.ExitCode -eq 0)
          }
          
          if (-not $result.Success) {
              Write-Warning "Failed to sign $file (Exit code: $($result.ExitCode))"
          }
          
          $results += $result
      }
      
      # Verify signatures
      $verification = $results | ForEach-Object {
          $verifyArgs = @('verify', '/pa', '/v', $_.File)
          $output = & $signtool $verifyArgs 2>&1 | Out-String
          
          [PSCustomObject]@{
              File = $_.File
              IsSigned = $output -match 'Successfully verified'
              Details = $output
          }
      }
      
      return @{
          SigningResults = $results
          Verification = $verification
      }
  }
  ```

#### Secure Boot Configuration
- **UEFI Secure Boot**
  - Verify Secure Boot status:
    ```powershell
    # Check Secure Boot status
    Confirm-SecureBootUEFI
    
    # Get Secure Boot policy details
    Get-SecureBootUEFI -Name 'PK', 'KEK', 'db', 'dbx' | Format-Table -AutoSize
    ```

- **Deployment Policies**
  - Group Policy settings for driver signing:
    ```powershell
    # Check current execution policy
    Get-ExecutionPolicy -List
    
    # Configure driver signing policy
    Set-ItemProperty -Path "HKLM:\\SOFTWARE\\Policies\\Microsoft\\Windows\\DriverSearching" -Name "DriverSigningPolicy" -Value 1
    Set-ItemProperty -Path "HKLM:\\SOFTWARE\\Policies\\Microsoft\\Windows NT\\Driver Signing" -Name "BehaviorOnFailedVerify" -Value 0
    ```

#### Verification and Compliance
- **Signature Verification**
  ```powershell
  # Verify driver signatures
  function Test-DriverSignatures {
      [CmdletBinding()]
      param (
          [Parameter(Mandatory=$true)]
          [string]$Path,
          
          [switch]$Recursive,
          
          [ValidateSet('All', 'Unsigned', 'Invalid', 'Expired', 'Revoked')]
          [string]$Filter = 'All'
      )
      
      $files = if ($Recursive) {
          Get-ChildItem -Path $Path -Recurse -Include '*.sys', '*.dll', '*.exe', '*.cat' -File
      } else {
          Get-ChildItem -Path $Path -Include '*.sys', '*.dll', '*.exe', '*.cat' -File
      }
      
      $results = foreach ($file in $files) {
          $signature = Get-AuthenticodeSignature -FilePath $file.FullName
          $cert = $signature.SignerCertificate
          
          $status = switch ($signature.Status) {
              'Valid' { 'SIGNED_VALID' }
              'NotSigned' { 'UNSIGNED' }
              'HashMismatch' { 'TAMPERED' }
              'NotTrusted' { 'UNTRUSTED' }
              default { $signature.Status }
          }
          
          $certInfo = if ($cert) {
              @{
                  Subject = $cert.Subject
                  Issuer = $cert.Issuer
                  Thumbprint = $cert.Thumbprint
                  NotBefore = $cert.NotBefore
                  NotAfter = $cert.NotAfter
                  SerialNumber = $cert.SerialNumber
              }
          } else {
              $null
          }
          
          [PSCustomObject]@{
              File = $file.FullName
              Status = $status
              TimeStamper = $signature.TimeStamperCertificate?.Subject
              IsOSBinary = $signature.IsOSBinary
              Certificate = $certInfo
          }
      }
      
      # Apply filter
      switch ($Filter) {
          'Unsigned' { $results = $results | Where-Object { $_.Status -eq 'UNSIGNED' } }
          'Invalid' { $results = $results | Where-Object { $_.Status -ne 'SIGNED_VALID' } }
          'Expired' { $results = $results | Where-Object { $_.Certificate?.NotAfter -and $_.Certificate.NotAfter -lt (Get-Date) } }
          'Revoked' { 
              # This would require checking against a CRL or OCSP
              $results = $results | Where-Object { 
                  $_.Status -eq 'SIGNED_VALID' -and 
                  # Placeholder for revocation check
                  $false
              }
          }
      }
      
      return $results
  }
  ```

- **Compliance Reporting**
  ```powershell
  # Generate compliance report
  function Get-DriverComplianceReport {
      [CmdletBinding()]
      param (
          [string]$OutputPath = "$env:TEMP\\DriverCompliance_$(Get-Date -Format 'yyyyMMdd').html"
      )
      
      $report = @"
      <!DOCTYPE html>
      <html>
      <head>
          <title>Driver Signing Compliance Report</title>
          <style>
              body { font-family: Arial, sans-serif; margin: 20px; }
              table { border-collapse: collapse; width: 100%; }
              th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
              th { background-color: #f2f2f2; }
              .valid { background-color: #dff0d8; }
              .invalid { background-color: #f2dede; }
              .warning { background-color: #fcf8e3; }
          </style>
      </head>
      <body>
          <h1>Driver Signing Compliance Report</h1>
          <p>Generated: $(Get-Date)</p>
          <h2>System Information</h2>
          <ul>
              <li>Computer: $env:COMPUTERNAME</li>
              <li>OS: $((Get-CimInstance Win32_OperatingSystem).Caption)</li>
              <li>Secure Boot: $(try { (Confirm-SecureBootUEFI).ToString() } catch { 'N/A' })</li>
          </ul>
  "@
  
      # Get all drivers
      $drivers = Get-WindowsDriver -Online -All | Select-Object *
      $signedDrivers = $drivers | Where-Object { $_.Inbox -eq $false -and $_.OriginalFileName }
      
      # Generate summary
      $summary = @{
          TotalDrivers = $drivers.Count
          SignedDrivers = ($drivers | Where-Object { $_.SignerName }).Count
          UnsignedDrivers = ($drivers | Where-Object { -not $_.SignerName }).Count
          ThirdPartyDrivers = $signedDrivers.Count
      }
      
      $report += @"
      <h2>Summary</h2>
      <table>
          <tr><th>Metric</th><th>Count</th></tr>
          <tr><td>Total Drivers</td><td>$($summary.TotalDrivers)</td></tr>
          <tr class="valid"><td>Signed Drivers</td><td>$($summary.SignedDrivers)</td></tr>
          <tr class="invalid"><td>Unsigned Drivers</td><td>$($summary.UnsignedDrivers)</td></tr>
          <tr><td>Third-Party Drivers</td><td>$($summary.ThirdPartyDrivers)</td></tr>
      </table>
  "@
  
      # Detailed driver report
      $report += @"
      <h2>Driver Details</h2>
      <table>
          <tr>
              <th>Driver</th>
              <th>Version</th>
              <th>Publisher</th>
              <th>Status</th>
              <th>Signer</th>
          </tr>
  "@
  
      foreach ($driver in $drivers | Sort-Object ProviderName, Driver) {
          $status = if ($driver.SignerName) {
              'Signed' 
          } else {
              'Unsigned'
          }
          
          $rowClass = switch ($status) {
              'Signed' { 'valid' }
              default { 'invalid' }
          }
          
          $report += @"
          <tr class="$rowClass">
              <td>$($driver.Driver)</td>
              <td>$($driver.Version)</td>
              <td>$($driver.ProviderName)</td>
              <td>$status</td>
              <td>$($driver.SignerName)</td>
          </tr>
  "@
      }
      
      $report += @"
      </table>
      </body>
      </html>
  "@
  
      # Save report
      $report | Out-File -FilePath $OutputPath -Encoding utf8
      Write-Output "Compliance report generated: $OutputPath"
      return $OutputPath
  }
  ```

#### Best Practices
1. **Certificate Management**
   - Store code signing certificates in secure hardware modules (HSM)
   - Implement certificate rotation policies
   - Maintain an inventory of all code signing certificates
   - Revoke and replace compromised certificates immediately

2. **Signing Process**
   - Sign drivers as part of the build pipeline
   - Use timestamping for long-term signature validity
   - Maintain detailed audit logs of all signing operations
   - Implement dual-control for production signing

3. **Verification**
   - Verify signatures before deployment
   - Check certificate revocation status
   - Validate the entire certificate chain
   - Monitor for expiring certificates

4. **Compliance**
   - Document signing policies and procedures
   - Maintain evidence of compliance with security standards
   - Regularly audit driver signatures
   - Implement automated alerts for unsigned or invalid drivers

### 8.4 Driver Package Maintenance

#### Update Strategy
- **Versioning**
  - Follow semantic versioning (MAJOR.MINOR.PATCH)
  - Document all changes in CHANGELOG.md
  - Maintain backward compatibility when possible

- **Testing**
  - Automated testing in virtual environments
  - Pilot deployment to test group
  - Rollback testing

#### Documentation
- **Package Documentation**
  - README.md with usage instructions
  - Known issues and workarounds
  - Dependencies and requirements
  - Support contact information

- **Change Management**
  - Change request process
  - Impact assessment
  - Approval workflow
  - Post-implementation review

#### Automation
- **CI/CD Pipeline**
  - Automated testing
  - Package signing
  - Deployment to staging/production
  - Notification system

- **Monitoring**
  - Driver health monitoring
  - Version compliance reporting
  - Automated alerting for issues

### 7.7 Driver Inventory Best Practices

#### Standardized Tools
- **Recommended Tools**
  ```markdown
  | Tool | Purpose | Platform | Notes |
  |------|---------|----------|-------|
  | PowerShell | Scripted inventory | Windows | Built-in, no installation required |
  | WMI/CIM | Hardware/software inventory | Cross-platform | Access via PowerShell or dedicated tools |
  | PDQ Inventory | Automated scanning | Windows | Free and Enterprise versions available |
  | Lansweeper | Enterprise inventory | Windows/Linux | Comprehensive asset management |
  | Microsoft Endpoint Manager | Enterprise management | Cloud/On-prem | Part of Microsoft 365 |
  | Chocolatey | Package management | Windows | For driver deployment |
  | Ansible | Configuration management | Cross-platform | Agentless automation |
  ```

- **PowerShell Module Example**
  ```powershell
  # Install required modules
  Install-Module -Name PSDepend -Force
  Install-Module -Name PSScriptAnalyzer -Force
  
  # Standard inventory collection function
  function Get-StandardInventory {
      [CmdletBinding()]
      param (
          [string[]]$ComputerName = $env:COMPUTERNAME,
          [PSCredential]$Credential,
          [string]$OutputPath = "$env:TEMP\Inventory_$(Get-Date -Format 'yyyyMMdd').json"
      )
      
      $inventory = @{
          CollectionDate = Get-Date -Format 'o'
          Systems = @()
      }
      
      foreach ($computer in $ComputerName) {
          try {
              $params = @{
                  ComputerName = $computer
                  ErrorAction = 'Stop'
              }
              if ($Credential) { $params.Credential = $Credential }
              
              $systemInfo = Get-CimInstance -ClassName Win32_ComputerSystem @params
              $osInfo = Get-CimInstance -ClassName Win32_OperatingSystem @params
              
              $inventory.Systems += [PSCustomObject]@{
                  ComputerName = $computer
                  LastBootTime = $osInfo.LastBootUpTime
                  OS = $osInfo.Caption
                  OSVersion = $osInfo.Version
                  Manufacturer = $systemInfo.Manufacturer
                  Model = $systemInfo.Model
                  Processors = (Get-CimInstance -ClassName Win32_Processor @params).Name
                  MemoryGB = [math]::Round($systemInfo.TotalPhysicalMemory / 1GB, 2)
                  NetworkAdapters = Get-CimInstance -ClassName Win32_NetworkAdapterConfiguration @params | 
                      Where-Object { $_.IPEnabled } | 
                      Select-Object Description, IPAddress, MACAddress
                  Disks = Get-CimInstance -ClassName Win32_DiskDrive @params | 
                      Select-Object Model, Size, InterfaceType
                  Drivers = Get-CimInstance -ClassName Win32_PnPSignedDriver @params | 
                      Where-Object { $_.DeviceName } |
                      Select-Object DeviceName, DriverVersion, DriverDate, IsSigned
              }
          }
          catch {
              Write-Warning "Failed to collect inventory from $computer : $_"
          }
      }
      
      $inventory | ConvertTo-Json -Depth 5 | Out-File -FilePath $OutputPath -Encoding utf8
      return $OutputPath
  }
  ```

#### Inventory Completeness Checklist
- **Pre-Collection**
  ```markdown
  - [ ] Verify network connectivity to all target systems
  - [ ] Ensure administrative privileges are available
  - [ ] Confirm sufficient disk space for output files
  - [ ] Schedule during maintenance windows if needed
  - [ ] Document baseline system state
  ```

- **Collection Process**
  ```markdown
  - [ ] Collect from all device categories (servers, workstations, mobile devices)
  - [ ] Include all hardware components (CPU, memory, storage, network)
  - [ ] Capture all installed drivers with versions
  - [ ] Document system configurations and settings
  - [ ] Record any custom or third-party drivers
  ```

- **Post-Collection**
  ```markdown
  - [ ] Verify all target systems were inventoried
  - [ ] Validate data completeness and accuracy
  - [ ] Check for any collection errors or warnings
  - [ ] Archive raw inventory data
  - [ ] Generate summary reports
  ```

#### Troubleshooting Common Issues
- **Missing Devices**
  ```powershell
  # Find devices with missing drivers
  $missingDevices = Get-PnpDevice | Where-Object { $_.Status -eq 'Error' }
  if ($missingDevices) {
      $missingDevices | ForEach-Object {
          $device = $_
          $hardwareID = ($_.HardwareID -join ", ")
          
          Write-Warning "Device with issues: $($device.FriendlyName)"
          Write-Host "  Hardware ID: $hardwareID"
          Write-Host "  Status: $($device.Status)"
          
          # Attempt to find driver in Windows Update
          $updates = Get-WindowsUpdate -MicrosoftUpdate -Verbose | 
              Where-Object { $_.Title -match [regex]::Escape($device.Name) }
              
          if ($updates) {
              Write-Host "  Available updates:"
              $updates | Select-Object Title, KB | Format-List | Out-String
          } else {
              Write-Host "  No updates found in Windows Update"
          }
          
          # Check manufacturer website
          $manufacturer = ($device.Manufacturer -replace ",.*$").Trim()
          Write-Host "  Check $manufacturer website for drivers using Hardware ID: $($hardwareID -split '\\' | Select-Object -Last 1)"
      }
  }
  ```

- **Driver Errors**
  ```powershell
  # Check system event log for driver errors
  $driverErrors = Get-WinEvent -FilterHashtable @{
      LogName = 'System'
      ProviderName = 'Microsoft-Windows-Kernel-PnP'
      Level = 2,3  # Error and Warning
  } -MaxEvents 50 | Where-Object {
      $_.Message -match 'driver' -or $_.Message -match 'device'
  }
  
  if ($driverErrors) {
      $driverErrors | ForEach-Object {
          [PSCustomObject]@{
              Time = $_.TimeCreated
              Level = $_.LevelDisplayName
              Source = $_.ProviderName
              Message = ($_.Message -split '\r?\n' | Select-Object -First 2) -join ' '
              EventID = $_.Id
          }
      } | Format-Table -AutoSize -Wrap
  }
  ```

#### Process Improvement
- **Review Cycle**
  ```markdown
  ### Quarterly Review Checklist
  - [ ] Evaluate new hardware models added to environment
  - [ ] Review Windows Update catalog for new drivers
  - [ ] Update driver packages in deployment repository
  - [ ] Test deployment on non-production systems
  - [ ] Update documentation and procedures
  - [ ] Train support staff on new processes
  ```

- **Version Control**
  ```powershell
  # Sample Git workflow for driver repository
  function Update-DriverRepository {
      param (
          [string]$RepoPath = "C:\DriverRepo",
          [string]$DriverSource = "\\fileserver\drivers"
      )
      
      if (-not (Test-Path $RepoPath)) {
          New-Item -ItemType Directory -Path $RepoPath -Force | Out-Null
          Set-Location $RepoPath
          git init
          git remote add origin <repository-url>
          git fetch
          git checkout -b main origin/main
      }
      
      Set-Location $RepoPath
      
      # Sync new drivers
      robocopy $DriverSource $RepoPath /MIR /NP /R:3 /W:10 /LOG+:$RepoPath\update.log
      
      # Commit and push changes
      git add .
      git commit -m "Update drivers - $(Get-Date -Format 'yyyy-MM-dd')"
      git push origin main
      
      # Generate change report
      $changes = git log --since="1 month ago" --pretty=format:"%h - %an, %ar : %s"
      $changes | Out-File -FilePath "$RepoPath\ChangeLog_$(Get-Date -Format 'yyyyMMdd').txt"
  }
  ```

- **Documentation Template**
  ```markdown
  # Driver Update Documentation
  
  ## Change Details
  - **Date**: $(Get-Date -Format 'yyyy-MM-dd')
  - **Version**: 1.0.0
  - **Affected Systems**: [List of systems/models]
  
  ## Changes Made
  - [ ] Updated drivers for [Hardware Model]
  - [ ] Added support for [New OS Version]
  - [ ] Resolved [Specific Issue]
  
  ## Testing
  - [ ] Verified on [Test System]
  - [ ] Confirmed driver signature validation
  - [ ] Tested all device functionality
  
  ## Rollback Plan
  1. Revert to previous driver version
  2. Restore from backup [Location]
  3. Contact [Support Contact] if issues persist
  
  ## Notes
  [Any additional information or special instructions]
  ```

## 8. Best Practices

### 6.1 Before Making Changes

#### Pre-Change Checklist
1. **Document Current Settings**
   - Take screenshots of BIOS/UEFI settings
   - Note current boot order
   - Document custom configurations

2. **Backup Critical Data**
   - System image backup
   - Document important settings
   - Export boot configuration

3. **Prepare Recovery Media**
   - Create bootable USB/DVD
   - Have OS installation media ready
   - Prepare diagnostic tools

### 6.2 Security Considerations

#### Secure Boot Configuration
- Keep Secure Boot enabled when possible
- Use signed bootloaders and drivers
- Manage platform keys carefully

#### Access Control
- Set BIOS/UEFI passwords
- Use TPM for disk encryption
- Disable unnecessary boot devices

#### Secure Boot Management
```powershell
# Check Secure Boot status (Windows)
Confirm-SecureBootUEFI

# View enrolled certificates (Linux)
sudo mokutil --list-enrolled
```

### 6.3 Performance Optimization

#### Boot Time Optimization
1. **Windows**
   ```powershell
   # Analyze boot performance
   Get-WinEvent -ProviderName Microsoft-Windows-Diagnostics-Performance -MaxEvents 1 | Format-List
   ```

2. **Linux**
   ```bash
   # Check boot time
   systemd-analyze
   
   # List slowest starting services
   systemd-analyze blame
   ```

3. **macOS**
   ```bash
   # Check startup items
   launchctl list | grep -v "-"
   ```

#### Boot Device Selection
- Prioritize NVMe > SATA SSD > HDD
- Disable unused boot devices
- Enable Fast Boot (if supported)

### 6.4 Maintenance and Updates

#### Regular Maintenance
1. **Firmware Updates**
   - Check manufacturer website
   - Follow update instructions carefully
   - Backup settings before updating

2. **Boot Configuration**
   - Periodically verify boot order
   - Clean up old boot entries
   - Remove unnecessary boot options

#### Update Procedures
- **Windows**:
  ```powershell
  # Check for firmware updates
  Get-Package -ProviderName NuGet -Name "*firmware*"
  ```

- **Linux**:
  ```bash
  # Update GRUB after kernel updates
  sudo update-grub
  ```

- **macOS**:
  - Use System Preferences > Software Update
  - Check for firmware updates separately

## 7. Frequently Asked Questions

### 7.1 General Questions

#### Q: How often should I check my boot order?
**A:** Check boot order when:
- Installing new hardware
- Experiencing boot issues
- After BIOS/UEFI updates
- When changing operating systems

#### Q: Will changing boot order affect my data?
**A:** No, changing boot order only affects which device the system attempts to boot from first. It doesn't modify any data on the drives.

#### Q: What's the difference between UEFI and Legacy boot?
| Feature | UEFI | Legacy BIOS |
|---------|------|-------------|
| **Partition Style** | GPT | MBR |
| **Max Disk Size** | 9.4 ZB | 2 TB |
| **Partitions** | 128 primary | 4 primary |
| **Boot Time** | Faster | Slower |
| **Secure Boot** | Supported | Not supported |

### 7.2 Technical Questions

#### Q: How do I know if I'm using UEFI or Legacy BIOS?
**Windows:**
```powershell
# Check firmware type
$env:firmware_type = (Get-ComputerInfo).BiosFirmwareType
Write-Host "Firmware Type: $firmware_type"
```

**Linux:**
```bash
# Check for EFI directory
[ -d /sys/firmware/efi ] && echo "UEFI" || echo "Legacy"
```

**macOS:**
```bash
# Check firmware version
system_profiler SPHardwareDataType | grep "Boot ROM"
```

#### Q: How do I change boot mode from Legacy to UEFI?
1. Backup all data
2. Convert disk to GPT (data will be erased)
3. Enable UEFI in BIOS
4. Disable CSM/Legacy support
5. Reinstall OS in UEFI mode

### 7.3 Troubleshooting Questions

#### Q: My PC won't boot after changing boot order. What should I do?
1. **Access BIOS/UEFI** (press Del/F2 during startup)
2. **Reset to defaults** (F9 or Load Optimized Defaults)
3. **Verify connections** for all drives
4. **Try one boot device** at a time
5. **Check for error messages**

#### Q: Why does my boot order keep resetting?
Common causes:
- Dead CMOS battery
- Failed BIOS update
- Hardware changes
- Power surges

**Solution:**
1. Replace CMOS battery (CR2032)
2. Update BIOS to latest version
3. Check for hardware issues
4. Reset BIOS to defaults

#### Q: Can I set a custom boot timeout?
**Windows:**
```powershell
# Set timeout to 5 seconds
bcdedit /timeout 5
```

**Linux (GRUB):**
```bash
# Edit GRUB config
sudo nano /etc/default/grub
# Set: GRUB_TIMEOUT=5
sudo update-grub
```

### 7.4 Advanced Configuration

#### Q: How do I create a custom boot entry?
**Windows:**
```powershell
# Create new boot entry
bcdedit /create /d "Windows 11 Safe Mode" /application osloader
# Configure the new entry (replace {GUID} with output from above)
bcdedit /set {GUID} device partition=C:
bcdedit /set {GUID} path \Windows\system32\winload.efi
bcdedit /set {GUID} osdevice partition=C:
bcdedit /set {GUID} safeboot minimal
```

**Linux (GRUB):**
```bash
# Add custom entry to /etc/grub.d/40_custom
menuentry 'Custom Linux' {
    set root='(hd0,1)'
    linux /vmlinuz-custom root=/dev/sda1
    initrd /initramfs-custom.img
}
# Update GRUB
sudo update-grub
```

### 7.5 Performance Questions

#### Q: How can I make my PC boot faster?
1. **Enable Fast Boot** in BIOS
2. **Disable unnecessary startup programs**
3. **Use SSD/NVMe** as boot drive
4. **Update drivers and firmware**
5. **Disable unused boot devices**

#### Q: Why is my boot time increasing?
Possible causes:
- Too many startup programs
- Disk errors
- Fragmented drive (HDD only)
- Too many boot entries
- Malware infection

**Diagnostic Commands:**
```powershell
# Windows: Check boot time
Get-WinEvent -ProviderName Microsoft-Windows-Diagnostics-Performance -MaxEvents 1 | Format-List

# Linux: Analyze boot process
systemd-analyze blame
```

## 8. Appendices

### 8.1 Manufacturer-Specific Information

#### BIOS/UEFI Access Keys
| Manufacturer | BIOS Key | Boot Menu | Recovery | Notes |
|--------------|----------|-----------|-----------|-------|
| **Acer** | F2, Del | F12 | Alt+F10 | Some models: F1, Ctrl+Alt+Esc |
| **ASUS** | F2, Del | F8 | F9 | Some models: Esc, Insert |
| **Dell** | F2, F12 | F12 | F8, F11 | Older models: Ctrl+Alt+Enter |
| **HP** | F10, Esc | F9 | F11 | Some models: F1, F6 |
| **Lenovo** | F1, F2 | F12 | F11, Novo button | ThinkPads: Enter then F1 |
| **MSI** | Del | F11 | F3 | Some models: F1, F2 |
| **Samsung** | F2, F10 | Esc | F4 | Some models: Del |
| **Sony** | F2, Assist | F11 | F10 | VAIO: F3 |
| **Toshiba** | F2, F12 | F12 | 0 (zero) during POST | Some models: Esc, F1 |

#### Support Resources
- **Acer**: [support.acer.com](https://www.acer.com/ac/en/US/content/support)
- **ASUS**: [www.asus.com/support](https://www.asus.com/support/)
- **Dell**: [www.dell.com/support](https://www.dell.com/support/home)
- **HP**: [support.hp.com](https://support.hp.com/)
- **Lenovo**: [support.lenovo.com](https://support.lenovo.com/)
- **MSI**: [www.msi.com/support](https://www.msi.com/support)

### 8.2 Command Reference

#### Windows Commands
```powershell
# View boot configuration
bcdedit /enum

# Set default OS
bcdedit /default {identifier}

# Change boot timeout (seconds)
bcdedit /timeout 5

# Rebuild BCD
bootrec /rebuildbcd
bootrec /fixmbr
bootrec /fixboot

# Check disk health
wmic diskdrive get status
```

#### Linux Commands
```bash
# List disks and partitions
lsblk
fdisk -l

# Check disk health
sudo smartctl -a /dev/sdX

# Update GRUB
sudo update-grub

# Check filesystem
sudo fsck /dev/sdX

# Mount EFI partition (adjust partition as needed)
sudo mount /dev/sda1 /mnt/efi
```

#### macOS Commands
```bash
# Set startup disk
sudo bless --mount /Volumes/YourVolume --setBoot

# Check disk health
diskutil verifyVolume /Volumes/YourVolume

# Reset NVRAM/PRAM
sudo nvram -c

# Check system logs
log show --predicate 'process == "kernel"' --last 10m
```

### 8.3 Glossary

#### Boot Terms
- **BIOS**: Basic Input/Output System
- **UEFI**: Unified Extensible Firmware Interface
- **MBR**: Master Boot Record
- **GPT**: GUID Partition Table
- **POST**: Power-On Self-Test
- **CMOS**: Complementary Metal-Oxide-Semiconductor
- **NVRAM**: Non-Volatile Random-Access Memory
- **TPM**: Trusted Platform Module
- **Secure Boot**: Security standard for UEFI
- **Fast Boot**: Feature to reduce boot time

#### File Systems
- **NTFS**: Windows NT File System
- **FAT32**: File Allocation Table 32-bit
- **exFAT**: Extended File Allocation Table
- **EXT4**: Fourth Extended Filesystem
- **APFS**: Apple File System
- **HFS+**: Hierarchical File System Plus

### 8.4 Additional Resources

#### Official Documentation
- [UEFI Specification](https://uefi.org/specifications)
- [Microsoft Boot Configuration Data](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/bcd-system-hive-file-settings)
- [GRUB Manual](https://www.gnu.org/software/grub/manual/grub/)

#### Useful Tools
- **Rufus**: Bootable USB creation
- **Ventoy**: Multi-boot USB solution
- **GParted**: Partition management
- **Hiren's BootCD**: Recovery tools
- **MemTest86**: Memory testing

#### Online Communities
- [Super User](https://superuser.com/)
- [Ask Ubuntu](https://askubuntu.com/)
- [Reddit r/techsupport](https://www.reddit.com/r/techsupport/)
- [Microsoft Community](https://answers.microsoft.com/)

#### Training Resources
- [Coursera: Operating Systems](https://www.coursera.org/learn/os)
- [edX: Linux Foundation](https://www.edx.org/learn/linux)
- [Microsoft Learn](https://learn.microsoft.com/)
- [Linux Documentation Project](https://tldp.org/)

---

## 1. Introduction to Boot Order

### 1.1 What is Boot Sequence?
The boot sequence is the ordered process that a computer follows to locate, load, and initialize the operating system when powered on or restarted. It determines the priority of storage devices that the system's firmware (BIOS/UEFI) will check for bootable media.

#### Key Components
- **Power-On Self-Test (POST)**: Initial hardware check
- **Firmware Initialization**: BIOS/UEFI loads and runs
- **Boot Device Selection**: System checks devices in specified order
- **Bootloader Execution**: Handles OS loading
- **OS Initialization**: Operating system takes control

### 1.2 Why Change Boot Order?
#### Common Reasons
1. **OS Installation/Recovery**
   - Installing a new operating system
   - Running recovery tools
   - Repairing system files

2. **Hardware Changes**
   - Adding new storage devices
   - Testing new hardware
   - Troubleshooting issues

3. **Security**
   - Preventing unauthorized boot devices
   - Enabling secure boot
   - Protecting against boot sector viruses

### 1.3 Common Devices in Boot Sequence
#### Primary Boot Devices
1. **Internal Storage**
   - SSDs (SATA/NVMe/M.2)
   - HDDs
   - Hardware RAID arrays

2. **External Storage**
   - USB drives
   - External HDDs/SSDs
   - eSATA devices

3. **Network**
   - PXE boot
   - iSCSI
   - FCoE

4. **Optical Media**
   - CD/DVD/Blu-ray
   - Recovery discs

---
[Previous sections continue with the same level of organization and detail...]
