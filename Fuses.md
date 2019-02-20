The Nintendo Switch makes use of Tegra's fuse driver for a number of
operations. This driver is mapped to physical address 0x7000F800 with a
total size of 0x400 bytes and exposes several registers for fuse
programming.

Registers from 0x7000F800 to 0x7000F800 + 0xFF can be used to directly
program the hardware fuse array, while registers from 0x7000F800 + 0x100
(FUSE\_CHIP\_REG\_START\_OFFSET) to 0x7000F800 + 0x3FC
(FUSE\_CHIP\_REG\_END\_OFFSET) represent cached values read from certain
fuses.

## Registers

Below is a list of fuse driver registers used by the Switch's
bootloaders.

### Driver registers

| Name                                                 | Address    |
| ---------------------------------------------------- | ---------- |
| [FUSE\_CTRL](#FUSE_CTRL "wikilink")                  | 0x7000F800 |
| [FUSE\_REG\_ADDR](#FUSE_REG_ADDR "wikilink")         | 0x7000F804 |
| [FUSE\_REG\_READ](#FUSE_REG_READ "wikilink")         | 0x7000F808 |
| [FUSE\_REG\_WRITE](#FUSE_REG_WRITE "wikilink")       | 0x7000F80C |
| FUSE\_TIME\_RD1                                      | 0x7000F810 |
| FUSE\_TIME\_RD2                                      | 0x7000F814 |
| FUSE\_TIME\_PGM1                                     | 0x7000F818 |
| [FUSE\_TIME\_PGM2](#FUSE_TIME_PGM2 "wikilink")       | 0x7000F81C |
| [FUSE\_PRIV2INTFC](#FUSE_PRIV2INTFC "wikilink")      | 0x7000F820 |
| FUSE\_FUSEBYPASS                                     | 0x7000F824 |
| FUSE\_PRIVATEKEYDISABLE                              | 0x7000F828 |
| [FUSE\_DIS\_PGM](#FUSE_DIS_PGM "wikilink")           | 0x7000F82C |
| [FUSE\_WRITE\_ACCESS](#FUSE_WRITE_ACCESS "wikilink") | 0x7000F830 |
| FUSE\_PWR\_GOOD\_SW                                  | 0x7000F834 |
| FUSE\_PRIVATE\_KEY0\_NONZERO                         | 0x7000F880 |
| FUSE\_PRIVATE\_KEY1\_NONZERO                         | 0x7000F884 |
| FUSE\_PRIVATE\_KEY2\_NONZERO                         | 0x7000F888 |
| FUSE\_PRIVATE\_KEY3\_NONZERO                         | 0x7000F88C |
| FUSE\_PRIVATE\_KEY4\_NONZERO                         | 0x7000F890 |

#### FUSE\_CTRL

| Bits  | Description                                                     |
| ----- | --------------------------------------------------------------- |
| 0-1   | Fuse command (1 = FUSE\_READ; 2 = FUSE\_WRITE; 3 = FUSE\_SENSE) |
| 16-20 | Fuse state (4 = STATE\_IDLE)                                    |
| 26    | Fuse power down mode flag (FUSE\_CTRL\_PD)                      |
| 30    | Fuse sense status (FUSE\_CTRL\_SENSE\_DONE)                     |

Before fuse reading/writing the power down mode must be disabled.
FUSE\_SENSE mode flushes programmed values into the [cache
registers](Fuses#Cache%20registers.md##Cache_registers "wikilink").

#### FUSE\_REG\_ADDR

This register takes the address of the fuse to be read/written/sensed.

#### FUSE\_REG\_READ

This register receives the value read from the fuse.

#### FUSE\_REG\_WRITE

This register takes the value to be written to the fuse.

#### FUSE\_TIME\_PGM2

This register takes the fuse programming pulse (0xC0 == 19200 kHz).

#### FUSE\_PRIV2INTFC

| Bits | Description                     |
| ---- | ------------------------------- |
| 0    | FUSE\_PRIV2INTFC\_SDATA         |
| 1    | FUSE\_PRIV2INTFC\_SKIP\_RECORDS |

#### FUSE\_DIS\_PGM

If set to 0x01, this register disables fuse programming.

#### FUSE\_WRITE\_ACCESS

If set to 0x01, this register disables software writes to the fuse
driver registers.

### Cache registers

| Name                                                   | Address    |
| ------------------------------------------------------ | ---------- |
| FUSE\_PRODUCTION\_MODE                                 | 0x7000F900 |
| FUSE\_JTAG\_SECUREID\_VALID                            | 0x7000F904 |
| FUSE\_ODM\_LOCK                                        | 0x7000F908 |
| [FUSE\_SKU\_INFO](#FUSE_SKU_INFO "wikilink")           | 0x7000F910 |
| FUSE\_CPU\_SPEEDO\_0                                   | 0x7000F914 |
| FUSE\_CPU\_IDDQ                                        | 0x7000F918 |
| FUSE\_DAC\_CRT\_CALIB                                  | 0x7000F91C |
| FUSE\_DAC\_HDTV\_CALIB                                 | 0x7000F920 |
| FUSE\_DAC\_SDTV\_CALIB                                 | 0x7000F924 |
| FUSE\_FT\_REV                                          | 0x7000F928 |
| FUSE\_CPU\_SPEEDO\_1                                   | 0x7000F92C |
| FUSE\_CPU\_SPEEDO\_2                                   | 0x7000F930 |
| FUSE\_SOC\_SPEEDO\_0                                   | 0x7000F934 |
| [FUSE\_SOC\_SPEEDO\_1](#FUSE_SOC_SPEEDO_1 "wikilink")  | 0x7000F938 |
| FUSE\_SOC\_SPEEDO\_2                                   | 0x7000F93C |
| FUSE\_SOC\_IDDQ                                        | 0x7000F940 |
| FUSE\_RESERVED\_PRODUCTION\_WP                         | 0x7000F944 |
| [FUSE\_FA](#FUSE_FA "wikilink")                        | 0x7000F948 |
| FUSE\_RESERVED\_PRODUCTION                             | 0x7000F94C |
| FUSE\_HDMI\_LANE0\_CALIB                               | 0x7000F950 |
| FUSE\_HDMI\_LANE1\_CALIB                               | 0x7000F954 |
| FUSE\_HDMI\_LANE2\_CALIB                               | 0x7000F958 |
| FUSE\_HDMI\_LANE3\_CALIB                               | 0x7000F95C |
| FUSE\_ENCRYPTION\_RATE                                 | 0x7000F960 |
| [FUSE\_PUBLIC\_KEY0](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F964 |
| [FUSE\_PUBLIC\_KEY1](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F968 |
| [FUSE\_PUBLIC\_KEY2](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F96C |
| [FUSE\_PUBLIC\_KEY3](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F970 |
| [FUSE\_PUBLIC\_KEY4](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F974 |
| [FUSE\_PUBLIC\_KEY5](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F978 |
| [FUSE\_PUBLIC\_KEY6](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F97C |
| [FUSE\_PUBLIC\_KEY7](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F980 |
| FUSE\_TSENSOR\_1                                       | 0x7000F984 |
| FUSE\_TSENSOR\_2                                       | 0x7000F988 |
| FUSE\_VSENSOR\_CALIB                                   | 0x7000F98C |
| FUSE\_CP\_REV                                          | 0x7000F990 |
| FUSE\_OPT\_PFG                                         | 0x7000F994 |
| FUSE\_TSENSOR\_0                                       | 0x7000F998 |
| FUSE\_FIRST\_BOOTROM\_PATCH\_SIZE\_REG                 | 0x7000F99C |
| FUSE\_SECURITY\_MODE                                   | 0x7000F9A0 |
| [FUSE\_PRIVATE\_KEY0](#FUSE_PRIVATE_KEY "wikilink")    | 0x7000F9A4 |
| [FUSE\_PRIVATE\_KEY1](#FUSE_PRIVATE_KEY "wikilink")    | 0x7000F9A8 |
| [FUSE\_PRIVATE\_KEY2](#FUSE_PRIVATE_KEY "wikilink")    | 0x7000F9AC |
| [FUSE\_PRIVATE\_KEY3](#FUSE_PRIVATE_KEY "wikilink")    | 0x7000F9B0 |
| [FUSE\_PRIVATE\_KEY4](#FUSE_PRIVATE_KEY "wikilink")    | 0x7000F9B4 |
| FUSE\_ARM\_JTAG\_DISABLE                               | 0x7000F9B8 |
| FUSE\_BOOT\_DEVICE\_INFO                               | 0x7000F9BC |
| [FUSE\_RESERVED\_SW](#FUSE_RESERVED_SW "wikilink")     | 0x7000F9C0 |
| FUSE\_VP8\_ENABLE                                      | 0x7000F9C4 |
| [FUSE\_RESERVED\_ODM0](#FUSE_RESERVED_ODM0 "wikilink") | 0x7000F9C8 |
| [FUSE\_RESERVED\_ODM1](#FUSE_RESERVED_ODM1 "wikilink") | 0x7000F9CC |
| [FUSE\_RESERVED\_ODM2](#FUSE_RESERVED_ODM2 "wikilink") | 0x7000F9D0 |
| [FUSE\_RESERVED\_ODM3](#FUSE_RESERVED_ODM3 "wikilink") | 0x7000F9D4 |
| [FUSE\_RESERVED\_ODM4](#FUSE_RESERVED_ODM4 "wikilink") | 0x7000F9D8 |
| FUSE\_RESERVED\_ODM5                                   | 0x7000F9DC |
| [FUSE\_RESERVED\_ODM6](#FUSE_RESERVED_ODM6 "wikilink") | 0x7000F9E0 |
| [FUSE\_RESERVED\_ODM7](#FUSE_RESERVED_ODM7 "wikilink") | 0x7000F9E4 |
| FUSE\_OBS\_DIS                                         | 0x7000F9E8 |
| FUSE\_NOR\_INFO                                        | 0x7000F9EC |
| FUSE\_SKU\_USB\_CALIB                                  | 0x7000F9F0 |
| FUSE\_SKU\_DIRECT\_CONFIG                              | 0x7000F9F4 |
| FUSE\_KFUSE\_PRIVKEY\_CTRL                             | 0x7000F9F8 |
| FUSE\_PACKAGE\_INFO                                    | 0x7000F9FC |
| FUSE\_VENDOR\_CODE                                     | 0x7000FA00 |
| FUSE\_FAB\_CODE                                        | 0x7000FA04 |
| FUSE\_LOT\_CODE\_0                                     | 0x7000FA08 |
| FUSE\_LOT\_CODE\_1                                     | 0x7000FA0C |
| FUSE\_WAFER\_ID                                        | 0x7000FA10 |
| FUSE\_X\_COORDINATE                                    | 0x7000FA14 |
| FUSE\_Y\_COORDINATE                                    | 0x7000FA18 |
| FUSE\_OPS\_RESERVED                                    | 0x7000FA20 |
| FUSE\_SATA\_CALIB                                      | 0x7000FA24 |
| FUSE\_GPU\_IDDQ                                        | 0x7000FA28 |
| FUSE\_TSENSOR\_3                                       | 0x7000FA2C |
| FUSE\_SKU\_BOND\_OUT\_L                                | 0x7000FA30 |
| FUSE\_SKU\_BOND\_OUT\_H                                | 0x7000FA34 |
| FUSE\_SKU\_BOND\_OUT\_U                                | 0x7000FA38 |
| FUSE\_SKU\_BOND\_OUT\_V                                | 0x7000FA3C |
| FUSE\_SKU\_BOND\_OUT\_W                                | 0x7000FA40 |
| FUSE\_OPT\_SUBREVISION                                 | 0x7000FA48 |
| FUSE\_TSENSOR\_4                                       | 0x7000FA54 |
| FUSE\_TSENSOR\_5                                       | 0x7000FA58 |
| FUSE\_TSENSOR\_6                                       | 0x7000FA5C |
| FUSE\_TSENSOR\_7                                       | 0x7000FA60 |
| FUSE\_OPT\_PRIV\_SEC\_DIS                              | 0x7000FA64 |
| [FUSE\_PKC\_DISABLE](#FUSE_PKC_DISABLE "wikilink")     | 0x7000FA68 |
| FUSE\_FALCON\_DEBUG\_DISABLE                           | 0x7000FA7C |
| FUSE\_TSENSOR\_COMMON                                  | 0x7000FA80 |
| FUSE\_DEBUG\_AUTH\_OVERRIDE                            | 0x7000FA9C |
| FUSE\_GCPLEX\_CONFIG\_FUSE                             | 0x7000FAC8 |
| FUSE\_TSENSOR\_8                                       | 0x7000FAD4 |
| FUSE\_DEBUG\_AUTHENTICATION                            | 0x7000FAE4 |
| FUSE\_SECURE\_PROVISION\_INDEX                         | 0x7000FAE8 |
| FUSE\_AID                                              | 0x7000FAF8 |
| FUSE\_SPARE\_REALIGNMENT\_REG                          | 0x7000FAFC |
| FUSE\_RESERVED\_CALIB0                                 | 0x7000FB04 |
| FUSE\_OPT\_GPU\_TPC0\_DISABLE                          | 0x7000FB0C |
| FUSE\_TSENSOR\_9                                       | 0x7000FB1C |
| FUSE\_OPT\_GPU\_TPC1\_DISABLE                          | 0x7000FB3C |
| FUSE\_USB\_CALIB\_EXT                                  | 0x7000FB50 |
| FUSE\_OPT\_ECC\_EN                                     | 0x7000FB58 |
| FUSE\_SPARE\_BIT\_0                                    | 0x7000FB80 |
| FUSE\_SPARE\_BIT\_1                                    | 0x7000FB84 |
| [FUSE\_SPARE\_BIT\_2](#FUSE_SPARE_BIT_2 "wikilink")    | 0x7000FB88 |
| [FUSE\_SPARE\_BIT\_3](#FUSE_SPARE_BIT_3 "wikilink")    | 0x7000FB8C |
| [FUSE\_SPARE\_BIT\_4](#FUSE_SPARE_BIT_4 "wikilink")    | 0x7000FB90 |
| [FUSE\_SPARE\_BIT\_5](#FUSE_SPARE_BIT_5 "wikilink")    | 0x7000FB94 |
| FUSE\_SPARE\_BIT\_6                                    | 0x7000FB98 |
| FUSE\_SPARE\_BIT\_7                                    | 0x7000FB9C |
| FUSE\_SPARE\_BIT\_8                                    | 0x7000FBA0 |
| FUSE\_SPARE\_BIT\_9                                    | 0x7000FBA4 |
| FUSE\_SPARE\_BIT\_10                                   | 0x7000FBA8 |
| FUSE\_SPARE\_BIT\_11                                   | 0x7000FBAC |
| FUSE\_SPARE\_BIT\_12                                   | 0x7000FBB0 |
| FUSE\_SPARE\_BIT\_13                                   | 0x7000FBB4 |
| FUSE\_SPARE\_BIT\_14                                   | 0x7000FBB8 |
| FUSE\_SPARE\_BIT\_15                                   | 0x7000FBBC |
| FUSE\_SPARE\_BIT\_16                                   | 0x7000FBC0 |
| FUSE\_SPARE\_BIT\_17                                   | 0x7000FBC4 |
| FUSE\_SPARE\_BIT\_18                                   | 0x7000FBC8 |
| FUSE\_SPARE\_BIT\_19                                   | 0x7000FBCC |
| FUSE\_SPARE\_BIT\_20                                   | 0x7000FBD0 |
| FUSE\_SPARE\_BIT\_21                                   | 0x7000FBD4 |
| FUSE\_SPARE\_BIT\_22                                   | 0x7000FBD8 |
| FUSE\_SPARE\_BIT\_23                                   | 0x7000FBDC |
| FUSE\_SPARE\_BIT\_24                                   | 0x7000FBE0 |
| FUSE\_SPARE\_BIT\_25                                   | 0x7000FBE4 |
| FUSE\_SPARE\_BIT\_26                                   | 0x7000FBE8 |
| FUSE\_SPARE\_BIT\_27                                   | 0x7000FBEC |
| FUSE\_SPARE\_BIT\_28                                   | 0x7000FBF0 |
| FUSE\_SPARE\_BIT\_29                                   | 0x7000FBF4 |
| FUSE\_SPARE\_BIT\_30                                   | 0x7000FBF8 |
| FUSE\_SPARE\_BIT\_31                                   | 0x7000FBFC |

#### FUSE\_SKU\_INFO

Stores the SKU ID (must be 0x83).

#### FUSE\_FA

Stores failure analysis mode.

#### FUSE\_SOC\_SPEEDO\_1

Stores the bootrom patch version.

#### FUSE\_RESERVED\_ODM0

This appears to store a hardware ID.

#### FUSE\_RESERVED\_ODM1

This appears to store a hardware ID.

#### FUSE\_RESERVED\_ODM2

| Bits | Description                       |
| ---- | --------------------------------- |
| 0-4  | \[5.0.0+\] Used as key generation |

This appears to store a hardware ID.

#### FUSE\_RESERVED\_ODM3

This appears to store a hardware
ID.

#### FUSE\_RESERVED\_ODM4

| Bits                               | Description                                   |
| ---------------------------------- | --------------------------------------------- |
| 0-1                                | Unit type (3 = debug; 0 = retail)             |
| 2                                  | Unknown config (must be 1 on retail)          |
| \[1.0.0-3.0.2\] 3-5 \[4.0.0+\] 3-7 | DRAM id                                       |
| 8                                  | Unknown config mask (must be 0 on retail)     |
| 9                                  | Unit type mask (0 = debug; 1 = retail)        |
| 10                                 | \[3.0.0+\] Kiosk mode (0 = retail; 1 = kiosk) |
| 11                                 | \[5.0.0+\] SoC variant (0 = T210; 1 = T214)   |
| 16-19                              | \[4.0.0+\] New unit type                      |

This stores some device configuration parameters.

#### FUSE\_RESERVED\_ODM6

This register returns the value programmed into index 0x3A of the fuse
array.

#### FUSE\_RESERVED\_ODM7

This register returns the value programmed into index 0x3C of the fuse
array.

#### FUSE\_SPARE\_BIT\_2

Stores part of the speedo fusing revision.

#### FUSE\_SPARE\_BIT\_3

Stores part of the speedo fusing revision.

#### FUSE\_SPARE\_BIT\_4

Stores part of the speedo fusing revision.

#### FUSE\_SPARE\_BIT\_5

Must be non-zero on retail units, otherwise the first bootloader panics.
On debug units it can be zero, which tells the bootloader to choose from
two debug master key seeds. If set to non-zero on a debug unit, it tells
the bootloader to choose from two retail master key seeds (only the last
one matches the retail master key seed).

#### FUSE\_PRIVATE\_KEY

This stores the 160-bit private key (128 bit SBK + 32-bit device key).
Reads to these registers after the SBK is locked out produce all-FF
output.

#### FUSE\_PUBLIC\_KEY

This stores the SHA256 hash of the 2048-bit RSA key expected at
BCT+0x210.

#### FUSE\_RESERVED\_SW

| Bits | Description                                                             |
| ---- | ----------------------------------------------------------------------- |
| 0-2  | Boot device                                                             |
| 3    | Skip device selection straps (0 = don't skip; 1 = skip)                 |
| 4    | ENABLE\_CHARGER\_DETECT                                                 |
| 5    | ENABLE\_WATCHDOG                                                        |
| 6    | Forced RCM two button mode (0 = Only VOLUME\_UP; 1 = VOLUME\_UP + HOME) |
| 7    | RCM USB controller mode (0 = USB 2.0; 1 = XUSB)                         |

This caches the value of the sw\_reserved fuse from the hardware array.

#### FUSE\_PKC\_DISABLE

This caches the value of the pkc\_disable fuse from the hardware array.

## eFuses

The actual hardware fuses can be programmed through the fuse driver
after enabling fuse programming.

Below is a list of common fuse indexes used by Tegra devices (and
applicable to the Switch). Note that the indexes are relative to the
start of the fuse array and each element is a 4 byte word. A single fuse
write operation always writes the same word at both fuse\_array + 0
(PRIMARY\_ALIAS) and fuse\_array + 1 (REDUNDANT\_ALIAS).

| Name                                          | Index | Bits |
| --------------------------------------------- | ----- | ---- |
| jtag\_disable                                 | 0x00  | 1    |
| odm\_production\_mode                         | 0x00  | 1    |
| odm\_lock                                     | 0x00  | 4    |
| public\_key                                   | 0x0C  | 256  |
| secure\_boot\_key                             | 0x22  | 128  |
| device\_key                                   | 0x2A  | 32   |
| sec\_boot\_dev\_cfg                           | 0x2C  | 16   |
| sec\_boot\_dev\_sel                           | 0x2C  | 3    |
| sw\_reserved                                  | 0x2E  | 12   |
| ignore\_dev\_sel\_straps                      | 0x2E  | 1    |
| [odm\_reserved](#odm_reserved "wikilink")     | 0x2E  | 256  |
| pkc\_disable                                  | 0x52  | 1    |
| debug\_authentication                         | 0x5A  | 5    |
| aid                                           | 0x67  | 32   |
| [bootrom\_ipatch](#bootrom_ipatch "wikilink") | 0x72  | 624  |

### odm\_reserved

The first bootloader only burns fuses in this region. Both fuse indexes
0x3A (odm\_reserved + 0x0C) and 0x3C (odm\_reserved + 0x0E) are used for
anti-downgrade control. These fuses will have their values cached into
[FUSE\_RESERVED\_ODM6](#FUSE_RESERVED_ODM6 "wikilink") and
[FUSE\_RESERVED\_ODM7](#FUSE_RESERVED_ODM7 "wikilink").

### bootrom\_ipatch

Tegra210 based hardware such as the Switch provides support for bootrom
patches. The patch data is burned to the hardware fuse array using a
specific format (see [shuffle2's ipatch
decoder](https://gist.github.com/shuffle2/f8728159da100e9df2606d43925de0af)).
The bootrom reads these fuses in order to initialize the IPATCH
hardware, which allows overriding data returned for code and data
fetches done by BPMP. The revision stored in FUSE\_CP\_REV indicates the
unique set of values stored in ipatch fuses.

The following represents the patch data dumped from a Switch
    console:

    RAM:00000000 ; =============== S U B R O U T I N E =======================================
    RAM:00000000
    RAM:00000000
    RAM:00000000 irom_svc_dispatch
    RAM:00000000   STMFD   SP!, {R0-R2}                  ; ipatches:
    RAM:00000000                                         ;  0  b57df00     16ae     df00 : svc #0x00 (offset 0x48)
    RAM:00000000                                         ;  1 1820df22     3040     df22 : svc #0x22 (offset 0x8c)
    RAM:00000000                                         ;  2 3797df26     6f2e     df26 : svc #0x26 (offset 0x94)
    RAM:00000000                                         ;  3 7d9e2000     fb3c     2000 : movs r0, #0x00
    RAM:00000000                                         ;  4  42bdf2c      856     df2c : svc #0x2c (offset 0xa0)
    RAM:00000000                                         ;  5 37aadf42     6f54     df42 : svc #0x42 (offset 0xcc)
    RAM:00000000                                         ;  6  972df4b     12e4     df4b : svc #0x4b (offset 0xde)
    RAM:00000000                                         ;  7 2293df54     4526     df54 : svc #0x54 (offset 0xf0)
    RAM:00000000                                         ;  8 21fadf5d     43f4     df5d : svc #0x5d (offset 0x102)
    RAM:00000000                                         ;  9 bba2ac57    17744     ac57 : data
    RAM:00000000                                         ; 10 bbac3d19    17758     3d19 : data
    RAM:00000000                                         ; 11 1e952001     3d2a     2001 : movs r0, #0x01
    RAM:00000004   MOV     R2, LR
    RAM:00000008   SUB     R2, R2, #2
    RAM:0000000C   LDR     R2, [R2]
    RAM:00000010   AND     R2, R2, #0xFF
    RAM:00000014   MOV     R2, R2,LSL#1
    RAM:00000018   LDR     R0, =0x1007B0
    RAM:0000001C   LDR     R1, =0x1007F8
    RAM:00000020   SUB     R1, R1, R0
    RAM:00000024   LDR     R0, =0x40004C30
    RAM:00000028   ADD     R0, R0, R1
    RAM:0000002C   ADD     R2, R2, R0
    RAM:00000030   ORR     R2, R2, #1
    RAM:00000034   LDMFD   SP!, {R0,R1}
    RAM:00000038   BX      R2
    RAM:00000038 ; End of function irom_svc_dispatch
    RAM:00000038
    RAM:00000038 ; ---------------------------------------------------------------------------
    RAM:0000003C dword_3C DCD 0x1007B0                   ; DATA XREF: irom_svc_dispatch+18↑r
    RAM:00000040 dword_40 DCD 0x1007F8                   ; DATA XREF: irom_svc_dispatch+1C↑r
    RAM:00000044 dword_44 DCD 0x40004C30                 ; DATA XREF: irom_svc_dispatch+24↑r
    RAM:00000048   CODE16
    RAM:00000048
    RAM:00000048 ; =============== S U B R O U T I N E =======================================
    RAM:00000048
    RAM:00000048
    RAM:00000048 sub_48
    RAM:00000048   MOVS    R2, #0                        ; 0  b57df00     16ae     df00 : svc #0x00 (offset 0x48)
    RAM:0000004A   MVNS    R2, R2
    RAM:0000004C   LDR     R1, =0x60006410
    RAM:0000004E   STR     R2, [R1,#0x30]
    RAM:00000050   STR     R2, [R1,#0x38]
    RAM:00000052   LDR     R1, =0x600060F8
    RAM:00000054   STR     R2, [R1]
    RAM:00000056   STR     R2, [R1,#4]
    RAM:00000058   LDR     R1, =0x60006284
    RAM:0000005A   STR     R2, [R1]
    RAM:0000005C   STR     R2, [R1,#0x18]
    RAM:0000005E   ADDS    R1, #0x80
    RAM:00000060   ADDS    R1, #0x1C
    RAM:00000062   STR     R2, [R1]
    RAM:00000064   STR     R2, [R1,#8]
    RAM:00000066   STR     R2, [R1,#0x10]
    RAM:00000068   ADDS    R1, #0x80
    RAM:0000006A   STR     R2, [R1]
    RAM:0000006C   STR     R2, [R1,#4]
    RAM:0000006E   LDR     R1, =0x60006554
    RAM:00000070   STR     R2, [R1]
    RAM:00000072   MOVS    R2, #0xA0000000
    RAM:00000076   LDR     R1, =0x60006148
    RAM:00000078   STR     R2, [R1]
    RAM:0000007A   ADDS    R1, #0x38 ; '8'
    RAM:0000007C   STR     R2, [R1]
    RAM:0000007E   MOVS    R2, #0xE0000000
    RAM:00000082   LDR     R1, =0x600066A0
    RAM:00000084   STR     R2, [R1]
    RAM:00000086   MOVS    R1, #0
    RAM:00000088   MOVS    R0, #0xE
    RAM:0000008A   B       pop_r2_mov_pc_lr
    RAM:0000008A ; End of function sub_48
    RAM:0000008A
    RAM:0000008C
    RAM:0000008C ; =============== S U B R O U T I N E =======================================
    RAM:0000008C
    RAM:0000008C
    RAM:0000008C sub_8C
    RAM:0000008C   LDR     R0, [R1,#0x18]                ; 1 1820df22     3040     df22 : svc #0x22 (offset 0x8c)
    RAM:0000008E   MOVS    R2, #1
    RAM:00000090   ORRS    R0, R2
    RAM:00000092   B       pop_r2_mov_pc_lr
    RAM:00000092 ; End of function sub_8C
    RAM:00000092
    RAM:00000094
    RAM:00000094 ; =============== S U B R O U T I N E =======================================
    RAM:00000094
    RAM:00000094
    RAM:00000094 sub_94
    RAM:00000094   LDR     R2, [R4,#0x50]                ; 2 3797df26     6f2e     df26 : svc #0x26 (offset 0x94)
    RAM:00000096   ADDS    R2, R2, #2
    RAM:00000098   STR     R2, [R4,#0x50]
    RAM:0000009A   SUBS    R1, #0x80
    RAM:0000009C   STR     R1, [R4,#0x34]
    RAM:0000009E   B       pop_r2_mov_pc_lr
    RAM:0000009E ; End of function sub_94
    RAM:0000009E
    RAM:000000A0
    RAM:000000A0 ; =============== S U B R O U T I N E =======================================
    RAM:000000A0
    RAM:000000A0
    RAM:000000A0 sub_A0
    RAM:000000A0
    RAM:000000A0 ; FUNCTION CHUNK AT RAM:00000148 SIZE 00000004 BYTES
    RAM:000000A0
    RAM:000000A0   MOVS    R0, #0x70000000               ; 4  42bdf2c      856     df2c : svc #0x2c (offset 0xa0)
    RAM:000000A4   LDR     R6, =dword_7000EF14
    RAM:000000A6   LDR     R2, =dword_7000E5B4
    RAM:000000A8   LDR     R2, [R2]
    RAM:000000AA   CMP     R2, #0
    RAM:000000AC   BEQ     loc_B4
    RAM:000000AE   LDR     R2, [R6]
    RAM:000000B0   STR     R2, [R0,#8]
    RAM:000000B2   B       loc_BC
    RAM:000000B4 ; ---------------------------------------------------------------------------
    RAM:000000B4
    RAM:000000B4 loc_B4                                  ; CODE XREF: sub_A0+C↑j
    RAM:000000B4   LDR     R2, [R0,#8]
    RAM:000000B6   LSRS    R0, R0, #0x12
    RAM:000000B8   ORRS    R2, R0
    RAM:000000BA   STR     R2, [R6]
    RAM:000000BC
    RAM:000000BC loc_BC                                  ; CODE XREF: sub_A0+12↑j
    RAM:000000BC   LDR     R6, =dword_7000E9C0
    RAM:000000BE   LDR     R0, [R6]
    RAM:000000C0   MOVS    R2, #0x4000
    RAM:000000C4   ORRS    R2, R0
    RAM:000000C6   STR     R2, [R6]
    RAM:000000C8   LDR     R0, [R5,#0x10]
    RAM:000000CA   B       pop_r2_mov_pc_lr
    RAM:000000CA ; End of function sub_A0
    RAM:000000CA
    RAM:000000CC
    RAM:000000CC ; =============== S U B R O U T I N E =======================================
    RAM:000000CC
    RAM:000000CC
    RAM:000000CC sub_CC
    RAM:000000CC   MOVS    R2, #0xF000000                ; 5 37aadf42     6f54     df42 : svc #0x42 (offset 0xcc)
    RAM:000000D0   BICS    R1, R2
    RAM:000000D2   STR     R1, [R4,#0x10]
    RAM:000000D4   LDR     R1, [R4,#0x50]
    RAM:000000D6   MOVS    R2, #7
    RAM:000000D8   BICS    R1, R2
    RAM:000000DA   STR     R1, [R4,#0x50]
    RAM:000000DC   B       pop_r2_mov_pc_lr
    RAM:000000DC ; End of function sub_CC
    RAM:000000DC
    RAM:000000DE
    RAM:000000DE ; =============== S U B R O U T I N E =======================================
    RAM:000000DE
    RAM:000000DE
    RAM:000000DE sub_DE
    RAM:000000DE   LDR     R2, =dword_7000FA9C           ; 6  972df4b     12e4     df4b : svc #0x4b (offset 0xde)
    RAM:000000E0   LDR     R2, [R2]
    RAM:000000E2   LSRS    R2, R2, #8
    RAM:000000E4   LSLS    R2, R2, #1
    RAM:000000E6   LDR     R1, [R4]
    RAM:000000E8   BICS    R1, R2
    RAM:000000EA   STR     R1, [R4]
    RAM:000000EC   CMP     R0, #0
    RAM:000000EE   B       pop_r2_mov_pc_lr
    RAM:000000EE ; End of function sub_DE
    RAM:000000EE
    RAM:000000F0
    RAM:000000F0 ; =============== S U B R O U T I N E =======================================
    RAM:000000F0
    RAM:000000F0
    RAM:000000F0 sub_F0
    RAM:000000F0
    RAM:000000F0 arg_0=  0
    RAM:000000F0
    RAM:000000F0   LDR     R0, =0x400049F0               ; 7 2293df54     4526     df54 : svc #0x54 (offset 0xf0)
    RAM:000000F2   LDR     R2, [R0]
    RAM:000000F4   STR     R2, [SP,#arg_0]
    RAM:000000F6   LDR     R0, =0x40010000
    RAM:000000F8   LSRS    R2, R2, #17
    RAM:000000FA   BEQ     pop_r2_mov_pc_lr              ; if ([0x400049F0] >> 17) == 0) {
    RAM:000000FA                                         ;   r2 = [0x400049F0];
    RAM:000000FA                                         ; } else {
    RAM:000000FC   LDR     R0, =APBDEV_PMC_CNTRL_0
    RAM:000000FE   STR     R4, [R0]                      ;  write APBDEV_PMC_CNTRL
    RAM:00000100
    RAM:00000100 loc_100                                 ; CODE XREF: sub_F0:loc_100↓j
    RAM:00000100   B       loc_100                       ;  hang
    RAM:00000100 ; End of function sub_F0                ; }
    RAM:00000100
    RAM:00000102
    RAM:00000102 ; =============== S U B R O U T I N E =======================================
    RAM:00000102
    RAM:00000102
    RAM:00000102 sub_102
    RAM:00000102
    RAM:00000102 arg_0=  0
    RAM:00000102
    RAM:00000102   LDR     R2, =0x40010220               ; 8 21fadf5d     43f4     df5d : svc #0x5d (offset 0x102)
    RAM:00000104   STR     R2, [SP,#arg_0]               ; set r2 retval = [0x40010220]
    RAM:00000106   LDR     R2, [R2,#0x18]
    RAM:00000108   ADDS    R0, #0xFC
    RAM:0000010A   STR     R2, [R0,#0x1C]                ; [r0+0x118] = [0x40010220 + 0x18]
    RAM:0000010C   B       pop_r2_mov_pc_lr
    RAM:0000010C ; End of function sub_102
    RAM:0000010C
    RAM:0000010C ; ---------------------------------------------------------------------------
    RAM:0000010E   DCB    0
    RAM:0000010F   DCB    0
    RAM:00000110 off_110 DCD 0x60006410                  ; DATA XREF: sub_48+4↑r
    RAM:00000114 off_114 DCD 0x600060F8                  ; DATA XREF: sub_48+A↑r
    RAM:00000118 off_118 DCD 0x60006284                  ; DATA XREF: sub_48+10↑r
    RAM:0000011C off_11C DCD 0x60006554                  ; DATA XREF: sub_48+26↑r
    RAM:00000120 off_120 DCD 0x60006148                  ; DATA XREF: sub_48+2E↑r
    RAM:00000124 off_124 DCD 0x600066A0                  ; DATA XREF: sub_48+3A↑r
    RAM:00000128 off_128 DCD dword_7000EF14              ; DATA XREF: sub_A0+4↑r
    RAM:0000012C off_12C DCD dword_7000E5B4              ; DATA XREF: sub_A0+6↑r
    RAM:00000130 off_130 DCD dword_7000E9C0              ; DATA XREF: sub_A0:loc_BC↑r
    RAM:00000134 off_134 DCD dword_7000FA9C              ; DATA XREF: sub_DE↑r
    RAM:00000138 off_138 DCD 0x400049F0                  ; DATA XREF: sub_F0↑r
    RAM:0000013C dword_13C DCD 0x40010000                ; DATA XREF: sub_F0+6↑r
    RAM:00000140 off_140 DCD APBDEV_PMC_CNTRL_0          ; DATA XREF: sub_F0+C↑r
    RAM:00000144 off_144 DCD 0x40010220                  ; DATA XREF: sub_102↑r
    RAM:00000148 ; ---------------------------------------------------------------------------
    RAM:00000148 ; START OF FUNCTION CHUNK FOR sub_A0
    RAM:00000148
    RAM:00000148 pop_r2_mov_pc_lr                        ; CODE XREF: sub_48+42↑j
    RAM:00000148                                         ; sub_8C+6↑j ...
    RAM:00000148   POP     {R2}
    RAM:0000014A   MOV     PC, LR
    RAM:0000014A ; END OF FUNCTION CHUNK FOR sub_A0

The last 4 patches are exclusive to the Switch, while the remaining ones
are often included in most Tegra210 based devices.

#### ipatch 0

This patch configures clock enables and clock gate overrides for new
hardware.

``` c
 u32 CLK_ENB_H_SET = 0x60006328;
 u32 CLK_ENB_L_SET = 0x60006320;
 u32 CLK_ENB_U_SET = 0x60006330; 
 u32 CLK_ENB_V_SET = 0x60006440;
 u32 CLK_ENB_W_SET = 0x60006448;
 u32 CLK_ENB_X_SET = 0x60006284;
 u32 CLK_ENB_Y_SET = 0x6000629C;
 u32 LVL2_CLK_GATE_OVRA = 0x600060F8;
 u32 LVL2_CLK_GATE_OVRB = 0x600060FC;
 u32 LVL2_CLK_GATE_OVRC = 0x600063A0;
 u32 LVL2_CLK_GATE_OVRD = 0x600063A4;
 u32 LVL2_CLK_GATE_OVRE = 0x60006554;
 u32 CLK_SOURCE_VI = 0x60006148;
 u32 CLK_SOURCE_HOST1X = 0x60006180;
 u32 CLK_SOURCE_NVENC = 0x600066A0; 

 // Set all clock enables and overrides
 *(u32 *)CLK_ENB_V_SET = 0xFFFFFFFF;
 *(u32 *)CLK_ENB_W_SET = 0xFFFFFFFF;
 *(u32 *)LVL2_CLK_GATE_OVRA = 0xFFFFFFFF;
 *(u32 *)LVL2_CLK_GATE_OVRB = 0xFFFFFFFF;
 *(u32 *)CLK_ENB_X_SET = 0xFFFFFFFF;
 *(u32 *)CLK_ENB_Y_SET = 0xFFFFFFFF;
 *(u32 *)CLK_ENB_L_SET = 0xFFFFFFFF;
 *(u32 *)CLK_ENB_H_SET = 0xFFFFFFFF;
 *(u32 *)CLK_ENB_U_SET = 0xFFFFFFFF;
 *(u32 *)LVL2_CLK_GATE_OVRC = 0xFFFFFFFF;
 *(u32 *)LVL2_CLK_GATE_OVRD = 0xFFFFFFFF;
 *(u32 *)LVL2_CLK_GATE_OVRE = 0xFFFFFFFF;

 // Set VI, HOST1X and NVENC clock sources to CLK_M
 *(u32 *)CLK_SOURCE_VI = 0xA0000000;
 *(u32 *)CLK_SOURCE_HOST1X = 0xA0000000;
 *(u32 *)CLK_SOURCE_NVENC = 0xE0000000;

 /*
     Untranslated instructions:

     MOVS    R1, #0
     MOVS    R0, #0xE
 */
 
 return;
```

#### ipatch 1

This patch is a bugfix.

LP0 resume code expects APBDEV\_PMC\_SCRATCH190\_0 to be set to 0x01,
but the bootrom didn't set it.

``` c
 u32 APBDEV_PMC_SCRATCH190_0 = 0x7000EC18;
 u32 pmc_scratch190_val = *(u32 *)APBDEV_PMC_SCRATCH190_0;
 
 return (pmc_scratch190_val | 0x01);
```

#### ipatch 2

This patch adjusts USB configurations.

``` c
 u32 USB1_UTMIP_SPARE_CFG0_0 = 0x7D000834;
 u32 USB1_UTMIP_BIAS_CFG2_0 = 0x7D000850;
 
 // Increase UTMIP_HSSQUELCH_LEVEL_NEW by 0x02
 *(u32 *)USB1_UTMIP_BIAS_CFG2_0 += 0x02;

 // Clear FUSE_HS_IREF_CAP_CFG
 *(u32 *)USB1_UTMIP_SPARE_CFG0_0 = ((*(u32 *)USB1_UTMIP_SPARE_CFG0_0 & ~(0x118)) - 0x80);
 
 return;
```

#### ipatch 3

This patch pertains to XHCI IRQ clearing checks and forces a result code
to be 0.

#### ipatch 4

This patch allows backing up and restoring strapping options for
warmboot.

``` c
 u32 APBDEV_PMC_SCRATCH0_0 = 0x7000E450;
 u32 APBDEV_PMC_RST_STATUS_0 = 0x7000E5B4;
 u32 APBDEV_PMC_SEC_DISABLE8_0 = 0x7000E9C0;
 u32 APBDEV_PMC_SECURE_SCRATCH111_0 = 0x7000EF14;
 u32 APB_MISC_PP_STRAPPING_OPT_A_0 = 0x70000008; 

 u32 reset_status = *(u32 *)APBDEV_PMC_RST_STATUS_0;

 // Check for regular power on
 if (reset_status == 0)
 {    
     // Set all buttons in RCM_STRAPS and backup to PMC scratch
     *(u32 *)APBDEV_PMC_SECURE_SCRATCH111_0 = (*(u32 *)APB_MISC_PP_STRAPPING_OPT_A_0 | 0x1C00);
 }
 else
 {
     // Restore strapping options from PMC scratch
     *(u32 *)APB_MISC_PP_STRAPPING_OPT_A_0 = *(u32 *)APBDEV_PMC_SECURE_SCRATCH111_0;
 }

 // Disable write access to APBDEV_PMC_SECURE_SCRATCH111_0
 *(u32 *)APBDEV_PMC_SEC_DISABLE8_0 |= 0x4000;
 
 return *(u32 *)APBDEV_PMC_SCRATCH0_0;
```

#### ipatch 5

This patch adjusts USB configurations.

``` c
 u32 USB1_UTMIP_HSRX_CFG0_0 = 0x7D000810;
 u32 USB1_UTMIP_BIAS_CFG2_0 = 0x7D000850;

 // Clear UTMIP_IDLE_WAIT, UTMIP_ELASTIC_LIMIT and UTMIP_PCOUNT_UPDN_DIV,
 // and set UTMIP_IDLE_WAIT to 0x11 and UTMIP_ELASTIC_LIMIT to 0x10 
 *(u32 *)USB1_UTMIP_HSRX_CFG0_0 = ((*(u32 *)USB1_UTMIP_HSRX_CFG0_0 & ~(0xF8000) + 0x88000 & ~(0x7C00) + 0x4000) & ~(0xF000000));
 
 // Clear UTMIP_HSSQUELCH_LEVEL_NEW
 *(u32 *)USB1_UTMIP_BIAS_CFG2_0 &= ~(0x07);
 
 return;
```

#### ipatch 6

This patch is a factory backdoor.

It allows controlling the debug authentication configuration using a
fuse.

``` c
 u32 FUSE_DEBUG_AUTH_OVERRIDE = 0x7000FA9C;

 u32 debug_auth_override_val = *(u32 *)FUSE_DEBUG_AUTH_OVERRIDE;
 debug_auth_override_val = ((debug_auth_override_val >> 0x08) << 0x01);

 // Override debug authentication value stored in IRAM
 *(u32 *)0x400028E4 &= ~(debug_auth_override_val);

 /*
     Untranslated instructions:
 
     CMP     R0, #0
 */
 
 return;
```

#### ipatch 7

This patch is a bugfix.

It prevents overflowing IRAM (0x40010000) when copying the warmboot
binary from DRAM.

``` c
 u32 APBDEV_PMC_CNTRL_0 = 0x7000E400;
 
 u32 warmboot_header_addr = 0x400049F0;
 u32 warmboot_bin_size = *(u32 *)warmboot_bin_header_addr;
 
 // Invalid warmboot binary size
 if (warmboot_size >> 0x11)
 {
     // Assert MAIN_RST
     // 0x40004BF0 comes from R4 and the bootrom doesn't bother to change it
     *(u32 *)APBDEV_PMC_CNTRL_0 = 0x40004BF0;

     // Deadlock
     while(1);
 }
 
 /*
     Untranslated instructions:
 
     LDR     R0, =0x40010000
     LDR     R2, [warmboot_bin_header_addr]
 */

 return;
```

#### ipatch 8

This patch is a bugfix.

It sets the correct warmboot binary entrypoint address for RSA signature
verification, which would be done in DRAM instead of IRAM without this
patch.

``` c
 u32 warmboot_addr_ptr = 0x40010238;
 u32 warmboot_entry_addr_ptr = 0x40004C28;

 *(u32 *)warmboot_entry_addr_ptr = *(u32 *)warmboot_addr_ptr;

 /*
     Untranslated instructions:
 
     LDR     R2, [warmboot_addr_ptr]
 */
 
 return;
```

#### ipatches 9 and 10

These patches modify the 256-bit Secure Provisioning AES key with index
0x3A.

#### ipatch 11

This patch pertains to the [Security
Engine](Security%20Engine.md "wikilink") context restore process and
forces SE\_OPERATION\_UNK1 to be 0x01.

## Anti-downgrade

The first bootloader verifies
[FUSE\_RESERVED\_ODM7](#FUSE_RESERVED_ODM7 "wikilink") to prevent
downgrading. How many fuses are expected to be burnt depends the
device's unit type as
below.

| System version | Expected number of burnt fuses (retail) | Expected number of burnt fuses (non-retail) |
| -------------- | --------------------------------------- | ------------------------------------------- |
| 1.0.0          | 1                                       | 0                                           |
| 2.0.0-2.3.0    | 2                                       | 0                                           |
| 3.0.0          | 3                                       | 1                                           |
| 3.0.1-3.0.2    | 4                                       | 1                                           |
| 4.0.0-4.1.0    | 5                                       | 1                                           |
| 5.0.0-5.1.0    | 6                                       | 1                                           |
| 6.0.0-6.1.0    | 7                                       | 1                                           |
| 6.2.0          | 8                                       | 1                                           |
| 7.0.0-7.0.1    | 9                                       | 1                                           |

If too many fuses are burnt the bootloader will panic immediately.

If too few are burnt, the bootloader will enable fuse programming and
write the expected value to fuse indexes 0x3A and 0x3C. Afterwards, fuse
programming is disabled and the panic value 0x21 is written to
PMC\_SCRATCH200 register (0x7000EC40). Finally, the watchdog timer is
initialized and programmed to force a reset.

On a subsequent boot, after the anti-downgrade fuses are checked again,
the PMC\_RST\_STATUS register (0x7000E5B4) is checked and if set to 0x01
(watchdog reset) the PMC\_SCRATCH200 register (0x7000EC40) will be
checked for the panic value 0x21. PMC\_RST\_STATUS will only be set back
to 0 (power on reset) if the fuse count matches the new expected value,
otherwise the system will panic.
