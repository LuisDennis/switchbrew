The only image data contained in this sysmodule is basically a saved
display framebuffer, no image data for actively-used
layers/framebuffers.

# caps:sc

This is "nn::capsrv::sf::IScreenShotControlService". This is available
with
\[2.0.0+\].

| Cmd                  | Name         | Notes                                                                                                                                                        |
| -------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1                    |              |                                                                                                                                                              |
| 2                    |              |                                                                                                                                                              |
| 3                    | \[5.0.0+\] ? | Takes a total of 8-bytes of input, no output.                                                                                                                |
| 5                    | \[5.0.0+\] ? | Takes a total of 0x10-bytes of input, no output.                                                                                                             |
| 210                  | \[6.0.0+\] ? | Takes a total of 0x50-bytes of input, a type-0x15 input buffer, and a type-0x45 input buffer, returns a total of 0x20-bytes of output.                       |
| \[2.0.0-4.1.0\] 1001 |              | Takes a total of 0x10-bytes of input, no output.                                                                                                             |
| \[2.0.0-4.1.0\] 1002 |              | Takes a total of 0x18-bytes of input, no output.                                                                                                             |
| \[3.0.0-4.1.0\] 1003 |              | Takes a total of 0x58-bytes of input, no output.                                                                                                             |
| 1004                 | \[5.0.0+\] ? | Takes a total of 0x60-bytes of input, no output.                                                                                                             |
| 1009                 | \[5.0.0+\] ? | Takes a total of 0x10-bytes of input, no output.                                                                                                             |
| 1010                 | \[5.0.0+\] ? | Takes a total of 0x10-bytes of input, no output.                                                                                                             |
| 1011                 |              | Takes a total of 8-bytes of input, no output.                                                                                                                |
| 1012                 |              | Takes a total of 8-bytes of input, no output.                                                                                                                |
| 1101                 | \[4.0.0+\] ? | Takes a total of 0x28-bytes of input and two type-0x46 output buffers.                                                                                       |
| 1106                 | \[4.0.0+\] ? | Takes a total of 0x30-bytes of input, two type-0x15 input buffers, a type-0x6 output buffer, and two type-0x46 output buffers, returns 0x18-bytes of output. |
| 1107                 | \[4.0.0+\] ? | Takes a total of 0x30-bytes of input, two type-0x15 input buffers, a type-0x6 output buffer, and a type-0x45 input buffer, returns 0x18-bytes of output.     |
| 1201                 | \[3.0.0+\] ? | Takes a total of 0x10-bytes of input, returns a total of 0x18-bytes of output.                                                                               |
| 1202                 | \[3.0.0+\] ? | No input/output.                                                                                                                                             |
| 1203                 | \[3.0.0+\] ? | Takes a total of 8-bytes of input and a type-0x6 output buffer, returns a total of 8-bytes of output.                                                        |

## Cmd1

Takes a type-0x46 output buffer, an input u32, two input u64s
**width**/**height**, an input s64 **buffer\_count**, and an input s64
**buffer\_index**.

**width**/**height** must match 1280/720. **buffer\_index** must be \<
**buffer\_count**. **buffer\_index** and **buffer\_count** must not be
negative.

**buffer\_index** and **buffer\_count** correspond to buffers with size
0x384000(1280\*720\*4).

Value 0 is usable for the input u32.

This takes a screenshot, the output buffer contains the RGBA8 image.

Stubbed with \[5.0.0+\], where it now returns error 0x7FECE.

## Cmd2

Calls the same internal func as cmd1, where the last param is an
additional cmd input u64 instead of hard-coded value 0x5f5e100.

Stubbed with \[5.0.0+\], where it now returns error 0x7FECE.

# caps:ss

This is "nn::capsrv::sf::IScreenShotService". This is available with
\[2.0.0+\].

| Cmd | Name |
| --- | ---- |
| 201 |      |
| 202 |      |
| 203 |      |
| 204 |      |

# caps:su

This is "nn::capsrv::sf::IScreenShotApplicationService".

| Cmd | Name                         |
| --- | ---------------------------- |
| 201 | SaveScreenShot               |
| 203 | SaveScreenShotEx0            |
| 210 | \[6.0.0+\] SaveScreenShotEx2 |

# cec-mgr

This is "nn::cec::ICecManager".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |
| 4   |      |
| 5   |      |
| 6   |      |

# mm:u

This is "nn::mmnv::IRequest".

NVIDIA multimedia (NvMM) platform service.

| Cmd | Name          |
| --- | ------------- |
| 0   | InitializeOld |
| 1   | FinalizeOld   |
| 2   | SetAndWaitOld |
| 3   | GetOld        |
| 4   | Initialize    |
| 5   | Finalize      |
| 6   | SetAndWait    |
| 7   | Get           |

# vi:u

This is "nn::visrv::sf::IApplicationRootService".

| Cmd | Name                                  |
| --- | ------------------------------------- |
| 0   | [GetDisplayService](#vi:u "wikilink") |
|     |                                       |

## GetDisplayService

Returns an
[\#IApplicationDisplayService](#IApplicationDisplayService "wikilink").
Takes an input u32, user-processes use 0 or 1, with 0 for
regular-applications normally. 0 = user-service(vi:u), 1 =
non-user-service? Returns an error when using value 1 with vi:u(same
error listed below for IApplicationDisplayService for unavailable
commands).

# vi:s

This is "nn::visrv::sf::ISystemRootService".

| Cmd | Name                                                       |
| --- | ---------------------------------------------------------- |
| 1   | [GetDisplayService](#vi:s "wikilink")                      |
| 3   | [GetDisplayServiceWithProxyNameExchange](#vi:s "wikilink") |
|     |                                                            |

## GetDisplayService

Returns an
[\#IApplicationDisplayService](#IApplicationDisplayService "wikilink").
Same input as vi:u.

## GetDisplayServiceWithProxyNameExchange

Returns an
[\#IApplicationDisplayService](#IApplicationDisplayService "wikilink").

# vi:m

This is "nn::visrv::sf::IManagerRootService".

| Cmd | Name                                                       |
| --- | ---------------------------------------------------------- |
| 2   | [GetDisplayService](#vi:m "wikilink")                      |
| 3   | [GetDisplayServiceWithProxyNameExchange](#vi:m "wikilink") |
|     |                                                            |

## GetDisplayService

Returns an
[\#IApplicationDisplayService](#IApplicationDisplayService "wikilink").
Same input as vi:u.

## GetDisplayServiceWithProxyNameExchange

Takes an input u64 and u32. Returns an
[\#IApplicationDisplayService](#IApplicationDisplayService "wikilink").

# IApplicationDisplayService

This is
"nn::visrv::sf::IApplicationDisplayService".

| Cmd  | Name                                                                                                  |
| ---- | ----------------------------------------------------------------------------------------------------- |
| 100  | [\#GetRelayService](#GetRelayService "wikilink")                                                      |
| 101  | [\#GetSystemDisplayService](#GetSystemDisplayService "wikilink")                                      |
| 102  | [\#GetManagerDisplayService](#GetManagerDisplayService "wikilink")                                    |
| 103  | \[2.0.0+\] [\#GetIndirectDisplayTransactionService](#GetIndirectDisplayTransactionService "wikilink") |
| 1000 | [\#ListDisplays](#ListDisplays "wikilink")                                                            |
| 1010 | [\#OpenDisplay](#OpenDisplay "wikilink")                                                              |
| 1011 | [\#OpenDefaultDisplay](#OpenDefaultDisplay "wikilink")                                                |
| 1020 | [\#CloseDisplay](#CloseDisplay "wikilink")                                                            |
| 1101 | [\#SetDisplayEnabled](#SetDisplayEnabled "wikilink")                                                  |
| 1102 | [\#GetDisplayResolution](#GetDisplayResolution "wikilink")                                            |
| 2020 | [\#OpenLayer](#OpenLayer "wikilink")                                                                  |
| 2021 | [\#CloseLayer](#CloseLayer "wikilink")                                                                |
| 2030 | [\#CreateStrayLayer](#CreateStrayLayer "wikilink")                                                    |
| 2031 | [\#DestroyStrayLayer](#DestroyStrayLayer "wikilink")                                                  |
| 2101 | [\#SetLayerScalingMode](#SetLayerScalingMode "wikilink")                                              |
| 2102 | \[5.0.0+\] ConvertScalingMode                                                                         |
| 2450 | [\#GetIndirectLayerImageMap](#GetIndirectLayerImageMap "wikilink")                                    |
| 2451 | [\#GetIndirectLayerImageCropMap](#GetIndirectLayerImageCropMap "wikilink")                            |
| 2460 | [\#GetIndirectLayerImageRequiredMemoryInfo](#GetIndirectLayerImageRequiredMemoryInfo "wikilink")      |
| 5202 | [\#GetDisplayVsyncEvent](#GetDisplayVsyncEvent "wikilink")                                            |
| 5203 | [\#GetDisplayVsyncEventForDebug](#GetDisplayVsyncEventForDebug "wikilink")                            |
|      |                                                                                                       |

Available sessions for each service:

  - "vi:u": Only GetRelayService.
  - "vi:s": Everything except GetManagerDisplayService.
  - "vi:m": All.

When attempting to use a get-session cmd with a service it's not
available with, error 0xA72 is returned.

These commands using PIDs have AppletResourceUserId as the last input
u64, hence AppletResourceUserId must
[match](IPC%20Marshalling.md "wikilink") the user-process PID(no special
handling for value 0).

## GetRelayService

Returns an
[IHOSBinderDriver](Nvnflinger%20services#dispdrv.md##dispdrv "wikilink")
interface which abstracts "nn::visrv::<service::RelayServiceImpl>".

## GetIndirectDisplayTransactionService

Returns an
[IHOSBinderDriver](Nvnflinger%20services#dispdrv.md##dispdrv "wikilink")
interface which abstracts
"nn::visrv::<service::IndirectDisplayTransactionServiceImpl>".

## GetSystemDisplayService

Returns an [\#ISystemDisplayService](#ISystemDisplayService "wikilink").

## GetManagerDisplayService

Returns an
[\#IManagerDisplayService](#IManagerDisplayService "wikilink").

## ListDisplays

Takes a type-0x6 output buffer containing the array of
[\#DisplayInfo](#DisplayInfo "wikilink") output entries. Returns an
output u64: total number of output entries.

Normally(?) this only returns the "Default" display.

## OpenDisplay

Takes a [\#DisplayName](#DisplayName "wikilink") as input. Returns an
output u64, the DisplayId.

To open the default display, input string "Default" can be used.

## OpenDefaultDisplay

Returns an output u64.

Probably not (?) used by newer official user-processes, since those use
OpenDisplay with the default string instead.

## CloseDisplay

Takes an input u64, DisplayId.

## SetDisplayEnabled

Takes an input u32 boolean, and an u64 DisplayId.

## GetDisplayResolution

Takes an input u64 DisplayId and returns two output u64s: width and
height.

## OpenLayer

Takes a PID-descriptor, a type-0x6 buffer for the output
[\#NativeWindow](#NativeWindow "wikilink"), a
[\#DisplayName](#DisplayName "wikilink")(which was previously used with
[\#OpenDisplay](#OpenDisplay "wikilink")), an u64 LayerId, and an u64
[AppletResourceUserId](AM%20services.md "wikilink"). Returns an output
u64 NativeWindow\_Size.

Official user-processes use a LayerId stored in a global state
field("...ExternalLayerId") if non-zero, otherwise:

  - When AppletResourceUserId==0,
    [\#CreateStrayLayer](#CreateStrayLayer "wikilink") is used instead
    of the OpenLayer cmd.
  - When AppletResourceUserId\!=0,
    [AM\_services\#CreateManagedDisplayLayer](AM%20services#CreateManagedDisplayLayer.md##CreateManagedDisplayLayer "wikilink")
    is used and the output from that is used for LayerId with the
    OpenLayer cmd.

This OpenLayer command returns error 0x272 when the AppletResourceUserId
is invalid.

## CloseLayer

Takes an input u64: LayerId which was used with
[\#OpenLayer](#OpenLayer "wikilink").

## CreateStrayLayer

Takes a type-0x6 buffer for the output
[\#NativeWindow](#NativeWindow "wikilink"), an u32(LayerFlags bitmask),
and an u64 DisplayId. Returns two output u64s: LayerId and
NativeWindow\_Size.

## DestroyStrayLayer

Takes an input u64: LayerId from
[\#CreateStrayLayer](#CreateStrayLayer "wikilink").

## SetLayerScalingMode

Takes an input u64("ScalingMode") and u64 ("LayerId").

## GetIndirectLayerImageMap

Takes a PID-descriptor, an type-0x46 buffer, and four u64s: width(s32),
height(s32), \<output from [AM](AM%20services.md "wikilink")
GetIndirectLayerConsumerHandle\>, and
[AppletResourceUserId](AM%20services.md "wikilink"). Returns two output
u64s.

Calls the same func as
[\#GetIndirectLayerImageCropMap](#GetIndirectLayerImageCropMap "wikilink")
internally, with the input floats set to 0.0f, then 1.0f for the rest.

## GetIndirectLayerImageCropMap

Takes a PID-descriptor, an type-0x46 buffer, four floats, four u64s(last
u64 is [AppletResourceUserId](AM%20services.md "wikilink")). Returns two
output u64s. The floats are stored immediately after each other(32bits).

## GetIndirectLayerImageRequiredMemoryInfo

Takes two input u64s: width and height. Returns two output u64s. First
u64 is the buffer size to use with the ImageMap cmds, second u64 is the
buffer address alignment for those cmds.

## GetDisplayVsyncEvent

Takes an input u64 DisplayId and returns a handle.

## GetDisplayVsyncEventForDebug

Takes an input u64 DisplayId and returns a handle.

## ISystemDisplayService

This is
"nn::visrv::sf::ISystemDisplayService".

| Cmd                  | Name                                           |
| -------------------- | ---------------------------------------------- |
| 1200                 | GetZOrderCountMin                              |
| 1202                 | GetZOrderCountMax                              |
| 1203                 | GetDisplayLogicalResolution                    |
| 1204                 | SetDisplayMagnification                        |
| 2201                 | SetLayerPosition                               |
| 2203                 | SetLayerSize                                   |
| 2204                 | GetLayerZ                                      |
| 2205                 | SetLayerZ                                      |
| 2207                 | SetLayerVisibility                             |
| 2209                 | SetLayerAlpha                                  |
| \[1.0.0-6.2.0\] 2312 | CreateStrayLayer                               |
| 2400                 | OpenIndirectLayer                              |
| 2401                 | CloseIndirectLayer                             |
| 2402                 | FlipIndirectLayer                              |
| 3000                 | ListDisplayModes                               |
| 3001                 | ListDisplayRgbRanges                           |
| 3002                 | ListDisplayContentTypes                        |
| 3200                 | GetDisplayMode                                 |
| 3201                 | SetDisplayMode                                 |
| 3202                 | GetDisplayUnderscan                            |
| 3203                 | SetDisplayUnderscan                            |
| 3204                 | GetDisplayContentType                          |
| 3205                 | SetDisplayContentType                          |
| 3206                 | GetDisplayRgbRange                             |
| 3207                 | SetDisplayRgbRange                             |
| 3208                 | GetDisplayCmuMode                              |
| 3209                 | SetDisplayCmuMode                              |
| 3210                 | GetDisplayContrastRatio                        |
| 3211                 | SetDisplayContrastRatio                        |
| 3214                 | GetDisplayGamma                                |
| 3215                 | SetDisplayGamma                                |
| 3216                 | GetDisplayCmuLuma                              |
| 3217                 | SetDisplayCmuLuma                              |
| 8225                 | \[4.0.0+\] GetSharedBufferMemoryHandleId       |
| 8250                 | \[4.0.0+\] OpenSharedLayer                     |
| 8251                 | \[4.0.0+\] CloseSharedLayer                    |
| 8252                 | \[4.0.0+\] ConnectSharedLayer                  |
| 8253                 | \[4.0.0+\] DisconnectSharedLayer               |
| 8254                 | \[4.0.0+\] AcquireSharedFrameBuffer            |
| 8255                 | \[4.0.0+\] PresentSharedFrameBuffer            |
| 8256                 | \[4.0.0+\] GetSharedFrameBufferAcquirableEvent |
| 8257                 | \[4.0.0+\] FillSharedFrameBufferColor          |
| 8258                 | \[5.0.0+\] CancelSharedFrameBuffer             |

## IManagerDisplayService

This is "nn::visrv::sf::IManagerDisplayService".

| Cmd  | Name                                                       |
| ---- | ---------------------------------------------------------- |
| 200  | \[4.0.0+\] AllocateProcessHeapBlock                        |
| 201  | \[4.0.0+\] FreeProcessHeapBlock                            |
| 1102 | GetDisplayResolution                                       |
| 2010 | CreateManagedLayer                                         |
| 2011 | DestroyManagedLayer                                        |
| 2012 | \[7.0.0+\] CreateStrayLayer                                |
| 2050 | CreateIndirectLayer                                        |
| 2051 | DestroyIndirectLayer                                       |
| 2052 | CreateIndirectProducerEndPoint                             |
| 2053 | DestroyIndirectProducerEndPoint                            |
| 2054 | CreateIndirectConsumerEndPoint                             |
| 2055 | DestroyIndirectConsumerEndPoint                            |
| 2300 | AcquireLayerTexturePresentingEvent                         |
| 2301 | ReleaseLayerTexturePresentingEvent                         |
| 2302 | GetDisplayHotplugEvent                                     |
| 2402 | GetDisplayHotplugState                                     |
| 2501 | \[4.0.0+\] GetCompositorErrorInfo                          |
| 2601 | \[4.0.0+\] GetDisplayErrorEvent                            |
| 4201 | SetDisplayAlpha                                            |
| 4203 | SetDisplayLayerStack                                       |
| 4205 | SetDisplayPowerState                                       |
| 4206 | \[4.0.0+\] SetDefaultDisplay                               |
| 6000 | AddToLayerStack                                            |
| 6001 | RemoveFromLayerStack                                       |
| 6002 | SetLayerVisibility                                         |
| 6003 | \[5.0.0+\] SetLayerConfig                                  |
| 6004 | \[5.0.0+\] AttachLayerPresentationTracer                   |
| 6005 | \[5.0.0+\] DetachLayerPresentationTracer                   |
| 6006 | \[5.0.0+\] StartLayerPresentationRecording                 |
| 6007 | \[5.0.0+\] StopLayerPresentationRecording                  |
| 6008 | \[5.0.0+\] StartLayerPresentationFenceWait                 |
| 6009 | \[5.0.0+\] StopLayerPresentationFenceWait                  |
| 6010 | \[5.0.0+\] GetLayerPresentationAllFencesExpiredEvent       |
| 7000 | SetContentVisibility                                       |
| 8000 | SetConductorLayer                                          |
| 8100 | SetIndirectProducerFlipOffset                              |
| 8200 | \[4.0.0+\] CreateSharedBufferStaticStorage                 |
| 8201 | \[4.0.0+\] CreateSharedBufferTransferMemory                |
| 8202 | \[4.0.0+\] DestroySharedBuffer                             |
| 8203 | \[4.0.0+\] BindSharedLowLevelLayerToManagedLayer           |
| 8204 | \[4.0.0+\] BindSharedLowLevelLayerToIndirectLayer          |
| 8207 | \[4.0.0+\] UnbindSharedLowLevelLayer                       |
| 8208 | \[4.0.0+\] ConnectSharedLowLevelLayerToSharedBuffer        |
| 8209 | \[4.0.0+\] DisconnectSharedLowLevelLayerFromSharedBuffer   |
| 8210 | \[4.0.0+\] CreateSharedLayer                               |
| 8211 | \[4.0.0+\] DestroySharedLayer                              |
| 8216 | \[4.0.0+\] AttachSharedLayerToLowLevelLayer                |
| 8217 | \[4.0.0+\] ForceDetachSharedLayerFromLowLevelLayer         |
| 8218 | \[4.0.0+\] StartDetachSharedLayerFromLowLevelLayer         |
| 8219 | \[4.0.0+\] FinishDetachSharedLayerFromLowLevelLayer        |
| 8220 | \[4.0.0+\] GetSharedLayerDetachReadyEvent                  |
| 8221 | \[4.0.0+\] GetSharedLowLevelLayerSynchronizedEvent         |
| 8222 | \[4.0.0+\] CheckSharedLowLevelLayerSynchronized            |
| 8223 | \[4.0.0+\] RegisterSharedBufferImporterAruid               |
| 8224 | \[4.0.0+\] UnregisterSharedBufferImporterAruid             |
| 8227 | \[4.0.0+\] CreateSharedBufferProcessHeap                   |
| 8228 | \[4.0.0+\] GetSharedLayerLayerStacks                       |
| 8229 | \[4.0.0+\] SetSharedLayerLayerStacks                       |
| 8291 | \[4.0.0+\] PresentDetachedSharedFrameBufferToLowLevelLayer |
| 8292 | \[4.0.0+\] FillDetachedSharedFrameBufferColor              |
| 8293 | \[4.0.0+\] GetDetachedSharedFrameBufferImage               |
| 8294 | \[4.0.0+\] SetDetachedSharedFrameBufferImage               |
| 8295 | \[4.0.0+\] CopyDetachedSharedFrameBufferImage              |
| 8296 | \[4.0.0+\] SetDetachedSharedFrameBufferSubImage            |
| 8297 | \[4.0.0+\] GetSharedFrameBufferContentParameter            |
| 8298 | \[5.0.0+\] ExpandStartupLogoOnSharedFrameBuffer            |

# DisplayInfo

| Offset | Size | Description                                                                                               |
| ------ | ---- | --------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x40 | [\#DisplayName](#DisplayName "wikilink")                                                                  |
| 0x40   | 0x1  | Whether or not the display has a constrained number of layers.                                            |
| 0x41   | 0x7  | Padding/Reserved                                                                                          |
| 0x48   | 0x8  | If this display has a constrained number of layers (0x40 is set), indicates the maximum number of layers. |
| 0x50   | 0x8  | Width in pixels                                                                                           |
| 0x58   | 0x8  | Height in pixels                                                                                          |

This is a 0x60-byte structure.

The width/height for the "Default" Display is the resolution for 1080p
even when in handheld-mode.

# DisplayName

This is a 0x40-byte block: a NUL-terminated string.

Can be "Default", "External",
"[Edid](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data)",
"Internal" or "Null".

# Parcel

| Offset | Size | Description         |
| ------ | ---- | ------------------- |
| 0x0    | 0x4  | ParcelDataSize      |
| 0x4    | 0x4  | ParcelDataOffset    |
| 0x8    | 0x4  | ParcelObjectsSize   |
| 0xC    | 0x4  | ParcelObjectsOffset |
| 0x10   | ?    | FlattenedBinder     |

# NativeWindow

Max size of this buffer is 0x100-bytes(outbuf size used by official
user-processes). Parsed("...DeserializeNativeWindow()") by a function
called by the code described under [\#OpenLayer](#OpenLayer "wikilink"),
which executes code with Android symbols.

This is a [\#Parcel](#Parcel "wikilink").

## ParcelData

This normally contains the following:

| Offset | Size | Description                      |
| ------ | ---- | -------------------------------- |
| 0x0    | 0x4  | 0x2                              |
| 0x4    | 0x4  | Probably the user-process PID?   |
| 0x8    | 0x4  | ID                               |
| 0xC    | 0xC  | All-zero normally?               |
| 0x18   | 0x8  | NUL-terminated "dispdrv" string. |
| 0x20   | 0x8  | All-zero normally?               |

The above ID is used for the ID param for the binder commands with
[IHOSBinderDriver](#GetRelayService "wikilink").

## ParcelObjects

This normally contains an u32 with value 0?

# Resolution handling

There doesn't seem to be a way to get the actual TV resolution while
using the "Default" Display. Official apps just hard-code what
resolution to use depending on the current
[OperationMode](AM%20services.md "wikilink").

[Category:Services](Category:Services "wikilink")
