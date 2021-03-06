Tickets are a format used to store an encrypted title key. The format
has been updated again since 3DS.

## Structure

| Offset | Size  | Description    |
| ------ | ----- | -------------- |
| 0x000  | Y     | Signature data |
| Y      | 0x2C0 | Ticket data    |

Y denotes the total size of the "signature data" section and depends on
the signature type.

### Signature data

| Offset  | Size | Description                                       |
| ------- | ---- | ------------------------------------------------- |
| 0x0     | 0x4  | Signature type                                    |
| 0x4     | X    | Signature                                         |
| 0x4 + X |      | Padding to align the signature data to 0x40 bytes |

#### Signature type

| Value    | Signature method | Signature size | Padding size |
| -------- | ---------------- | -------------- | ------------ |
| 0x010000 | RSA\_4096 SHA1   | 0x200          | 0x3C         |
| 0x010001 | RSA\_2048 SHA1   | 0x100          | 0x3C         |
| 0x010002 | ECDSA SHA1       | 0x3C           | 0x40         |
| 0x010003 | RSA\_4096 SHA256 | 0x200          | 0x3C         |
| 0x010004 | RSA\_2048 SHA256 | 0x100          | 0x3C         |
| 0x010005 | ECDSA SHA256     | 0x3C           | 0x40         |

The hash for the signature is calculated over the ticket data.

### Ticket data

| Offset | Size  | Description         |
| ------ | ----- | ------------------- |
| 0x0    | 0x40  | Issuer              |
| 0x40   | 0x100 | Title key block     |
| 0x140  | 0x1   | Unknown             |
| 0x141  | 0x1   | Title key type      |
| 0x142  | 0x3   | Unknown             |
| 0x145  | 0x1   | Master key revision |
| 0x146  | 0xA   | Unknown             |
| 0x150  | 0x8   | Ticket ID           |
| 0x158  | 0x8   | Device ID           |
| 0x160  | 0x10  | Rights ID           |
| 0x170  | 0x4   | Account ID          |
| 0x174  | 0xC   | Unknown             |
| 0x180  | 0x140 | Unknown             |

The title key can be stored as a 16-byte block when tickets are "common"
\[2.0.0+\] with title key type 0, or as a "personalized" RSA-2048
message when title key type is 1. The latter is used for titles
requiring stronger licensing (applications, add-on content), while the
former (old) method is used for patches.

When RSA is used, this uses an SPL key handle that is initialized with
the console-unique RSA-2048 ticket
key.

## Certificate chain

| Certificate | Signature type | Retail cert name | Debug cert name | Description                                                                         |
| ----------- | -------------- | ---------------- | --------------- | ----------------------------------------------------------------------------------- |
| Ticket      | RSA-2048       | XS00000021       | ?               | Used to verify ticket signatures using RSA title key block ("personalized" tickets) |
| Ticket      | RSA-2048       | XS00000020       | ?               | Used to verify ticket signatures using AES title key block                          |
| CA          | RSA-4096       | CA00000003       | CA00000004      | Used to verify the ticket certificate                                               |

The CA certificate is issued by 'Root', the public key for which is
stored in ES.
