This is the Switch equivalent of 3DS
[exheader](https://www.3dbrew.org/wiki/NCCH/Extended_Header). This is
the file with extension ".npdm" in {Switch ExeFS}. The size of this file
varies.

| Offset     | Size       | Description |
| ---------- | ---------- | ----------- |
| 0x0        | 0x80       | META        |
| 0x80       | <Varies>   | ACID        |
| <See META> | <See META> | ACI0        |

# META

| Offset | Size | Description                                                                                                                                                                                               |
| ------ | ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x4  | Magicnum "META"                                                                                                                                                                                           |
| 0x4    | 0x8  | Reserved                                                                                                                                                                                                  |
| 0xC    | 0x1  | MMU flags (bit0 = use 64-bit instructions, bit1 = use 64-bit address space, bit2 = use 32-bit address space, bit3 = use 32-bit address space without reserved region, bit4 = optimize memory allocation?) |
| 0xD    | 0x1  | Reserved                                                                                                                                                                                                  |
| 0xE    | 0x1  | Main thread priority (0-63)                                                                                                                                                                               |
| 0xF    | 0x1  | Main thread core number                                                                                                                                                                                   |
| 0x10   | 0x4  | Reserved                                                                                                                                                                                                  |
| 0x14   | 0x4  | \[3.0.0+\] System resource (PersonalMmHeap) size (max size as of 5.x: 534773760)                                                                                                                          |
| 0x18   | 0x4  | Version (0 for all titles prior to [8.1.0](8.1.0.md "wikilink"), 1 for certain titles since).                                                                                                             |
| 0x1C   | 0x4  | Main thread stack size (Should(?) be page-aligned. In non-nspwn scenarios, values of 0 can also rarely break in Horizon. This might be something auto-adapting or a security feature of some sort?)       |
| 0x20   | 0x10 | Title name (usually/always "Application")                                                                                                                                                                 |
| 0x30   | 0x10 | Product code (usually/always all zeroes)                                                                                                                                                                  |
| 0x40   | 0x30 | Reserved                                                                                                                                                                                                  |
| 0x70   | 0x4  | [\#ACI0](#ACI0 "wikilink") offset                                                                                                                                                                         |
| 0x74   | 0x4  | [\#ACI0](#ACI0 "wikilink") size                                                                                                                                                                           |
| 0x78   | 0x4  | [\#ACID](#ACID "wikilink") offset                                                                                                                                                                         |
| 0x7C   | 0x4  | [\#ACID](#ACID "wikilink") size                                                                                                                                                                           |

# ACID

| Offset | Size  | Description                                                                                                                                                                                                   |
| ------ | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x100 | RSA-2048 signature over the data starting at 0x100 with the size field from 0x204                                                                                                                             |
| 0x100  | 0x100 | RSA-2048 public key for the second [NCA](NCA%20Format.md "wikilink") signature                                                                                                                                |
| 0x200  | 0x4   | Magicnum "ACID"                                                                                                                                                                                               |
| 0x204  | 0x4   | Data size                                                                                                                                                                                                     |
| 0x208  | 0x4   | Reserved                                                                                                                                                                                                      |
| 0x20C  | 0x4   | Flags (bit0 = ProductionFlag, bit1 = UnqualifiedApproval, \[5.0.0+\] bit2-3: PoolPartition? For applets set to 0b01, for sysmodules set to 0b10. Exceptions: "starter" is set to 0, "nvservices" is set to 3) |
| 0x210  | 0x8   | TitleIdRange\_Min                                                                                                                                                                                             |
| 0x218  | 0x8   | TitleIdRange\_Max                                                                                                                                                                                             |
| 0x220  | 0x4   | [\#FS Access Control](#FS_Access_Control "wikilink") offset                                                                                                                                                   |
| 0x224  | 0x4   | [\#FS Access Control](#FS_Access_Control "wikilink") size                                                                                                                                                     |
| 0x228  | 0x4   | [\#Service Access Control](#Service_Access_Control "wikilink") offset                                                                                                                                         |
| 0x22C  | 0x4   | [\#Service Access Control](#Service_Access_Control "wikilink") size                                                                                                                                           |
| 0x230  | 0x4   | [\#Kernel Access Control](#Kernel_Access_Control "wikilink") offset                                                                                                                                           |
| 0x234  | 0x4   | [\#Kernel Access Control](#Kernel_Access_Control "wikilink") size                                                                                                                                             |
| 0x238  | 0x8   | Reserved                                                                                                                                                                                                      |

# ACI0

| Offset | Size | Description                                                           |
| ------ | ---- | --------------------------------------------------------------------- |
| 0x0    | 0x4  | Magicnum "ACI0"                                                       |
| 0x4    | 0xC  | Reserved                                                              |
| 0x10   | 0x8  | Title ID                                                              |
| 0x18   | 0x8  | Reserved                                                              |
| 0x20   | 0x4  | [\#FS Access Header](#FS_Access_Header "wikilink") offset             |
| 0x24   | 0x4  | [\#FS Access Header](#FS_Access_Header "wikilink") size               |
| 0x28   | 0x4  | [\#Service Access Control](#Service_Access_Control "wikilink") offset |
| 0x2C   | 0x4  | [\#Service Access Control](#Service_Access_Control "wikilink") size   |
| 0x30   | 0x4  | [\#Kernel Access Control](#Kernel_Access_Control "wikilink") offset   |
| 0x34   | 0x4  | [\#Kernel Access Control](#Kernel_Access_Control "wikilink") size     |
| 0x38   | 0x8  | Reserved                                                              |

# FS Access Header

| Offset                            | Size                                       | Description                                                                       |
| --------------------------------- | ------------------------------------------ | --------------------------------------------------------------------------------- |
| 0x0                               | 0x1                                        | Version (always 1, must be non-zero)                                              |
| 0x1                               | 0x3                                        | Padding                                                                           |
| 0x4                               | 0x8                                        | Permissions bitmask                                                               |
| 0xC                               | 0x4                                        | Data Size (always 0x1C)                                                           |
| 0x10                              | 0x4                                        | Size of Content Owner ID section.                                                 |
| 0x14                              | 0x4                                        | Data size (0x1C) plus Content Owner size                                          |
| 0x18                              | 0x4                                        | Size of Save Data owners section (for applications that wish to share save data?) |
| 0x1C                              | 0x4                                        | (OPTIONAL) Amount of content owner id's                                           |
| 0x1C                              | 0x8 \* Content Owner ID's                  | Content owner ID's as uint64's.                                                   |
| VARIABLE                          | 0x4                                        | Amount of save owner id's                                                         |
| VARIABLE                          | 0x1 \* Save data owner accessibilities (?) | Sets flags for what save data owners can do with other applications save data (?) |
| VARIABLE (Pad to nearest 4 bytes) | 0x8 \* Amount of save owner ID's           | Save data owner ID's                                                              |

# FS Access Control

| Offset | Size | Description                          |
| ------ | ---- | ------------------------------------ |
| 0x0    | 0x1  | Version (always 1, must be non-zero) |
| 0x1    | 0x3  | Padding                              |
| 0x4    | 0x8  | Permissions bitmask                  |
| 0xC    | 0x20 | Reserved                             |

[Permissions](Filesystem%20services#Permissions.md##Permissions "wikilink")
bitmask:

| Bit   | Name                     | Description                                                                                                                                                 |
| ----- | ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0     | ApplicationInfo          | MountContent\* is accessible when set.                                                                                                                      |
| 1     | BootModeControl          |                                                                                                                                                             |
| 2     | Calibration              |                                                                                                                                                             |
| 3     | SystemSaveData           |                                                                                                                                                             |
| 4     | GameCard                 |                                                                                                                                                             |
| 5     | SaveDataBackUp           |                                                                                                                                                             |
| 6     | SaveDataManagement       |                                                                                                                                                             |
| 7     | BisAllRaw                |                                                                                                                                                             |
| 8     | GameCardRaw              |                                                                                                                                                             |
| 9     | GameCardPrivate          |                                                                                                                                                             |
| 10    | SetTime                  |                                                                                                                                                             |
| 11    | ContentManager           |                                                                                                                                                             |
| 12    | ImageManager             |                                                                                                                                                             |
| 13    | CreateSaveData           |                                                                                                                                                             |
| 14    | SystemSaveDataManagement |                                                                                                                                                             |
| 15    | BisFileSystem            |                                                                                                                                                             |
| 16    | SystemUpdate             |                                                                                                                                                             |
| 17    | SaveDataMeta             |                                                                                                                                                             |
| 18    | DeviceSaveData           |                                                                                                                                                             |
| 19    | SettingsControl          |                                                                                                                                                             |
| 20    | SystemData               |                                                                                                                                                             |
| 21    | SdCard                   |                                                                                                                                                             |
| 22    | Host                     |                                                                                                                                                             |
| 23    | FillBis                  |                                                                                                                                                             |
| 24    | CorruptSaveData          |                                                                                                                                                             |
| 25    | SaveDataForDebug         |                                                                                                                                                             |
| 26    | FormatSdCard             |                                                                                                                                                             |
| 27    | GetRightsId              |                                                                                                                                                             |
| 28    | RegisterExternalKey      |                                                                                                                                                             |
| 29    | RegisterUpdatePartition  |                                                                                                                                                             |
| 30    | SaveDataTransfer         |                                                                                                                                                             |
| 31    | DeviceDetection          |                                                                                                                                                             |
| 32    | AccessFailureResolution  |                                                                                                                                                             |
| 33    | SaveDataTransferVersion2 |                                                                                                                                                             |
| 34-61 | Reserved                 |                                                                                                                                                             |
| 62    | Debug                    | See [here](SPL%20services#GetConfig.md##GetConfig "wikilink").                                                                                              |
| 63    | FullPermission           | Enables access to everything: all [permission types](Filesystem%20services#Permissions.md##Permissions "wikilink") which check a bitmask have this bit set. |

Web-applets permissions:

  - "LibAppletWeb" and "LibAppletOff" have same access control: bit0 and
    bit3 set, and bit62 set.
  - Rest of the web-applets: Same as above except bit0 isn't set.

# Service Access Control

This is a list of [service](Services%20API.md "wikilink")-name strings
which the title has access to, with the following structure:

` +0: control_byte`  
` +1: {service-name without nul-terminator}`

Bitmask 0x07 in control\_byte is the {length of the service-name without
nul-terminator} - 1.

Bitmask 0x80 in control\_byte means service is allowed to be registered.

The service string can contain a wildcard `*` character.

# Kernel Access Control

On Switch, descriptors are identified by pattern 01..11 in low bits.

| Pattern of lower bits | Lowest clear bitmask/bit | Type                 | Fields                                                                                                                                                                                                                                              |
| --------------------- | ------------------------ | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `0bxxxxxxxxxxxx0111`  | Bit3                     | KernelFlags          | Bit31-24: Highest allowed cpu id, bit23-16: Lowest allowed cpu id, bit15-10: Highest allowed thread prio, bit9-4: Lowest allowed thread prio                                                                                                        |
| `0bxxxxxxxxxxx01111`  | Bit4                     | SyscallMask          | Bits 29-31: Syscall mask table index; Bits 5-28: Mask                                                                                                                                                                                               |
| `0bxxxxxxxxx0111111`  | Bit6                     | MapIoOrNormalRange   | Bits 7-30: Alternating start page and number of pages, bit31: Alternating read-only flag then MemoryAttribute 0x2001/0x42002 selector flag                                                                                                          |
| `0bxxxxxxxx01111111`  | Bit7                     | MapNormalPage (RW)   | Bits 8-31: Page                                                                                                                                                                                                                                     |
| `0bxxxx011111111111`  | Bit11                    | InterruptPair        | Bits 12-21: Irq0, bits 22-31: Irq1, 0x3FF means empty.                                                                                                                                                                                              |
| `0bxx01111111111111`  | Bit13                    | ApplicationType      | Bit16-14: ApplicationType (0=sysmodule, 1=application, 2=applet), bit16 ignored. Parsed by [Process Manager services](Process%20Manager%20services.md "wikilink"). Defaults to 0 if descriptor doesn't exist. Can only run 1 application at a time. |
| `0bx011111111111111`  | Bit14                    | KernelReleaseVersion | Bits 15-X: Version. The raw descriptor is compared with 0x80000, when less than an error is returned. This is equivalent to comparing the bits starting at bit15 with 0x10. This enforces a minimum required version, not a maximum.                |
| `0b0111111111111111`  | Bit15                    | HandleTableSize      | Bit25-16: Number of handles the table shall fit.                                                                                                                                                                                                    |
| `0b1111111111111111`  | Bit16                    | DebugFlags           | Bit17: can be debugged, bit18: can debug others                                                                                                                                                                                                     |
| All ones              |                          | Ignored              |                                                                                                                                                                                                                                                     |

## Mapping restrictions

The physaddr range 0x80060000-0x2000000000 is not allowed to be mapped
as IO. The physaddr range 0x80000000-0x2000000000 is not allowed to be
mapped as Normal.

\[2.0.0-4.1.0\] The range for IO was changed into 0x80060000-0x81D3FFFF.

\[2.0.0-4.1.0\] A blacklist was added for IO and Normal mappings:

  - 0x50040000-0x50060000 (ARM, Interrupt Controller)
  - 0x6000F000 (Exception Vectors)
  - 0x6001DC00-0x6001E000 (IPATCH)
  - 0x7000E000 (RTC/PMC)
  - 0x70019000 (MC)
  - 0x7001C000 (MC0)
  - 0x7001D000 (MC1)

\[5.0.0+\] For IO, this blacklist was abandoned and instead two range
checks were added. For Normal mappings it is still applied

## Kernel versions

| Firmware | Kernel Version | Minimum Allowed |
| -------- | -------------- | --------------- |
| 1.0.0    | 5.0.0          | 3.0.0           |
| 2.0.0    | 6.1.0          | 3.0.0           |
| 3.0.0    | 7.4.0          | 3.0.0           |
| 3.0.2    | 7.4.0          | 3.0.0           |
| 5.0.0    | 9.3.0          | 3.0.0           |

Bit31-19: Major version</br> Bit18-15: Minor version</br> Bit14-0:
Zeroes
