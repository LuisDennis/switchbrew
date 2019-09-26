The Switch uses a customized NVIDIA driver.

# nvdrv, nvdrv:a, nvdrv:s, nvdrv:t

This is "nns::nvdrv::INvDrvServices".

Main NVIDIA driver service.

Each service is used by:

  - "nvdrv": regular applications
  - "nvdrv:a": applets
  - "nvdrv:s": sysmodules
  - "nvdrv:t": factory titles

| Cmd | Name                                                              |
| --- | ----------------------------------------------------------------- |
| 0   | [\#Open](#Open "wikilink")                                        |
| 1   | [\#Ioctl](#Ioctl "wikilink")                                      |
| 2   | [\#Close](#Close "wikilink")                                      |
| 3   | [\#Initialize](#Initialize "wikilink")                            |
| 4   | [\#QueryEvent](#QueryEvent "wikilink")                            |
| 5   | [\#MapSharedMem](#MapSharedMem "wikilink")                        |
| 6   | [\#GetStatus](#GetStatus "wikilink")                              |
| 7   | [\#SetAruid](#SetAruid "wikilink")                                |
| 8   | [\#SetAruidByPID](#SetAruidByPID "wikilink")                      |
| 9   | [\#DumpGraphicsMemoryInfo](#DumpGraphicsMemoryInfo "wikilink")    |
| 10  | \[3.0.0+\] [\#InitializeDevtools](#InitializeDevtools "wikilink") |
| 11  | \[3.0.0+\] [\#Ioctl2](#Ioctl2 "wikilink")                         |
| 12  | \[3.0.0+\] [\#Ioctl3](#Ioctl3 "wikilink")                         |
| 13  | \[3.0.0+\] [\#FinishInitialize](#FinishInitialize "wikilink")     |

## Open

Takes a type-0x5 input buffer for the device-path. Returns the output
32bit **fd** and the u32 **error\_code**.

## Ioctl

Takes a 32bit **fd**, an u32 **ioctl\_cmd**, a type-0x21 input buffer,
and a type-0x22 output buffer. Returns an output u32 (**error\_code**).

The addr/size for send/recv buffers are only set when the associated
direction bit is set in the ioctl cmd (addr/size = 0 otherwise).

## Close

Takes a 32bit **fd**. Returns an output u32 (**error\_code**).

## Initialize

Takes two copy-handles (**current\_process** and **transfer\_memory**)
and an input u32 (**transfer\_memory\_size**). Returns an output u32
(**error\_code**).

Webkit applet creates the transfer-memory with perm = 0 and size
0x300000.

## QueryEvent

Takes two input u32s (**fd** and **event\_id**), with the second word
immediately after the first one. Returns an output u32 (**error\_code**)
and a copy-handle (**event\_handle**).

QueryEvent is only supported on (and implemented differently on):

  - /dev/nvhost-gpu
      - 1: SmException\_BptIntReport
      - 2: SmException\_BptPauseReport
      - 3: ErrorNotifierEvent
  - /dev/nvhost-ctrl: Used to get events for SyncPts.
      - If bit31-28 is 1, then lower 16-bits contain event\_slot,
        bit27-16 contain syncpt\_number.
      - If bit31-28 is 0, then lower 4-bits contain event\_slot, bit31-4
        contains syncpt\_number.
  - /dev/nvhost-ctrl-gpu
      - 1: Returns error\_event\_handle.
      - 2: Returns unknown event.
  - /dev/nvhost-dbg-gpu
      - Ignores event\_id.

## MapSharedMem

Takes a copy-handle (**transfer\_memory**) and two input u32s (**fd**
and **nvmap\_handle**). Returns an output u32 (**error\_code**).

## GetStatus

Takes no input. Returns 0x10-bytes and an output u32 (**error\_code**).

## SetAruid

Takes an input u64 which must [match](IPC%20Marshalling.md "wikilink")
the user-process PID
([AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink")).
Returns an output u32 (**error\_code**).

## SetAruidByPID

Takes a PID-descriptor and an u64 which must
[match](IPC%20Marshalling.md "wikilink") the user-process PID
([AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink")).
Returns an output u32 (**error\_code**).

## DumpGraphicsMemoryInfo

No input or output. Does nothing.

## InitializeDevtools

Takes a copy-handle and an input u32. Returns an output u32
(**error\_code**).

## Ioctl2

Takes a type-0x21 buffer, a type-0x22 buffer, a type-0x21 buffer, and
two input u32s. Returns an output u32 (**error\_code**).

## Ioctl3

Takes a type-0x21 buffer, a type-0x22 buffer, another type-0x22 buffer,
and two input u32s. Returns an output u32 (error\_code). Cmdhdr\_word1
is 0x100B instead of 0xC0B.

## FinishInitialize

Takes an input u64. No output.

This sets a boolean value based on the input u64 and the value of the
"nv\!nv\_graphics\_firmware\_memory\_margin" system configuration, but
only for "nvdrv" (the other services default to false).

Official user-processes starting with 3.0.0 now use this at the end of
nvdrv service init with value 0x1.

# Ioctls

The ioctl number is generated with the following primitive (see Linux
kernel):

`#define _IOC(inout, group, num, len) \`  
`   (inout | ((len & IOCPARM_MASK) << 16) | ((group) << 8) | (num))`

The following table contains known ioctls.

## /dev/nvhost-ctrl

| Value      | Direction | Size | Description                                                                                                       |
| ---------- | --------- | ---- | ----------------------------------------------------------------------------------------------------------------- |
| 0xC0080014 | Inout     | 8    | [\#NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ](#NVHOST_IOCTL_CTRL_SYNCPT_READ "wikilink")                                  |
| 0x40040015 | In        | 4    | [\#NVHOST\_IOCTL\_CTRL\_SYNCPT\_INCR](#NVHOST_IOCTL_CTRL_SYNCPT_INCR "wikilink")                                  |
| 0xC00C0016 | Inout     | 12   | [\#NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAIT](#NVHOST_IOCTL_CTRL_SYNCPT_WAIT "wikilink")                                  |
| 0x40080017 | In        | 8    | [\#NVHOST\_IOCTL\_CTRL\_MODULE\_MUTEX](#NVHOST_IOCTL_CTRL_MODULE_MUTEX "wikilink")                                |
| 0xC0180018 | Inout     | 24   | [\#NVHOST\_IOCTL\_CTRL\_MODULE\_REGRDWR](#NVHOST_IOCTL_CTRL_MODULE_REGRDWR "wikilink")                            |
| 0xC0100019 | Inout     | 16   | [\#NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAITEX](#NVHOST_IOCTL_CTRL_SYNCPT_WAITEX "wikilink")                              |
| 0xC008001A | Inout     | 8    | [\#NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ\_MAX](#NVHOST_IOCTL_CTRL_SYNCPT_READ_MAX "wikilink")                         |
| 0xC183001B | Inout     | 387  | [\#NVHOST\_IOCTL\_CTRL\_GET\_CONFIG](#NVHOST_IOCTL_CTRL_GET_CONFIG "wikilink")                                    |
| 0xC004001C | Inout     | 4    | [\#NVHOST\_IOCTL\_CTRL\_EVENT\_SIGNAL](#NVHOST_IOCTL_CTRL_EVENT_SIGNAL "wikilink")                                |
| 0xC010001D | Inout     | 16   | [\#NVHOST\_IOCTL\_CTRL\_EVENT\_WAIT](#NVHOST_IOCTL_CTRL_EVENT_WAIT "wikilink")                                    |
| 0xC010001E | Inout     | 16   | [\#NVHOST\_IOCTL\_CTRL\_EVENT\_WAIT\_ASYNC](#NVHOST_IOCTL_CTRL_EVENT_WAIT_ASYNC "wikilink")                       |
| 0xC004001F | Inout     | 4    | [\#NVHOST\_IOCTL\_CTRL\_EVENT\_REGISTER](#NVHOST_IOCTL_CTRL_EVENT_REGISTER "wikilink")                            |
| 0xC0040020 | Inout     | 4    | [\#NVHOST\_IOCTL\_CTRL\_EVENT\_UNREGISTER](#NVHOST_IOCTL_CTRL_EVENT_UNREGISTER "wikilink")                        |
| 0x40080021 | In        | 8    | [\#NVHOST\_IOCTL\_CTRL\_EVENT\_KILL](#NVHOST_IOCTL_CTRL_EVENT_KILL "wikilink")                                    |
| 0xC0040022 | Inout     | 4    | [\#NVHOST\_IOCTL\_CTRL\_GET\_MAX\_EVENT\_FIFO\_CHANNEL](#NVHOST_IOCTL_CTRL_GET_MAX_EVENT_FIFO_CHANNEL "wikilink") |

### NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ

Identical to Linux driver.

` struct {`  
`   __in  u32 id;`  
`   __out u32 value;`  
` };`

### NVHOST\_IOCTL\_CTRL\_SYNCPT\_INCR

Identical to Linux driver.

` struct {`  
`   __in u32 id;`  
` };`

### NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAIT

Identical to Linux driver.

` struct {`  
`   __in u32 id;`  
`   __in u32 thresh;`  
`   __in s32 timeout;`  
` };`

### NVHOST\_IOCTL\_CTRL\_MODULE\_MUTEX

Identical to Linux driver.

` struct {`  
`   __in u32 id;`  
`   __in u32 lock;        // (0==unlock; 1==lock)`  
` };`

### NVHOST\_IOCTL\_CTRL\_MODULE\_REGRDWR

Identical to Linux driver. Uses 32-bit version and doesn't work.

` struct {`  
`   __in u32 id;`  
`   __in u32 num_offsets;`  
`   __in u32 block_size;`  
`   __in u32 offsets;`  
`   __in u32 values;`  
`   __in u32 write;`  
` };`

### NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAITEX

Identical to Linux driver.

` struct {`  
`   __in  u32 id;`  
`   __in  u32 thresh;`  
`   __in  s32 timeout;`  
`   __out u32 value;`  
` };`

### NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ\_MAX

Identical to Linux driver.

` struct {`  
`   __in  u32 id;`  
`   __out u32 value;`  
` };`

### NVHOST\_IOCTL\_CTRL\_GET\_CONFIG

Gets configured settings. Not available in production mode.

` struct {`  
`   __in char domain_str[0x41];       // "nv"`  
`   __in char param_str[0x41];`  
`   __out char config_str[0x101];`  
` };`

### NVHOST\_IOCTL\_CTRL\_EVENT\_SIGNAL

Signals an user event. Exclusive to the Switch.

` struct {`  
`   __in u32 user_event_id;      // ranges from 0x00 to 0x3F`  
` };`

### NVHOST\_IOCTL\_CTRL\_EVENT\_WAIT

Waits on an event. If waiting fails, returns error code 0x05 (Timeout)
and sets **value** to ((**syncpt\_id** \<\< 0x10) | 0x10000000).

Depending on **threshold**, an **user\_event\_id** may be returned for
using with other event ioctls.

` struct {`  
`   __in    u32 syncpt_id;`  
`   __in    u32 threshold;`  
`   __in    s32 timeout;`  
`   __inout u32 value;           // in=user_event_id (ignored); out=syncpt_value or user_event_id`  
` };`

### NVHOST\_IOCTL\_CTRL\_EVENT\_WAIT\_ASYNC

Waits on an event (async version). If waiting fails, returns error code
0x0B (BadValue).

Depending on **threshold**, an **user\_event\_id** may be returned for
using with other event ioctls.

` struct {`  
`   __in    u32 syncpt_id;`  
`   __in    u32 threshold;`  
`   __in    u32 timeout;`  
`   __inout u32 value;           // in=user_event_id (ignored); out=syncpt_value or user_event_id`  
` };`

### NVHOST\_IOCTL\_CTRL\_EVENT\_REGISTER

Registers an user event. Exclusive to the Switch.

` struct {`  
`   __in u32 user_event_id;      // ranges from 0x00 to 0x3F`  
` };`

### NVHOST\_IOCTL\_CTRL\_EVENT\_UNREGISTER

Unregisters an user event. Exclusive to the Switch.

` struct {`  
`   __in u32 user_event_id;      // ranges from 0x00 to 0x3F`  
` };`

### NVHOST\_IOCTL\_CTRL\_EVENT\_KILL

Kills user events. Exclusive to the Switch.

` struct {`  
`   __in u64 user_events;       // 64-bit bitfield where each bit represents one event`  
` };`

### NVHOST\_IOCTL\_CTRL\_GET\_MAX\_EVENT\_FIFO\_CHANNEL

If event FIFO is enabled, returns the maximum channel number. Exclusive
to the Switch.

` struct {`  
`   __out u32 max_channel;      // 0x00 (FIFO disabled) or 0x60 (FIFO enabled)`  
` };`

## /dev/nvmap

| Value      | Direction | Size | Description                                                                                 |
| ---------- | --------- | ---- | ------------------------------------------------------------------------------------------- |
| 0xC0080101 | Inout     | 8    | [\#NVMAP\_IOC\_CREATE](#NVMAP_IOC_CREATE "wikilink")                                        |
| 0x00000102 | \-        | 0    | [\#NVMAP\_IOC\_CLAIM](#NVMAP_IOC_CLAIM "wikilink")                                          |
| 0xC0080103 | Inout     | 8    | [\#NVMAP\_IOC\_FROM\_ID](#NVMAP_IOC_FROM_ID "wikilink")                                     |
| 0xC0200104 | Inout     | 32   | [\#NVMAP\_IOC\_ALLOC](#NVMAP_IOC_ALLOC "wikilink")                                          |
| 0xC0180105 | Inout     | 24   | [\#NVMAP\_IOC\_FREE](#NVMAP_IOC_FREE "wikilink")                                            |
| 0xC0280106 | Inout     | 40   | [\#NVMAP\_IOC\_MMAP](#NVMAP_IOC_MMAP "wikilink")                                            |
| 0xC0280107 | Inout     | 40   | [\#NVMAP\_IOC\_WRITE](#NVMAP_IOC_WRITE "wikilink")                                          |
| 0xC0280108 | Inout     | 40   | [\#NVMAP\_IOC\_READ](#NVMAP_IOC_READ "wikilink")                                            |
| 0xC00C0109 | Inout     | 12   | [\#NVMAP\_IOC\_PARAM](#NVMAP_IOC_PARAM "wikilink")                                          |
| 0xC010010A | Inout     | 16   | [\#NVMAP\_IOC\_PIN\_MULT](#NVMAP_IOC_PIN_MULT "wikilink")                                   |
| 0xC010010B | Inout     | 16   | [\#NVMAP\_IOC\_UNPIN\_MULT](#NVMAP_IOC_UNPIN_MULT "wikilink")                               |
| 0xC008010C | Inout     | 8    | [\#NVMAP\_IOC\_CACHE](#NVMAP_IOC_CACHE "wikilink")                                          |
| 0xC004010D | Inout     | 4    | [\#NVMAP\_IOC\_GET\_IVC\_ID](#NVMAP_IOC_GET_IVC_ID "wikilink")                              |
| 0xC008010E | Inout     | 8    | [\#NVMAP\_IOC\_GET\_ID](#NVMAP_IOC_GET_ID "wikilink")                                       |
| 0xC004010F | Inout     | 4    | [\#NVMAP\_IOC\_FROM\_IVC\_ID](#NVMAP_IOC_FROM_IVC_ID "wikilink")                            |
| 0x40040110 | In        | 4    | [\#NVMAP\_IOC\_SET\_ALLOCATION\_TAG\_LABEL](#NVMAP_IOC_SET_ALLOCATION_TAG_LABEL "wikilink") |
| 0x00000111 | \-        | 0    | [\#NVMAP\_IOC\_RESERVE](#NVMAP_IOC_RESERVE "wikilink")                                      |
| 0x40100112 | In        | 16   | [\#NVMAP\_IOC\_EXPORT\_FOR\_ARUID](#NVMAP_IOC_EXPORT_FOR_ARUID "wikilink")                  |
| 0x40100113 | In        | 16   | [\#NVMAP\_IOC\_IS\_OWNED\_BY\_ARUID](#NVMAP_IOC_IS_OWNED_BY_ARUID "wikilink")               |
| 0x40100114 | In        | 16   | [\#NVMAP\_IOC\_REMOVE\_EXPORT\_FOR\_ARUID](#NVMAP_IOC_REMOVE_EXPORT_FOR_ARUID "wikilink")   |

### NVMAP\_IOC\_CREATE

Creates an nvmap object. Identical to Linux driver.

` struct {`  
`   __in  u32 size;`  
`   __out u32 handle;`  
` };`

### NVMAP\_IOC\_CLAIM

Returns [NotSupported](#Errors "wikilink").

### NVMAP\_IOC\_FROM\_ID

Get handle to an existing nvmap object. Identical to Linux driver.

` struct {`  
`   __in  u32 id;`  
`   __out u32 handle;`  
` };`

### NVMAP\_IOC\_ALLOC

Allocate memory for the nvmap object. Nintendo extended this one with 16
bytes, and changed it from in to inout.

` struct {`  
`   __in u32 handle;`  
`   __in u32 heapmask;`  
`   __in u32 flags;    // (0=read-only, 1=read-write)`  
`   __in u32 align;`  
`   __in u8  kind;`  
`   u8       pad[7];`  
`   __inout u64 addr;`  
` };`

### NVMAP\_IOC\_FREE

This one is completely custom. Partly because the Linux driver passed
the handle as the ioctl "arg-ptr", and HIPC can't handle that voodoo.

` struct {`  
`   __in  u32 handle;`  
`   u32       pad;`  
`   __out u64 refcount;`  
`   __out u32 size;`  
`   __out u32 flags;    // 1=NOT_FREED_YET`  
` };`

### NVMAP\_IOC\_MMAP

Returns [NotSupported](#Errors "wikilink").

### NVMAP\_IOC\_WRITE

Returns [NotSupported](#Errors "wikilink").

### NVMAP\_IOC\_READ

Returns [NotSupported](#Errors "wikilink").

### NVMAP\_IOC\_PARAM

Returns info about a nvmap object. Identical to Linux driver, but
extended with further params.

` struct {`  
`   __in  u32 handle;`  
`   __in  u32 param;  // 1=SIZE, 2=ALIGNMENT, 3=BASE (returns error), 4=HEAP (always 0x40000000), 5=KIND, 6=COMPR (unused)`  
`   __out u32 result;`  
` };`

### NVMAP\_IOC\_PIN\_MULT

Returns [NotSupported](#Errors "wikilink").

### NVMAP\_IOC\_UNPIN\_MULT

Returns [NotSupported](#Errors "wikilink").

### NVMAP\_IOC\_CACHE

Returns [NotSupported](#Errors "wikilink").

### NVMAP\_IOC\_GET\_IVC\_ID

Returns [NotSupported](#Errors "wikilink").

### NVMAP\_IOC\_GET\_ID

Returns an id for a nvmap object. Identical to Linux driver.

` struct {`  
`   __out u32 id; //~0 indicates error`  
`   __in  u32 handle;`  
` };`

### NVMAP\_IOC\_FROM\_IVC\_ID

Returns [NotSupported](#Errors "wikilink").

### NVMAP\_IOC\_SET\_ALLOCATION\_TAG\_LABEL

Returns [NotSupported](#Errors "wikilink").

### NVMAP\_IOC\_RESERVE

Returns [NotSupported](#Errors "wikilink").

### NVMAP\_IOC\_EXPORT\_FOR\_ARUID

Binds a nvmap object to an
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").

` struct {`  
`   __in  u64 aruid;`  
`   __in  u32 handle;`  
`   u8        pad[4];`  
` };`

### NVMAP\_IOC\_IS\_OWNED\_BY\_ARUID

Checks if a nvmap object is bound to an
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").

` struct {`  
`   __in  u64 aruid;`  
`   __in  u32 handle;`  
`   u8        pad[4];`  
` };`

### NVMAP\_IOC\_REMOVE\_EXPORT\_FOR\_ARUID

Unbinds a nvmap object from an
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").

` struct {`  
`   __in  u64 aruid;`  
`   __in  u32 handle;`  
`   u8        pad[4];`  
` };`

## /dev/nvdisp-ctrl

| Value                                       | Direction               | Size                      | Description                                                                                               |
| ------------------------------------------- | ----------------------- | ------------------------- | --------------------------------------------------------------------------------------------------------- |
| 0x80040212                                  | Out                     | 4                         | NVDISP\_CTRL\_GET\_NUM\_OUTPUTS                                                                           |
| 0xC0140213                                  | Inout                   | 20                        | NVDISP\_CTRL\_GET\_OUTPUT\_PROPERTIES                                                                     |
| 0xC1100214                                  | Inout                   | 272                       | NVDISP\_CTRL\_GET\_OUTPUT\_EDID                                                                           |
| 0xC0080216</br>(\[1.0.0-3.0.0\] 0xC0040216) | Inout                   | 8</br>(\[1.0.0-3.0.0\] 4) | NVDISP\_CTRL\_GET\_EXT\_HPD\_IN\_OUT\_EVENTS</br>(\[1.0.0-3.0.0\] NVDISP\_CTRL\_GET\_EXT\_HPD\_IN\_EVENT) |
| (\[1.0.0-3.0.0\] 0xC0040217)                | (\[1.0.0-3.0.0\] Inout) | (\[1.0.0-3.0.0\] 4)       | (\[1.0.0-3.0.0\] NVDISP\_CTRL\_GET\_EXT\_HPD\_OUT\_EVENT)                                                 |
| 0xC0100218                                  | Inout                   | 16                        | NVDISP\_CTRL\_GET\_VBLANK\_HEAD0\_EVENT                                                                   |
| 0xC0100219                                  | Inout                   | 16                        | NVDISP\_CTRL\_GET\_VBLANK\_HEAD1\_EVENT                                                                   |
| 0xC0040220                                  | Inout                   | 4                         | NVDISP\_CTRL\_GET\_HPD\_IRQ                                                                               |

## /dev/nvdisp-disp0, /dev/nvdisp-disp1

| Value      | Direction | Size  | Description                    |
| ---------- | --------- | ----- | ------------------------------ |
| 0x40040201 | In        | 4     | NVDISP\_GET\_WINDOW            |
| 0x40040202 | In        | 4     | NVDISP\_PUT\_WINDOW            |
| 0xC4C80203 | In        | 1224  | NVDISP\_FLIP                   |
| 0x80380204 | Out       | 56    | NVDISP\_GET\_MODE              |
| 0x40380205 | Out       | 56    | NVDISP\_SET\_MODE              |
| 0x430C0206 | In        | 780   | NVDISP\_SET\_LUT               |
| 0x40010207 | In        | 1     | NVDISP\_ENABLE\_DISABLE\_CRC   |
| 0x80040208 | Out       | 4     | NVDISP\_GET\_CRC               |
| 0x80040209 | Out       | 4     | NVDISP\_GET\_HEAD\_STATUS      |
| 0xC038020A | Inout     | 56    | NVDISP\_VALIDATE\_MODE         |
| 0x4018020B | In        | 24    | NVDISP\_SET\_CSC               |
| 0xC004020C | Inout     | 4     | NVDISP\_GET\_VBLANK\_SYNCPT    |
| 0x8040020D | Out       | 64    | NVDISP\_GET\_UNDERFLOWS        |
| 0xC99A020E | Inout     | 2458  | NVDISP\_SET\_CMU               |
| 0xC004020F | Inout     | 4     | NVDISP\_DPMS                   |
| 0x80600210 | Out       | 96    | NVDISP\_GET\_AVI\_INFOFRAME    |
| 0x40600211 | In        | 96    | NVDISP\_SET\_AVI\_INFOFRAME    |
| 0xEBFC0215 | Inout     | 11260 | NVDISP\_GET\_MODE\_DB          |
| 0xC003021A | Inout     | 3     | NVDISP\_PANEL\_GET\_VENDOR\_ID |
| 0x803C021B | Out       | 60    | NVDISP\_GET\_MODE2             |
| 0x403C021C | In        | 60    | NVDISP\_SET\_MODE2             |
| 0xC03C021D | Inout     | 60    | NVDISP\_VALIDATE\_MODE2        |
| 0xEF20021E | Inout     | 12064 | NVDISP\_GET\_MODE\_DB2         |
| 0xC004021F | Inout     | 4     | NVDISP\_GET\_WINMASK           |

## /dev/nvcec-ctrl

| Value      | Direction | Size | Description                          |
| ---------- | --------- | ---- | ------------------------------------ |
| 0x40010301 | In        | 1    | NVCEC\_CTRL\_ENABLE                  |
| 0x804C0302 | Out       | 76   | NVCEC\_CTRL\_GET\_PADDR              |
| 0x40040303 | In        | 4    | NVCEC\_CTRL\_SET\_LADDR              |
| 0xC04C0304 | Inout     | 76   | NVCEC\_CTRL\_WRITE                   |
| 0xC04C0305 | Inout     | 76   | NVCEC\_CTRL\_READ                    |
| 0x804C0306 | Out       | 76   | NVCEC\_CTRL\_GET\_CONNECTION\_STATUS |
| 0x804C0307 | Out       | 76   | NVCEC\_CTRL\_GET\_WRITE\_STATUS      |

## /dev/nvhdcp\_up-ctrl

| Value      | Direction | Size | Description             |
| ---------- | --------- | ---- | ----------------------- |
| 0xC4880401 | Inout     | 1160 | NVHDCP\_READ\_M         |
| 0xC4880402 | Inout     | 1160 | NVHDCP\_READ\_S         |
| 0x40010403 | In        | 1    | NVHDCP\_ON\_OFF         |
| 0xC0080404 | Inout     | 8    | NVHDCP\_READ\_EVENT     |
| 0xC0010405 | Inout     | 1    | NVHDCP\_EVENTS\_ON\_OFF |

## /dev/nvdcutil-disp0, /dev/nvdcutil-disp1

| Value      | Direction | Size | Description                         |
| ---------- | --------- | ---- | ----------------------------------- |
| 0x40010501 | In        | 1    | NVDCUTIL\_SW\_HOTPLUG\_IN\_OUT      |
| 0x40010502 | In        | 1    | NVDCUTIL\_VIRTUAL\_EDID\_ON\_OFF    |
| 0x42040503 | In        | 1056 | NVDCUTIL\_VIRTUAL\_EDID\_SET\_DATA  |
| 0x803C0504 | Out       | 60   | NVDCUTIL\_GET\_MODE                 |
| 0x40010505 | In        | 1    | NVDCUTIL\_TELEMETRY\_TEST\_ON\_OFF  |
| 0x400C0506 | In        | 12   | NVDCUTIL\_DSI\_PACKET\_SHORT\_WRITE |
| 0x40F80507 | In        | 248  | NVDCUTIL\_DSI\_PACKET\_LONG\_WRITE  |
| 0xC0F40508 | Inout     | 244  | NVDCUTIL\_DSI\_PACKET\_READ         |

## /dev/nvsched-ctrl

This is a customized scheduler device.

The way this device is exposed and configured is exclusive to the
Switch, since other sources don't have an actual interface for the
scheduler.

| Value                                       | Direction | Size                        | Description                                                                                       |
| ------------------------------------------- | --------- | --------------------------- | ------------------------------------------------------------------------------------------------- |
| 0x00000601                                  | \-        | 0                           | [\#NVSCHED\_CTRL\_ENABLE](#NVSCHED_CTRL_ENABLE "wikilink")                                        |
| 0x00000602                                  | \-        | 0                           | [\#NVSCHED\_CTRL\_DISABLE](#NVSCHED_CTRL_DISABLE "wikilink")                                      |
| 0x40180603                                  | In        | 24                          | [\#NVSCHED\_CTRL\_ADD\_APPLICATION](#NVSCHED_CTRL_ADD_APPLICATION "wikilink")                     |
| 0x40180604                                  | In        | 24                          | [\#NVSCHED\_CTRL\_UPDATE\_APPLICATION](#NVSCHED_CTRL_UPDATE_APPLICATION "wikilink")               |
| 0x40080605                                  | In        | 8                           | [\#NVSCHED\_CTRL\_REMOVE\_APPLICATION](#NVSCHED_CTRL_REMOVE_APPLICATION "wikilink")               |
| 0x80080606                                  | Out       | 8                           | [\#NVSCHED\_CTRL\_GET\_ID](#NVSCHED_CTRL_GET_ID "wikilink")                                       |
| 0x80080607                                  | Out       | 8                           | [\#NVSCHED\_CTRL\_ADD\_RUNLIST](#NVSCHED_CTRL_ADD_RUNLIST "wikilink")                             |
| 0x40180608                                  | In        | 24                          | [\#NVSCHED\_CTRL\_UPDATE\_RUNLIST](#NVSCHED_CTRL_UPDATE_RUNLIST "wikilink")                       |
| 0x40100609                                  | In        | 16                          | [\#NVSCHED\_CTRL\_LINK\_RUNLIST](#NVSCHED_CTRL_LINK_RUNLIST "wikilink")                           |
| 0x4010060A                                  | In        | 16                          | [\#NVSCHED\_CTRL\_UNLINK\_RUNLIST](#NVSCHED_CTRL_UNLINK_RUNLIST "wikilink")                       |
| 0x4008060B                                  | In        | 8                           | [\#NVSCHED\_CTRL\_REMOVE\_RUNLIST](#NVSCHED_CTRL_REMOVE_RUNLIST "wikilink")                       |
| 0x8001060C                                  | Out       | 1                           | [\#NVSCHED\_CTRL\_HAS\_OVERRUN\_EVENT](#NVSCHED_CTRL_HAS_OVERRUN_EVENT "wikilink")                |
| 0x8020060D</br>(\[1.0.0-3.0.0\] 0x8010060D) | Out       | 32</br>(\[1.0.0-3.0.0\] 16) | [\#NVSCHED\_CTRL\_GET\_NEXT\_OVERRUN\_EVENT](#NVSCHED_CTRL_GET_NEXT_OVERRUN_EVENT "wikilink")     |
| 0x400C060E                                  | In        | 12                          | [\#NVSCHED\_CTRL\_PUT\_CONDUCTOR\_FLIP\_FENCE](#NVSCHED_CTRL_PUT_CONDUCTOR_FLIP_FENCE "wikilink") |
| 0x4008060F                                  | In        | 8                           | [\#NVSCHED\_CTRL\_DETACH\_APPLICATION](#NVSCHED_CTRL_DETACH_APPLICATION "wikilink")               |
| 0x40100610                                  | In        | 16                          | NVSCHED\_CTRL\_LINK\_RUNLIST\_EX                                                                  |
| 0x40100611                                  | In        | 16                          | NVSCHED\_CTRL\_UNLINK\_RUNLIST\_EX                                                                |
| 0x40010612                                  | In        | 1                           | NVSCHED\_CTRL\_OVERRUN\_EVENTS\_ON\_OFF                                                           |

### NVSCHED\_CTRL\_ENABLE

Enables the scheduler.

### NVSCHED\_CTRL\_DISABLE

Disables the scheduler.

### NVSCHED\_CTRL\_ADD\_APPLICATION

Adds a new application to the scheduler.

` struct {`  
`   __in u64 application_id;`  
`   __in u64 priority;`  
`   __in u64 timeslice;`  
` };`

### NVSCHED\_CTRL\_UPDATE\_APPLICATION

Updates the application parameters in the scheduler.

` struct {`  
`   __in u64 application_id;`  
`   __in u64 priority;`  
`   __in u64 timeslice;`  
` };`

### NVSCHED\_CTRL\_REMOVE\_APPLICATION

Removes the application from the scheduler.

` struct {`  
`   __in u64 application_id;`  
` };`

### NVSCHED\_CTRL\_GET\_ID

Returns the ID of the last scheduled object.

` struct {`  
`   __out u64 id;`  
` };`

### NVSCHED\_CTRL\_ADD\_RUNLIST

Creates a new runlist and returns it's ID.

` struct {`  
`   __out u64 runlist_id;`  
` };`

### NVSCHED\_CTRL\_UPDATE\_RUNLIST

Updates the runlist parameters in the scheduler.

` struct {`  
`   __in u64 runlist_id;`  
`   __in u64 priority;`  
`   __in u64 timeslice;`  
` };`

### NVSCHED\_CTRL\_LINK\_RUNLIST

Links a runlist to a given application in the scheduler.

` struct {`  
`   __in u64 runlist_id;`  
`   __in u64 application_id;`  
` };`

### NVSCHED\_CTRL\_UNLINK\_RUNLIST

Unlinks a runlist from a given application in the scheduler.

` struct {`  
`   __in u64 runlist_id;`  
`   __in u64 application_id;`  
` };`

### NVSCHED\_CTRL\_REMOVE\_RUNLIST

Removes the runlist from the scheduler.

` struct {`  
`   __in u64 runlist_id;`  
` };`

### NVSCHED\_CTRL\_HAS\_OVERRUN\_EVENT

Returns a boolean to tell if the scheduler has an overrun event or not.

` struct {`  
`   __out u8 has_overrun;`  
` };`

### NVSCHED\_CTRL\_GET\_NEXT\_OVERRUN\_EVENT

Returns the overrun event's data from the scheduler.

` struct {`  
`   __out u64 runlist_id;`  
`   __out u64 debt;`  
`   __out u64 unk0;           // 3.0.0+ only`  
`   __out u64 unk1;           // 3.0.0+ only`  
` };`

### NVSCHED\_CTRL\_PUT\_CONDUCTOR\_FLIP\_FENCE

Installs a fence swap event?

` struct {`  
`   __in u32 fence_id;`  
`   __in u32 fence_value;`  
`   __in u32 swap_interval;`  
` };`

### NVSCHED\_CTRL\_DETACH\_APPLICATION

Places the given application in detached state.

` struct {`  
`   __in u64 application_id;`  
` };`

## /dev/nverpt-ctrl

Added in firmware version 3.0.0.

| Value      | Direction | Size | Description                              |
| ---------- | --------- | ---- | ---------------------------------------- |
| 0xC1280701 | Inout     | 296  | NVERPT\_TELEMETRY\_SUBMIT\_DATA          |
| 0xCF580702 | Inout     | 3928 | NVERPT\_TELEMETRY\_SUBMIT\_DISPLAY\_DATA |

## /dev/nvhost-as-gpu

Each fd opened to this device creates an address space. An address space
is then later bound with a channel.

Once a nvgpu channel has been bound to an address space it cannot be
unbound. There is no support for allowing an nvgpu channel to change
from one address space to another (or from one to none).

| Value      | Direction | Size     | Description                                                                       |
| ---------- | --------- | -------- | --------------------------------------------------------------------------------- |
| 0x40044101 | In        | 4        | [\#NVGPU\_AS\_IOCTL\_BIND\_CHANNEL](#NVGPU_AS_IOCTL_BIND_CHANNEL "wikilink")      |
| 0xC0184102 | Inout     | 24       | [\#NVGPU\_AS\_IOCTL\_ALLOC\_SPACE](#NVGPU_AS_IOCTL_ALLOC_SPACE "wikilink")        |
| 0xC0104103 | Inout     | 16       | [\#NVGPU\_AS\_IOCTL\_FREE\_SPACE](#NVGPU_AS_IOCTL_FREE_SPACE "wikilink")          |
| 0xC0184104 | Inout     | 24       | [\#NVGPU\_AS\_IOCTL\_MAP\_BUFFER](#NVGPU_AS_IOCTL_MAP_BUFFER "wikilink")          |
| 0xC0084105 | Inout     | 8        | [\#NVGPU\_AS\_IOCTL\_UNMAP\_BUFFER](#NVGPU_AS_IOCTL_UNMAP_BUFFER "wikilink")      |
| 0xC0284106 | Inout     | 40       | [\#NVGPU\_AS\_IOCTL\_MODIFY](#NVGPU_AS_IOCTL_MODIFY "wikilink")                   |
| 0x40104107 | In        | 16       | [\#NVGPU\_AS\_IOCTL\_INITIALIZE](#NVGPU_AS_IOCTL_INITIALIZE "wikilink")           |
| 0xC0404108 | Inout     | 64       | [\#NVGPU\_AS\_IOCTL\_GET\_VA\_REGIONS](#NVGPU_AS_IOCTL_GET_VA_REGIONS "wikilink") |
| 0x40284109 | In        | 40       | [\#NVGPU\_AS\_IOCTL\_INITIALIZE\_EX](#NVGPU_AS_IOCTL_INITIALIZE_EX "wikilink")    |
| 0xC038410A | Inout     | 56       | [\#NVGPU\_AS\_IOCTL\_MAP\_BUFFER\_EX](#NVGPU_AS_IOCTL_MAP_BUFFER_EX "wikilink")   |
| 0xC0??4114 | Inout     | Variable | [\#NVGPU\_AS\_IOCTL\_REMAP](#NVGPU_AS_IOCTL_REMAP "wikilink")                     |

### NVGPU\_AS\_IOCTL\_BIND\_CHANNEL

Identical to Linux driver.

` struct {`  
`   __in u32 fd;`  
` };`

### NVGPU\_AS\_IOCTL\_ALLOC\_SPACE

Reserves pages in the device address space.

` struct {`  
`   __in u32 pages;`  
`   __in u32 page_size;`  
`   __in u32 flags;`  
`   u32      pad;`  
`   union {`  
`     __out u64 offset;`  
`     __in  u64 align;`  
`   };`  
` };`

### NVGPU\_AS\_IOCTL\_FREE\_SPACE

Frees pages from the device address space.

` struct {`  
`   __in u64 offset;`  
`   __in u32 pages;`  
`   __in u32 page_size;`  
` };`

### NVGPU\_AS\_IOCTL\_MAP\_BUFFER

Maps a memory region in the device address space. Identical to Linux
driver pretty much.

On success, the mapped memory region is locked by having
[SVC\#MemoryState](SVC#MemoryState.md##MemoryState "wikilink") bit34
set.

` struct {`  
`   __in    u32 flags;        // bit0: fixed_offset, bit2: cacheable`  
`   u32         pad;`  
`   __in    u32 nvmap_handle;`  
`   __inout u32 page_size;    // 0 means don't care`  
`   union {`  
`     __out u64 offset;`  
`     __in  u64 align;`  
`   };`  
` };`

### NVGPU\_AS\_IOCTL\_MODIFY

Modifies a memory region in the device address space.

Unaligned size will cause a [\#Panic](#Panic "wikilink").

On success, the mapped memory region is locked by having
[SVC\#MemoryState](SVC#MemoryState.md##MemoryState "wikilink") bit34
set.

` struct {`  
`   __in      u32 flags;          // bit0: fixed_offset, bit2: cacheable`  
`   __in      u32 kind;           // -1 is default`  
`   __in      u32 nvmap_handle;`  
`   __inout   u32 page_size;      // 0 means don't care`  
`   __in      u64 buffer_offset;`  
`   __in      u64 mapping_size;`  
`   __inout   u64 offset;`  
` };`

### NVGPU\_AS\_IOCTL\_UNMAP\_BUFFER

Unmaps a memory region from the device address space.

`struct {`  
`   __in u64 offset;`  
` };`

### NVGPU\_AS\_IOCTL\_INITIALIZE

Nintendo's custom implementation of NVGPU\_GPU\_IOCTL\_ALLOC\_AS
(unavailable).

` struct {`  
`   __in u32 big_page_size;   // depends on GPU's available_big_page_sizes; 0=default`  
`   __in s32 as_fd;           // ignored; passes 0`  
`   __in u32 flags;           // ignored; passes 0`  
`   __in u32 reserved;        // ignored; passes 0`  
` };`

### NVGPU\_AS\_IOCTL\_GET\_VA\_REGIONS

Nintendo's custom implementation to get rid of pointer in struct.

` struct va_region {`  
`   u64 offset;`  
`   u32 page_size;`  
`   u32 pad;`  
`   u64 pages;`  
` };`  
` `  
` struct {`  
`   u64           not_used;   // (contained output user ptr on linux, ignored)`  
`   __inout u32   bufsize;    // forced to 2*sizeof(struct va_region)`  
`   u32           pad;`  
`   __out struct  va_region regions[2];`  
` };`

### NVGPU\_AS\_IOCTL\_INITIALIZE\_EX

Nintendo's custom implementation of NVGPU\_GPU\_IOCTL\_ALLOC\_AS
(unavailable) with extra params.

` struct {`  
`   __in u32 big_page_size;   // depends on GPU's available_big_page_sizes; 0=default`  
`   __in s32 as_fd;           // ignored; passes 0`  
`   __in u32 flags;           // passes 0`  
`   __in u32 reserved;        // ignored; passes 0`  
`   __in u64 unk0;`  
`   __in u64 unk1;`  
`   __in u64 unk2;`  
` };`

### NVGPU\_AS\_IOCTL\_MAP\_BUFFER\_EX

Maps a memory region in the device address space with extra params.

`   struct {`  
`   __in      u32 flags;          // bit0: fixed_offset, bit2: cacheable`  
`   __in      u32 kind;           // -1 is default`  
`   __in      u32 nvmap_handle;`  
`   __inout   u32 page_size;      // 0 means don't care`  
`   __in      u64 buffer_offset;`  
`   __in      u64 mapping_size;`  
`   __inout   u64 offset;`  
`   __in      u64 unk0;`  
`   __in      u32 unk1;`  
`   u32            pad;`  
` };`

### NVGPU\_AS\_IOCTL\_REMAP

Nintendo's custom implementation of address space remapping.

` struct remap_entry {`  
`   __in u16 flags;        // 0 or 4`  
`   __in u16 kind;           `  
`   __in u32 nvmap_handle;`  
`   __in u32 padding;`  
`   __in u32 offset;       // (alloc_space_offset >> 0x10)`  
`   __in u32 pages;        // alloc_space_pages`  
` };`  
  
`struct {`  
`   __in struct remap_entry entries[];`  
`};`

## /dev/nvhost-dbg-gpu

Returns [NotSupported](#Errors "wikilink") on Open unless
nn::settings::detail::GetDebugModeFlag is set.

| Value      | Direction | Size     | Description                                                                                                  |
| ---------- | --------- | -------- | ------------------------------------------------------------------------------------------------------------ |
| 0x40084401 | In        | 8        | NVGPU\_DBG\_GPU\_IOCTL\_BIND\_CHANNEL                                                                        |
| 0xC0??4402 | Inout     | Variable | NVGPU\_DBG\_GPU\_IOCTL\_REG\_OPS                                                                             |
| 0x40084403 | In        | 8        | NVGPU\_DBG\_GPU\_IOCTL\_EVENTS\_CTRL                                                                         |
| 0x40044404 | In        | 4        | NVGPU\_DBG\_GPU\_IOCTL\_POWERGATE                                                                            |
| 0x40044405 | In        | 4        | NVGPU\_DBG\_GPU\_IOCTL\_SMPC\_CTXSW\_MODE                                                                    |
| 0x40044406 | In        | 4        | NVGPU\_DBG\_GPU\_IOCTL\_SUSPEND\_RESUME\_ALL\_SMS                                                            |
| 0xC0184407 | Inout     | 24       | NVGPU\_DBG\_GPU\_IOCTL\_PERFBUF\_MAP                                                                         |
| 0x40084408 | In        | 8        | NVGPU\_DBG\_GPU\_IOCTL\_PERFBUF\_UNMAP                                                                       |
| 0x40084409 | In        | 8        | NVGPU\_DBG\_GPU\_IOCTL\_PC\_SAMPLING                                                                         |
| 0x4008440A | In        | 8        | NVGPU\_DBG\_GPU\_IOCTL\_TIMEOUT                                                                              |
| 0x8008440B | Out       | 8        | NVGPU\_DBG\_GPU\_IOCTL\_GET\_TIMEOUT                                                                         |
| 0x8004440C | Out       | 4        | NVGPU\_DBG\_GPU\_IOCTL\_GET\_GR\_CONTEXT\_SIZE                                                               |
| 0x0000440D | None      | 0        | [\#NVGPU\_DBG\_GPU\_IOCTL\_GET\_GR\_CONTEXT](#NVGPU_DBG_GPU_IOCTL_GET_GR_CONTEXT "wikilink")                 |
| 0xC018440F | Inout     | 24       | NVGPU\_DBG\_GPU\_IOCTL\_GET\_GPU\_VA\_RANGE\_NUM\_PDES                                                       |
| 0xC0104410 | Inout     | 16       | [\#NVGPU\_DBG\_GPU\_IOCTL\_GET\_GPU\_VA\_RANGE\_PDES](#NVGPU_DBG_GPU_IOCTL_GET_GPU_VA_RANGE_PDES "wikilink") |
| 0xC0184411 | Inout     | 24       | NVGPU\_DBG\_GPU\_IOCTL\_GET\_GPU\_VA\_RANGE\_NUM\_PTES                                                       |
| 0xC0104412 | Inout     | 16       | [\#NVGPU\_DBG\_GPU\_IOCTL\_GET\_GPU\_VA\_RANGE\_PTES](#NVGPU_DBG_GPU_IOCTL_GET_GPU_VA_RANGE_PTES "wikilink") |
| 0xC0684413 | Inout     | 104      | NVGPU\_DBG\_GPU\_IOCTL\_GET\_COMPTAG\_INFO                                                                   |
| 0xC0184414 | Inout     | 24       | [\#NVGPU\_DBG\_GPU\_IOCTL\_READ\_COMPTAGS](#NVGPU_DBG_GPU_IOCTL_READ_COMPTAGS "wikilink")                    |
| 0xC0184415 | Inout     | 24       | [\#NVGPU\_DBG\_GPU\_IOCTL\_WRITE\_COMPTAGS](#NVGPU_DBG_GPU_IOCTL_WRITE_COMPTAGS "wikilink")                  |
| 0xC0104416 | Inout     | 16       | NVGPU\_DBG\_GPU\_IOCTL\_RESERVE\_COMPTAGS                                                                    |
| 0xC0104417 | Inout     | 16       | NVGPU\_DBG\_GPU\_IOCTL\_FREE\_RESERVED\_COMPTAGS                                                             |
| 0xC0104418 | Inout     | 16       | NVGPU\_DBG\_GPU\_IOCTL\_RESERVE\_PA                                                                          |
| 0xC0104419 | Inout     | 16       | NVGPU\_DBG\_GPU\_IOCTL\_FREE\_RESERVED\_PA                                                                   |
| 0xC018441A | Inout     | 24       | NVGPU\_DBG\_GPU\_IOCTL\_LAZY\_ALLOC\_RESERVED\_PA                                                            |

### NVGPU\_DBG\_GPU\_IOCTL\_GET\_GR\_CONTEXT

Uses [Ioctl3](#Ioctl3 "wikilink").

### NVGPU\_DBG\_GPU\_IOCTL\_GET\_GPU\_VA\_RANGE\_PDES

Uses [Ioctl3](#Ioctl3 "wikilink").

### NVGPU\_DBG\_GPU\_IOCTL\_GET\_GPU\_VA\_RANGE\_PTES

Uses [Ioctl3](#Ioctl3 "wikilink").

### NVGPU\_DBG\_GPU\_IOCTL\_READ\_COMPTAGS

Uses [Ioctl3](#Ioctl3 "wikilink").

### NVGPU\_DBG\_GPU\_IOCTL\_WRITE\_COMPTAGS

Uses [Ioctl2](#Ioctl2 "wikilink").

## /dev/nvhost-prof-gpu

Returns [NotSupported](#Errors "wikilink") on Open unless
nn::settings::detail::GetDebugModeFlag is set.

This device is identical to
[/dev/nvhost-dbg-gpu](#/dev/nvhost-dbg-gpu "wikilink").

## /dev/nvhost-ctrl-gpu

This device is for global (context independent) operations on the gpu.

| Value                                       | Direction | Size                       | Description                                                                                               |
| ------------------------------------------- | --------- | -------------------------- | --------------------------------------------------------------------------------------------------------- |
| 0x80044701                                  | Out       | 4                          | [\#NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_CTX\_SIZE](#NVGPU_GPU_IOCTL_ZCULL_GET_CTX_SIZE "wikilink")              |
| 0x80284702                                  | Out       | 40                         | [\#NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_INFO](#NVGPU_GPU_IOCTL_ZCULL_GET_INFO "wikilink")                       |
| 0x402C4703                                  | In        | 44                         | [\#NVGPU\_GPU\_IOCTL\_ZBC\_SET\_TABLE](#NVGPU_GPU_IOCTL_ZBC_SET_TABLE "wikilink")                         |
| 0xC0344704                                  | Inout     | 52                         | [\#NVGPU\_GPU\_IOCTL\_ZBC\_QUERY\_TABLE](#NVGPU_GPU_IOCTL_ZBC_QUERY_TABLE "wikilink")                     |
| 0xC0B04705                                  | Inout     | 176                        | [\#NVGPU\_GPU\_IOCTL\_GET\_CHARACTERISTICS](#NVGPU_GPU_IOCTL_GET_CHARACTERISTICS "wikilink")              |
| 0xC0184706                                  | Inout     | 24                         | NVGPU\_GPU\_IOCTL\_GET\_TPC\_MASKS                                                                        |
| 0x40084707                                  | In        | 8                          | [\#NVGPU\_GPU\_IOCTL\_FLUSH\_L2](#NVGPU_GPU_IOCTL_FLUSH_L2 "wikilink")                                    |
| 0x4008470D                                  | In        | 8                          | NVGPU\_GPU\_IOCTL\_INVAL\_ICACHE                                                                          |
| 0x4008470E                                  | In        | 8                          | NVGPU\_GPU\_IOCTL\_SET\_MMUDEBUG\_MODE                                                                    |
| 0x4010470F                                  | In        | 16                         | NVGPU\_GPU\_IOCTL\_SET\_SM\_DEBUG\_MODE                                                                   |
| 0xC0304710</br>(\[1.0.0-6.1.0\] 0xC0084710) | Inout     | 48</br>(\[1.0.0-6.1.0\] 8) | NVGPU\_GPU\_IOCTL\_WAIT\_FOR\_PAUSE                                                                       |
| 0x80084711                                  | Out       | 8                          | NVGPU\_GPU\_IOCTL\_GET\_TPC\_EXCEPTION\_EN\_STATUS                                                        |
| 0x80084712                                  | Out       | 8                          | NVGPU\_GPU\_IOCTL\_NUM\_VSMS                                                                              |
| 0xC0044713                                  | Inout     | 4                          | NVGPU\_GPU\_IOCTL\_VSMS\_MAPPING                                                                          |
| 0x80084714                                  | Out       | 8                          | [\#NVGPU\_GPU\_IOCTL\_ZBC\_GET\_ACTIVE\_SLOT\_MASK](#NVGPU_GPU_IOCTL_ZBC_GET_ACTIVE_SLOT_MASK "wikilink") |
| 0x80044715                                  | Out       | 4                          | NVGPU\_GPU\_IOCTL\_PMU\_GET\_GPU\_LOAD                                                                    |
| 0x40084716                                  | In        | 8                          | NVGPU\_GPU\_IOCTL\_SET\_CG\_CONTROLS                                                                      |
| 0xC0084717                                  | Inout     | 8                          | NVGPU\_GPU\_IOCTL\_GET\_CG\_CONTROLS                                                                      |
| 0x40084718                                  | In        | 8                          | NVGPU\_GPU\_IOCTL\_SET\_PG\_CONTROLS                                                                      |
| 0xC0084719                                  | Inout     | 8                          | NVGPU\_GPU\_IOCTL\_GET\_PG\_CONTROLS                                                                      |
| 0x8018471A                                  | Out       | 24                         | NVGPU\_GPU\_IOCTL\_PMU\_DUMP\_ELPG\_STATS                                                                 |
| 0xC008471B                                  | Inout     | 8                          | NVGPU\_GPU\_IOCTL\_GET\_ERROR\_CHANNEL\_USER\_DATA                                                        |
| 0xC010471C                                  | Inout     | 16                         | NVGPU\_GPU\_IOCTL\_GET\_GPU\_TIME                                                                         |
| 0xC108471D                                  | Inout     | 264                        | NVGPU\_GPU\_IOCTL\_GET\_CPU\_TIME\_CORRELATION\_INFO                                                      |

### NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_CTX\_SIZE

Returns the GPU's ZCULL context size. Identical to Linux driver.

`struct {`  
`   __out u32 size;`  
` };`

### NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_INFO

Returns GPU's ZCULL information. Identical to Linux driver.

`struct {`  
`   __out u32 width_align_pixels;`  
`   __out u32 height_align_pixels;`  
`   __out u32 pixel_squares_by_aliquots;`  
`   __out u32 aliquot_total;`  
`   __out u32 region_byte_multiplier;`  
`   __out u32 region_header_size;`  
`   __out u32 subregion_header_size;`  
`   __out u32 subregion_width_align_pixels;`  
`   __out u32 subregion_height_align_pixels;`  
`   __out u32 subregion_count;`  
` };`

### NVGPU\_GPU\_IOCTL\_ZBC\_SET\_TABLE

Sets the active ZBC table. Identical to Linux driver.

`struct {`  
`   __in u32 color_ds[4];`  
`   __in u32 color_l2[4];`  
`   __in u32 depth;`  
`   __in u32 format;`  
`   __in u32 type;         // 1=color, 2=depth`  
` };`

### NVGPU\_GPU\_IOCTL\_ZBC\_QUERY\_TABLE

Queries the active ZBC table. Identical to Linux driver.

`struct {`  
`   __out u32 color_ds[4];`  
`   __out u32 color_l2[4];`  
`   __out u32 depth;`  
`   __out u32 ref_cnt;`  
`   __out u32 format;`  
`   __out u32 type;`  
`   __inout u32 index_size;`  
` };`

### NVGPU\_GPU\_IOCTL\_GET\_CHARACTERISTICS

Returns the GPU characteristics. Modified to return inline data instead
of using a pointer.

` struct gpu_characteristics {`  
`   u32 arch;                       // 0x120 (NVGPU_GPU_ARCH_GM200)`  
`   u32 impl;                       // 0xB (NVGPU_GPU_IMPL_GM20B) or 0xE (NVGPU_GPU_IMPL_GM20B_B)`  
`   u32 rev;                        // 0xA1 (Revision A1)`  
`   u32 num_gpc;                    // 0x1`  
`   u64 l2_cache_size;              // 0x40000`  
`   u64 on_board_video_memory_size; // 0x0 (not used)`  
`   u32 num_tpc_per_gpc;            // 0x2`  
`   u32 bus_type;                   // 0x20 (NVGPU_GPU_BUS_TYPE_AXI)`  
`   u32 big_page_size;              // 0x20000`  
`   u32 compression_page_size;      // 0x20000`  
`   u32 pde_coverage_bit_count;     // 0x1B`  
`   u32 available_big_page_sizes;   // 0x30000`  
`   u32 gpc_mask;                   // 0x1`  
`   u32 sm_arch_sm_version;         // 0x503 (Maxwell Generation 5.0.3)`  
`   u32 sm_arch_spa_version;        // 0x503 (Maxwell Generation 5.0.3)`  
`   u32 sm_arch_warp_count;         // 0x80`  
`   u32 gpu_va_bit_count;           // 0x28`  
`   u32 reserved;                   // NULL`  
`   u64 flags;                      // 0x55 (HAS_SYNCPOINTS | SUPPORT_SPARSE_ALLOCS | SUPPORT_CYCLE_STATS | SUPPORT_CYCLE_STATS_SNAPSHOT)`  
`   u32 twod_class;                 // 0x902D (FERMI_TWOD_A)`  
`   u32 threed_class;               // 0xB197 (MAXWELL_B)`  
`   u32 compute_class;              // 0xB1C0 (MAXWELL_COMPUTE_B)`  
`   u32 gpfifo_class;               // 0xB06F (MAXWELL_CHANNEL_GPFIFO_A)`  
`   u32 inline_to_memory_class;     // 0xA140 (KEPLER_INLINE_TO_MEMORY_B)`  
`   u32 dma_copy_class;             // 0xB0B5 (MAXWELL_DMA_COPY_A)`  
`   u32 max_fbps_count;             // 0x1`  
`   u32 fbp_en_mask;                // 0x0 (disabled)`  
`   u32 max_ltc_per_fbp;            // 0x2`  
`   u32 max_lts_per_ltc;            // 0x1`  
`   u32 max_tex_per_tpc;            // 0x0 (not supported)`  
`   u32 max_gpc_count;              // 0x1`  
`   u32 rop_l2_en_mask_0;           // 0x21D70 (fuse_status_opt_rop_l2_fbp_r)`  
`   u32 rop_l2_en_mask_1;           // 0x0`  
`   u64 chipname;                   // 0x6230326D67 ("gm20b")`  
`   u64 gr_compbit_store_base_hw;   // 0x0 (not supported)`  
` };`  
  
` struct {`  
`   __inout u64 gpu_characteristics_buf_size;   // must not be NULL, but gets overwritten with 0xA0=max_size`  
`   __in    u64 gpu_characteristics_buf_addr;   // ignored, but must not be NULL`  
`   __out struct gpu_characteristics gc;`  
` };`

### NVGPU\_GPU\_IOCTL\_FLUSH\_L2

Flushes the GPU L2 cache.

` struct {`  
`   __in u32 flush;          // l2_flush | l2_invalidate << 1 | fb_flush << 2`  
`   u32      reserved;`  
` };`

### NVGPU\_GPU\_IOCTL\_ZBC\_GET\_ACTIVE\_SLOT\_MASK

Returns the mask value for a ZBC slot.

` struct {`  
`   __out u32 slot;       // always 0x07`  
`   __out u32 mask;`  
` };`

## Channels

Channels are a concept for NVIDIA hardware blocks that share a common
interface.

| Path                | Name                   |
| ------------------- | ---------------------- |
| /dev/nvhost-gpu     | GPU                    |
| /dev/nvhost-msenc   | Video Encoder          |
| /dev/nvhost-nvdec   | Video Decoder          |
| /dev/nvhost-nvjpg   | JPEG Decoder           |
| /dev/nvhost-vic     | Video Image Compositor |
| /dev/nvhost-display | Display                |

## Channel Ioctls

| Value                                       | Size     | Description                                                                                                  |
| ------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------ |
| 0xC0??0001                                  | Variable | NVHOST\_IOCTL\_CHANNEL\_SUBMIT                                                                               |
| 0xC0080002                                  | 8        | [\#NVHOST\_IOCTL\_CHANNEL\_GET\_SYNCPOINT](#NVHOST_IOCTL_CHANNEL_GET_SYNCPOINT "wikilink")                   |
| 0xC0080003                                  | 8        | [\#NVHOST\_IOCTL\_CHANNEL\_GET\_WAITBASE](#NVHOST_IOCTL_CHANNEL_GET_WAITBASE "wikilink")                     |
| 0xC0080004                                  | 8        | [\#NVHOST\_IOCTL\_CHANNEL\_GET\_MODMUTEX](#NVHOST_IOCTL_CHANNEL_GET_MODMUTEX "wikilink")                     |
| 0x40040007                                  | 4        | [\#NVHOST\_IOCTL\_CHANNEL\_SET\_SUBMIT\_TIMEOUT](#NVHOST_IOCTL_CHANNEL_SET_SUBMIT_TIMEOUT "wikilink")        |
| 0x40080008                                  | 8        | [\#NVHOST\_IOCTL\_CHANNEL\_SET\_CLK\_RATE](#NVHOST_IOCTL_CHANNEL_SET_CLK_RATE "wikilink")                    |
| 0xC0??0009                                  | Variable | [\#NVHOST\_IOCTL\_CHANNEL\_MAP\_CMD\_BUFFER](#NVHOST_IOCTL_CHANNEL_MAP_CMD_BUFFER "wikilink")                |
| 0xC0??000A                                  | Variable | [\#NVHOST\_IOCTL\_CHANNEL\_UNMAP\_CMD\_BUFFER](#NVHOST_IOCTL_CHANNEL_UNMAP_CMD_BUFFER "wikilink")            |
| 0x00000013                                  | 0        | [\#NVHOST\_IOCTL\_CHANNEL\_SET\_TIMEOUT\_EX](#NVHOST_IOCTL_CHANNEL_SET_TIMEOUT_EX "wikilink")                |
| 0xC0080023</br>(\[1.0.0-7.0.1\] 0xC0080014) | 8        | [\#NVHOST\_IOCTL\_CHANNEL\_GET\_CLK\_RATE](#NVHOST_IOCTL_CHANNEL_GET_CLK_RATE "wikilink")                    |
| 0xC0??0024                                  | Variable | NVHOST\_IOCTL\_CHANNEL\_SUBMIT\_EX                                                                           |
| 0xC0??0025                                  | Variable | [\#NVHOST\_IOCTL\_CHANNEL\_MAP\_CMD\_BUFFER\_EX](#NVHOST_IOCTL_CHANNEL_MAP_CMD_BUFFER_EX "wikilink")         |
| 0xC0??0026                                  | Variable | [\#NVHOST\_IOCTL\_CHANNEL\_UNMAP\_CMD\_BUFFER\_EX](#NVHOST_IOCTL_CHANNEL_UNMAP_CMD_BUFFER_EX "wikilink")     |
| 0x40044801                                  | 4        | [\#NVGPU\_IOCTL\_CHANNEL\_SET\_NVMAP\_FD](#NVGPU_IOCTL_CHANNEL_SET_NVMAP_FD "wikilink")                      |
| 0x40044803                                  | 4        | NVGPU\_IOCTL\_CHANNEL\_SET\_TIMEOUT                                                                          |
| 0x40084805                                  | 8        | [\#NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO](#NVGPU_IOCTL_CHANNEL_ALLOC_GPFIFO "wikilink")                       |
| 0x40184806                                  |          | NVGPU\_IOCTL\_CHANNEL\_WAIT                                                                                  |
| 0xC0044807                                  | 4        | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS                                                                          |
| 0xC0??4808                                  | Variable | [\#NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO](#NVGPU_IOCTL_CHANNEL_SUBMIT_GPFIFO "wikilink")                     |
| 0xC0104809                                  | 16       | [\#NVGPU\_IOCTL\_CHANNEL\_ALLOC\_OBJ\_CTX](#NVGPU_IOCTL_CHANNEL_ALLOC_OBJ_CTX "wikilink")                    |
| 0x4008480A                                  |          | NVHOST\_IOCTL\_CHANNEL\_FREE\_OBJ\_CTX                                                                       |
| 0xC010480B                                  | 16       | [\#NVGPU\_IOCTL\_CHANNEL\_ZCULL\_BIND](#NVGPU_IOCTL_CHANNEL_ZCULL_BIND "wikilink")                           |
| 0xC018480C                                  | 24       | [\#NVGPU\_IOCTL\_CHANNEL\_SET\_ERROR\_NOTIFIER](#NVGPU_IOCTL_CHANNEL_SET_ERROR_NOTIFIER "wikilink")          |
| 0x4004480D                                  | 4        | [\#NVGPU\_IOCTL\_CHANNEL\_SET\_PRIORITY](#NVGPU_IOCTL_CHANNEL_SET_PRIORITY "wikilink")                       |
| 0x0000480E                                  | 0        | [\#NVGPU\_IOCTL\_CHANNEL\_ENABLE](#NVGPU_IOCTL_CHANNEL_ENABLE "wikilink")                                    |
| 0x0000480F                                  | 0        | [\#NVGPU\_IOCTL\_CHANNEL\_DISABLE](#NVGPU_IOCTL_CHANNEL_DISABLE "wikilink")                                  |
| 0x00004810                                  | 0        | [\#NVGPU\_IOCTL\_CHANNEL\_PREEMPT](#NVGPU_IOCTL_CHANNEL_PREEMPT "wikilink")                                  |
| 0x00004811                                  | 0        | [\#NVGPU\_IOCTL\_CHANNEL\_FORCE\_RESET](#NVGPU_IOCTL_CHANNEL_FORCE_RESET "wikilink")                         |
| 0x40084812                                  | 8        | [\#NVGPU\_IOCTL\_CHANNEL\_EVENT\_ID\_CONTROL](#NVGPU_IOCTL_CHANNEL_EVENT_ID_CONTROL "wikilink")              |
| 0xC0104813                                  | 16       | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS\_SNAPSHOT                                                                |
| 0x80804816                                  | 128      | NVGPU\_IOCTL\_CHANNEL\_GET\_ERROR\_INFO                                                                      |
| 0xC0104817                                  | 16       | [\#NVGPU\_IOCTL\_CHANNEL\_GET\_ERROR\_NOTIFICATION](#NVGPU_IOCTL_CHANNEL_GET_ERROR_NOTIFICATION "wikilink")  |
| 0x40204818                                  | 32       | [\#NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX](#NVGPU_IOCTL_CHANNEL_ALLOC_GPFIFO_EX "wikilink")                |
| 0xC0??4819                                  | Variable | [\#NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO\_RETRY](#NVGPU_IOCTL_CHANNEL_SUBMIT_GPFIFO_RETRY "wikilink")        |
| 0xC020481A                                  | 32       | [\#NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX2](#NVGPU_IOCTL_CHANNEL_ALLOC_GPFIFO_EX2 "wikilink")              |
| 0xC018481B                                  | 24       | [\#NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO\_EX](#NVGPU_IOCTL_CHANNEL_SUBMIT_GPFIFO_EX "wikilink")              |
| 0xC018481C                                  | 24       | [\#NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO\_RETRY\_EX](#NVGPU_IOCTL_CHANNEL_SUBMIT_GPFIFO_RETRY_EX "wikilink") |
| 0xC004481D                                  | 4        | [\#NVGPU\_IOCTL\_CHANNEL\_SET\_TIMESLICE](#NVGPU_IOCTL_CHANNEL_SET_TIMESLICE "wikilink")                     |
| 0x40084714                                  | 8        | NVGPU\_IOCTL\_CHANNEL\_SET\_USER\_DATA                                                                       |
| 0x80084715                                  | 8        | NVGPU\_IOCTL\_CHANNEL\_GET\_USER\_DATA                                                                       |

### NVHOST\_IOCTL\_CHANNEL\_GET\_SYNCPOINT

Returns the current syncpoint value for a given module. Identical to
Linux driver.

` struct {`  
`   __in    u32 module_id;`  
`   __out   u32 syncpt_value;`  
` };`

### NVHOST\_IOCTL\_CHANNEL\_GET\_WAITBASE

Returns the current waitbase value for a given module. Always returns 0.

` struct {`  
`   __in    u32 module_id;`  
`   __out   u32 waitbase_value;`  
` };`

### NVHOST\_IOCTL\_CHANNEL\_GET\_MODMUTEX

Stubbed. Does a debug print and returns 0.

### NVHOST\_IOCTL\_CHANNEL\_SET\_SUBMIT\_TIMEOUT

Sets the submit timeout value for the channel. Identical to Linux
driver.

` struct {`  
`   __in    u32 timeout;`  
` };`

### NVHOST\_IOCTL\_CHANNEL\_SET\_CLK\_RATE

Sets the clock rate value for a given module. Identical to Linux driver.

` struct {`  
`   __in    u32 clk_rate;`  
`   __in    u32 module_id;`  
` };`

### NVHOST\_IOCTL\_CHANNEL\_MAP\_CMD\_BUFFER

Uses **nvmap\_pin** internally to pin a given number of nvmap handles to
an appropriate device physical address.

` struct handle {`  
`   u32 handle_id_in;                 // nvmap handle to map`  
`   u32 phys_addr_out;                // returned device physical address mapped to the handle`  
` };`  
  
` struct {`  
`   __in    u32 num_handles;          // number of nvmap handles to map`  
`   __in    u32 padding;              // ignored`  
`   __in    u8  is_compr;             // memory to map is compressed`  
`   __in    u8  padding[3];           // ignored`  
`   __inout struct handle handles[];  // depends on num_handles`  
` };`

### NVHOST\_IOCTL\_CHANNEL\_UNMAP\_CMD\_BUFFER

Uses **nvmap\_unpin** internally to unpin a given number of nvmap
handles from their device physical address.

` struct handle {`  
`   u32 handle_id_in;                 // nvmap handle to unmap`  
`   u32 padding;                      // ignored`  
` };`  
  
` struct {`  
`   __in    u32 num_handles;          // number of nvmap handles to unmap`  
`   __in    u32 padding;              // ignored`  
`   __in    u8  is_compr;             // memory to unmap is compressed`  
`   __in    u8  padding[3];           // ignored`  
`   __inout struct handle handles[];  // depends on num_handles`  
` };`

### NVHOST\_IOCTL\_CHANNEL\_SET\_TIMEOUT\_EX

Sets the global timeout value for the channel. Identical to Linux
driver.

` struct {`  
`   __in    u32 timeout;`  
`   __in    u32 flags;`  
` };`

### NVHOST\_IOCTL\_CHANNEL\_GET\_CLK\_RATE

Returns the clock rate value for a given module. Identical to Linux
driver.

` struct {`  
`   __out   u32 clk_rate;`  
`   __in    u32 module_id;`  
` };`

### NVHOST\_IOCTL\_CHANNEL\_MAP\_CMD\_BUFFER\_EX

Same as
[NVHOST\_IOCTL\_CHANNEL\_MAP\_CMD\_BUFFER](#NVHOST_IOCTL_CHANNEL_MAP_CMD_BUFFER "wikilink"),
but calls **nvmap\_unpin** internally in case of error.

### NVHOST\_IOCTL\_CHANNEL\_UNMAP\_CMD\_BUFFER\_EX

Same as
[NVHOST\_IOCTL\_CHANNEL\_UNMAP\_CMD\_BUFFER](#NVHOST_IOCTL_CHANNEL_UNMAP_CMD_BUFFER "wikilink").

### NVGPU\_IOCTL\_CHANNEL\_SET\_NVMAP\_FD

Binds a nvmap object to this channel. Identical to Linux driver.

` struct {`  
`   __in u32 nvmap_fd;`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO

Allocates gpfifo entries. Identical to Linux driver.

` struct {`  
`   __in u32 num_entries;`  
`   __in u32 flags;`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO

Submits a gpfifo object. Modified to take inline entry objects instead
of a pointer.

` struct fence {`  
`   u32 syncpt_id;`  
`   u32 syncpt_value;`  
` };`  
` `  
` struct gpfifo_entry {`  
`   u64 entry;                               // gpu_iova | (unk_2bits << 40) | (size << 42) | (unk_flag << 63)`  
` };`  
` `  
` struct {`  
`   __in    u64 gpfifo;                      // (ignored) pointer to gpfifo fence structs`  
`   __in    u32 num_entries;                 // number of fence objects being submitted`  
`   __in    u32 flags;`  
`   __inout struct fence fence_out;          // returned new fence object for others to wait on`  
`   __in    struct gpfifo_entry entries[];   // depends on num_entries`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ALLOC\_OBJ\_CTX

Allocates a graphics context object. Modified to ignore object's ID.

You can only have one object context allocated at a time. You must have
bound an address space before using this.

` struct {`  
`   __in  u32 class_num;    // 0x902D=2d, 0xB197=3d, 0xB1C0=compute, 0xA140=kepler, 0xB0B5=DMA, 0xB06F=channel_gpfifo`  
`   __in  u32 flags;        // bit0: LOCKBOOST_ZERO`  
`   __out u64 obj_id;       // (ignored) used for FREE_OBJ_CTX ioctl, which is not supported`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ZCULL\_BIND

Binds a ZCULL context to the channel. Identical to Linux driver.

`struct {`  
`   __in u64 gpu_va;`  
`   __in u32 mode;         // 0=global, 1=no_ctxsw, 2=separate_buffer, 3=part_of_regular_buf`  
`   __in u32 padding;`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_SET\_ERROR\_NOTIFIER

Initializes the error notifier for this channel. Unlike for the Linux
kernel, the Switch driver cannot write to an arbitrary userspace buffer.
Thus new ioctls have been introduced to fetch the error information
rather than using a shared memory buffer.

` struct {`  
`   __in u64 offset;  // ignored`  
`   __in u64 size;    // ignored`  
`   __in u32 mem;     // must be non-zero to initialize, zero to de-initialize`  
`   __in u32 padding; // ignored`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_SET\_PRIORITY

Changes channel's priority. Identical to Linux driver.

` struct {`  
`   __in u32 priority;    // 0x32 is low, 0x64 is medium and 0x96 is high`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ENABLE

Enables the current channel. Identical to Linux driver.

### NVGPU\_IOCTL\_CHANNEL\_DISABLE

Disables the current channel. Identical to Linux driver.

### NVGPU\_IOCTL\_CHANNEL\_PREEMPT

Clears the FIFO pipe for this channel. Identical to Linux driver.

### NVGPU\_IOCTL\_CHANNEL\_FORCE\_RESET

Forces the channel to reset. Identical to Linux driver.

### NVGPU\_IOCTL\_CHANNEL\_EVENT\_ID\_CONTROL

Controls event notifications.

` struct {`  
`   __in u32 cmd;    // 0=disable, 1=enable, 2=clear`  
`   __in u32 id;     // same id's as for `[`#QueryEvent`](#QueryEvent "wikilink")  
` };`

### NVGPU\_IOCTL\_CHANNEL\_GET\_ERROR\_NOTIFICATION

Returns the current error notification caught by the error notifier.
Exclusive to the Switch.

Despite being marked as inout this is all output.

` struct {`  
`   __out u64 timestamp;    // fetched straight from armGetSystemTick`  
`   __out u32 info32;       // error code`  
`   __out u16 info16;       // additional error info`  
`   __out u16 status;       // always 0xFFFF`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX

Allocates gpfifo entries with additional parameters. Exclusive to the
Switch.

`struct fence {`  
`  u32 syncpt_id;`  
`  u32 syncpt_value;`  
`};`  
  
`struct {`  
`  __in    u32 num_entries;`  
`  __in    u32 num_jobs;`  
`  __in    u32 flags;`  
`  __out   struct fence fence_out;          // returned new fence object for others to wait on`  
`  __in    u32 reserved[3];                 // ignored`  
`};`

### NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO\_RETRY

Submits a gpfifo object (async version). Exclusive to the Switch.

` struct fence {`  
`   u32 syncpt_id;`  
`   u32 syncpt_value;`  
` };`  
` `  
` struct gpfifo_entry {`  
`   u64 entry;                               // gpu_iova | (unk_2bits << 40) | (size << 42) | (unk_flag << 63)`  
` };`  
` `  
` struct {`  
`   __in    u64 gpfifo;                      // (ignored) pointer to gpfifo fence structs`  
`   __in    u32 num_entries;                 // number of fence objects being submitted`  
`   __in    u32 flags;`  
`   __inout struct fence fence_out;          // returned new fence object for others to wait on`  
`   __in    struct gpfifo_entry entries[];   // depends on num_entries`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX2

Same as
[NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX](#NVGPU_IOCTL_CHANNEL_ALLOC_GPFIFO_EX "wikilink").

### NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO\_EX

Identical to
[NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO](#NVGPU_IOCTL_CHANNEL_SUBMIT_GPFIFO "wikilink").
Uses [Ioctl2](#Ioctl2 "wikilink").

### NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO\_RETRY\_EX

Identical to
[NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO\_RETRY](#NVGPU_IOCTL_CHANNEL_SUBMIT_GPFIFO_RETRY "wikilink").
Uses [Ioctl2](#Ioctl2 "wikilink").

### NVGPU\_IOCTL\_CHANNEL\_SET\_TIMESLICE

Changes channel's timeslice. Identical to Linux driver.

` struct {`  
`   __in u32 timeslice;`  
` };`

# nvmemp

NVIDIA memory profiler (this service is not available on retail units).
/dev/nvhost-ctrl sends the ioctl NVHOST\_IOCTL\_CTRL\_GET\_CONFIG to
check the config "nv\!NV\_MEMORY\_PROFILER". If config\_str returns "1",
the applications attempts to talk to use nvmemp.

| Cmd | Name   |
| --- | ------ |
| 0   | Open   |
| 1   | GetPid |

# nvdrvdbg

This is "nns::nvdrv::INvDrvDebugFSServices".

| Cmd | Name                               |
| --- | ---------------------------------- |
| 0   | [\#OpenLog](#OpenLog "wikilink")   |
| 1   | [\#CloseLog](#CloseLog "wikilink") |
| 2   | [\#ReadLog](#ReadLog "wikilink")   |
| 3   |                                    |
| 4   |                                    |

## OpenLog

Takes process handle. Returns an fd.

## CloseLog

Takes fd and closes it.

## ReadLog

Takes fd and reads log into a type-6 buffer.

# nvgem:c

This is "nv::gemcontrol::INvGemControl".

| Cmd               | Name       |
| ----------------- | ---------- |
| 0                 |            |
| 1                 |            |
| 2                 |            |
| 3                 |            |
| 4                 |            |
| \[1.0.0-4.1.0\] 5 |            |
| 6                 |            |
| 7                 | \[3.0.0+\] |

# nvgem:cd

This is "nv::gemcoredump::INvGemCoreDump".

| Cmd               | Name       |
| ----------------- | ---------- |
| 0                 |            |
| 1                 |            |
| \[1.0.0-8.1.0\] 2 |            |
| 3                 | \[8.0.0+\] |
| 4                 | \[8.0.0+\] |

# Errors

Most nvidia driver commands return an error code apart from the normal
return code.

| Cmd     | Name                 |
| ------- | -------------------- |
| 0       | Success              |
| 1       | NotImplemented       |
| 2       | NotSupported         |
| 3       | NotInitialized       |
| 4       | BadParameter         |
| 5       | Timeout              |
| 6       | InsufficientMemory   |
| 7       | ReadOnlyAttribute    |
| 8       | InvalidState         |
| 9       | InvalidAddress       |
| 0xA     | InvalidSize          |
| 0xB     | BadValue             |
| 0xD     | AlreadyAllocated     |
| 0xE     | Busy                 |
| 0xF     | ResourceError        |
| 0x10    | CountMismatch        |
| 0x1000  | SharedMemoryTooSmall |
| 0x30003 | FileOperationFailed  |
| 0x30004 | DirOperationFailed   |
| 0x3000F | IoctlFailed          |
| 0x30010 | AccessDenied         |
| 0x30013 | FileNotFound         |
| 0xA000E | ModuleNotPresent     |

# Panic

In some cases, a panic may occur. NV forces a crash by doing:

`(void *)0 = 0xCAFE;`

End result is that the system hangs with a white-screen.

## Gpfifo Panic

When the gpfifo data in the gpu\_va buffers specified by the submitted
gpfifo entries is invalid(?), eventually the user-process will be
force-terminated after using the submit-gpfifo ioctl. It's unknown how
exactly this is done.

[Category:Services](Category:Services "wikilink")
