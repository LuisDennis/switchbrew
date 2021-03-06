# aoc:u

This is "nn::aocsrv::detail::IAddOnContentManager".

| Cmd | Name                                                                                   |
| --- | -------------------------------------------------------------------------------------- |
| 0   | \[1.0.0-6.2.0\] CountAddOnContentByApplicationId                                       |
| 1   | \[1.0.0-6.2.0\] ListAddOnContentByApplicationId                                        |
| 2   | CountAddOnContent                                                                      |
| 3   | ListAddOnContent                                                                       |
| 4   | \[1.0.0-6.2.0\] GetAddOnContentBaseIdByApplicationId                                   |
| 5   | GetAddOnContentBaseId                                                                  |
| 6   | \[1.0.0-6.2.0\] PrepareAddOnContentByApplicationId                                     |
| 7   | PrepareAddOnContent                                                                    |
| 8   | \[4.0.0+\] GetAddOnContentListChangedEvent                                             |
| 100 | \[7.0.0+\] [CreateEcPurchasedEventManager](#IPurchaseEventManager "wikilink")          |
| 101 | \[9.0.0+\] [CreatePermanentEcPurchasedEventManager](#IPurchaseEventManager "wikilink") |

## IPurchaseEventManager

This is "nn::ec::IPurchaseEventManager".

| Cmd | Name                                      |
| --- | ----------------------------------------- |
| 0   | SetDefaultDeliveryTarget                  |
| 1   | SetDeliveryTarget                         |
| 2   | GetPurchasedEventReadableHandle           |
| 3   | PopPurchasedProductInfo                   |
| 4   | \[9.0.0+\] PopPurchasedProductInfoWithUid |

# ns:am

This is "nn::ns::detail::IApplicationManagerInterface".

\[3.0.0+\] This service was replaced by
[ns:am2](#ns:am2,_ns:ec,_ns:rid,_ns:rt,_ns:web "wikilink").

| Cmd  | Name                                                                                               |
| ---- | -------------------------------------------------------------------------------------------------- |
| 0    | [\#ListApplicationRecord](#ListApplicationRecord "wikilink")                                       |
| 1    | GenerateApplicationRecordCount                                                                     |
| 2    | GetApplicationRecordUpdateSystemEvent                                                              |
| 3    | GetApplicationViewDeprecated                                                                       |
| 4    | DeleteApplicationEntity                                                                            |
| 5    | DeleteApplicationCompletely                                                                        |
| 6    | IsAnyApplicationEntityRedundant                                                                    |
| 7    | DeleteRedundantApplicationEntity                                                                   |
| 8    | IsApplicationEntityMovable                                                                         |
| 9    | MoveApplicationEntity                                                                              |
| 11   | CalculateApplicationOccupiedSize                                                                   |
| 16   | PushApplicationRecord                                                                              |
| 17   | ListApplicationRecordContentMeta                                                                   |
| 18   |                                                                                                    |
| 19   | [\#LaunchApplication](#LaunchApplication "wikilink")                                               |
| 21   | [\#GetApplicationContentPath](#GetApplicationContentPath "wikilink")                               |
| 22   | TerminateApplication                                                                               |
| 23   | \[2.0.0+\] ResolveApplicationContentPath                                                           |
| 26   | BeginInstallApplication                                                                            |
| 27   | DeleteApplicationRecord                                                                            |
| 30   | RequestApplicationUpdateInfo                                                                       |
| 31   | RequestUpdateApplication                                                                           |
| 32   | CancelApplicationDownload                                                                          |
| 33   | ResumeApplicationDownload                                                                          |
| 34   |                                                                                                    |
| 35   | UpdateVersionList                                                                                  |
| 36   | PushLaunchVersion                                                                                  |
| 37   | ListRequiredVersion                                                                                |
| 38   | CheckApplicationLaunchVersion                                                                      |
| 39   | CheckApplicationLaunchRights                                                                       |
| 40   | GetApplicationLogoData                                                                             |
| 41   | CalculateApplicationDownloadRequiredSize                                                           |
| 42   | CleanupSdCard                                                                                      |
| 43   | CheckSdCardMountStatus                                                                             |
| 44   | GetSdCardMountStatusChangedEvent                                                                   |
| 45   | GetGameCardAttachmentEvent                                                                         |
| 46   | GetGameCardAttachmentInfo                                                                          |
| 47   | [\#GetTotalSpaceSize](#GetTotalSpaceSize "wikilink")                                               |
| 48   | [\#GetFreeSpaceSize](#GetFreeSpaceSize "wikilink")                                                 |
| 49   | GetSdCardRemovedEvent                                                                              |
| 52   | GetGameCardUpdateDetectionEvent                                                                    |
| 53   | DisableApplicationAutoDelete                                                                       |
| 54   | EnableApplicationAutoDelete                                                                        |
| 55   | [\#GetApplicationDesiredLanguage](#GetApplicationDesiredLanguage "wikilink")                       |
| 56   | SetApplicationTerminateResult                                                                      |
| 57   | ClearApplicationTerminateResult                                                                    |
| 58   | GetLastSdCardMountUnexpectedResult                                                                 |
| 59   | ConvertApplicationLanguageToLanguageCode                                                           |
| 60   | [\#ConvertLanguageCodeToApplicationLanguage](#ConvertLanguageCodeToApplicationLanguage "wikilink") |
| 61   | GetBackgroundDownloadStressTaskInfo                                                                |
| 62   | GetGameCardStopper                                                                                 |
| 63   | IsSystemProgramInstalled                                                                           |
| 64   | \[2.0.0+\] StartApplyDeltaTask                                                                     |
| 65   | \[2.0.0+\] GetRequestServerStopper                                                                 |
| 100  | ResetToFactorySettings                                                                             |
| 101  | ResetToFactorySettingsWithoutUserSaveData                                                          |
| 102  | \[2.0.0+\] ResetToFactorySettingsForRefurbishment                                                  |
| 200  | CalculateUserSaveDataStatistics                                                                    |
| 201  | DeleteUserSaveDataAll                                                                              |
| 210  | DeleteUserSystemSaveData                                                                           |
| 220  | UnregisterNetworkServiceAccount                                                                    |
| 300  | GetApplicationShellEvent                                                                           |
| 301  | PopApplicationShellEventInfo                                                                       |
| 302  | LaunchLibraryApplet                                                                                |
| 303  | TerminateLibraryApplet                                                                             |
| 304  | LaunchSystemApplet                                                                                 |
| 305  | TerminateSystemApplet                                                                              |
| 306  | LaunchOverlayApplet                                                                                |
| 307  | TerminateOverlayApplet                                                                             |
| 400  | [\#GetApplicationControlData](#GetApplicationControlData "wikilink")                               |
| 401  | InvalidateAllApplicationControlCache                                                               |
| 402  | RequestDownloadApplicationControlData                                                              |
| 403  | GetMaxApplicationControlCacheCount                                                                 |
| 404  | \[2.0.0+\] InvalidateApplicationControlCache                                                       |
| 405  | \[2.0.0+\] ListApplicationControlCacheEntryInfo                                                    |
| 502  | \[2.0.0+\] RequestCheckGameCardRegistration                                                        |
| 503  | \[2.0.0+\] RequestGameCardRegistrationGoldPoint                                                    |
| 504  | \[2.0.0+\] RequestRegisterGameCard                                                                 |
| 600  | \[2.0.0+\] CountApplicationContentMeta                                                             |
| 601  | \[2.0.0+\] [\#ListApplicationContentMetaStatus](#ListApplicationContentMetaStatus "wikilink")      |
| 602  | \[2.0.0+\] ListAvailableAddOnContent                                                               |
| 603  | \[2.0.0+\] GetOwnedApplicationContentMetaStatus                                                    |
| 604  | \[2.0.0+\] RegisterContentsExternalKey                                                             |
| 605  | \[2.0.0+\] ListApplicationContentMetaStatusWithRightsCheck                                         |
| 700  | \[2.0.0+\] PushDownloadTaskList                                                                    |
| 701  | \[2.0.0+\] ClearTaskStatusList                                                                     |
| 702  | \[2.0.0+\] RequestDownloadTaskList                                                                 |
| 703  | \[2.0.0+\] RequestEnsureDownloadTask                                                               |
| 704  | \[2.0.0+\] ListDownloadTaskStatus                                                                  |
| 705  | \[2.0.0+\] RequestDownloadTaskListData                                                             |
| 800  | \[2.0.0+\] RequestVersionList                                                                      |
| 801  | \[2.0.0+\] ListVersionList                                                                         |
| 900  | \[2.0.0+\] GetApplicationRecord                                                                    |
| 901  | \[2.0.0+\] GetApplicationRecordProperty                                                            |
| 902  | \[2.0.0+\] EnableApplicationAutoUpdate                                                             |
| 903  | \[2.0.0+\] DisableApplicationAutoUpdate                                                            |
| 904  | \[2.0.0+\] TouchApplication                                                                        |
| 905  | \[2.0.0+\] RequestApplicationUpdate                                                                |
| 906  | \[2.0.0+\] IsApplicationUpdateRequested                                                            |
| 907  | \[2.0.0+\] WithdrawApplicationUpdateRequest                                                        |
| 908  | \[2.0.0+\] ListApplicationRecordInstalledContentMeta                                               |
| 1000 | \[2.0.0+\] RequestVerifyApplicationDeprecated                                                      |
| 1001 | \[2.0.0+\] CorruptApplicationForDebug                                                              |
| 1200 | \[2.0.0+\] [\#NeedsUpdateVulnerability](#NeedsUpdateVulnerability "wikilink")                      |
| 1300 | \[2.0.0+\] IsAnyApplicationEntityInstalled                                                         |
| 1301 | \[2.0.0+\] DeleteApplicationContentEntities                                                        |
| 1302 | \[2.0.0+\] CleanupUnrecordedApplicationEntity                                                      |
| 1400 | \[2.0.0+\] PrepareShutdown                                                                         |
| 1500 | \[2.0.0+\] FormatSdCard                                                                            |
| 1501 | \[2.0.0+\] NeedsSystemUpdateToFormatSdCard                                                         |
| 1502 | \[2.0.0+\] GetLastSdCardFormatUnexpectedResult                                                     |
| 1503 | \[2.0.0+\]                                                                                         |
| 1600 | \[2.0.0+\] GetSystemSeedForPseudoDeviceId                                                          |
| 1700 | \[2.0.0+\] ListApplicationDownloadingContentMeta                                                   |
| 1800 | \[2.0.0+\] IsNotificationSetupCompleted                                                            |
| 1801 | \[2.0.0+\] GetLastNotificationInfoCount                                                            |
| 1802 | \[2.0.0+\] ListLastNotificationInfo                                                                |

## ListApplicationRecord

Takes a type-0x6 output buffer containing an array of the below record
and an s32 entry\_offset, returns an output s32 out\_entrycount.

Returns an array of entries with the below format using the specified
offset and count.

### Application Record Format

| Offset | Size | Description                                                                 |
| ------ | ---- | --------------------------------------------------------------------------- |
| 0x0    | 0x8  | Title ID                                                                    |
| 0x8    | 0x1  | Type? (Known values: 2=Installing?, 3=Gamecard?, 4=Installed?)              |
| 0x9    | 0x1  | Unknown, usually 0x02                                                       |
| 0xA    | 0x6  | Unknown, usually zeros?                                                     |
| 0x10   | 0x1  | Unknown, seems to change between reboots and removing/reinserting gamecards |
| 0x11   | 0x7  | Unknown, usually zeros?                                                     |

## LaunchApplication

Takes an input u64 titleID, returns an output u64 PID.

Launches an application title which is registered with NS.

## GetApplicationContentPath

Takes a 0x16-type output buffer, an u8 [title
type](NCM%20services#Title%20Types.md##Title_Types "wikilink"), and an
u64 titleID.

The input titleID is used with the application-title table like various
other cmds, anything not in that table can't be used with this.

Returns a string path for the specified type of patch content with this
titleID, otherwise returns regular-application paths when update-title
not installed. Returns an error when the specified type of content
doesn't exist for this title. Starts with
"@{SdCardContent,UserContent}://" and ends in ".nca".

For gamecard content, the output path is: "@GcSXXXXXXXX:/<NcaId>.nca".
NCA-type0 with gamecard returns 0 with an empty output string.

The output string is then used by the user-process with
[FS](Filesystem%20services.md "wikilink") to mount the content.

## GetTotalSpaceSize

Takes an input media-id that must be 5.

Returns the u64 from
[Content\_Manager\_services\#IContentStorage](Content%20Manager%20services#IContentStorage.md##IContentStorage "wikilink")
cmd22.

## GetFreeSpaceSize

Takes an input media-id that must be 5.

Returns the u64 from
[Content\_Manager\_services\#IContentStorage](Content%20Manager%20services#IContentStorage.md##IContentStorage "wikilink")
cmd23.

## GetApplicationDesiredLanguage

Takes an input u8 language-bitmask, returns an output u8
[control.nacp](Control.nacp.md "wikilink") langentry index.

User-processes generate the language-bitmask with the following for all
16 lang-entries: `if(<either string in langentry[i] is
non-empty>)bitmask |= 1<<i`

## ConvertLanguageCodeToApplicationLanguage

Takes an input u8 pointer for the resulting Id to be written to and a
string represented as a u64 (i.e 0x53552D6E65 for 'en-US').

Returns 0 if an ID was successfully found, otherwise returns 0x25810.

## GetApplicationControlData

Takes an input u8
[\#ApplicationControlSource](#ApplicationControlSource "wikilink"), an
u64 titleID, and a type-0x6 output buffer. Returns an output u32 for
actual\_size. Official user-processes use buffer size 0x24000.
[qlaunch](Qlaunch.md "wikilink") only uses flag value 0x1 (Storage if
not in cache).

Loads cached [control.nacp](Control.nacp.md "wikilink") to buf+0 and the
cached icon to buf+0x4000. Returns an error if the buffer is too small.

### ApplicationControlSource

| Value | Description                                                 |
| ----- | ----------------------------------------------------------- |
| 0x0   | CacheOnly (Returns data from cache)                         |
| 0x1   | Storage (Returns data from storage if not present in cache) |
| 0x2   | StorageOnly (Returns data from storage without using cache) |
|       |                                                             |

## ListApplicationContentMetaStatus

Takes a type-0x6 output buffer containing an array of the below entries,
an input s32 index and u64 titleID, returns an output s32
out\_entrycount.

Returns 0x10-byte entries using the specified titleID starting at the
specified index. Can only return game titles. The second entry if any is
the update-title usually. When the input entryindex is \>= totalentries,
this will return 0 with out\_entrycount=0.

Entry structure:

| Offset | Size | Description                                                                                          |
| ------ | ---- | ---------------------------------------------------------------------------------------------------- |
| 0x0    | 0x1  | u8 "type". [Title type](Content%20Manager%20services.md "wikilink") (String is from web-applet)      |
| 0x1    | 0x1  | u8 "installedStorage" / [StorageId](Filesystem%20services.md "wikilink") (String is from web-applet) |
| 0x2    | 0x1  | Unknown. Non-zero with output from cmd 605, differs for app/update titles.                           |
| 0x3    | 0x1  | Padding                                                                                              |
| 0x4    | 0x4  | u32 Title-version                                                                                    |
| 0x8    | 0x8  | u64 titleID                                                                                          |

# ns:am2, ns:ec, ns:rid, ns:rt, ns:web

These services are all, at the top level,
"nn::ns::detail::IServiceGetterInterface". These commands check a state
field for a command-specific bit and returns an error if not set, this
is likely a permissions check for service+command.

| Cmd  | Name                                                                                                           |
| ---- | -------------------------------------------------------------------------------------------------------------- |
| 7988 | \[6.0.0+\] [GetDynamicRightsInterface](#IDynamicRightsInterface "wikilink").                                   |
| 7989 | \[5.1.0+\] [GetReadOnlyApplicationControlDataInterface](#IReadOnlyApplicationControlDataInterface "wikilink"). |
| 7991 | \[5.0.0+\] [GetReadOnlyApplicationRecordInterface](#IReadOnlyApplicationRecordInterface "wikilink").           |
| 7992 | \[4.0.0+\] [GetECommerceInterface](#IECommerceInterface "wikilink")                                            |
| 7993 | \[4.0.0+\] [GetApplicationVersionInterface](#IApplicationVersionInterface "wikilink")                          |
| 7994 | [GetFactoryResetInterface](#IFactoryResetInterface "wikilink")                                                 |
| 7995 | [GetAccountProxyInterface](#IAccountProxyInterface "wikilink")                                                 |
| 7996 | [GetApplicationManagerInterface](#IApplicationManagerInterface "wikilink")                                     |
| 7997 | [GetDownloadTaskInterface](#IDownloadTaskInterface "wikilink")                                                 |
| 7998 | [GetContentManagementInterface](#IContentManagementInterface "wikilink")                                       |
| 7999 | [GetDocumentInterface](#IDocumentInterface "wikilink")                                                         |

### IAccountProxyInterface

This is "nn::ns::detail::IAccountProxyInterface".

| Cmd | Name              |
| --- | ----------------- |
| 0   | CreateUserAccount |

### IApplicationManagerInterface

This is "nn::ns::detail::IApplicationManagerInterface".

| Cmd  | Name                                                                                                          |
| ---- | ------------------------------------------------------------------------------------------------------------- |
| 0    | [\#ListApplicationRecord](#ListApplicationRecord "wikilink")                                                  |
| 1    | GenerateApplicationRecordCount                                                                                |
| 2    | GetApplicationRecordUpdateSystemEvent                                                                         |
| 3    | GetApplicationViewDeprecated                                                                                  |
| 4    | DeleteApplicationEntity                                                                                       |
| 5    | DeleteApplicationCompletely                                                                                   |
| 6    | IsAnyApplicationEntityRedundant                                                                               |
| 7    | DeleteRedundantApplicationEntity                                                                              |
| 8    | IsApplicationEntityMovable                                                                                    |
| 9    | MoveApplicationEntity                                                                                         |
| 11   | CalculateApplicationOccupiedSize                                                                              |
| 16   | PushApplicationRecord                                                                                         |
| 17   | ListApplicationRecordContentMeta                                                                              |
| 19   | \[1.0.0-5.1.0\] LaunchApplicationOld                                                                          |
| 21   | [\#GetApplicationContentPath](#GetApplicationContentPath "wikilink")                                          |
| 22   | TerminateApplication                                                                                          |
| 23   | ResolveApplicationContentPath                                                                                 |
| 26   | BeginInstallApplication                                                                                       |
| 27   | DeleteApplicationRecord                                                                                       |
| 30   | [\#RequestApplicationUpdateInfo](#RequestApplicationUpdateInfo "wikilink")                                    |
| 31   | \[1.0.0-3.0.2\]                                                                                               |
| 32   | CancelApplicationDownload                                                                                     |
| 33   | ResumeApplicationDownload                                                                                     |
| 35   | UpdateVersionList                                                                                             |
| 36   | PushLaunchVersion                                                                                             |
| 37   | ListRequiredVersion                                                                                           |
| 38   | CheckApplicationLaunchVersion                                                                                 |
| 39   | \[1.0.0-6.2.0\] CheckApplicationLaunchRights                                                                  |
| 40   | GetApplicationLogoData                                                                                        |
| 41   | CalculateApplicationDownloadRequiredSize                                                                      |
| 42   | CleanupSdCard                                                                                                 |
| 43   | CheckSdCardMountStatus                                                                                        |
| 44   | GetSdCardMountStatusChangedEvent                                                                              |
| 45   | GetGameCardAttachmentEvent                                                                                    |
| 46   | GetGameCardAttachmentInfo                                                                                     |
| 47   | [\#GetTotalSpaceSize](#GetTotalSpaceSize "wikilink")                                                          |
| 48   | [\#GetFreeSpaceSize](#GetFreeSpaceSize "wikilink")                                                            |
| 49   | GetSdCardRemovedEvent                                                                                         |
| 52   | GetGameCardUpdateDetectionEvent                                                                               |
| 53   | DisableApplicationAutoDelete                                                                                  |
| 54   | EnableApplicationAutoDelete                                                                                   |
| 55   | GetApplicationDesiredLanguage                                                                                 |
| 56   | SetApplicationTerminateResult                                                                                 |
| 57   | ClearApplicationTerminateResult                                                                               |
| 58   | GetLastSdCardMountUnexpectedResult                                                                            |
| 59   | ConvertApplicationLanguageToLanguageCode                                                                      |
| 60   | [\#ConvertLanguageCodeToApplicationLanguage](#ConvertLanguageCodeToApplicationLanguage "wikilink")            |
| 61   | GetBackgroundDownloadStressTaskInfo                                                                           |
| 62   | GetGameCardStopper                                                                                            |
| 63   | IsSystemProgramInstalled                                                                                      |
| 64   | StartApplyDeltaTask                                                                                           |
| 65   | GetRequestServerStopper                                                                                       |
| 66   | \[3.0.0+\] GetBackgroundApplyDeltaStressTaskInfo                                                              |
| 67   | \[3.0.0+\] CancelApplicationApplyDelta                                                                        |
| 68   | \[3.0.0+\] ResumeApplicationApplyDelta                                                                        |
| 69   | \[3.0.0+\] CalculateApplicationApplyDeltaRequiredSize                                                         |
| 70   | \[3.0.0+\] ResumeAll                                                                                          |
| 71   | \[3.0.0+\] GetStorageSize                                                                                     |
| 80   | \[3.0.0+\] RequestDownloadApplication                                                                         |
| 81   | \[3.0.0+\] RequestDownloadAddOnContent                                                                        |
| 82   | \[3.0.0+\] DownloadApplication                                                                                |
| 83   | \[4.0.0-6.2.0\] CheckApplicationResumeRights                                                                  |
| 84   | \[4.0.0+\] GetDynamicCommitEvent                                                                              |
| 85   | \[4.0.0+\] RequestUpdateApplication2                                                                          |
| 86   | \[4.0.0+\] EnableApplicationCrashReport                                                                       |
| 87   | \[4.0.0+\] IsApplicationCrashReportEnabled                                                                    |
| 90   | \[4.0.0-8.1.0\] BoostSystemMemoryResourceLimit                                                                |
| 91   | \[5.0.0+\] DeprecatedLaunchApplication                                                                        |
| 92   | \[5.0.0+\] GetRunningApplicationProgramId                                                                     |
| 93   | \[5.0.0+\] GetMainApplicationProgramIndex                                                                     |
| 94   | \[6.0.0+\] LaunchApplication                                                                                  |
| 95   | \[6.0.0+\] GetApplicationLaunchInfo                                                                           |
| 96   | \[6.0.0+\] AcquireApplicationLaunchInfo                                                                       |
| 97   | \[6.0.0+\] GetMainApplicationProgramIndexByApplicationLaunchInfo                                              |
| 98   | \[6.0.0+\] EnableApplicationAllThreadDumpOnCrash                                                              |
| 99   | \[8.0.0+\] [\#LaunchDevMenu](#LaunchDevMenu "wikilink")                                                       |
| 100  | ResetToFactorySettings                                                                                        |
| 101  | ResetToFactorySettingsWithoutUserSaveData                                                                     |
| 102  | ResetToFactorySettingsForRefurbishment                                                                        |
| 200  | CalculateUserSaveDataStatistics                                                                               |
| 201  | DeleteUserSaveDataAll                                                                                         |
| 210  | DeleteUserSystemSaveData                                                                                      |
| 211  | \[6.0.0+\] DeleteSaveData                                                                                     |
| 220  | UnregisterNetworkServiceAccount                                                                               |
| 221  | \[6.0.0+\] UnregisterNetworkServiceAccountWithUserSaveDataDeletion                                            |
| 300  | GetApplicationShellEvent                                                                                      |
| 301  | PopApplicationShellEventInfo                                                                                  |
| 302  | LaunchLibraryApplet                                                                                           |
| 303  | TerminateLibraryApplet                                                                                        |
| 304  | LaunchSystemApplet                                                                                            |
| 305  | TerminateSystemApplet                                                                                         |
| 306  | LaunchOverlayApplet                                                                                           |
| 307  | TerminateOverlayApplet                                                                                        |
| 400  | GetApplicationControlData                                                                                     |
| 401  | InvalidateAllApplicationControlCache                                                                          |
| 402  | RequestDownloadApplicationControlData                                                                         |
| 403  | GetMaxApplicationControlCacheCount                                                                            |
| 404  | InvalidateApplicationControlCache                                                                             |
| 405  | ListApplicationControlCacheEntryInfo                                                                          |
| 406  | \[6.0.0+\] GetApplicationControlProperty                                                                      |
| 407  | \[8.0.0+\] [\#ListApplicationTitle](#ListApplicationTitle "wikilink")                                         |
| 408  | \[8.0.0+\] [\#ListApplicationIcon](#ListApplicationIcon "wikilink")                                           |
| 502  | RequestCheckGameCardRegistration                                                                              |
| 503  | [\#RequestGameCardRegistrationGoldPoint](#RequestGameCardRegistrationGoldPoint "wikilink")                    |
| 504  | RequestRegisterGameCard                                                                                       |
| 505  | \[3.0.0+\] GetGameCardMountFailureEvent                                                                       |
| 506  | \[3.0.0+\] IsGameCardInserted                                                                                 |
| 507  | \[3.0.0+\] EnsureGameCardAccess                                                                               |
| 508  | \[3.0.0+\] GetLastGameCardMountFailureResult                                                                  |
| 509  | \[5.0.0+\] ListApplicationIdOnGameCard                                                                        |
| 510  | \[9.0.0+\] [\#GetGameCardPlatformRegion](#GetGameCardPlatformRegion "wikilink")                               |
| 600  | CountApplicationContentMeta                                                                                   |
| 601  | [\#ListApplicationContentMetaStatus](#ListApplicationContentMetaStatus "wikilink")                            |
| 602  | \[2.0.0-5.1.0\] ListAvailableAddOnContent                                                                     |
| 603  | GetOwnedApplicationContentMetaStatus                                                                          |
| 604  | RegisterContentsExternalKey                                                                                   |
| 605  | ListApplicationContentMetaStatusWithRightsCheck                                                               |
| 606  | \[3.0.0+\] GetContentMetaStorage                                                                              |
| 607  | \[6.0.0+\] ListAvailableAddOnContent                                                                          |
| 700  | PushDownloadTaskList                                                                                          |
| 701  | ClearTaskStatusList                                                                                           |
| 702  | RequestDownloadTaskList                                                                                       |
| 703  | RequestEnsureDownloadTask                                                                                     |
| 704  | ListDownloadTaskStatus                                                                                        |
| 705  | [\#RequestDownloadTaskListData](#RequestDownloadTaskListData "wikilink")                                      |
| 800  | RequestVersionList                                                                                            |
| 801  | ListVersionList                                                                                               |
| 802  | \[3.0.0+\] [\#RequestVersionListData](#RequestVersionListData "wikilink")                                     |
| 900  | GetApplicationRecord                                                                                          |
| 901  | GetApplicationRecordProperty                                                                                  |
| 902  | EnableApplicationAutoUpdate                                                                                   |
| 903  | DisableApplicationAutoUpdate                                                                                  |
| 904  | TouchApplication                                                                                              |
| 905  | RequestApplicationUpdate                                                                                      |
| 906  | IsApplicationUpdateRequested                                                                                  |
| 907  | WithdrawApplicationUpdateRequest                                                                              |
| 908  | ListApplicationRecordInstalledContentMeta                                                                     |
| 909  | \[3.0.0+\] WithdrawCleanupAddOnContentsWithNoRightsRecommendation                                             |
| 910  | \[5.0.0+\] HasApplicationRecord                                                                               |
| 911  | \[5.1.0+\] SetPreInstalledApplication                                                                         |
| 912  | \[5.1.0+\] ClearPreInstalledApplicationFlag                                                                   |
| 913  | \[9.0.0+\] ListAllApplicationRecord                                                                           |
| 914  | \[9.0.0+\] HideApplicationRecord                                                                              |
| 915  | \[9.0.0+\] ShowApplicationRecord                                                                              |
| 1000 | RequestVerifyApplicationDeprecated                                                                            |
| 1001 | CorruptApplicationForDebug                                                                                    |
| 1002 | \[3.0.0+\] RequestVerifyAddOnContentsRights                                                                   |
| 1003 | \[5.0.0+\] RequestVerifyApplication                                                                           |
| 1004 | \[5.0.0+\] CorruptContentForDebug                                                                             |
| 1200 | [\#NeedsUpdateVulnerability](#NeedsUpdateVulnerability "wikilink")                                            |
| 1300 | IsAnyApplicationEntityInstalled                                                                               |
| 1301 | DeleteApplicationContentEntities                                                                              |
| 1302 | CleanupUnrecordedApplicationEntity                                                                            |
| 1303 | \[3.0.0+\] CleanupAddOnContentsWithNoRights                                                                   |
| 1304 | \[3.0.0+\] DeleteApplicationContentEntity                                                                     |
| 1308 | \[5.0.0+\] DeleteApplicationCompletelyForDebug                                                                |
| 1309 | \[6.0.0+\] CleanupUnavailableAddOnContents                                                                    |
| 1400 | PrepareShutdown                                                                                               |
| 1500 | FormatSdCard                                                                                                  |
| 1501 | NeedsSystemUpdateToFormatSdCard                                                                               |
| 1502 | GetLastSdCardFormatUnexpectedResult                                                                           |
| 1504 | \[3.0.0+\] InsertSdCard                                                                                       |
| 1505 | \[3.0.0+\] RemoveSdCard                                                                                       |
| 1506 | \[9.0.0+\] GetSdCardStartupStatus                                                                             |
| 1600 | GetSystemSeedForPseudoDeviceId                                                                                |
| 1601 | \[3.0.0+\] ResetSystemSeedForPseudoDeviceId                                                                   |
| 1700 | ListApplicationDownloadingContentMeta                                                                         |
| 1701 | \[3.0.0+\] GetApplicationView                                                                                 |
| 1702 | \[3.0.0+\] GetApplicationDownloadTaskStatus                                                                   |
| 1703 | \[4.0.0+\] GetApplicationViewDownloadErrorContext                                                             |
| 1704 | \[8.0.0+\] GetApplicationViewWithPromotionInfo                                                                |
| 1800 | IsNotificationSetupCompleted                                                                                  |
| 1801 | GetLastNotificationInfoCount                                                                                  |
| 1802 | ListLastNotificationInfo                                                                                      |
| 1803 | \[3.0.0+\] ListNotificationTask                                                                               |
| 1900 | \[3.0.0+\] IsActiveAccount                                                                                    |
| 1901 | \[4.0.0+\] RequestDownloadApplicationPrepurchasedRights                                                       |
| 1902 | \[5.0.0+\] GetApplicationTicketInfo                                                                           |
| 2000 | \[4.0.0+\] GetSystemDeliveryInfo                                                                              |
| 2001 | \[4.0.0+\] SelectLatestSystemDeliveryInfo                                                                     |
| 2002 | \[4.0.0+\] VerifyDeliveryProtocolVersion                                                                      |
| 2003 | \[4.0.0+\] GetApplicationDeliveryInfo                                                                         |
| 2004 | \[4.0.0+\] HasAllContentsToDeliver                                                                            |
| 2005 | \[4.0.0+\] CompareApplicationDeliveryInfo                                                                     |
| 2006 | \[4.0.0+\] CanDeliverApplication                                                                              |
| 2007 | \[4.0.0+\] ListContentMetaKeyToDeliverApplication                                                             |
| 2008 | \[4.0.0+\] NeedsSystemUpdateToDeliverApplication                                                              |
| 2009 | \[4.0.0+\] EstimateRequiredSize                                                                               |
| 2010 | \[4.0.0+\] RequestReceiveApplication                                                                          |
| 2011 | \[4.0.0+\] CommitReceiveApplication                                                                           |
| 2012 | \[4.0.0+\] GetReceiveApplicationProgress                                                                      |
| 2013 | \[4.0.0+\] RequestSendApplication                                                                             |
| 2014 | \[4.0.0+\] GetSendApplicationProgress                                                                         |
| 2015 | \[4.0.0+\] CompareSystemDeliveryInfo                                                                          |
| 2016 | \[4.0.0+\] ListNotCommittedContentMeta                                                                        |
| 2017 | \[4.0.0+\] RecoverDownloadTask                                                                                |
| 2018 | \[5.0.0+\] GetApplicationDeliveryInfoHash                                                                     |
| 2050 | \[6.0.0+\] GetApplicationRightsOnClient                                                                       |
| 2051 | \[9.0.0+\] InvalidateRightsIdCache                                                                            |
| 2100 | \[6.0.0+\] GetApplicationTerminateResult                                                                      |
| 2101 | \[6.0.0+\] GetRawApplicationTerminateResult                                                                   |
| 2150 | \[6.0.0+\] CreateRightsEnvironment                                                                            |
| 2151 | \[6.0.0+\] DestroyRightsEnvironment                                                                           |
| 2152 | \[6.0.0+\] ActivateRightsEnvironment                                                                          |
| 2153 | \[6.0.0+\] DeactivateRightsEnvironment                                                                        |
| 2154 | \[6.0.0+\] ForceActivateRightsContextForExit                                                                  |
| 2155 | \[7.0.0+\] UpdateRightsEnvironmentStatus                                                                      |
| 2156 | \[9.0.0+\] CreateRightsEnvironmentForPreomia                                                                  |
| 2160 | \[6.0.0+\] AddTargetApplicationToRightsEnvironment                                                            |
| 2161 | \[6.0.0+\] SetUsersToRightsEnvironment                                                                        |
| 2170 | \[6.0.0+\] GetRightsEnvironmentStatus                                                                         |
| 2171 | \[6.0.0+\] GetRightsEnvironmentStatusChangedEvent                                                             |
| 2180 | \[6.0.0+\] RequestExtendExpirationInRightsEnvironment                                                         |
| 2181 | \[6.0.0+\] GetResultOfExtendExpirationInRightsEnvironment                                                     |
| 2182 | \[6.0.0+\] SetActiveRightsContextUsingStateToRightsEnvironment                                                |
| 2190 | \[6.0.0+\] [\#GetRightsEnvironmentHandleForApplication](#GetRightsEnvironmentHandleForApplication "wikilink") |
| 2199 | \[6.0.0+\] GetRightsEnvironmentCountForDebug                                                                  |
| 2200 | \[6.0.0+\] GetGameCardApplicationCopyIdentifier                                                               |
| 2201 | \[6.0.0+\] GetInstalledApplicationCopyIdentifier                                                              |
| 2250 | \[6.0.0-6.2.0\] RequestReportActiveELicence                                                                   |
| 2300 | \[6.0.0-8.1.0\] ListEventLog                                                                                  |
| 2350 | \[7.0.0+\] PerformAutoUpdateByApplicationId                                                                   |
| 2351 | \[9.0.0+\] [\#RequestNoDownloadRightsErrorResolution](#RequestNoDownloadRightsErrorResolution "wikilink")     |
| 2352 | \[9.0.0+\] [\#RequestResolveNoDownloadRightsError](#RequestResolveNoDownloadRightsError "wikilink")           |
| 2400 | \[8.0.0+\] GetPromotionInfo                                                                                   |
| 2401 | \[8.0.0+\] CountPromotionInfo                                                                                 |
| 2402 | \[8.0.0+\] ListPromotionInfo                                                                                  |
| 2403 | \[8.0.0+\] ImportPromotionJsonForDebug                                                                        |
| 2404 | \[8.0.0+\] ClearPromotionInfoForDebug                                                                         |
| 2500 | \[8.0.0+\] ConfirmAvailableTime                                                                               |
| 2510 | \[9.0.0+\] [\#CreateApplicationResource](#CreateApplicationResource "wikilink")                               |
| 2511 | \[9.0.0+\] [\#GetApplicationResource](#GetApplicationResource "wikilink")                                     |
| 2513 | \[9.0.0+\] LaunchPreomia                                                                                      |
| 2514 | \[9.0.0+\] ClearTaskOfAsyncTaskManager                                                                        |
| 2800 | \[9.0.0+\] GetApplicationIdOfPreomia                                                                          |

\[4.0.0+\] RequestDownloadAddOnContent now takes an additional 8-bytes
of input.

#### RequestApplicationUpdateInfo

Takes an input u64 titleID (`nn::ncm::ApplicationId`), returns an output
Event handle and an [\#IAsyncValue](#IAsyncValue "wikilink").

The data that can be read from the
[\#IAsyncValue](#IAsyncValue "wikilink") is
[\#ApplicationUpdateInfo](#ApplicationUpdateInfo "wikilink").

#### LaunchDevMenu

No input/output.

This is used by AM cmd
[LaunchDevMenu](Applet%20Manager%20services#LaunchDevMenu.md##LaunchDevMenu "wikilink").

This loads titleIDs from
[system-settings](System%20Settings.md "wikilink")
`ns.applet!devmenu_id` and `ns.applet!devoverlaydisp_id`, which only
exists on devunits. An error is thrown if loading these fail.

[NCM](NCM%20services.md "wikilink") OpenContentMetaDatabase is used with
StorageId = NandSystem, then IContentMetaDatabase
GetLatestContentMetaKey is used with both of the above titleIDs to
verify that the cmd is successful.

Then if the above succeeds, the above titles are launched with the above
StorageId via [pmshell](Process%20Manager%20services.md "wikilink")
LaunchProgram, with a 0.5s sleep-thread afterwards on success.

#### ListApplicationTitle

Takes a total of 0x10-bytes of input, a type-0x5 input buffer, an input
handle, returns an output Event handle and an
[\#IAsyncValue](#IAsyncValue "wikilink").

#### ListApplicationIcon

Takes a total of 0x10-bytes of input, a type-0x5 input buffer, an input
handle, returns an output Event handle and an
[\#IAsyncValue](#IAsyncValue "wikilink").

#### RequestGameCardRegistrationGoldPoint

Takes a total of 0x18-bytes of input, returns an output Event handle and
an [\#IAsyncValue](#IAsyncValue "wikilink").

#### GetGameCardPlatformRegion

No input, returns an u8 **PlatformRegion** (0x00 = Default, 0x01 =
China).

This calls [fsp-srv
IDeviceOperator](Filesystem%20services#IDeviceOperator.md##IDeviceOperator "wikilink")
GetGameCardCompatibilityType and returns the result.

#### RequestDownloadTaskListData

No input, returns an output Event handle and an
[\#IAsyncValue](#IAsyncValue "wikilink").

#### GetRightsEnvironmentHandleForApplication

No input, returns a total of 8-bytes of output.

\[9.0.0+\] Now takes a total of 8-bytes of input, returns a total of
8-bytes of output.

#### RequestNoDownloadRightsErrorResolution

Takes an input u64 titleID (`nn::ncm::ApplicationId`), returns an output
Event handle and an [\#IAsyncValue](#IAsyncValue "wikilink").

The data that can be read from the
[\#IAsyncValue](#IAsyncValue "wikilink") is
[\#NoDownloadRightsErrorResolution](#NoDownloadRightsErrorResolution "wikilink").

#### RequestResolveNoDownloadRightsError

Takes an input u64 titleID (`nn::ncm::ApplicationId`), returns an output
Event handle and an [\#IAsyncValue](#IAsyncValue "wikilink").

The data that can be read from the
[\#IAsyncValue](#IAsyncValue "wikilink") is
[\#NoDownloadRightsErrorResolution](#NoDownloadRightsErrorResolution "wikilink").

#### CreateApplicationResource

Returns an [\#IApplicationResource](#IApplicationResource "wikilink").

#### GetApplicationResource

Returns an [\#IApplicationResource](#IApplicationResource "wikilink").

### IApplicationVersionInterface

This is "nn::ns::detail::IApplicationVersionInterface".

This was added with \[4.0.0+\].

| Cmd  | Name                                                           |
| ---- | -------------------------------------------------------------- |
| 0    | GetLaunchRequiredVersion                                       |
| 1    | UpgradeLaunchRequiredVersion                                   |
| 35   | UpdateVersionList                                              |
| 36   | PushLaunchVersion                                              |
| 37   | ListRequiredVersion                                            |
| 800  | RequestVersionList                                             |
| 801  | ListVersionList                                                |
| 802  | [\#RequestVersionListData](#RequestVersionListData "wikilink") |
| 1000 | PerformAutoUpdate                                              |

#### RequestVersionListData

No input, returns an output Event handle and an
[\#IAsyncValue](#IAsyncValue "wikilink").

The data that can be read from the
[\#IAsyncValue](#IAsyncValue "wikilink") is
[\#VersionListData](#VersionListData "wikilink").

### IContentManagerInterface

This is "nn::ns::detail::IContentManagementInterface".

| Cmd | Name                                            |
| --- | ----------------------------------------------- |
| 11  | CalculateApplicationOccupiedSize                |
| 43  | CheckSdCardMountStatus                          |
| 47  | GetTotalSpaceSize                               |
| 48  | GetFreeSpaceSize                                |
| 600 | CountApplicationContentMeta                     |
| 601 | ListApplicationContentMetaStatus                |
| 605 | ListApplicationContentMetaStatusWithRightsCheck |
| 607 | IsAnyApplicationRunning                         |

### IDocumentInterface

This is "nn::ns::detail::IDocumentInterface".

| Cmd | Name                                      |
| --- | ----------------------------------------- |
| 21  | GetApplicationContentPath                 |
| 23  | ResolveApplicationContentPath             |
| 92  | \[5.0.0+\] GetRunningApplicationProgramId |

### IDownloadTaskInterface

This is "nn::ns::detail::IDownloadTaskInterface".

| Cmd | Name                                                                     |
| --- | ------------------------------------------------------------------------ |
| 701 | ClearTaskStatusList                                                      |
| 702 | RequestDownloadTaskList                                                  |
| 703 | RequestEnsureDownloadTask                                                |
| 704 | ListDownloadTaskStatus                                                   |
| 705 | [\#RequestDownloadTaskListData](#RequestDownloadTaskListData "wikilink") |
| 706 | \[4.0.0+\] TryCommitCurrentApplicationDownloadTask                       |
| 707 | \[4.0.0+\] EnableAutoCommit                                              |
| 708 | \[4.0.0+\] DisableAutoCommit                                             |
| 709 | \[4.0.0+\] TriggerDynamicCommitEvent                                     |

### IReadOnlyApplicationRecordInterface

This is "nn::ns::detail::IReadOnlyApplicationRecordInterface".

This was added with \[5.0.0+\].

| Cmd | Name                 | Notes                                                                                      |
| --- | -------------------- | ------------------------------------------------------------------------------------------ |
| 0   | HasApplicationRecord | Same as [\#IApplicationManagerInterface](#IApplicationManagerInterface "wikilink") cmd 910 |

### IReadOnlyApplicationControlDataInterface

This is "nn::ns::detail::IReadOnlyApplicationControlDataInterface".

This was added with \[5.1.0+\].

| Cmd | Name                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| 0   | [\#GetApplicationControlData](#GetApplicationControlData "wikilink")                               | Same as [\#IApplicationManagerInterface](#IApplicationManagerInterface "wikilink") cmd 400 |
| 1   | [\#GetApplicationDesiredLanguage](#GetApplicationDesiredLanguage "wikilink")                       | Same as [\#IApplicationManagerInterface](#IApplicationManagerInterface "wikilink") cmd 55  |
| 2   | ConvertApplicationLanguageToLanguageCode                                                           | Same as [\#IApplicationManagerInterface](#IApplicationManagerInterface "wikilink") cmd 59  |
| 3   | [\#ConvertLanguageCodeToApplicationLanguage](#ConvertLanguageCodeToApplicationLanguage "wikilink") | Same as [\#IApplicationManagerInterface](#IApplicationManagerInterface "wikilink") cmd 60  |
| 4   | \[9.0.0+\] SelectApplicationDesiredLanguage                                                        |                                                                                            |

### IDynamicRightsInterface

This is "nn::ns::detail::IDynamicRightsInterface".

This was added with \[6.0.0+\].

| Cmd | Name                                                                                                          | Notes |
| --- | ------------------------------------------------------------------------------------------------------------- | ----- |
| 0   | [\#RequestApplicationRightsOnServer](#RequestApplicationRightsOnServer "wikilink")                            |       |
| 1   | RequestAssignRights                                                                                           |       |
| 4   | DeprecatedRequestAssignRightsToResume                                                                         |       |
| 5   | VerifyActivatedRightsOwners                                                                                   |       |
| 6   | DeprecatedGetApplicationRightsStatus                                                                          |       |
| 7   | RequestPrefetchForDynamicRights                                                                               |       |
| 8   | GetDynamicRightsState                                                                                         |       |
| 9   | \[7.0.0+\] [\#RequestApplicationRightsOnServerToResume](#RequestApplicationRightsOnServerToResume "wikilink") |       |
| 10  | \[7.0.0+\] RequestAssignRightsToResume                                                                        |       |
| 11  | \[7.0.0+\] GetActivatedRightsUsers                                                                            |       |
| 12  | \[8.0.0+\] GetApplicationRightsStatus                                                                         |       |
| 13  | \[8.0.0+\] GetRunningApplicationStatus                                                                        |       |

#### RequestApplicationRightsOnServer

Takes a total of 0x20-bytes of input, returns an output Event handle and
an [\#IAsyncValue](#IAsyncValue "wikilink").

#### RequestApplicationRightsOnServerToResume

Takes a total of 8-bytes of input, returns an output Event handle and an
[\#IAsyncValue](#IAsyncValue "wikilink").

### IECommerceInterface

This is "nn::ns::detail::IECommerceInterface".

This was added with \[4.0.0+\].

| Cmd | Name                                                 | Notes                                                                                        |
| --- | ---------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| 0   | RequestLinkDevice                                    | Takes a total of 0x10-bytes of input, returns an [\#IAsyncResult](#IAsyncResult "wikilink"). |
| 1   | \[6.0.0+\] RequestCleanupAllPreInstalledApplications | No input, returns an [\#IAsyncResult](#IAsyncResult "wikilink").                             |
| 2   | \[6.0.0+\] RequestCleanupPreInstalledApplication     | Takes a total of 0x8-bytes of input, returns an [\#IAsyncResult](#IAsyncResult "wikilink").  |
| 3   | \[6.0.0+\] RequestSyncRights                         | No input, returns an [\#IAsyncResult](#IAsyncResult "wikilink").                             |
| 4   | \[6.0.0+\] RequestUnlinkDevice                       | Takes a total of 0x10-bytes of input, returns an [\#IAsyncResult](#IAsyncResult "wikilink"). |
| 5   | \[6.1.0+\] RequestRevokeAllELicense                  | Takes a total of 0x10-bytes of input, returns an [\#IAsyncResult](#IAsyncResult "wikilink"). |
| 6   | \[9.0.0+\] RequestSyncRightsBasedOnAssignedELicenses |                                                                                              |

### IFactoryResetInterface

This is "nn::ns::detail::IFactoryResetInterface".

| Cmd | Name                                      |
| --- | ----------------------------------------- |
| 100 | ResetToFactorySettings                    |
| 101 | ResetToFactorySettingsWithoutUserSaveData |
| 102 | ResetToFactorySettingsForRefurbishment    |

### IApplicationResource

This is "nn::ns::detail::IApplicationResource".

This was added with \[9.0.0+\].

| Cmd | Name                           |
| --- | ------------------------------ |
| 0   | Attach                         |
| 1   | BoostSystemMemoryResourceLimit |

# ns:vm

This is "nn::ns::detail::IVulnerabilityManagerInterface".

| Cmd  | Name                                                                                        |
| ---- | ------------------------------------------------------------------------------------------- |
| 1200 | \[3.0.0+\] [\#NeedsUpdateVulnerability](#NeedsUpdateVulnerability "wikilink")               |
| 1201 | \[4.0.0+\] [\#UpdateSafeSystemVersionForDebug](#UpdateSafeSystemVersionForDebug "wikilink") |
| 1202 | \[4.0.0+\] [\#GetSafeSystemVersion](#GetSafeSystemVersion "wikilink")                       |

## NeedsUpdateVulnerability

No input, returns an output u8 bool flag.

Web-applets use this command to check if the system needs an update.

## UpdateSafeSystemVersionForDebug

Takes an input u64 **titleID** and an u32 **version**.

This command is not available for retail units. On a debug unit, if the
[system setting](System%20Settings.md "wikilink")
`vulnerability!enable_debug` is set, this mounts the system savegame
[0x8000000000000049](Flash%20Filesystem#System%20Savegames.md##System_Savegames "wikilink")
as "ns\_ssversion:/", opens the file "ns\_ssversion:/entry" and writes
the supplied **titleID** and **version** in it.

Finally, it calls
[OpenContentMetaDatabase](NCM%20services#ncm.md##ncm "wikilink") with
[StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink") 3,
then calls
[GetLatestContentMetaKey](NCM%20services#IContentMetaDatabase.md##IContentMetaDatabase "wikilink")
with the supplied **titleID** and compares the version field from the
returned [Content Meta
Record](CNMT#Content%20Meta%20Records.md##Content_Meta_Records "wikilink")
with the supplied **version**.

If the supplied **version** is higher than the one in NCM's database,
the value returned by
[NeedsUpdateVulnerability](NS%20Services#NeedsUpdateVulnerability.md##NeedsUpdateVulnerability "wikilink")
is set to "true".

## GetSafeSystemVersion

No input, returns an output
[ContentMetaKey](NCM%20services#ContentMetaKey.md##ContentMetaKey "wikilink")
with the cached contents of "ns\_ssversion:/entry" (u64 **titleID**, u32
**version** and u32 **policy** from
`vulnerability!needs_update_vulnerability_policy`).

# ns:su

This is "nn::ns::detail::ISystemUpdateInterface".

| Cmd | Name                                                                                                                   |
| --- | ---------------------------------------------------------------------------------------------------------------------- |
| 0   | [\#GetBackgroundNetworkUpdateState](#GetBackgroundNetworkUpdateState "wikilink")                                       |
| 1   | [\#OpenSystemUpdateControl](#OpenSystemUpdateControl "wikilink")                                                       |
| 2   | [\#NotifyExFatDriverRequired](#NotifyExFatDriverRequired "wikilink")                                                   |
| 3   | [\#ClearExFatDriverStatusForDebug](#ClearExFatDriverStatusForDebug "wikilink")                                         |
| 4   | [\#RequestBackgroundNetworkUpdate](#RequestBackgroundNetworkUpdate "wikilink")                                         |
| 5   | [\#NotifyBackgroundNetworkUpdate](#NotifyBackgroundNetworkUpdate "wikilink")                                           |
| 6   | [\#NotifyExFatDriverDownloadedForDebug](#NotifyExFatDriverDownloadedForDebug "wikilink")                               |
| 9   | [\#GetSystemUpdateNotificationEventForContentDelivery](#GetSystemUpdateNotificationEventForContentDelivery "wikilink") |
| 10  | [\#NotifySystemUpdateForContentDelivery](#NotifySystemUpdateForContentDelivery "wikilink")                             |
| 11  | \[3.0.0+\] [\#PrepareShutdown](#PrepareShutdown "wikilink")                                                            |
| 12  | \[3.0.0-3.0.2\]                                                                                                        |
| 13  | \[3.0.0-3.0.2\]                                                                                                        |
| 14  | \[3.0.0-3.0.2\]                                                                                                        |
| 15  | \[3.0.0-3.0.2\]                                                                                                        |
| 16  | \[4.0.0+\] [\#DestroySystemUpdateTask](#DestroySystemUpdateTask "wikilink")                                            |
| 17  | \[4.0.0+\] [\#RequestSendSystemUpdate](#RequestSendSystemUpdate "wikilink")                                            |
| 18  | \[4.0.0+\] [\#GetSendSystemUpdateProgress](#GetSendSystemUpdateProgress "wikilink")                                    |

## GetBackgroundNetworkUpdateState

No input, returns an output
[\#BackgroundNetworkUpdateState](#BackgroundNetworkUpdateState "wikilink").

This is similar to [\#HasDownloaded](#HasDownloaded "wikilink"), see
[\#BackgroundNetworkUpdateState](#BackgroundNetworkUpdateState "wikilink").

## OpenSystemUpdateControl

No input, returns an
[\#ISystemUpdateControl](#ISystemUpdateControl "wikilink").

## NotifyExFatDriverRequired

No input/output.

Only usable when an
[\#ISystemUpdateControl](#ISystemUpdateControl "wikilink") isn't open.

This uses [nim](NIM%20services.md "wikilink") ListSystemUpdateTask, then
when a task is returned uses it with DestroySystemUpdateTask.

Then this runs ExFat handling, updates state, and sets the same state
flag as
[\#RequestBackgroundNetworkUpdate](#RequestBackgroundNetworkUpdate "wikilink").

## ClearExFatDriverStatusForDebug

No input/output.

## RequestBackgroundNetworkUpdate

No input/output.

Only usable when an
[\#ISystemUpdateControl](#ISystemUpdateControl "wikilink") isn't open.

This sets a state flag to value 1.

## NotifyBackgroundNetworkUpdate

Takes an input
[ContentMetaKey](NCM%20services#ContentMetaKey.md##ContentMetaKey "wikilink"),
no output.

This checks whether a sysupdate is needed with the input ContentMetaKey
using [NCM](NCM%20services.md "wikilink") commands, if not this will
just return 0. Otherwise, this will then run code which is identical to
[\#RequestBackgroundNetworkUpdate](#RequestBackgroundNetworkUpdate "wikilink").

## NotifyExFatDriverDownloadedForDebug

No input/output.

## GetSystemUpdateNotificationEventForContentDelivery

No input, returns an output Event handle with EventClearMode=0.

## NotifySystemUpdateForContentDelivery

No input/output.

Signals the Event returned by
[\#GetSystemUpdateNotificationEventForContentDelivery](#GetSystemUpdateNotificationEventForContentDelivery "wikilink").

## PrepareShutdown

No input/output.

This is used by [AM](AM%20services.md "wikilink").

Just returns 0 when an
[\#ISystemUpdateControl](#ISystemUpdateControl "wikilink") is open.

This does various cleanup / uses various service-cmds etc for shutdown
preparation.

## DestroySystemUpdateTask

No input/output.

Only usable when an
[\#ISystemUpdateControl](#ISystemUpdateControl "wikilink") isn't open.

This uses [nim](NIM%20services.md "wikilink") ListSystemUpdateTask, then
when a task is returned uses it with DestroySystemUpdateTask.

## RequestSendSystemUpdate

Takes a type-0x15 input buffer containing a
[\#SystemDeliveryInfo](#SystemDeliveryInfo "wikilink"), an u16, an u32,
returns an output Event handle and an
[\#IAsyncResult](#IAsyncResult "wikilink").

[qlaunch](Qlaunch.md "wikilink") uses value 0xD904 (55556) for the u16.

## GetSendSystemUpdateProgress

No input, returns an output
[\#SystemUpdateProgress](#SystemUpdateProgress "wikilink").

Same as [\#GetReceiveProgress](#GetReceiveProgress "wikilink") except
this uses nim cmd81 and cmd78.

## ISystemUpdateControl

| Cmd | Name                                                                                                                          |
| --- | ----------------------------------------------------------------------------------------------------------------------------- |
| 0   | [\#HasDownloaded](#HasDownloaded "wikilink")                                                                                  |
| 1   | [\#RequestCheckLatestUpdate](#RequestCheckLatestUpdate "wikilink")                                                            |
| 2   | [\#RequestDownloadLatestUpdate](#RequestDownloadLatestUpdate "wikilink")                                                      |
| 3   | [\#GetDownloadProgress](#GetDownloadProgress "wikilink")                                                                      |
| 4   | [\#ApplyDownloadedUpdate](#ApplyDownloadedUpdate "wikilink")                                                                  |
| 5   | [\#RequestPrepareCardUpdate](#RequestPrepareCardUpdate "wikilink")                                                            |
| 6   | [\#GetPrepareCardUpdateProgress](#GetPrepareCardUpdateProgress "wikilink")                                                    |
| 7   | [\#HasPreparedCardUpdate](#HasPreparedCardUpdate "wikilink")                                                                  |
| 8   | [\#ApplyCardUpdate](#ApplyCardUpdate "wikilink")                                                                              |
| 9   | [\#GetDownloadedEulaDataSize](#GetDownloadedEulaDataSize "wikilink")                                                          |
| 10  | [\#GetDownloadedEulaData](#GetDownloadedEulaData "wikilink")                                                                  |
| 11  | [\#SetupCardUpdate](#SetupCardUpdate "wikilink")                                                                              |
| 12  | [\#GetPreparedCardUpdateEulaDataSize](#GetPreparedCardUpdateEulaDataSize "wikilink")                                          |
| 13  | [\#GetPreparedCardUpdateEulaData](#GetPreparedCardUpdateEulaData "wikilink")                                                  |
| 14  | \[4.0.0+\] [\#SetupCardUpdateViaSystemUpdater](#SetupCardUpdateViaSystemUpdater "wikilink")                                   |
| 15  | \[4.0.0+\] [\#HasReceived](#HasReceived "wikilink")                                                                           |
| 16  | \[4.0.0+\] [\#RequestReceiveSystemUpdate](#RequestReceiveSystemUpdate "wikilink")                                             |
| 17  | \[4.0.0+\] [\#GetReceiveProgress](#GetReceiveProgress "wikilink")                                                             |
| 18  | \[4.0.0+\] [\#ApplyReceivedUpdate](#ApplyReceivedUpdate "wikilink")                                                           |
| 19  | \[4.0.0+\] [\#GetReceivedEulaDataSize](#GetReceivedEulaDataSize "wikilink")                                                   |
| 20  | \[4.0.0+\] [\#GetReceivedEulaData](#GetReceivedEulaData "wikilink")                                                           |
| 21  | \[4.0.0+\] [\#SetupToReceiveSystemUpdate](#SetupToReceiveSystemUpdate "wikilink")                                             |
| 22  | \[6.0.0+\] [\#RequestCheckLatestUpdateIncludesRebootlessUpdate](#RequestCheckLatestUpdateIncludesRebootlessUpdate "wikilink") |

Only 1 ISystemUpdateControl can be open at a time.

All Card cmds except SetupCardUpdate\* require
[\#SetupCardUpdate](#SetupCardUpdate "wikilink")/[\#SetupCardUpdateViaSystemUpdater](#SetupCardUpdateViaSystemUpdater "wikilink")
to be used previously.
[\#GetPreparedCardUpdateEulaDataSize](#GetPreparedCardUpdateEulaDataSize "wikilink")/[\#GetPreparedCardUpdateEulaData](#GetPreparedCardUpdateEulaData "wikilink")
checks a different state flag.

### HasDownloaded

No input, returns an output u8 bool flag.

Gets whether a network sysupdate was downloaded, with install pending.

Uses [nim](NIM%20services.md "wikilink") ListSystemUpdateTask and
[nim](NIM%20services.md "wikilink") GetSystemUpdateTaskInfo. When
ListSystemUpdateTask successfully returns a task and
GetSystemUpdateTaskInfo is successful, the output flag is set to:
`*((u8*)(taskinfo+0) == 0x3`. Otherwise, flag=0.

This always returns 0, however this will assert if
GetSystemUpdateTaskInfo fails with ret\!=0x3C89.

### RequestCheckLatestUpdate

No input, returns an output Event handle and an
[\#IAsyncValue](#IAsyncValue "wikilink").

The data that can be read from the
[\#IAsyncValue](#IAsyncValue "wikilink") is
[\#LatestSystemUpdate](#LatestSystemUpdate "wikilink").

### RequestDownloadLatestUpdate

No input, returns an output Event handle and an
[\#IAsyncResult](#IAsyncResult "wikilink").

### GetDownloadProgress

No input, returns an output
[\#SystemUpdateProgress](#SystemUpdateProgress "wikilink").

Similar to [\#HasDownloaded](#HasDownloaded "wikilink") except instead
of a flag, this returns the 0x10-bytes from taskinfo+8. The output
struct is cleared when the task(info) isn't available.

### ApplyDownloadedUpdate

No input/output.

Runs code similar to [\#HasDownloaded](#HasDownloaded "wikilink"),
throwing an error if a network sysupdate isn't ready for install. Then
the sysupdate is installed:

  - Uses ListSystemUpdateTask again, then
    [nim](NIM%20services.md "wikilink") IsExFatDriverIncluded. Runs
    ExFat handling when the output flag is set.
  - On newer system-versions, this uses
    [nim](NIM%20services.md "wikilink") GetSystemUpdateTaskInfo then on
    success uses data from there to save a SystemPlayReport when a state
    flag is set (by default it's not set).
      - The EventId is "systemupdate\_dl\_throughput" with ApplicationId
        0100000000001018.
      - The following fields are added to the report, see [nim
        SystemUpdateTaskInfo](NIM%20services#SystemUpdateTaskInfo.md##SystemUpdateTaskInfo "wikilink"):
        "ContentMetaId", "Version", "DownloadSize", and
        "ThroughputKBps",
  - On newer system-versions, this saves another SystemPlayReport when a
    state flag is set (same flag mentioned above).
      - The EventId is "systemupdate\_pass" with ApplicationId
        0100000000001021.
      - This report has the following fields:
          - "Type"
          - "SourceSystemUpdateMetaId"
          - "SourceSystemUpdateMetaVersion"
          - "SourceExFatStatus"
          - "DestinationSystemUpdateMetaId"
          - "DestinationSystemUpdateMetaVersion"
          - "DestinationExFatStatus"
          - "Rebootless"
  - Since FIRM will be installed later, the two flags in
    [Flash\_Filesystem\#System\_Update\_Control](Flash%20Filesystem#System%20Update%20Control.md##System_Update_Control "wikilink")
    are set to 1.
  - Uses [nim](NIM%20services.md "wikilink") CommitSystemUpdateTask and
    [nim](NIM%20services.md "wikilink") DestroySystemUpdateTask.
  - Installs FIRM. After installing each FIRM, the associated flag in
    [Flash\_Filesystem\#System\_Update\_Control](Flash%20Filesystem#System%20Update%20Control.md##System_Update_Control "wikilink")
    is set to 0.
  - On newer system versions when an input flag is set, this uses
    [NotifySystemDataUpdateEvent](Filesystem%20services.md "wikilink"),
    however this doesn't happen with ApplyDownloadedUpdate since that
    input flag is 0.

### RequestPrepareCardUpdate

No input, returns an output Event handle and an
[\#IAsyncResult](#IAsyncResult "wikilink").

### GetPrepareCardUpdateProgress

No input, returns an output
[\#SystemUpdateProgress](#SystemUpdateProgress "wikilink").

### HasPreparedCardUpdate

No input, returns an output u8 bool flag.

### ApplyCardUpdate

No input/output.

### GetDownloadedEulaDataSize

Takes a type-0x15 input buffer
[\#EulaDataPath](#EulaDataPath "wikilink"), returns an output u64
**filesize**.

Runs code similar to [\#HasDownloaded](#HasDownloaded "wikilink"),
throwing an error if a network sysupdate isn't ready for install.

Uses ListSystemUpdateTask again. Then
[nim](NIM%20services.md "wikilink") GetDownloadedSystemDataPath, with
the output ContentPath being used to mount the EULA title with FS.

Then "<mountname>:/\<[\#EulaDataPath](#EulaDataPath "wikilink")\>" is
opened, gets the **filesize**, then runs cleanup.

### GetDownloadedEulaData

Takes a type-0x15 input buffer
[\#EulaDataPath](#EulaDataPath "wikilink") and a type-0x6 output buffer,
returns an output u64 **filesize**.

Similar to
[\#GetDownloadedEulaDataSize](#GetDownloadedEulaDataSize "wikilink")
except this reads the file instead, using the specified output buffer
with size=filesize. This will throw an error if the filesize is larger
than the buffer size.

### SetupCardUpdate

Takes an input u64 size and a TransferMemory handle, no output.

Official sw creates the TransferMemory with an user-specified buffer,
with permissions=None.

[qlaunch](Qlaunch.md "wikilink") uses size 0x100000 for the
TransferMemory buffer.

### GetPreparedCardUpdateEulaDataSize

Takes a type-0x15 input buffer
[\#EulaDataPath](#EulaDataPath "wikilink"), returns an output u64
**filesize**.

This is similar to
[\#GetDownloadedEulaDataSize](#GetDownloadedEulaDataSize "wikilink").

### GetPreparedCardUpdateEulaData

Takes a type-0x15 input buffer
[\#EulaDataPath](#EulaDataPath "wikilink") and a type-0x6 output buffer,
returns an output u64 **filesize**.

This is similar to
[\#GetDownloadedEulaData](#GetDownloadedEulaData "wikilink").

### SetupCardUpdateViaSystemUpdater

Takes an input u64 size and a TransferMemory handle, no output.

The permissions for the TransferMemory is None.

Same as [\#SetupCardUpdate](#SetupCardUpdate "wikilink"), except this
doesn't have the code for
[GetGameCardHandle/GetGameCardUpdatePartitionInfo](Filesystem%20services.md "wikilink"),
and uses
[OpenRegisteredUpdatePartition](Filesystem%20services.md "wikilink")
instead of
[OpenGameCardFileSystem](Filesystem%20services.md "wikilink"). This uses
the same is\_initialized bool state flag.

### HasReceived

No input, returns an output u8 bool.

Same as [\#HasDownloaded](#HasDownloaded "wikilink") except this uses
[nim](NIM%20services.md "wikilink") cmd71 and cmd73.

### RequestReceiveSystemUpdate

Takes a type-0x15 input buffer containing a
[\#SystemDeliveryInfo](#SystemDeliveryInfo "wikilink"), an u16, an u32,
returns an output Event handle and an
[\#IAsyncResult](#IAsyncResult "wikilink").

[qlaunch](Qlaunch.md "wikilink") uses the same value for the u16 as
[\#RequestSendSystemUpdate](#RequestSendSystemUpdate "wikilink").

### GetReceiveProgress

No input, returns an output
[\#SystemUpdateProgress](#SystemUpdateProgress "wikilink").

Same as [\#GetDownloadProgress](#GetDownloadProgress "wikilink") except
this uses [nim](NIM%20services.md "wikilink") cmd71 and cmd73.

### ApplyReceivedUpdate

No input/output.

### GetReceivedEulaDataSize

Takes a type-0x15 input buffer
[\#EulaDataPath](#EulaDataPath "wikilink"), returns an output u64
**filesize**.

This is similar to
[\#GetDownloadedEulaDataSize](#GetDownloadedEulaDataSize "wikilink").

### GetReceivedEulaData

Takes a type-0x15 input buffer
[\#EulaDataPath](#EulaDataPath "wikilink") and a type-0x6 output buffer,
returns an output u64 **filesize**.

This is similar to
[\#GetDownloadedEulaData](#GetDownloadedEulaData "wikilink").

### SetupToReceiveSystemUpdate

No input/output.

This just uses [nim](NIM%20services.md "wikilink") ListSystemUpdateTask,
then when a task is returned uses it with DestroySystemUpdateTask.

### RequestCheckLatestUpdateIncludesRebootlessUpdate

No input, returns an output Event handle and an
[\#IAsyncValue](#IAsyncValue "wikilink").

## BackgroundNetworkUpdateState

| Value | Description                       |
| ----- | --------------------------------- |
| 0     | No sysupdate task exists.         |
| 1     | Sysupdate download in progress.   |
| 2     | Sysupdate ready, pending install. |

This is "nn::ns::BackgroundNetworkUpdateState". This is an u8.

Similar to [\#HasDownloaded](#HasDownloaded "wikilink"),
[\#GetBackgroundNetworkUpdateState](#GetBackgroundNetworkUpdateState "wikilink")
uses [nim](NIM%20services.md "wikilink") ListSystemUpdateTask and
[nim](NIM%20services.md "wikilink") GetSystemUpdateTaskInfo. When
ListSystemUpdateTask successfully returns a task and
GetSystemUpdateTaskInfo is successful, the output value is set to: `1 +
*((u8*)(taskinfo+0) == 0x3`. Otherwise, value=0.

[\#GetBackgroundNetworkUpdateState](#GetBackgroundNetworkUpdateState "wikilink")
always returns Result 0, however this will assert if
GetSystemUpdateTaskInfo fails with ret\!=0x3C89.

## SystemUpdateProgress

| Offset | Size | Description                                                                                                                                                                                                                        |
| ------ | ---- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | s64 Current size. This value can be larger than total\_size when the async operation is finishing. When total\_size is \<=0, this current\_size field may contain a progress value for when the total\_size is not yet determined. |
| 0x8    | 0x8  | s64 Total size, this field is only valid when \>0.                                                                                                                                                                                 |

This is "nn::ns::SystemUpdateProgress". This is a 0x10-byte struct.

Commands which have this as output will return 0 with the output
cleared, when no task is available.

## EulaDataPath

This is "nn::ns::detail::EulaDataPath". This is a 0x100-byte struct.

This contains a file path.

## SystemDeliveryInfo

| Offset | Size | Description                                                                                                                                                                 |
| ------ | ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x4  | Must be \<= to and match [system-setting](System%20Settings.md "wikilink") <code>contents\_delivery\!system\_delivery\_protocol\_version<code>.                             |
| 0x4    | 0x8  | Unused by [\#RequestSendSystemUpdate](#RequestSendSystemUpdate "wikilink")/[\#RequestReceiveSystemUpdate](#RequestReceiveSystemUpdate "wikilink"), besides HMAC validation. |
| 0xC    | 0x4  | SystemUpdate meta version.                                                                                                                                                  |
| 0x10   | 0x8  | SystemUpdate meta titleID.                                                                                                                                                  |
| 0x18   | 0x1  | Copied into state by [\#RequestSendSystemUpdate](#RequestSendSystemUpdate "wikilink").                                                                                      |
| 0x19   | 0xC7 | Unused by [\#RequestSendSystemUpdate](#RequestSendSystemUpdate "wikilink")/[\#RequestReceiveSystemUpdate](#RequestReceiveSystemUpdate "wikilink"), besides HMAC validation. |
| 0xE0   | 0x20 | HMAC-SHA256 over the previous 0xE0-bytes.                                                                                                                                   |

This is "nn::ns::SystemDeliveryInfo". This is a 0x100-byte struct.

## LatestSystemUpdate

| Value        | Description |
| ------------ | ----------- |
| 1            | Unknown.    |
| 2            | Unknown.    |
| Other values | Unknown.    |

This is "nn::ns::LatestSystemUpdate". This is an u8.

# IAsyncValue

This is "nn::ns::detail::IAsyncValue".

| Cmd | Name                       |
| --- | -------------------------- |
| 0   | GetSize                    |
| 1   | Get                        |
| 2   | Cancel                     |
| 3   | \[4.0.0+\] GetErrorContext |

Official sw creates a container object for this using the output from
the service commands, which contains the IAsyncValue object, and the
Event with EventClearMode=0.

  - GetSize: No input, returns an output u64.
  - Get: Takes a type-0x6 output buffer, no output. Official sw waits on
    the Event prior to using this cmd.
  - Cancel: No input/output. Used by official sw when closing the
    object, when the serv-obj is initialized (after using the cmd,
    official sw will also wait on the Event). This cmd is also used in
    other official sw funcs.
  - GetErrorContext: No input/output, takes a type-0x16 output buffer
    containing an
    [ErrorContext](Error%20Applet#ErrorContext.md##ErrorContext "wikilink").

# IAsyncResult

This is "nn::ns::detail::IAsyncResult".

| Cmd | Name                       |
| --- | -------------------------- |
| 0   | Get                        |
| 1   | Cancel                     |
| 2   | \[4.0.0+\] GetErrorContext |

Official sw creates a container object for this using the output from
the service commands, which contains the IAsyncResult object, and the
Event with EventClearMode=0.

  - Get: No input/output. Official sw waits on the Event prior to using
    this cmd.
  - Cancel: No input/output. Used by official sw when closing the
    object, when the serv-obj is initialized (after using the cmd,
    official sw will also wait on the Event). This cmd is also used in
    other official sw funcs.
  - GetErrorContext: No input/output, takes a type-0x16 output buffer
    containing an
    [ErrorContext](Error%20Applet#ErrorContext.md##ErrorContext "wikilink").

# ns:dev

This is "nn::ns::detail::IDevelopInterface".

| Cmd | Name                                                                                                |
| --- | --------------------------------------------------------------------------------------------------- |
| 0   | [\#LaunchProgram](#LaunchProgram "wikilink")                                                        |
| 1   | [\#TerminateProcess](#TerminateProcess "wikilink")                                                  |
| 2   | [\#TerminateProgram](#TerminateProgram "wikilink")                                                  |
| 4   | [\#GetShellEvent](#GetShellEvent "wikilink")                                                        |
| 5   | [\#GetShellEventInfo](#GetShellEventInfo "wikilink")                                                |
| 6   | [\#TerminateApplication](#TerminateApplication "wikilink")                                          |
| 7   | [\#PrepareLaunchProgramFromHost](#PrepareLaunchProgramFromHost "wikilink")                          |
| 8   | [\#LaunchApplicationForDevelop](#LaunchApplicationForDevelop "wikilink")                            |
| 9   | [\#LaunchApplicationWithStorageIdForDevelop](#LaunchApplicationWithStorageIdForDevelop "wikilink")  |
| 10  | \[6.0.0-8.1.0\] IsSystemMemoryResourceLimitBoosted                                                  |
| 11  | \[6.0.0+\] GetRunningApplicationProcessIdForDevelop                                                 |
| 12  | \[6.0.0+\] SetCurrentApplicationRightsEnvironmentCanBeActiveForDevelop                              |
| 13  | \[9.0.0+\] [\#CreateApplicationResourceForDevelop](#CreateApplicationResourceForDevelop "wikilink") |
| 14  | \[9.0.0+\] [\#IsPreomiaForDevelop](#IsPreomiaForDevelop "wikilink")                                 |

## LaunchProgram

Wrapper for "pm:shell"
[LaunchProcess](Process%20Manager%20services#pm:shell.md##pm:shell "wikilink").

## TerminateProcess

Wrapper for "pm:shell"
[TerminateProcess](Process%20Manager%20services#pm:shell.md##pm:shell "wikilink").

## TerminateProgram

Wrapper for "pm:shell"
[TerminateProgram](Process%20Manager%20services#pm:shell.md##pm:shell "wikilink").

## GetShellEvent

Wrapper for "pm:shell"
[GetProcessEventHandle](Process%20Manager%20services#pm:shell.md##pm:shell "wikilink").

## GetShellEventInfo

Wrapper for "pm:shell"
[GetProcessEventInfo](Process%20Manager%20services#pm:shell.md##pm:shell "wikilink").

## TerminateApplication

Calls "pm:shell"
[GetApplicationProcessIdForShell](Process%20Manager%20services#pm:shell.md##pm:shell "wikilink")
and sends PID to
[TerminateProcess](Process%20Manager%20services#pm:shell.md##pm:shell "wikilink").

## PrepareLaunchProgramFromHost

Takes a type-0x5 input buffer containing the
[ContentPath](Filesystem%20services.md "wikilink"), returns an output
0x10-byte struct.

Calls
[IPathResolverForStorage](NCM%20services#IPathResolverForStorage.md##IPathResolverForStorage "wikilink")
Set...NcaPath functions.

## LaunchApplicationForDevelop

Takes an input u32
[LaunchFlags](Process%20Manager%20services#LaunchFlags.md##LaunchFlags "wikilink")
and u64 titleID, returns an output u64 PID.

Same as LaunchApplicationWithStorageId except the last two params passed
to the internal vtable funcptr call are value 0x6, instead of from the
command input.

## LaunchApplicationWithStorageIdForDevelop

Takes 2 input u8s, an u32
[LaunchFlags](Process%20Manager%20services#LaunchFlags.md##LaunchFlags "wikilink"),
and an u64 titleID. Returns an output u64 PID.

Launches an application title which is registered with NS.

## CreateApplicationResourceForDevelop

Takes an input u32 (1 = Preomia). Returns an
[\#IApplicationResource](#IApplicationResource "wikilink").

## IsPreomiaForDevelop

Takes an u64 titleID. Returns a bool.

# VersionListData

This is "nn::ns::VersionListData".

# ApplicationUpdateInfo

This is "nn::ns::ApplicationUpdateInfo".

# NoDownloadRightsErrorResolution

This is "nn::ns::NoDownloadRightsErrorResolution".

[Category:Services](Category:Services "wikilink")
