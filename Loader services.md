# ldr:dmnt

This is
"nn::ldr::detail::IDebugMonitorInterface".

| Cmd | Name                                                                                                                       |
| --- | -------------------------------------------------------------------------------------------------------------------------- |
| 0   | [AddProcessToDebugLaunchQueue](Loader%20services#AddProcessToDebugLaunchQueue.md##AddProcessToDebugLaunchQueue "wikilink") |
| 1   | [ClearDebugLaunchQueue](Loader%20services#ClearDebugLaunchQueue.md##ClearDebugLaunchQueue "wikilink")                      |
| 2   | [GetNsoInfos](Loader%20services#GetNsoInfos.md##GetNsoInfos "wikilink")                                                    |

## AddProcessToDebugLaunchQueue

Same as
[AddProcessToLaunchQueue](Loader%20services#AddProcessToLaunchQueue.md##AddProcessToLaunchQueue "wikilink")
but for processes marked as debug.

## ClearDebugLaunchQueue

Same as
[ClearLaunchQueue](Loader%20services#ClearLaunchQueue.md##ClearLaunchQueue "wikilink").

## GetNsoInfos

Takes in a u64 ProcessID, and a C descriptor. Returns the number of
NsoInfos copied to output.

NsoInfo has the following layout:

| Offset | Size | Description                       |
| ------ | ---- | --------------------------------- |
| 0x0    | 0x20 | "Build ID", from NSO header+0x40. |
| 0x20   | 0x8  | Mapped address for this NSO       |
| 0x28   | 0x8  | Mapped size for this NSO          |
|        |      |                                   |

# ldr:pm

This is "nn::ldr::detail::IProcessManagerInterface".

| Cmd | Name                                             |
| --- | ------------------------------------------------ |
| 0   | CreateProcess                                    |
| 1   | [\#GetProgramInfo](#GetProgramInfo "wikilink")   |
| 2   | [\#RegisterTitle](#RegisterTitle "wikilink")     |
| 3   | [\#UnregisterTitle](#UnregisterTitle "wikilink") |

## GetProgramInfo

Takes a TitleId + StorageId, parses the NPDM, and writes output to a C
descriptor buffer as
follows:

| Offset   | Size     | Description                                                                                                    |
| -------- | -------- | -------------------------------------------------------------------------------------------------------------- |
| 0x0      | 0x1      | MainThreadPrio. Arg1 to svcStartProcess                                                                        |
| 0x1      | 0x1      | DefaultCpuId. Arg2 to svcStartProcess                                                                          |
| 0x2      | 0x1      | ApplicationType, see [here](Process%20Manager%20services.md "wikilink").                                       |
| 0x3      | 0x1      | Padding                                                                                                        |
| 0x4      | 0x4      | MainThreadStackSize. Arg3 to svcStartProcess                                                                   |
| 0x8      | 0x8      | TitleIdRange\_Min                                                                                              |
| 0x10     | 0x4      | ACID [Service Access Control](NPDM#Service%20Access%20Control.md##Service_Access_Control "wikilink") list size |
| 0x14     | 0x4      | ACI0 [Service Access Control](NPDM#Service%20Access%20Control.md##Service_Access_Control "wikilink") list size |
| 0x18     | 0x4      | ACID [FS Access Control](NPDM#FS%20Access%20Control.md##FS_Access_Control "wikilink") buffer size              |
| 0x1C     | 0x4      | ACI0 [FS Access Control](NPDM#FS%20Access%20Control.md##FS_Access_Control "wikilink") buffer size              |
| 0x20     | <Varies> | ACID [Service Access Control](NPDM#Service%20Access%20Control.md##Service_Access_Control "wikilink") list      |
| <Varies> | <Varies> | ACI0 [Service Access Control](NPDM#Service%20Access%20Control.md##Service_Access_Control "wikilink") list      |
| <Varies> | <Varies> | ACID [FS Access Control](NPDM#FS%20Access%20Control.md##FS_Access_Control "wikilink") buffer                   |
| <Varies> | <Varies> | ACI0 [FS Access Control](NPDM#FS%20Access%20Control.md##FS_Access_Control "wikilink")                          |

## RegisterTitle

Takes a TitleId + StorageId, returns an index.

## UnregisterTitle

Takes the index from [\#RegisterTitle](#RegisterTitle "wikilink").

# ldr:shel

This is
"nn::ldr::detail::IShellInterface".

| Cmd | Name                                                             |
| --- | ---------------------------------------------------------------- |
| 0   | [\#AddProcessToLaunchQueue](#AddProcessToLaunchQueue "wikilink") |
| 1   | [\#ClearLaunchQueue](#ClearLaunchQueue "wikilink")               |

## AddProcessToLaunchQueue

Takes a type-0x19 input buffer with launch arguments (as string), an u32
(size of arguments string), and an input title-id.

Loads a process for the specified title-id and passes along the supplied
arguments. Loaded processes are kept in a queue waiting for PM to launch
them. The maximum number of waiting processes in this list is 10.

## ClearLaunchQueue

Clears the loaded processes waiting queue.

# ldr:ro

\[1.0.0-2.3.0\] This is "nn::ldr::detail::IRoInterface"

\[3.0.0+\] This is
"nn::ro::detail::IRoInterface".

| Cmd | Name                                                                                    |
| --- | --------------------------------------------------------------------------------------- |
| 0   | [\#LoadNro](#LoadNro "wikilink")                                                        |
| 1   | UnloadNro                                                                               |
| 2   | [\#LoadNrr](#LoadNrr "wikilink")                                                        |
| 3   | UnloadNrr                                                                               |
| 4   | [\#Initialize](#Initialize "wikilink")                                                  |
| 10  | \[7.0.0+\] ? (Takes a total of 0x18-bytes of input, an input handle and PID, no output) |

## LoadNro

| Word | Value                    |
| ---- | ------------------------ |
| 0    | 0x00000004               |
| 1    | 0x80000012               |
| 2    | 0x00000001               |
| 0-1  | Pid                      |
| 0    | "SCFI"                   |
| 1    | 0x00000000               |
| 2    | Always 0.                |
| 3    | Nro heap address         |
| 4    | Nro size                 |
| 5    | Bss backing heap address |
| 6    | Bss size                 |

## LoadNrr

| Word | Value       |
| ---- | ----------- |
| 0    | 0x00000004  |
| 1    | 0x8000000E  |
| 2    | 0x00000001  |
|      |             |
| 0-1  | Pid         |
| 0    | "SFCI"      |
| 1    | 0x00000002  |
| 2    | Always 0.   |
| 3    | Nrr address |
| 4    | Nrr size    |

## Initialize

| Word | Value                       |
| ---- | --------------------------- |
| 0    | 0x00000004                  |
| 1    | 0x8000000A                  |
| 2    | 0x00000003                  |
| 0-1  | Pid                         |
| 2    | Process handle (0xFFFF8001) |
| 0    | "SFCI"                      |
| 1    | 0x00000004                  |
| 2    | Always 0.                   |

[Category:Services](Category:Services "wikilink")
