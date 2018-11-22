## BootROM

The bootrom initializes two keyslots in the hardware engine:

  - the SBK (Secure Boot Key) in keyslot 14
  - the SSK (Secure Storage Key) in keyslot 15.

Reads from both of these keyslots are disabled by the bootROM. The SBK
is stored in
[FUSE\_PRIVATE\_KEY](Fuses#FUSE%20PRIVATE%20KEY.md##FUSE_PRIVATE_KEY "wikilink"),
which are locked to read out only FFs after the bootrom finishes.

SBK is **unique** per console, and not shared among consoles as
originally believed.

The SSK is derived on boot via the SBK, the 32-bit console-unique
"Device Key", and hardware information stored in fuses.

Pseudocode for the derivation is as
follows:

` void generateSSK() {`  
`     char keyBuffer[0x10]; // Used to store keydata`  
`     uint hwInfoBuffer[4]; // Used to store info about hardware from fuses`  
`     uint deviceKey = getDeviceKey(); // Reads 32-bit device key from FUSE_PRIVATE_KEY4.`  
`     for (int i = 0; i < 4; i++) { // Keybuffer = deviceKey || deviceKey || deviceKey || deviceKey`  
`         ((uint *)keyBuffer)[i] = deviceKey;`  
`     }`  
`     `  
`     encryptWithSBK(keyBuffer); // keyBuffer = AES-ECB(SBK, deviceKey || {...})`  
`     `  
`     // Set up Hardware info buffer`  
`     uint vendor_code = *((uint *)0x7000FA00) & 0x0000000F; // FUSE_VENDOR_CODE`  
`     uint fab_code    = *((uint *)0x7000FA04) & 0x0000003F; // FUSE_FAB_CODE`  
`     uint lot_code_0  = *((uint *)0x7000FA08) & 0xFFFFFFFF; // FUSE_LOT_CODE_0`  
`     uint lot_code_1  = *((uint *)0x7000FA0C) & 0x0FFFFFFF; // FUSE_LOT_CODE_1`  
`     uint wafer_id    = *((uint *)0x7000FA10) & 0x0000003F; // FUSE_WAFER_ID`  
`     uint x_coord     = *((uint *)0x7000FA14) & 0x000001FF; // FUSE_X_COORDINATE`  
`     uint y_coord     = *((uint *)0x7000FA18) & 0x000001FF; // FUSE_Y_COORDINATE`  
`     uint unk_hw_fuse = *((uint *)0x7000FA20) & 0x0000003F; // Unknown cached fuse.`  
`     `  
`     // HARDWARE_INFO_BUFFER = unk_hw_fuse || Y_COORD || X_COORD || WAFER_ID || LOT_CODE || FAB_CODE || VENDOR_ID`  
`     hwInfoBuffer[0] = (lot_code_1 << 30) | (wafer_id << 24) | (x_coord << 15) | (y_coord << 6) | unk_hw_fuse;`  
`     hwInfoBuffer[1] = (lot_code_0 << 26) | (lot_code_1 >> 2);`  
`     hwInfoBuffer[2] = (fab_code << 26) | (lot_code_0 >> 6);`  
`     hwInfoBuffer[3] = vendor_code;`  
`     `  
`     for (int i = 0; i < 0x10; i++) { // keyBuffer = XOR(AES-ECB(SBK, deviceKey || {...}), HARDWARE_INFO_BUFFER)`  
`         keyBuffer[i] ^= ((char *)hwInfoBuffer)[i];`  
`     }`  
`     `  
`     encryptWithSBK(keyBuffer); // keyBuffer = AES-ECB(SBK, XOR(AES-ECB(SBK, deviceKey || {...}), HARDWARE_INFO_BUFFER))`  
`     `  
`     setKeyslot(KEYSLOT_SSK, keyBuffer); // SSK = keyBuffer.`  
` }`  

## Falcon coprocessor

The falcon processor (TSEC) generates a special console-unique key (that
will be referred to as the "tsec key").

This is presumably using data stored in fuses that only microcode
authenticated by NVidia has access
to.

## Package1ldr

### Key table during package1ldr

| Keyslot | Name             | Set by                                                         | Per-console | Per-firmware |
| ------- | ---------------- | -------------------------------------------------------------- | ----------- | ------------ |
| 11      | Package1Key      | [Package1ldr](Package1#Package1ldr.md##Package1ldr "wikilink") | No          | Yes          |
| 14      | SecureBootKey    | Bootrom                                                        | Yes         | No           |
| 15      | SecureStorageKey | Bootrom                                                        | Yes         | No           |

### \[1.0.0-3.0.2\] Key table after package1ldr

| Keyslot | Name          | Set by                                                         | Per-console | Per-firmware             |
| ------- | ------------- | -------------------------------------------------------------- | ----------- | ------------------------ |
| 12      | MasterKey     | [Package1ldr](Package1#Package1ldr.md##Package1ldr "wikilink") | No          | Yes, on security updates |
| 13      | PerConsoleKey | [Package1ldr](Package1#Package1ldr.md##Package1ldr "wikilink") | Yes         | No                       |

### \[4.0.0\]+ Key table after package1ldr (Secure Monitor boot)

| Keyslot | Name                                             | Set by                                                         | Per-console | Per-firmware             |
| ------- | ------------------------------------------------ | -------------------------------------------------------------- | ----------- | ------------------------ |
| 12      | MasterKey                                        | [Package1ldr](Package1#Package1ldr.md##Package1ldr "wikilink") | No          | Yes, on security updates |
| 13      | PerConsoleKeyForFirmwareSpecificPerConsoleKeyGen | [Package1ldr](Package1#Package1ldr.md##Package1ldr "wikilink") | Yes         | No                       |
| 14      | StaticKeyForFirmwareSpecificPerConsoleKeyGen     | [Package1ldr](Package1#Package1ldr.md##Package1ldr "wikilink") | No          | Yes, on security updates |
| 15      | PerConsoleKey                                    | [Package1ldr](Package1#Package1ldr.md##Package1ldr "wikilink") | Yes         | No                       |

### \[4.0.0\]+ Key table after package1ldr (Secure Monitor runtime)

| Keyslot | Name                          | Set by                                                         | Per-console | Per-firmware             |
| ------- | ----------------------------- | -------------------------------------------------------------- | ----------- | ------------------------ |
| 12      | MasterKey                     | [Package1ldr](Package1#Package1ldr.md##Package1ldr "wikilink") | No          | Yes, on security updates |
| 13      | FirmwareSpecificPerConsoleKey | Secure Monitor init                                            | Yes         | Yes, on security updates |
| 15      | PerConsoleKey                 | [Package1ldr](Package1#Package1ldr.md##Package1ldr "wikilink") | Yes         | No                       |

### Key generation

Note: aes\_unwrap(wrapped\_key, wrap\_key) is just another name for a
single AES-128 block decryption.

If bit0 of 0x7000FB94 is clear, it will initialize keys like this
(probably used for internal development units
only):

` // Final keys:`  
` package1_key    /* slot11 */ = aes_unwrap(f5b1eadb.., sbk)`  
` master_key      /* slot12 */ = aes_unwrap(bct->pubkey[0] == 0x11 ? simpleseed_dev0 : simpleseed_dev1, aes_unwrap(5ff9c2d9.., sbk))`  
` per_console_key /* slot13 */ = aes_unwrap(4f025f0e..., aes_unwrap(6e4a9592.., ssk))`

\[4.0.0+\] Above method was removed.

Normal key generation looks like this on
1.0.0/2.0.0:

` keyblob_key /* slot13 */ = aes_unwrap(aes_unwrap(wrapped_keyblob_key, tsec_key /* slot13 */), sbk /* slot14 */)`  
` cmac_key    /* slot11 */ = aes_unwrap(59c7fb6f.., keyblob_key)`  
` `  
` if aes_cmac(buf=keyblob+0x10, len=0xA0, cmac_key) != keyblob[0:0x10]:`  
`   panic()`  
` `  
` aes_ctr_decrypt(buf=keyblob+0x20, len=0x90, iv=keyblob+0x10 key=keyblob_key)`  
` `  
` // Final keys:`  
` package1_key    /* slot11 */ = keyblob[0x80:0x90]`  
` master_key      /* slot12 */ = aes_unwrap(bct->pubkey[0] == 0x4f ? normalseed_dev : normalseed_retail, keyblob+0x20)`  
` per_console_key /* slot13 */ = aes_unwrap(4f025f0e.., keyblob_key)`

.. and on 3.0.0, they moved keyslots around a little to generate the
same per-console key as
1.0.0:

` old_keyblob_key /* slot10 */ = aes_unwrap(aes_unwrap(df206f59.., tsec_key /* slot13 */), sbk /* slot14 */)`  
` keyblob_key     /* slot13 */ = aes_unwrap(aes_unwrap(wrapped_keyblob_key, tsec_key /* slot13 */), sbk /* slot14 */)`  
` cmac_key        /* slot11 */ = aes_unwrap(59c7fb6f.., keyblob_key)`  
` `  
` if aes_cmac(buf=keyblob+0x10, len=0xA0, cmac_key) != keyblob[0:0x10]:`  
`   panic()`  
` `  
` aes_ctr_decrypt(buf=keyblob+0x20, len=0x90, iv=keyblob+0x10 key=keyblob_key)`  
` `  
` // Final keys:`  
` package1_key    /* slot11 */ = keyblob[0x80:0x90]`  
` master_key      /* slot12 */ = aes_unwrap(bct->pubkey[0] == 0x4f ? normalseed_dev : normalseed_retail, keyblob+0x20)`  
` per_console_key /* slot13 */ = aes_unwrap(4f025f0e.., old_keyblob_key)`

.. and on 4.0.0 it was further moved
around:

` old_keyblob_key /* slot15 */ = aes_unwrap(aes_unwrap(df206f59.., tsec_key /* slot13 */), sbk /* slot14 */)`  
` keyblob_key     /* slot13 */ = aes_unwrap(aes_unwrap(wrapped_keyblob_key, tsec_key /* slot13 */), sbk /* slot14 */)`  
` cmac_key        /* slot11 */ = aes_unwrap(59c7fb6f.., keyblob_key)`  
` `  
` if aes_cmac(buf=keyblob+0x10, len=0xA0, cmac_key) != keyblob[0:0x10]:`  
`   panic()`  
` `  
` aes_ctr_decrypt(buf=keyblob+0x20, len=0x90, iv=keyblob+0x10 key=keyblob_key)`  
` `  
` // Final keys:`  
` package1_key        /* slot11 */ = keyblob[0x80:0x90]`  
` master_key          /* slot12 */ = aes_unwrap(normalseed_retail, keyblob+0x20)`  
` new_master_key      /* slot14 */ = aes_unwrap(2dc1f48d.., keyblob+0x20)`  
` new_per_console_key /* slot13 */ = aes_unwrap(0c9109db.., old_keyblob_key)`  
` per_console_key     /* slot15 */ = aes_unwrap(4f025f0e.., old_keyblob_key)`

SBK and SSK keyslots are cleared after keys have been generated.

See table above for which keys are console unique.

The key used to verify a keyblob's MAC is not the keyblob key but a key
derived from it; this is likely part of an attempt to mitigate
side-channel attacks as the MAC is an alterable part of the keyblob.

The bootloader only stores the hardcoded constants for the keyblob used
in the current revision. Nintendo are withholding all the future
hardcoded constants.

This means that if you have an attack on the bootloader, you need to
re-preform it every time they move to a new keyblob.

Dumping the SBK and TSEC key of any single system should be enough to
derive all key material on the system.

The key-derivation is described in more detail
[here](Package1#Key%20generation.md##Key_generation "wikilink").

#### Keyblob

There are 32 keyblobs written to NAND at factory, with each keyblob
encrypted with a console-unique key derived from the console's SBK, the
console's tsec key, and a constant specific to each keyblob.

Despite being encrypted with console unique keys, though, the decrypted
keyblob contents are shared for all
consoles.

#### Seeds

` normalseed_retail = d8a2410a...`  
` `  
` [1.0.0] wrapped_keyblob_key = df206f59...`  
` [1.0.0] simpleseed_dev0   = aff11423...`  
` [1.0.0] simpleseed_dev1   = 5e177ee1...`  
` [1.0.0] normalseed_dev    = 0542a0fd...`  
` `  
` [3.0.0] wrapped_keyblob_key = 0c25615d...  `  
` [3.0.0] simpleseed_dev0   = de00216a...`  
` [3.0.0] simpleseed_dev1   = 2db7c0a1...`  
` [3.0.0] normalseed_dev    = 678c5a03...`  
` `  
` [3.0.1] wrapped_keyblob_key = 337685ee...  `  
` [3.0.1] simpleseed_dev0   = e045f5ba...`  
` [3.0.1] simpleseed_dev1   = 84d92e0d...`  
` [3.0.1] normalseed_dev    = cd88155b...`  
` `  
` [4.0.0] wrapped_keyblob_key = 2d1f4880...`

#### Table of used keyblobs

| System version | Used keyblob | Used master static key encryption key in keyblob |
| -------------- | ------------ | ------------------------------------------------ |
| 1.0.0-2.3.0    | 1            | 1                                                |
| 3.0.0          | 2            | 1                                                |
| 3.0.1-3.0.2    | 3            | 1                                                |
| 4.0.0-4.1.0    | 4            | 1                                                |
| 5.0.0-5.1.0    | 5            | 1                                                |
| 6.0.0-6.1.0    | 6            | 1                                                |
| 6.2.0          | 7            | 1                                                |

## Secure Monitor Init

On all versions, the key to decrypt [Package2](Package2.md "wikilink")
is generated by decrypting a constant seed with the master key. The key
is erased after use.

Additionally, starting from 4.0.0, the Secure Monitor init will decrypt
another constant seed successively with a special per console key and a
special static key passed by package1loader, to generate the firmware
specific per-console key. The operation will erase these special keys
passed by package1loader.

## Secure Monitor

The secure monitor performs some runtime cryptographic operations. See
[SMC](SMC.md "wikilink") for what operations it provides.
