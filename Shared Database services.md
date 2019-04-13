# pl:u

This is
"nn::pl::detail::ISharedFontManager".

| Cmd | Name                                                                           |
| --- | ------------------------------------------------------------------------------ |
| 0   | [\#RequestLoad](#RequestLoad "wikilink")                                       |
| 1   | [\#GetLoadState](#GetLoadState "wikilink")                                     |
| 2   | [\#GetSize](#GetSize "wikilink")                                               |
| 3   | [\#GetSharedMemoryAddressOffset](#GetSharedMemoryAddressOffset "wikilink")     |
| 4   | [\#GetSharedMemoryNativeHandle](#GetSharedMemoryNativeHandle "wikilink")       |
| 5   | [\#GetSharedFontInOrderOfPriority](#GetSharedFontInOrderOfPriority "wikilink") |

## RequestLoad

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), no
output.

## GetLoadState

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), returns
the [\#LoadState](#LoadState "wikilink") (uint32).

### LoadState

| Value | Description |
| ----- | ----------- |
| 0x00  | Loading     |
| 0x01  | Loaded      |

## GetSize

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), returns
the Font Size (uint32).

## GetSharedMemoryAddressOffset

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), returns
the offset (uint32) to the Font Address.

## GetSharedMemoryNativeHandle

No input, returns an output SharedMemory handle.

User-processes map this SharedMemory with size=0x1100000 and
permissions=R--.

Font data is TTF, located at the offset returned by
[\#GetSharedMemoryAddressOffset](#GetSharedMemoryAddressOffset "wikilink").

## GetSharedFontInOrderOfPriority

Takes an input u64
[LanguageCode](Settings%20services#LanguageCode.md##LanguageCode "wikilink")
and 3 type-0x6 output buffers, returns an output u8 and u32. The u8 is a
bool to specify if the fonts are loaded or not and the u32 is the font
count. The first buffer contains a list of [Shared font
types](#SharedFontType "wikilink"), the second buffer contains the font
offsets and the final buffer contains the font sizes. The buffers are an
array of u32s which specify information about a specific font.
Buffer1\[n\] is related to Buffer2\[n\] and Buffer3\[n\]. Example: Font
index 0s offset is at Buffer2\[0\], size is at Buffer3\[0\]. The fonts
are relative to the shared memory created by
[\#GetSharedMemoryNativeHandle](#GetSharedMemoryNativeHandle "wikilink")

## SharedFontType

| Value | Description                     |
| ----- | ------------------------------- |
| 0x00  | Japan, US and Europe (Standard) |
| 0x01  | Chinese Simplified              |
| 0x02  | Extended Chinese Simplified     |
| 0x03  | Chinese Traditional             |
| 0x04  | Korean (Hangul)                 |
| 0x05  | Nintendo Extended               |

  - Nintendo Extended: Contains Nintendo-specific characters, including
    HID buttons, HID controller styles, applet icons, Wii(U) icons, etc.

# mii:u, mii:e

This is "nn::mii::detail::IStaticService".

| Cmd | Name               |
| --- | ------------------ |
| 0   | GetDatabaseService |

## IDatabaseService

This is "nn::mii::detail::IDatabaseService".

| Cmd | Name                           |
| --- | ------------------------------ |
| 0   | IsUpdated                      |
| 1   | IsFullDatabase                 |
| 2   | GetCount                       |
| 3   | Get                            |
| 4   | Get1                           |
| 5   | UpdateLatest                   |
| 6   | BuildRandom                    |
| 7   | BuildDefault                   |
| 8   | Get2                           |
| 9   | Get3                           |
| 10  | UpdateLatest1                  |
| 11  | FindIndex                      |
| 12  | Move                           |
| 13  | AddOrReplace                   |
| 14  | Delete                         |
| 15  | DestroyFile                    |
| 16  | DeleteFile                     |
| 17  | Format                         |
| 18  | Import                         |
| 19  | Export                         |
| 20  | IsBrokenDatabaseWithClearFlag  |
| 21  | GetIndex                       |
| 22  | \[5.0.0+\] SetInterfaceVersion |
| 23  | \[5.0.0+\] Convert             |
| 24  | \[7.0.0+\]                     |
| 25  | \[7.0.0+\]                     |

# miiimg

This is "nn::mii::detail::IImageDatabaseService".

| Cmd | Name             |
| --- | ---------------- |
| 0   | Initialize       |
| 10  | Reload           |
| 11  | GetCount         |
| 12  | IsEmpty          |
| 13  | IsFull           |
| 14  | GetAttribute     |
| 15  | LoadImage        |
| 16  | AddOrUpdateImage |
| 17  | DeleteImages     |
| 100 | DeleteFile       |
| 101 | DestroyFile      |
| 102 | ImportFile       |
| 103 | ExportFile       |
| 104 | ForceInitialize  |

# pdm:ntfy

This is "nn::pdm::detail::INotifyService".

| Cmd | Name       |
| --- | ---------- |
| 0   |            |
| 2   |            |
| 3   |            |
| 4   |            |
| 5   |            |
| 6   |            |
| 7   |            |
| 8   | \[6.0.0+\] |

# pdm:qry

This is "nn::pdm::detail::IQueryService".

| Cmd               | Name       |
| ----------------- | ---------- |
| 0                 |            |
| \[1.0.0-6.2.0\] 1 |            |
| \[1.0.0-6.2.0\] 2 |            |
| \[1.0.0-6.2.0\] 3 |            |
| 4                 |            |
| 5                 |            |
| \[1.0.0-6.2.0\] 6 |            |
| 7                 |            |
| 8                 |            |
| 9                 |            |
| 10                |            |
| 11                |            |
| 12                |            |
| 13                |            |
| 14                | \[6.0.0+\] |
| 15                | \[6.0.0+\] |
| 16                | \[6.0.0+\] |

# avm

This is "nn::avm::srv::IAvmService".

This was added with
\[6.0.0+\].

| Cmd  | Name                                                                             |
| ---- | -------------------------------------------------------------------------------- |
| 100  |                                                                                  |
| 101  |                                                                                  |
| 102  |                                                                                  |
| 103  | No input, returns an [\#IVersionListImporter](#IVersionListImporter "wikilink"). |
| 200  |                                                                                  |
| 202  |                                                                                  |
| 1000 |                                                                                  |
| 1001 |                                                                                  |
| 1002 |                                                                                  |

## IVersionListImporter

This is "nn::avm::srv::IVersionListImporter".

This was added with \[6.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |

[Category:Services](Category:Services "wikilink")
