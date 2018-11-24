AM (Applet Manager) provides services for interacting with system
applets while abstracting several aspects of power and operation
management.

Contains multiple raw images, with at least the following:
"NN\_OMM\_CHARGING\_BIN\_{begin|end}"(charging icon), low-battery icon,
and the Nintendo Switch logo displayed during system boot.

# appletAE

This is
"nn::am::<service::IAllSystemAppletProxiesService>".

| Cmd  | Name                                                                      | Notes                                                                                        |
| ---- | ------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| 100  | OpenSystemAppletProxy                                                     | Returns an [\#ISystemAppletProxy](#ISystemAppletProxy "wikilink").                           |
| 200  | OpenLibraryAppletProxyOld (\[1.0.0-2.3.0\] OpenLibraryAppletProxy)        | Returns an [\#ILibraryAppletProxy](#ILibraryAppletProxy "wikilink").                         |
| 201  | \[3.0.0+\] [\#OpenLibraryAppletProxy](#OpenLibraryAppletProxy "wikilink") | Returns an [\#ILibraryAppletProxy](#ILibraryAppletProxy "wikilink").                         |
| 300  | OpenOverlayAppletProxy                                                    | Returns an [\#IOverlayAppletProxy](#IOverlayAppletProxy "wikilink").                         |
| 350  | OpenSystemApplicationProxy                                                | Returns an [\#IApplicationProxy](#IApplicationProxy "wikilink").                             |
| 400  | CreateSelfLibraryAppletCreatorForDevelop                                  | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").                     |
| 410  | \[6.0.0+\] GetSystemAppletControllerForDebug                              | Returns an [\#ISystemAppletControllerForDebug](#ISystemAppletControllerForDebug "wikilink"). |
| 1000 | \[6.0.0+\] GetDebugFunctions                                              | Returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").                                 |

All of these commands except
[\#OpenLibraryAppletProxy](#OpenLibraryAppletProxy "wikilink") take the
same input as
[\#OpenApplicationProxy](#OpenApplicationProxy "wikilink"), with the
same user-process retry-loop as
[\#OpenApplicationProxy](#OpenApplicationProxy "wikilink"). These
Open\*Proxy commands (including appletOE) doesn't seem to usable from
processes which aren't actual applets (such as sysmodules), at least for
applet-types which aren't already in use.

This service is used by all system non-regular-applications.

The 01000000000010XX system [titles](Title%20list.md "wikilink") use the
following applet types(above Open{type}Proxy commands):

  - "qlaunch": SystemApplet
  - "overlay": OverlayApplet
  - "starter": SystemApplication
  - "maintenance": SystemApplet
  - All others: LibraryApplet

## OpenLibraryAppletProxy

Returns an [\#ILibraryAppletProxy](#ILibraryAppletProxy "wikilink").

Takes a [reserved](IPC%20Marshalling.md "wikilink") input u64(official
user-processes use hard-coded value 0), a PID,a process
copy-handle(cur-proc handle alias), and an 0x80-byte type-0x15 input
buffer **AppletAttribute**.

Official user-processes use the same retry loop with this as the other
Open\*Proxy
commands.

## ISystemAppletProxy

| Cmd  | Name                        | Notes                                                                            |
| ---- | --------------------------- | -------------------------------------------------------------------------------- |
| 0    | GetCommonStateGetter        | Returns an [\#ICommonStateGetter](#ICommonStateGetter "wikilink").               |
| 1    | GetSelfController           | Returns an [\#ISelfController](#ISelfController "wikilink").                     |
| 2    | GetWindowController         | Returns an [\#IWindowController](#IWindowController "wikilink").                 |
| 3    | GetAudioController          | Returns an [\#IAudioController](#IAudioController "wikilink").                   |
| 4    | GetDisplayController        | Returns an [\#IDisplayController](#IDisplayController "wikilink").               |
| 10   | GetProcessWindingController | Returns an [\#IProcessWindingController](#IProcessWindingController "wikilink"). |
| 11   | GetLibraryAppletCreator     | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").         |
| 20   | GetHomeMenuFunctions        | Returns an [\#IHomeMenuFunctions](#IHomeMenuFunctions "wikilink").               |
| 21   | GetGlobalStateController    | Returns an [\#IGlobalStateController](#IGlobalStateController "wikilink").       |
| 22   | GetApplicationCreator       | Returns an [\#IApplicationCreator](#IApplicationCreator "wikilink").             |
| 1000 | GetDebugFunctions           | Returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").                     |

### IHomeMenuFunctions

| Cmd | Name                                           | Notes                                                    |
| --- | ---------------------------------------------- | -------------------------------------------------------- |
| 10  | RequestToGetForeground                         |                                                          |
| 11  | LockForeground                                 |                                                          |
| 12  | UnlockForeground                               |                                                          |
| 20  | PopFromGeneralChannel                          | Returns an [\#IStorage](#IStorage "wikilink").           |
| 21  | GetPopFromGeneralChannelEvent                  |                                                          |
| 30  | GetHomeButtonWriterLockAccessor                | Returns an [\#ILockAccessor](#ILockAccessor "wikilink"). |
| 31  | \[2.0.0+\] GetWriterLockAccessorEx             | Returns an [\#ILockAccessor](#ILockAccessor "wikilink"). |
| 100 | \[6.0.0+\] PopRequestLaunchApplicationForDebug |                                                          |

#### ILockAccessor

| Cmd | Name     |
| --- | -------- |
| 1   | TryLock  |
| 2   | Unlock   |
| 3   | GetEvent |

### IGlobalStateController

| Cmd | Name                                         |
| --- | -------------------------------------------- |
| 0   | RequestToEnterSleep                          |
| 1   | EnterSleep                                   |
| 2   | StartSleepSequence                           |
| 3   | StartShutdownSequence                        |
| 4   | StartRebootSequence                          |
| 10  | LoadAndApplyIdlePolicySettings               |
| 11  | \[2.0.0+\] NotifyCecSettingsChanged          |
| 12  | \[2.0.0+\] SetDefaultHomeButtonLongPressTime |
| 13  | \[2.0.0+\] UpdateDefaultDisplayResolution    |
| 14  | \[2.0.0+\] ShouldSleepOnBoot                 |
| 15  | \[4.0.0+\] GetHdcpAuthenticationFailedEvent  |

### IApplicationCreator

| Cmd | Name                                 | Notes                                                                  |
| --- | ------------------------------------ | ---------------------------------------------------------------------- |
| 0   | CreateApplication                    | Returns an [\#IApplicationAccessor](#IApplicationAccessor "wikilink"). |
| 1   | PopLaunchRequestedApplication        | Returns an [\#IApplicationAccessor](#IApplicationAccessor "wikilink"). |
| 10  | CreateSystemApplication              | Returns an [\#IApplicationAccessor](#IApplicationAccessor "wikilink"). |
| 100 | PopFloatingApplicationForDevelopment | Returns an [\#IApplicationAccessor](#IApplicationAccessor "wikilink"). |

#### IApplicationAccessor

| Cmd | Name                                       | Notes                                                        |
| --- | ------------------------------------------ | ------------------------------------------------------------ |
| 0   | GetAppletStateChangedEvent                 |                                                              |
| 1   | IsCompleted                                |                                                              |
| 10  | Start                                      |                                                              |
| 20  | RequestExit                                |                                                              |
| 25  | Terminate                                  |                                                              |
| 30  | GetResult                                  |                                                              |
| 101 | RequestForApplicationToGetForeground       |                                                              |
| 110 | TerminateAllLibraryApplets                 |                                                              |
| 111 | AreAnyLibraryAppletsLeft                   |                                                              |
| 112 | GetCurrentLibraryApplet                    | Returns an [\#IAppletAccessor](#IAppletAccessor "wikilink"). |
| 120 | GetApplicationId                           |                                                              |
| 121 | PushLaunchParameter                        | Takes an [\#IStorage](#IStorage "wikilink").                 |
| 122 | GetApplicationControlProperty              |                                                              |
| 123 | \[2.0.0+\] GetApplicationLaunchProperty    |                                                              |
| 124 | \[6.0.0+\] GetApplicationLaunchRequestInfo |                                                              |
| 130 | \[6.0.0+\] SetUsers                        |                                                              |
| 131 | \[6.0.0+\] CheckRightsEnvironmentAvailable |                                                              |
| 132 | \[6.0.0+\] GetNsRightsEnvironmentHandle    |                                                              |
| 140 | \[6.0.0+\] GetDesirableUids                |                                                              |
| 150 | \[6.0.0+\] ReportApplicationExitTimeout    |                                                              |

##### IAppletAccessor

| Cmd | Name                       |
| --- | -------------------------- |
| 0   | GetAppletStateChangedEvent |
| 1   | IsCompleted                |
| 10  | Start                      |
| 20  | RequestExit                |
| 25  | Terminate                  |
| 30  | GetResult                  |

## ILibraryAppletProxy

| Cmd  | Name                          | Notes                                                                              |
| ---- | ----------------------------- | ---------------------------------------------------------------------------------- |
| 0    | GetCommonStateGetter          | Returns an [\#ICommonStateGetter](#ICommonStateGetter "wikilink").                 |
| 1    | GetSelfController             | Returns an [\#ISelfController](#ISelfController "wikilink").                       |
| 2    | GetWindowController           | Returns an [\#IWindowController](#IWindowController "wikilink").                   |
| 3    | GetAudioController            | Returns an [\#IAudioController](#IAudioController "wikilink").                     |
| 4    | GetDisplayController          | Returns an [\#IDisplayController](#IDisplayController "wikilink").                 |
| 10   | GetProcessWindingController   | Returns an [\#IProcessWindingController](#IProcessWindingController "wikilink").   |
| 11   | GetLibraryAppletCreator       | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").           |
| 20   | OpenLibraryAppletSelfAccessor | Returns an [\#ILibraryAppletSelfAccessor](#ILibraryAppletSelfAccessor "wikilink"). |
| 1000 | GetDebugFunctions             | Returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").                       |

### ILibraryAppletSelfAccessor

| Cmd | Name                                                                                                        | Notes                                          |
| --- | ----------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| 0   | PopInData                                                                                                   | Returns an [\#IStorage](#IStorage "wikilink"). |
| 1   | PushOutData                                                                                                 | Takes an [\#IStorage](#IStorage "wikilink").   |
| 2   | PopInteractiveInData                                                                                        | Returns an [\#IStorage](#IStorage "wikilink"). |
| 3   | PushInteractiveOutData                                                                                      | Takes an [\#IStorage](#IStorage "wikilink").   |
| 5   | GetPopInDataEvent                                                                                           |                                                |
| 6   | GetPopInteractiveInDataEvent                                                                                |                                                |
| 10  | [\#ExitProcessAndReturn](#ExitProcessAndReturn "wikilink")                                                  |                                                |
| 11  | [\#GetLibraryAppletInfo](#GetLibraryAppletInfo "wikilink")                                                  |                                                |
| 12  | GetMainAppletIdentityInfo                                                                                   |                                                |
| 13  | CanUseApplicationCore                                                                                       |                                                |
| 14  | GetCallerAppletIdentityInfo                                                                                 |                                                |
| 15  | \[2.0.0+\] GetMainAppletApplicationControlProperty                                                          |                                                |
| 16  | \[2.0.0+\] GetMainAppletStorageId                                                                           |                                                |
| 17  | \[2.0.0+\] GetCallerAppletIdentityInfoStack                                                                 |                                                |
| 18  | \[4.0.0+\] GetNextReturnDestinationAppletIdentityInfo                                                       |                                                |
| 19  | \[4.0.0+\] GetDesirableKeyboardLayout                                                                       |                                                |
| 20  | PopExtraStorage                                                                                             | Returns an [\#IStorage](#IStorage "wikilink"). |
| 25  | GetPopExtraStorageEvent                                                                                     |                                                |
| 30  | UnpopInData                                                                                                 | Takes an [\#IStorage](#IStorage "wikilink").   |
| 31  | UnpopExtraStorage                                                                                           | Takes an [\#IStorage](#IStorage "wikilink").   |
| 40  | \[2.0.0+\] GetIndirectLayerProducerHandle                                                                   |                                                |
| 50  | \[2.0.0+\] ReportVisibleError                                                                               |                                                |
| 51  | \[4.0.0+\] ReportVisibleErrorWithErrorContext                                                               |                                                |
| 60  | \[4.0.0+\] [\#GetMainAppletApplicationDesiredLanguage](#GetMainAppletApplicationDesiredLanguage "wikilink") |                                                |
| 80  | \[6.0.0+\] RequestExitToSelf                                                                                |                                                |
| 90  | \[5.0.0+\] CreateApplicationAndPushAndRequestToLaunch                                                       |                                                |
| 100 | \[4.0.0+\] [\#CreateGameMovieTrimmer](#CreateGameMovieTrimmer "wikilink")                                   |                                                |
| 101 | \[6.0.0+\] ReserveResourceForMovieOperation                                                                 |                                                |
| 102 | \[6.0.0+\] UnreserveResourceForMovieOperation                                                               |                                                |
| 110 | \[6.0.0+\] GetMainAppletAvailableUsers                                                                      |                                                |

#### ExitProcessAndReturn

No input/output.

Exits the LibraryApplet and returns to running the title which launched
this LibraryApplet ([qlaunch](Qlaunch.md "wikilink") for example).

#### GetLibraryAppletInfo

No input. Returns an u64 LibraryAppletInfo: +0 u32 is
[\#AppletId](#AppletId "wikilink"), +4 u32 is
[\#LibraryAppletMode](#LibraryAppletMode "wikilink").

#### GetMainAppletApplicationDesiredLanguage

No input, returns an output
[LanguageCode](Settings%20services#LanguageCode.md##LanguageCode "wikilink").

#### CreateGameMovieTrimmer

Takes an input u64 and handle, returns a GRC
[IGameMovieTrimmer](GRC%20services#IGameMovieTrimmer.md##IGameMovieTrimmer "wikilink").

## IOverlayAppletProxy

| Cmd  | Name                        | Notes                                                                            |
| ---- | --------------------------- | -------------------------------------------------------------------------------- |
| 0    | GetCommonStateGetter        | Returns an [\#ICommonStateGetter](#ICommonStateGetter "wikilink").               |
| 1    | GetSelfController           | Returns an [\#ISelfController](#ISelfController "wikilink").                     |
| 2    | GetWindowController         | Returns an [\#IWindowController](#IWindowController "wikilink").                 |
| 3    | GetAudioController          | Returns an [\#IAudioController](#IAudioController "wikilink").                   |
| 4    | GetDisplayController        | Returns an [\#IDisplayController](#IDisplayController "wikilink").               |
| 10   | GetProcessWindingController | Returns an [\#IProcessWindingController](#IProcessWindingController "wikilink"). |
| 11   | GetLibraryAppletCreator     | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").         |
| 20   | GetOverlayFunctions         | Returns an [\#IOverlayFunctions](#IOverlayFunctions "wikilink").                 |
| 1000 | GetDebugFunctions           | Returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").                     |

### IOverlayFunctions

| Cmd | Name                                             |
| --- | ------------------------------------------------ |
| 0   | BeginToWatchShortHomeButtonMessage               |
| 1   | EndToWatchShortHomeButtonMessage                 |
| 2   | GetApplicationIdForLogo                          |
| 3   | SetGpuTimeSliceBoost                             |
| 4   | \[2.0.0+\] SetAutoSleepTimeAndDimmingTimeEnabled |
| 5   | \[2.0.0+\] TerminateApplicationAndSetReason      |
| 6   | \[2.0.0+\] SetScreenShotPermissionGlobally       |
| 10  | \[6.0.0+\] StartShutdownSequenceForOverlay       |
| 11  | \[6.0.0+\] StartRebootSequenceForOverlay         |
| 101 | \[6.0.0+\] BeginToObserveHidInputForDevelop      |

## IApplicationProxy

| Cmd  | Name                        | Notes                                                                            |
| ---- | --------------------------- | -------------------------------------------------------------------------------- |
| 0    | GetCommonStateGetter        | Returns an [\#ICommonStateGetter](#ICommonStateGetter "wikilink").               |
| 1    | GetSelfController           | Returns an [\#ISelfController](#ISelfController "wikilink").                     |
| 2    | GetWindowController         | Returns an [\#IWindowController](#IWindowController "wikilink").                 |
| 3    | GetAudioController          | Returns an [\#IAudioController](#IAudioController "wikilink").                   |
| 4    | GetDisplayController        | Returns an [\#IDisplayController](#IDisplayController "wikilink").               |
| 10   | GetProcessWindingController | Returns an [\#IProcessWindingController](#IProcessWindingController "wikilink"). |
| 11   | GetLibraryAppletCreator     | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").         |
| 20   | GetApplicationFunctions     | Returns an [\#IApplicationFunctions](#IApplicationFunctions "wikilink").         |
| 1000 | GetDebugFunctions           | Returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").                     |

### IApplicationFunctions

| Cmd  | Name                                                                                  | Notes                                          |
| ---- | ------------------------------------------------------------------------------------- | ---------------------------------------------- |
| 1    | PopLaunchParameter                                                                    | Returns an [\#IStorage](#IStorage "wikilink"). |
| 10   | CreateApplicationAndPushAndRequestToStart                                             | Takes an [\#IStorage](#IStorage "wikilink").   |
| 11   | \[2.0.0+\] CreateApplicationAndPushAndRequestToStartForQuest                          | Takes an [\#IStorage](#IStorage "wikilink").   |
| 12   | \[4.0.0+\] CreateApplicationAndRequestToStart                                         |                                                |
| 13   | \[4.0.0+\] CreateApplicationAndRequestToStartForQuest                                 |                                                |
| 20   | EnsureSaveData                                                                        |                                                |
| 21   | [\#GetDesiredLanguage](#GetDesiredLanguage "wikilink")                                |                                                |
| 22   | [\#SetTerminateResult](#SetTerminateResult "wikilink")                                |                                                |
| 23   | GetDisplayVersion                                                                     |                                                |
| 24   | \[2.0.0+\] GetLaunchStorageInfoForDebug                                               |                                                |
| 25   | \[2.0.0+\] ExtendSaveData                                                             |                                                |
| 26   | \[2.0.0+\] GetSaveDataSize                                                            |                                                |
| 27   | \[5.0.0+\] CreateCacheStorage                                                         |                                                |
| 30   | BeginBlockingHomeButtonShortAndLongPressed                                            |                                                |
| 31   | EndBlockingHomeButtonShortAndLongPressed                                              |                                                |
| 32   | [\#BeginBlockingHomeButton](#BeginBlockingHomeButton "wikilink")                      |                                                |
| 33   | EndBlockingHomeButton                                                                 |                                                |
| 40   | [\#NotifyRunning](#NotifyRunning "wikilink")                                          |                                                |
| 50   | \[2.0.0+\] GetPseudoDeviceId                                                          |                                                |
| 60   | \[2.0.0+\] SetMediaPlaybackStateForApplication                                        |                                                |
| 65   | \[3.0.0+\] [\#IsGamePlayRecordingSupported](#IsGamePlayRecordingSupported "wikilink") |                                                |
| 66   | \[3.0.0+\] [\#InitializeGamePlayRecording](#InitializeGamePlayRecording "wikilink")   |                                                |
| 67   | \[3.0.0+\] [\#SetGamePlayRecordingState](#SetGamePlayRecordingState "wikilink")       |                                                |
| 68   | \[4.0.0+\] RequestFlushGamePlayingMovieForDebug                                       |                                                |
| 70   | \[3.0.0+\] RequestToShutdown                                                          |                                                |
| 71   | \[3.0.0+\] RequestToReboot                                                            |                                                |
| 80   | \[4.0.0+\] ExitAndRequestToShowThanksMessage                                          |                                                |
| 90   | \[4.0.0+\] EnableApplicationCrashReport                                               |                                                |
| 100  | \[5.0.0+\] InitializeApplicationCopyrightFrameBuffer                                  |                                                |
| 101  | \[5.0.0+\] SetApplicationCopyrightImage                                               |                                                |
| 102  | \[5.0.0+\] SetApplicationCopyrightVisibility                                          |                                                |
| 110  | \[5.0.0+\] QueryApplicationPlayStatistics                                             |                                                |
| 111  | \[6.0.0+\] QueryApplicationPlayStatisticsByUid                                        |                                                |
| 120  | \[5.0.0+\] ExecuteProgram                                                             |                                                |
| 121  | \[5.0.0+\] ClearUserChannel                                                           |                                                |
| 122  | \[5.0.0+\] UnpopToUserChannel                                                         |                                                |
| 123  | \[6.0.0+\] GetPreviousProgramIndex                                                    |                                                |
| 124  | \[6.0.0+\] EnableApplicationAllThreadDumpOnCrash                                      |                                                |
| 500  | \[5.0.0+\] StartContinuousRecordingFlushForDebug                                      |                                                |
| 1000 | \[5.0.0+\] [\#CreateMovieMaker](#CreateMovieMaker "wikilink")                         |                                                |
| 1001 | \[5.0.0+\] [\#PrepareForJit](#PrepareForJit "wikilink")                               |                                                |

The BOTW game uses this GamePlayRecording functionality from the
main-nso "nninitStartup" function, with size 0x6000000(96MiB). The
official GamePlayRecording-enable code does the following(this will
panic on any failure):

  - [Creates](SVC.md "wikilink") TransferMemory using the input buffer
    and size, with permissions=0.
  - Uses
    [\#InitializeGamePlayRecording](#InitializeGamePlayRecording "wikilink")
    with the TransferMemory.
  - Closes the TransferMemory handle, + TransferMemory cleanup.
  - Uses
    [\#SetGamePlayRecordingState](#SetGamePlayRecordingState "wikilink")
    with value 0x1.

This GamePlayRecording functionality presumably enables the
video-recording usable starting with [4.0.0](4.0.0.md "wikilink").

#### GetDesiredLanguage

No input, returns an output
[LanguageCode](Settings%20services#LanguageCode.md##LanguageCode "wikilink").

#### SetTerminateResult

Takes an input u32 **Result**, no output.

For example, in some cases official apps use this with
[error](Error%20codes.md "wikilink") 0x2A2 then uses svcBreak.

#### BeginBlockingHomeButton

Takes an input s64 nanoseconds, no output. The input nanoseconds can be
zero.

#### NotifyRunning

Takes no input. Returns an output u8, which is ignored by official
user-processes.

#### IsGamePlayRecordingSupported

No input, returns an output u8 bool.

#### InitializeGamePlayRecording

Takes a TransferMemory handle and an u64 for the size of the
TransferMemory. The size must match 0x6000000 otherwise an error is
returned.

#### SetGamePlayRecordingState

Takes an input u32. 0 = disable/pause, 1 = enable/restart.

#### CreateMovieMaker

Takes an input u64 and handle, returns an
[\#IMovieMaker](#IMovieMaker "wikilink").

#### PrepareForJit

Takes no input. Launches title 010000000000003B (currently not present
on retail systems) if some context variable is set.

### IMovieMaker

| Cmd | Name                                               |
| --- | -------------------------------------------------- |
| 0   | [\#GetGrcMovieMaker](#GetGrcMovieMaker "wikilink") |
| 1   | [\#GetLayerHandle](#GetLayerHandle "wikilink")     |

#### GetGrcMovieMaker

No input, returns a GRC [IMovieMaker](GRC%20services.md "wikilink").

#### GetLayerHandle

No input, returns an output
u64.

## ILibraryAppletCreator

| Cmd | Name                           | Notes                                                                      |
| --- | ------------------------------ | -------------------------------------------------------------------------- |
| 0   | CreateLibraryApplet            | Returns an [\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink"). |
| 1   | TerminateAllLibraryApplets     |                                                                            |
| 2   | AreAnyLibraryAppletsLeft       |                                                                            |
| 10  | CreateStorage                  | Returns an [\#IStorage](#IStorage "wikilink").                             |
| 11  | CreateTransferMemoryStorage    | Returns an [\#IStorage](#IStorage "wikilink").                             |
| 12  | \[2.0.0+\] CreateHandleStorage | Returns an [\#IStorage](#IStorage "wikilink").                             |

### ILibraryAppletAccessor

| Cmd | Name                                      | Notes                                          |
| --- | ----------------------------------------- | ---------------------------------------------- |
| 0   | GetAppletStateChangedEvent                |                                                |
| 1   | IsCompleted                               |                                                |
| 10  | Start                                     |                                                |
| 20  | RequestExit                               |                                                |
| 25  | Terminate                                 |                                                |
| 30  | GetResult                                 |                                                |
| 50  | SetOutOfFocusApplicationSuspendingEnabled |                                                |
| 100 | PushInData                                | Takes an [\#IStorage](#IStorage "wikilink").   |
| 101 | PopOutData                                | Returns an [\#IStorage](#IStorage "wikilink"). |
| 102 | PushExtraStorage                          | Takes an [\#IStorage](#IStorage "wikilink").   |
| 103 | PushInteractiveInData                     | Takes an [\#IStorage](#IStorage "wikilink").   |
| 104 | PopInteractiveOutData                     | Returns an [\#IStorage](#IStorage "wikilink"). |
| 105 | GetPopOutDataEvent                        |                                                |
| 106 | GetPopInteractiveOutDataEvent             |                                                |
| 110 | NeedsToExitProcess                        |                                                |
| 120 | GetLibraryAppletInfo                      |                                                |
| 150 | RequestForAppletToGetForeground           |                                                |
| 160 | \[2.0.0+\] GetIndirectLayerConsumerHandle |                                                |

## ICommonStateGetter

| Cmd | Name                                                          | Notes                                                    |
| --- | ------------------------------------------------------------- | -------------------------------------------------------- |
| 0   | [\#GetEventHandle](#GetEventHandle "wikilink")                |                                                          |
| 1   | [\#ReceiveMessage](#ReceiveMessage "wikilink")                |                                                          |
| 2   | GetThisAppletKind                                             |                                                          |
| 3   | AllowToEnterSleep                                             |                                                          |
| 4   | DisallowToEnterSleep                                          |                                                          |
| 5   | [\#GetOperationMode](#GetOperationMode "wikilink")            |                                                          |
| 6   | [\#GetPerformanceMode](#GetPerformanceMode "wikilink")        |                                                          |
| 7   | GetCradleStatus                                               |                                                          |
| 8   | GetBootMode                                                   |                                                          |
| 9   | [\#GetCurrentFocusState](#GetCurrentFocusState "wikilink")    |                                                          |
| 10  | RequestToAcquireSleepLock                                     |                                                          |
| 11  | ReleaseSleepLock                                              |                                                          |
| 12  | ReleaseSleepLockTransiently                                   |                                                          |
| 13  | GetAcquiredSleepLockEvent                                     |                                                          |
| 20  | PushToGeneralChannel                                          | Takes an [\#IStorage](#IStorage "wikilink").             |
| 30  | GetHomeButtonReaderLockAccessor                               | Returns an [\#ILockAccessor](#ILockAccessor "wikilink"). |
| 31  | \[2.0.0+\] GetReaderLockAccessorEx                            | Returns an [\#ILockAccessor](#ILockAccessor "wikilink"). |
| 40  | \[2.0.0+\] GetCradleFwVersion                                 |                                                          |
| 50  | \[3.0.0+\] IsVrModeEnabled                                    |                                                          |
| 51  | \[3.0.0+\] [\#SetVrModeEnabled](#SetVrModeEnabled "wikilink") |                                                          |
| 52  | \[4.0.0+\] SetLcdBacklighOffEnabled                           |                                                          |
| 55  | \[3.0.0+\] IsInControllerFirmwareUpdateSection                |                                                          |
| 60  | \[3.0.0+\] GetDefaultDisplayResolution                        |                                                          |
| 61  | \[3.0.0+\] GetDefaultDisplayResolutionChangeEvent             |                                                          |
| 62  | \[4.0.0+\] GetHdcpAuthenticationState                         |                                                          |
| 63  | \[4.0.0+\] GetHdcpAuthenticationStateChangeEvent              |                                                          |
| 64  | \[5.0.0+\] SetTvPowerStateMatchingMode                        |                                                          |
| 65  | \[6.0.0+\] GetApplicationIdByContentActionName                |                                                          |
| 66  | \[6.0.0+\] SetCpuAndGpuBoostMode                              |                                                          |
| 80  | \[6.0.0+\] PerformSystemButtonPressingIfInFocus               |                                                          |

Officially notification messages are handled by the application itself,
not sdk-nso in ExeFS. Official apps call code in sdk-nso which basically
uses svcWaitSynchronization with the event from
[\#GetEventHandle](#GetEventHandle "wikilink") to check whether a
message is available, then if so it uses
[\#ReceiveMessage](#ReceiveMessage "wikilink"). The actual handling for
message IDs is done in the app itself(see
[\#NotificationMessage](#NotificationMessage "wikilink")).

### GetEventHandle

No input. Returns an output event handle. This is signalled when a
message is available with
[\#ReceiveMessage](#ReceiveMessage "wikilink").

### ReceiveMessage

No input. Returns an output u32. Error 0x680 indicates no message is
available.

### GetOperationMode

No input. Returns an output u8 for the current
[\#OperationMode](#OperationMode "wikilink").

### GetPerformanceMode

No input. Returns an output u32 for the current PerformanceMode.

### GetCurrentFocusState

No input. Returns an output u8:

  - 1: In focus.
  - 2/3: Out of focus(running in "background").

### SetVrModeEnabled

Takes an input u8 bool flag. No output.

Updates internal AM state fields. If the new state doesn't match the
previous state, this uses the
[Backlight\_services](Backlight%20services.md "wikilink")
{Disable/Enable}VrMode command depending on whether
flag={disable/enable}.

When the VrMode is set to true, the console shows a screen rendered like
vr asking the user to move his face away and hit the 'close' button.
When this button is pressed, the console resets the vrMode to
false.

## ISelfController

| Cmd | Name                                                                                         |
| --- | -------------------------------------------------------------------------------------------- |
| 0   | [\#Exit](#Exit "wikilink")                                                                   |
| 1   | [\#LockExit](#LockExit "wikilink")                                                           |
| 2   | [\#UnlockExit](#UnlockExit "wikilink")                                                       |
| 3   | \[2.0.0+\] [\#EnterFatalSection](#EnterFatalSection "wikilink")                              |
| 4   | \[2.0.0+\] [\#LeaveFatalSection](#LeaveFatalSection "wikilink")                              |
| 9   | GetLibraryAppletLaunchableEvent                                                              |
| 10  | [\#SetScreenShotPermission](#SetScreenShotPermission "wikilink")                             |
| 11  | [\#SetOperationModeChangedNotification](#SetOperationModeChangedNotification "wikilink")     |
| 12  | [\#SetPerformanceModeChangedNotification](#SetPerformanceModeChangedNotification "wikilink") |
| 13  | [\#SetFocusHandlingMode](#SetFocusHandlingMode "wikilink")                                   |
| 14  | SetRestartMessageEnabled                                                                     |
| 15  | \[2.0.0+\] [\#SetScreenShotAppletIdentityInfo](#SetScreenShotAppletIdentityInfo "wikilink")  |
| 16  | \[2.0.0+\] [\#SetOutOfFocusSuspendingEnabled](#SetOutOfFocusSuspendingEnabled "wikilink")    |
| 17  | \[3.0.0+\] SetControllerFirmwareUpdateSection                                                |
| 18  | \[3.0.0+\] SetRequiresCaptureButtonShortPressedMessage                                       |
| 19  | \[3.0.0+\] [\#SetScreenShotImageOrientation](#SetScreenShotImageOrientation "wikilink")      |
| 20  | \[4.0.0+\] SetDesirableKeyboardLayout                                                        |
| 40  | [\#CreateManagedDisplayLayer](#CreateManagedDisplayLayer "wikilink")                         |
| 41  | \[4.0.0+\] IsSystemBufferSharingEnabled                                                      |
| 42  | \[4.0.0+\] GetSystemSharedLayerHandle                                                        |
| 43  | \[6.0.0+\] GetSystemSharedBufferHandle                                                       |
| 50  | SetHandlesRequestToDisplay                                                                   |
| 51  | ApproveToDisplay                                                                             |
| 60  | OverrideAutoSleepTimeAndDimmingTime                                                          |
| 61  | SetMediaPlaybackState                                                                        |
| 62  | SetIdleTimeDetectionExtension                                                                |
| 63  | GetIdleTimeDetectionExtension                                                                |
| 64  | SetInputDetectionSourceSet                                                                   |
| 65  | \[2.0.0+\] ReportUserIsActive                                                                |
| 66  | \[3.0.0+\] GetCurrentIlluminance                                                             |
| 67  | \[3.0.0+\] IsIlluminanceAvailable                                                            |
| 68  | \[4.0.0+\] SetAutoSleepDisabled                                                              |
| 69  | \[4.0.0+\] IsAutoSleepDisabled                                                               |
| 70  | \[5.0.0+\] ReportMultimediaError                                                             |
| 71  | \[6.0.0+\] GetCurrentIlluminanceEx                                                           |
| 80  | \[5.0.0+\] SetWirelessPriorityMode                                                           |
| 90  | \[6.0.0+\] GetAccumulatedSuspendedTickValue                                                  |
| 91  | \[6.0.0+\] GetAccumulatedSuspendedTickChangedEvent                                           |

### Exit

No input/output.

### LockExit

No input/output.

Locks exit process of pressing X to close in HOME Menu for an
application or HOME button for an applet. When locked, it will show the
"waiting for software to be closed dialog" until UnlockExit is called or
a 15 seconds timeout (when the latter occurs, the process is
force-terminated).

### UnlockExit

No input/output.

Unlocks exit process, if LockExit was previously used.

### EnterFatalSection

No input/output.

### LeaveFatalSection

No input/output.

### SetScreenShotPermission

Takes an input s32. No output.

Controls whether screenshot-capture is allowed. 0 = disable, 1 = enable,
2 = unknown.

### SetOperationModeChangedNotification

Takes an input u8 bool flag. No output.

### SetPerformanceModeChangedNotification

Takes an input u8 bool flag. No output.

### SetFocusHandlingMode

Takes 3 input u8s with each field located immediately after the previous
u8, these are bool flags. No output.

### SetScreenShotAppletIdentityInfo

Takes an input 0x10-byte struct AppletIdentityInfo. No output.

### SetOutOfFocusSuspendingEnabled

Takes an input u8(bool flag). No output.

### SetScreenShotImageOrientation

Takes an input s32. No output.

### CreateManagedDisplayLayer

Returns an output u64 LayerId which is then used by the user-process
with
[Display\_services\#OpenLayer](Display%20services#OpenLayer.md##OpenLayer "wikilink").

## IWindowController

| Cmd | Name                                                             | Notes                      |
| --- | ---------------------------------------------------------------- | -------------------------- |
| 0   | CreateWindow                                                     | Returns an IWindow object. |
| 1   | [\#GetAppletResourceUserId](#GetAppletResourceUserId "wikilink") |                            |
| 2   | \[6.0.0+\] GetAppletResourceUserIdOfCallerApplet                 |                            |
| 10  | [\#AcquireForegroundRights](#AcquireForegroundRights "wikilink") |                            |
| 11  | ReleaseForegroundRights                                          |                            |
| 12  | RejectToChangeIntoBackground                                     |                            |

### GetAppletResourceUserId

Returns an output u64:
[\#AppletResourceUserId](#AppletResourceUserId "wikilink").

### AcquireForegroundRights

No input/output.

## IAudioController

| Cmd | Name                                 |
| --- | ------------------------------------ |
| 0   | SetExpectedMasterVolume              |
| 1   | GetMainAppletExpectedMasterVolume    |
| 2   | GetLibraryAppletExpectedMasterVolume |
| 3   | ChangeMainAppletMasterVolume         |
| 4   | SetTransparentVolumeRate             |

GetMainAppletExpectedMasterVolume/SetExpectedMasterVolume are used for
saving/restoring state for LibraryApplet launching, with
SetExpectedMasterVolume being used with new state prior to launching a
LibraryApplet. With official sw these applet funcs are used directly in
the main-codebin.

## IDisplayController

| Cmd | Name                                                 |
| --- | ---------------------------------------------------- |
| 0   | GetLastForegroundCaptureImage                        |
| 1   | UpdateLastForegroundCaptureImage                     |
| 2   | GetLastApplicationCaptureImage                       |
| 3   | GetCallerAppletCaptureImage                          |
| 4   | UpdateCallerAppletCaptureImage                       |
| 5   | GetLastForegroundCaptureImageEx                      |
| 6   | GetLastApplicationCaptureImageEx                     |
| 7   | GetCallerAppletCaptureImageEx                        |
| 8   | \[2.0.0+\] TakeScreenShotOfOwnLayer                  |
| 9   | \[5.0.0+\] CopyBetweenCaptureBuffers                 |
| 10  | AcquireLastApplicationCaptureBuffer                  |
| 11  | ReleaseLastApplicationCaptureBuffer                  |
| 12  | AcquireLastForegroundCaptureBuffer                   |
| 13  | ReleaseLastForegroundCaptureBuffer                   |
| 14  | AcquireCallerAppletCaptureBuffer                     |
| 15  | ReleaseCallerAppletCaptureBuffer                     |
| 16  | AcquireLastApplicationCaptureBufferEx                |
| 17  | AcquireLastForegroundCaptureBufferEx                 |
| 18  | AcquireCallerAppletCaptureBufferEx                   |
| 20  | \[2.0.0+\] ClearCaptureBuffer                        |
| 21  | \[2.0.0+\] ClearAppletTransitionBuffer               |
| 22  | \[4.0.0+\] AcquireLastApplicationCaptureSharedBuffer |
| 23  | \[4.0.0+\] ReleaseLastApplicationCaptureSharedBuffer |
| 24  | \[4.0.0+\] AcquireLastForegroundCaptureSharedBuffer  |
| 25  | \[4.0.0+\] ReleaseLastForegroundCaptureSharedBuffer  |
| 26  | \[4.0.0+\] AcquireCallerAppletCaptureSharedBuffer    |
| 27  | \[4.0.0+\] ReleaseCallerAppletCaptureSharedBuffer    |
| 28  | \[6.0.0+\] TakeScreenShotOfOwnLayerEx                |

## ILibraryAppletCreator

| Cmd | Name                           | Notes                                                                     |
| --- | ------------------------------ | ------------------------------------------------------------------------- |
| 0   | CreateLibraryApplet            | Returns a [\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink"). |
| 1   | TerminateAllLibraryApplets     |                                                                           |
| 2   | AreAnyLibraryAppletsLeft       |                                                                           |
| 10  | CreateStorage                  | Returns an [\#IStorage](#IStorage "wikilink").                            |
| 11  | CreateTransferMemoryStorage    | Returns an [IStorage](# "wikilink").                                      |
| 12  | \[2.0.0+\] CreateHandleStorage | Returns an [\#IStorage](#IStorage "wikilink").                            |

## ISystemAppletControllerForDebug

| Cmd | Name                             | Notes |
| --- | -------------------------------- | ----- |
| 1   | RequestLaunchApplicationForDebug |       |

## IProcessWindingController

| Cmd | Name                                             | Notes                                                                      |
| --- | ------------------------------------------------ | -------------------------------------------------------------------------- |
| 0   | [\#GetLaunchReason](#GetLaunchReason "wikilink") |                                                                            |
| 11  | OpenCallingLibraryApplet                         | Returns an [\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink"). |
| 21  | PushContext                                      | Takes an [\#IStorage](#IStorage "wikilink").                               |
| 22  | PopContext                                       | Returns an [\#IStorage](#IStorage "wikilink").                             |
| 23  | CancelWindingReservation                         |                                                                            |
| 30  | WindAndDoReserved                                |                                                                            |
| 40  | ReserveToStartAndWaitAndUnwindThis               | Returns an [\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink"). |
| 41  | \[4.0.0+\] ReserveToStartAndWait                 |                                                                            |

### GetLaunchReason

No input. Returns an u32 AppletProcessLaunchReason.

Used by
LibraryApplets.

## IDebugFunctions

| Cmd | Name                                                           | Notes                                                                  |
| --- | -------------------------------------------------------------- | ---------------------------------------------------------------------- |
| 0   | NotifyMessageToHomeMenuForDebug                                |                                                                        |
| 1   | OpenMainApplication                                            | Returns an [\#IApplicationAccessor](#IApplicationAccessor "wikilink"). |
| 10  | EmulateButtonEvent                                             |                                                                        |
| 20  | InvalidateTransitionLayer                                      |                                                                        |
| 30  | \[6.0.0+\] RequestLaunchApplicationWithUserAndArgumentForDebug |                                                                        |
| 40  | \[6.0.0+\] GetAppletResourceUsageInfo                          |                                                                        |

## IStorage

| Cmd | Name                | Notes                                                                                    |
| --- | ------------------- | ---------------------------------------------------------------------------------------- |
| 0   | Open                | No input. Returns an [\#IStorageAccessor](#IStorageAccessor "wikilink").                 |
| 1   | OpenTransferStorage | No input. Returns an [\#ITransferStorageAccessor](#ITransferStorageAccessor "wikilink"). |

Commands which take an IStorage as input use an unknown input u32 for
that.

## IStorageAccessor

| Cmd | Name    | Notes                                             |
| --- | ------- | ------------------------------------------------- |
| 0   | GetSize | No input. Returns an s64.                         |
| 10  | Write   | Takes an input s64 and a type-0x21 input buffer.  |
| 11  | Read    | Takes an input s64 and a type-0x22 output buffer. |

## ITransferStorageAccessor

| Cmd | Name      | Notes                                       |
| --- | --------- | ------------------------------------------- |
| 0   | GetSize   | No input. Returns an output s64.            |
| 1   | GetHandle | No input. Returns an output u64 and handle. |

# appletOE

This is
"nn::am::<service::IApplicationProxyService>".

| Cmd | Name                                                       | Notes |
| --- | ---------------------------------------------------------- | ----- |
| 0   | [\#OpenApplicationProxy](#OpenApplicationProxy "wikilink") |       |

This is used by all regular-applications, including
[flog](Flog.md "wikilink") and "Retail Interactive Display Menu". Only
one session can be open for this service at a time.

## OpenApplicationProxy

Returns an [\#IApplicationProxy](#IApplicationProxy "wikilink"). See
[\#appletAE](#appletAE "wikilink").

Takes a [reserved](IPC%20Marshalling.md "wikilink") input u64(official
user-processes use hard-coded value 0), a PID, and a process
copy-handle(cur-proc handle alias).

On failure, official user-processes will retry using this command in a
loop while the retval is 0x19280, with svcSleepThread(10000000) being
called first.

# idle:sys

This is "nn::idle::detail::IPolicyManagerSystem"

| Cmd | Name                  |
| --- | --------------------- |
| 0   | GetAutoPowerDownEvent |
| 1   | \[1.0.0-3.0.2\]       |
| 2   | \[1.0.0-3.0.2\]       |
| 3   | SetHandlingContext    |
| 4   | LoadAndApplySettings  |
| 5   | ReportUserIsActive    |

# omm

This is "nn::omm::detail::IOperationModeManager"

Operation Mode Manager (OMM) is a service responsible for arbitrating
the operation changes between docked and handheld modes. Besides
[PTM\_services](PTM%20services.md "wikilink"), this is the only service
that interacts with the [Dock](Dock.md "wikilink") through
[usb:pd\*](USB%20services.md "wikilink").

| Cmd | Name                                                   |
| --- | ------------------------------------------------------ |
| 0   | GetOperationMode                                       |
| 1   | GetOperationModeChangeEvent                            |
| 2   | EnableAudioVisual                                      |
| 3   | DisableAudioVisual                                     |
| 4   | EnterSleepAndWait                                      |
| 5   | GetCradleStatus                                        |
| 6   | FadeInDisplay                                          |
| 7   | FadeOutDisplay                                         |
| 8   | \[2.0.0+\] GetCradleFwVersion                          |
| 9   | \[2.0.0+\] NotifyCecSettingsChanged                    |
| 10  | \[3.0.0+\] SetOperationModePolicy                      |
| 11  | \[3.0.0+\] GetDefaultDisplayResolution                 |
| 12  | \[3.0.0+\] GetDefaultDisplayResolutionChangeEvent      |
| 13  | \[3.0.0+\] UpdateDefaultDisplayResolution              |
| 14  | \[3.0.0+\] ShouldSleepOnBoot                           |
| 15  | \[4.0.0+\] NotifyHdcpApplicationExecutionStarted       |
| 16  | \[4.0.0+\] NotifyHdcpApplicationExecutionFinished      |
| 17  | \[4.0.0+\] NotifyHdcpApplicationDrawingStarted         |
| 18  | \[4.0.0+\] NotifyHdcpApplicationDrawingFinished        |
| 19  | \[4.0.0+\] GetHdcpAuthenticationFailedEvent            |
| 20  | \[4.0.0+\] GetHdcpAuthenticationFailedEmulationEnabled |
| 21  | \[4.0.0+\] SetHdcpAuthenticationFailedEmulation        |
| 22  | \[4.0.0+\] GetHdcpStateChangeEvent                     |
| 23  | \[4.0.0+\] GetHdcpState                                |
| 24  | \[5.0.0+\] ShowCardUpdateProcessing                    |
| 25  | \[5.0.0+\] SetApplicationCecSettingsAndNotifyChanged   |

# spsm

This is "nn::spsm::detail::IPowerStateInterface".

| Cmd | Name                                          |
| --- | --------------------------------------------- |
| 0   | GetState                                      |
| 1   | SleepSystemAndWaitAwake                       |
| 2   |                                               |
| 3   |                                               |
| 4   | GetNotificationMessageEventHandle             |
| 5   |                                               |
| 6   |                                               |
| 7   |                                               |
| 8   | AnalyzePerformanceLogForLastSleepWakeSequence |
| 9   | ChangeHomeButtonLongPressingTime              |
| 10  |                                               |
| 11  | \[1.0.0-3.0.2\]                               |

# tcap

This is "nn::tcap::server::IManager".

| Cmd | Name                                  |
| --- | ------------------------------------- |
| 0   | GetContinuousHighSkinTemperatureEvent |
| 1   | SetOperationMode                      |
| 2   | LoadAndApplySettings                  |

# Enums

### AppletId

See also [:Category:Library
Applets](:Category:Library%20Applets.md "wikilink").

| ID   | Title-id         | Description                                                                                                      |
| ---- | ---------------- | ---------------------------------------------------------------------------------------------------------------- |
| 0x02 | 010000000000100C | "overlayDisp"                                                                                                    |
| 0x03 | 0100000000001000 | "qlaunch"                                                                                                        |
| 0x04 | 0100000000001012 | "starter"                                                                                                        |
| 0x0A | 0100000000001001 | "auth"                                                                                                           |
| 0x0B | 0100000000001002 | "cabinet"                                                                                                        |
| 0x0C | 0100000000001003 | "controller"                                                                                                     |
| 0x0D | 0100000000001004 | "dataErase"                                                                                                      |
| 0x0E | 0100000000001005 | "error"                                                                                                          |
| 0x0F | 0100000000001006 | "netConnect"                                                                                                     |
| 0x10 | 0100000000001007 | "playerSelect"                                                                                                   |
| 0x11 | 0100000000001008 | ["swkbd"](Software%20Keyboard.md "wikilink")                                                                     |
| 0x12 | 0100000000001009 | "miiEdit"                                                                                                        |
| 0x13 | 010000000000100A | "LibAppletWeb" [WebApplet](Internet%20Browser#010000000000100A.md##010000000000100A "wikilink") applet           |
| 0x14 | 010000000000100B | "LibAppletShop" [ShopN](Internet%20Browser#ShopN.md##ShopN "wikilink") applet                                    |
| 0x15 | 010000000000100D | "photoViewer"                                                                                                    |
| 0x16 | 010000000000100E | "set"                                                                                                            |
| 0x17 | 010000000000100F | "LibAppletOff" [Offline](Internet%20Browser#Offline%20Applet.md##Offline_Applet "wikilink") applet               |
| 0x18 | 0100000000001010 | "LibAppletLns" [Whitelisted](Internet%20Browser#Whitelisted%20Applets.md##Whitelisted_Applets "wikilink") applet |
| 0x19 | 0100000000001011 | "LibAppletAuth" [WifiWebAuth](Internet%20Browser#WifiWebAuthApplet.md##WifiWebAuthApplet "wikilink") applet      |
| 0x1A | 0100000000001013 | "myPage"                                                                                                         |

### LibraryAppletMode

| ID  | Description   |
| --- | ------------- |
| 0x0 | AllForeground |
|     |               |

### ShimKind

This is from strings and code in the [
web-applets](Internet%20Browser.md "wikilink").

This indicates the type of web-applet.

| shimKind value | Description       |
| -------------- | ----------------- |
| 2              | LoginApplet       |
| 4              | ShareApplet       |
| 5              | WebApplet         |
| 6              | WifiWebAuthApplet |
| 7              | LobbyApplet       |

### NotificationMessage

| ID   | Description                                            |
| ---- | ------------------------------------------------------ |
| 0x4  | Exit requested                                         |
| 0xF  | [FocusState](#GetCurrentFocusState "wikilink") changed |
| 0x10 | ?                                                      |
| 0x1E | OperationMode changed                                  |
| 0x1F | PerformanceMode changed                                |

### OperationMode

| Value | Description |
| ----- | ----------- |
| 0     | Handheld    |
| 1     | Docked      |

# AppletResourceUserId

This u64 is officially called "nn::applet::AppletResourceUserId". Used
by a number of non-AM services.

[Category:Services](Category:Services "wikilink")
