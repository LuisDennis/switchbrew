This page describes the format of savegames contained in NAND. NAND
savegames do not use an container with the entire file encrypted.
Various areas of the saveimage is uninitialized data, resulting in
encrypted data in those areas (like 3DS did).

## Main header

The header is 0x4000 bytes long.

There are 2 headers stored at 0x0 and 0x4000, presumably for commit and
rollback purposes.

| Image offset | Length | Description                   |
| ------------ | ------ | ----------------------------- |
| 0x000        | 0x100  | AES-CMAC header               |
| 0x100        | 0x200  | DISF header                   |
| 0x300        | 0x44   | Duplex header                 |
| 0x344        | 0xC4   | Integrity verification header |
| 0x408        | 0x200  | Journal header                |
| 0x608        | 0x48   | Save header                   |
| 0x650        | 0x40   | Main data remap header        |
| 0x690        | 0x40   | Meta data remap header        |
| 0x6D0        | 0x8    | Unknown                       |
| 0x6D8        | 0x200  | Extra data A                  |
| 0x8D8        | 0x200  | Extra data B                  |
| 0xAD8        | 0x3528 | Additional storage            |

The additional storage at the end of the header is used to store any
extra header data. This data's structure is determined by offsets stored
in the main part of the header.

### AES CMAC header

| Image offset | Length | Description                            |
| ------------ | ------ | -------------------------------------- |
| 0x00         | 0x10   | AES-CMAC over DISF header (size 0x200) |
| 0x10         | 0xF0   | Zero padding                           |

The final CMAC key used for this is generated using GenerateAesKek with
a kek source and the device key, along with and LoadAesKey and a set key
seed.

#### DISF

  - This is located @ 0x100 in the image, following the CMAC
header.

| Start | Length | Description                                                                 |
| ----- | ------ | --------------------------------------------------------------------------- |
| 0x000 | 4      | Magic ("DISF")                                                              |
| 0x004 | 4      | Magic Number (0x40000)                                                      |
| 0x008 | 32     | Hash of start of DPFS to end of 0x4000 block (usually/always? 0x300-0x3FFF) |
| 0x028 | 8      | Primary Partition Table Offset                                              |
| 0x030 | 8      | Primary Partition Table Size                                                |
| 0x038 | 8      | Secondary Partition Table Offset                                            |
| 0x040 | 8      | Secondary Partition Table Size                                              |
| 0x048 | 8      | Save Partition Offset                                                       |
| 0x050 | 8      | Save Partition Size                                                         |
| 0x258 |        | End                                                                         |

#### DPFS

  - This is located @ 0x300 in the image, following DISF.
  - Block sizes are log2

| Start | Length | Description            |
| ----- | ------ | ---------------------- |
| 0x00  | 4      | Magic ("DPFS")         |
| 0x04  | 4      | Magic Number (0x10000) |
| 0x08  | 8      | Offset 0               |
| 0x10  | 8      | Size 0                 |
| 0x18  | 4      | Block Size 0, in log 2 |
| 0x1C  | 8      | Offset 1               |
| 0x24  | 8      | Size 1                 |
| 0x2C  | 4      | Block Size 1, in log 2 |
| 0x30  | 8      | Offset 2               |
| 0x38  | 8      | Size 2                 |
| 0x40  | 4      | Block Size 2, in log 2 |
|       |        |                        |

#### IVFC

  - Generally follows DPFS, similar to 3DS.

| Start | Length | Description                  |
| ----- | ------ | ---------------------------- |
| 0x00  | 4      | Magic ("IVFC")               |
| 0x04  | 4      | Magic Number (0x20000)       |
| 0x08  | 8      | Master hash size?            |
| 0x10  | 8      | Level 1 offset               |
| 0x18  | 8      | Level 1 size                 |
| 0x20  | 4      | Level 1 block size, in log2  |
| 0x24  | 4      | Reserved                     |
| 0x28  | 8      | Level 2 offset               |
| 0x30  | 8      | Level 2 size                 |
| 0x38  | 4      | Level 2 block size, in log2. |
| 0x3C  | 4      | Reserved                     |
| 0x40  | 8      | Level 3 offset               |
| 0x48  | 8      | Level 3 size                 |
| 0x50  | 4      | Level 3 block size, in log2. |
| 0x54  | 4      | Reserved                     |
| 0x58  | 8      | Level 4 offset               |
| 0x60  | 8      | Level 4 size                 |
| 0x68  | 4      | Level 4 block size, in log2. |
| 0x6C  | 4      | Reserved                     |
| 0x70  | 48     | Unknown, reserved?           |
| 0xA0  | 32     | Hash                         |
|       |        |                              |

#### JNGL

  - Generally follows IVFC

| Start | Length | Description            |
| ----- | ------ | ---------------------- |
| 0x00  | 4      | Magic ("JNGL")         |
| 0x04  | 4      | Magic Number (0x10000) |
| 0x08  | 8      | Savedata Size          |
| 0x10  | 8      | Unknown, Size          |
| 0x18  | 8      | Savedata Blocksize?    |
| 0x20  | 4      | Unknown                |
| 0x24  | 4      | Unknown                |
| 0x28  | 8      | Unknown                |
| 0x30  | 464    | Padding?               |
|       |        |                        |

#### SAVE

  - Generally follows JNGL, structure is different from 3DS.

| Start | Length | Description            |
| ----- | ------ | ---------------------- |
| 0x00  | 4      | Magic ("SAVE")         |
| 0x04  | 4      | Magic Number (0x60000) |
| 0x08  | 8      | Unknown, number        |
| 0x10  | 8      | Unknown, block size    |
| 0x18  | 8      | Unknown, block size    |
| 0x20  | 8      | Unknown                |
|       |        |                        |

#### RMAP

  - There are generally two RMAP blocks in sequence.

| Start | Length | Description            |
| ----- | ------ | ---------------------- |
| 0x00  | 4      | Magic ("RMAP")         |
| 0x04  | 4      | Magic Number (0x10000) |
|       |        |                        |

## Files

### File Offset Table

  - Indexes 0 and 1 are reserved to point towards the folder and file
    tables.

#### File Offset Table Entry

| Start | Length | Description            |
| ----- | ------ | ---------------------- |
| 0x00  | 3      | Data offset, in blocks |
| 0x03  | 1      | Unknown, 80            |
| 0x04  | 4      | Unknown, 0             |

### File/Folder Table Entry

  - The root file/folder index is generally 2

| Start | Length | Description                                       |
| ----- | ------ | ------------------------------------------------- |
| 0x00  | 4      | Parent Folder Index                               |
| 0x04  | 64     | Filename                                          |
| 0x44  | 4      | File/Folder Index?                                |
| 0x48  | 4      | File offset index in offset table, 0 for folders  |
| 0x4c  | 8      | File size, or number of files for folders         |
| 0x54  | 8      | Unknown                                           |
| 0x5c  | 4      | Next File Index, same as folder index for folders |
|       |        |                                                   |
