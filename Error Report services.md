# erpt:c

This is "nn::erpt::sf::IContext".

| Cmd | Name                                                |
| --- | --------------------------------------------------- |
| 0   | [\#SubmitContext](#SubmitContext "wikilink")        |
| 1   | [\#CreateReport](#CreateReport "wikilink")          |
| 2   | \[3.0.0+\] SetInitialLaunchSettingsCompletionTime   |
| 3   | \[3.0.0+\] ClearInitialLaunchSettingsCompletionTime |
| 4   | \[3.0.0+\] UpdatePowerOnTime                        |
| 5   | \[3.0.0+\] UpdateAwakeTime                          |
| 6   | \[5.0.0+\] SubmitMultipleCategoryContext            |
| 7   | \[6.0.0+\] UpdateApplicationLaunchTime              |
| 8   | \[6.0.0+\] ClearApplicationLaunchTime               |
| 9   | \[8.0.0+\] SubmitAttachment                         |
| 10  | \[8.0.0+\] CreateReportWithAttachments              |

## SubmitContext

Takes 2 type-5 input buffers (**ContextStruct** and **FieldList**).

### ContextStruct

This is a 0x160 bytes structure used to encapsulate an error report
context.

| Offset | Size  | Description                   |
| ------ | ----- | ----------------------------- |
| 0x0    | 0x4   | Empty                         |
| 0x4    | 0x4   | Empty                         |
| 0x8    | 0x4   | CategoryId                    |
| 0xC    | 0x144 | Empty                         |
| 0x150  | 0x8   | Pointer to a FieldList object |
| 0x158  | 0x4   | FieldList free size           |
| 0x15C  | 0x4   | FieldList total size          |

## CreateReport

Takes a u32 (**ReportType**) and 3 type-5 input buffers
(**ContextStruct**, **FieldList** and **ReportMetaData**).

# erpt:r

This is "nn::erpt::sf::ISession".

| Cmd | Name                      |
| --- | ------------------------- |
| 0   | OpenReport                |
| 1   | OpenManager               |
| 2   | \[8.0.0+\] OpenAttachment |

## IReport

This is "nn::erpt::sf::IReport".

| Cmd | Name     |
| --- | -------- |
| 0   | Open     |
| 1   | Read     |
| 2   | SetFlags |
| 3   | GetFlags |
| 4   | Close    |
| 5   | GetSize  |

## IManager

This is "nn::erpt::sf::IManager".

| Cmd | Name                                 |
| --- | ------------------------------------ |
| 0   | GetReportList                        |
| 1   | GetEvent                             |
| 2   | \[4.0.0+\] CleanupReports            |
| 3   | \[5.0.0+\] DeleteReport              |
| 4   | \[5.0.0+\] GetStorageUsageStatistics |
| 5   | \[8.0.0+\] GetAttachmentList         |

## IAttachment

This is "nn::erpt::sf::IAttachment".

| Cmd | Name     |
| --- | -------- |
| 0   | Open     |
| 1   | Read     |
| 2   | SetFlags |
| 3   | GetFlags |
| 4   | Close    |
| 5   | GetSize  |

# Reports

## Fields

| FieldId | Name                                                                | Format  | Description                                                           |
| ------- | ------------------------------------------------------------------- | ------- | --------------------------------------------------------------------- |
| 0x0     | TestU64                                                             |         |                                                                       |
| 0x1     | TestU32                                                             |         |                                                                       |
| 0x2     | TestI64                                                             |         |                                                                       |
| 0x3     | TestI32                                                             |         |                                                                       |
| 0x4     | TestString                                                          |         |                                                                       |
| 0x5     | TestU8Array                                                         |         |                                                                       |
| 0x6     | TestU32Array                                                        |         |                                                                       |
| 0x7     | TestU64Array                                                        |         |                                                                       |
| 0x8     | TestI32Array                                                        |         |                                                                       |
| 0x9     | TestI64Array                                                        |         |                                                                       |
| 0xA     | ErrorCode                                                           |         |                                                                       |
| 0xB     | ErrorDescription                                                    |         |                                                                       |
| 0xC     | OccurrenceTimestamp                                                 | Integer | UTC unix timestamp from [user-time](PCV%20services.md "wikilink").    |
| 0xD     | ReportIdentifier                                                    |         |                                                                       |
| 0xE     | ConnectionStatus                                                    |         |                                                                       |
| 0xF     | AccessPointSSID                                                     |         |                                                                       |
| 0x10    | AccessPointSecurityType                                             |         |                                                                       |
| 0x11    | RadioStrength                                                       |         |                                                                       |
| 0x12    | NXMacAddress                                                        |         |                                                                       |
| 0x13    | IPAddressAcquisitionMethod                                          |         |                                                                       |
| 0x14    | CurrentIPAddress                                                    |         |                                                                       |
| 0x15    | SubnetMask                                                          |         |                                                                       |
| 0x16    | GatewayIPAddress                                                    |         |                                                                       |
| 0x17    | DNSType                                                             |         |                                                                       |
| 0x18    | PriorityDNSIPAddress                                                |         |                                                                       |
| 0x19    | AlternateDNSIPAddress                                               |         |                                                                       |
| 0x1A    | UseProxyFlag                                                        |         |                                                                       |
| 0x1B    | ProxyIPAddress                                                      |         |                                                                       |
| 0x1C    | ProxyPort                                                           |         |                                                                       |
| 0x1D    | ProxyAutoAuthenticateFlag                                           |         |                                                                       |
| 0x1E    | MTU                                                                 |         |                                                                       |
| 0x1F    | ConnectAutomaticallyFlag                                            |         |                                                                       |
| 0x20    | UseStealthNetworkFlag                                               |         |                                                                       |
| 0x21    | LimitHighCapacityFlag                                               |         |                                                                       |
| 0x22    | NATType                                                             |         |                                                                       |
| 0x23    | WirelessAPMacAddress                                                |         |                                                                       |
| 0x24    | GlobalIPAddress                                                     |         |                                                                       |
| 0x25    | EnableWirelessInterfaceFlag                                         |         |                                                                       |
| 0x26    | EnableWifiFlag                                                      |         |                                                                       |
| 0x27    | EnableBluetoothFlag                                                 |         |                                                                       |
| 0x28    | EnableNFCFlag                                                       |         |                                                                       |
| 0x29    | NintendoZoneSSIDListVersion                                         |         |                                                                       |
| 0x2A    | LANAdapterMacAddress                                                |         |                                                                       |
| 0x2B    | ApplicationID                                                       |         |                                                                       |
| 0x2C    | ApplicationTitle                                                    |         |                                                                       |
| 0x2D    | ApplicationVersion                                                  |         |                                                                       |
| 0x2E    | ApplicationStorageLocation                                          |         |                                                                       |
| 0x2F    | DownloadContentType                                                 |         |                                                                       |
| 0x30    | InstallContentType                                                  |         |                                                                       |
| 0x31    | ConsoleStartingUpFlag                                               |         |                                                                       |
| 0x32    | SystemStartingUpFlag                                                |         |                                                                       |
| 0x33    | ConsoleFirstInitFlag                                                |         |                                                                       |
| 0x34    | HomeMenuScreenDisplayedFlag                                         |         |                                                                       |
| 0x35    | DataManagementScreenDisplayedFlag                                   |         |                                                                       |
| 0x36    | ConnectionTestingFlag                                               |         |                                                                       |
| 0x37    | ApplicationRunningFlag                                              |         |                                                                       |
| 0x38    | DataCorruptionDetectedFlag                                          |         |                                                                       |
| 0x39    | ProductModel                                                        |         |                                                                       |
| 0x3A    | CurrentLanguage                                                     |         |                                                                       |
| 0x3B    | UseNetworkTimeProtocolFlag                                          |         |                                                                       |
| 0x3C    | TimeZone                                                            |         |                                                                       |
| 0x3D    | ControllerFirmware                                                  |         |                                                                       |
| 0x3E    | VideoOutputSetting                                                  |         |                                                                       |
| 0x3F    | NANDFreeSpace                                                       |         |                                                                       |
| 0x40    | SDCardFreeSpace                                                     |         |                                                                       |
| 0x41    | SerialNumber                                                        |         |                                                                       |
| 0x42    | OsVersion                                                           |         |                                                                       |
| 0x43    | ScreenBrightnessAutoAdjustFlag                                      |         |                                                                       |
| 0x44    | HdmiAudioOutputMode                                                 |         |                                                                       |
| 0x45    | SpeakerAudioOutputMode                                              |         |                                                                       |
| 0x46    | HeadphoneAudioOutputMode                                            |         |                                                                       |
| 0x47    | MuteOnHeadsetUnpluggedFlag                                          |         |                                                                       |
| 0x48    | NumUserRegistered                                                   |         |                                                                       |
| 0x49    | StorageAutoOrganizeFlag                                             |         |                                                                       |
| 0x4A    | ControllerVibrationVolume                                           |         |                                                                       |
| 0x4B    | LockScreenFlag                                                      |         |                                                                       |
| 0x4C    | InternalBatteryLotNumber                                            |         |                                                                       |
| 0x4D    | LeftControllerSerialNumber                                          |         |                                                                       |
| 0x4E    | RightControllerSerialNumber                                         |         |                                                                       |
| 0x4F    | NotifyInGameDownloadCompletionFlag                                  |         |                                                                       |
| 0x50    | NotificationSoundFlag                                               |         |                                                                       |
| 0x51    | TVResolutionSetting                                                 |         |                                                                       |
| 0x52    | RGBRangeSetting                                                     |         |                                                                       |
| 0x53    | ReduceScreenBurnFlag                                                |         |                                                                       |
| 0x54    | TVAllowsCecFlag                                                     |         |                                                                       |
| 0x55    | HandheldModeTimeToScreenSleep                                       |         |                                                                       |
| 0x56    | ConsoleModeTimeToScreenSleep                                        |         |                                                                       |
| 0x57    | StopAutoSleepDuringContentPlayFlag                                  |         |                                                                       |
| 0x58    | LastConnectionTestDownloadSpeed                                     |         |                                                                       |
| 0x59    | LastConnectionTestUploadSpeed                                       |         |                                                                       |
| 0x5A    | \[5.0.0+\] DEPRECATED\_ServerFQDN (\[1.0.0-4.1.0\] ServerFQDN)      |         |                                                                       |
| 0x5B    | HTTPRequestContents                                                 |         |                                                                       |
| 0x5C    | HTTPRequestResponseContents                                         |         |                                                                       |
| 0x5D    | EdgeServerIPAddress                                                 |         |                                                                       |
| 0x5E    | CDNContentPath                                                      |         |                                                                       |
| 0x5F    | FileAccessPath                                                      |         |                                                                       |
| 0x60    | GameCardCID                                                         |         |                                                                       |
| 0x61    | NANDCID                                                             |         |                                                                       |
| 0x62    | MicroSDCID                                                          |         |                                                                       |
| 0x63    | NANDSpeedMode                                                       |         |                                                                       |
| 0x64    | MicroSDSpeedMode                                                    |         |                                                                       |
| 0x65    | GameCardSpeedMode                                                   |         |                                                                       |
| 0x66    | UserAccountInternalID                                               |         |                                                                       |
| 0x67    | NetworkServiceAccountInternalID                                     |         |                                                                       |
| 0x68    | NintendoAccountInternalID                                           |         |                                                                       |
| 0x69    | USB3AvailableFlag                                                   |         |                                                                       |
| 0x6A    | CallStack                                                           |         |                                                                       |
| 0x6B    | SystemStartupLog                                                    |         |                                                                       |
| 0x6C    | RegionSetting                                                       |         |                                                                       |
| 0x6D    | NintendoZoneConnectedFlag                                           |         |                                                                       |
| 0x6E    | ForcedSleepHighTemperatureReading                                   |         |                                                                       |
| 0x6F    | ForcedSleepFanSpeedReading                                          |         |                                                                       |
| 0x70    | ForcedSleepHWInfo                                                   |         |                                                                       |
| 0x71    | AbnormalPowerStateInfo                                              |         |                                                                       |
| 0x72    | ScreenBrightnessLevel                                               |         |                                                                       |
| 0x73    | ProgramId                                                           |         |                                                                       |
| 0x74    | AbortFlag                                                           |         |                                                                       |
| 0x75    | ReportVisibilityFlag                                                |         |                                                                       |
| 0x76    | FatalFlag                                                           |         |                                                                       |
| 0x77    | OccurrenceTimestampNet                                              | Integer | UTC unix timestamp from [network-time](PCV%20services.md "wikilink"). |
| 0x78    | ResultBacktrace                                                     |         |                                                                       |
| 0x79    | GeneralRegisterAarch32                                              |         |                                                                       |
| 0x7A    | StackBacktrace32                                                    |         |                                                                       |
| 0x7B    | ExceptionInfoAarch32                                                |         |                                                                       |
| 0x7C    | GeneralRegisterAarch64                                              |         |                                                                       |
| 0x7D    | ExceptionInfoAarch64                                                |         |                                                                       |
| 0x7E    | StackBacktrace64                                                    |         |                                                                       |
| 0x7F    | RegisterSetFlag32                                                   |         |                                                                       |
| 0x80    | RegisterSetFlag64                                                   |         |                                                                       |
| 0x81    | ProgramMappedAddr32                                                 |         |                                                                       |
| 0x82    | ProgramMappedAddr64                                                 |         |                                                                       |
| 0x83    | AbortType                                                           |         |                                                                       |
| 0x84    | PrivateOsVersion                                                    |         |                                                                       |
| 0x85    | CurrentSystemPowerState                                             |         |                                                                       |
| 0x86    | PreviousSystemPowerState                                            |         |                                                                       |
| 0x87    | DestinationSystemPowerState                                         |         |                                                                       |
| 0x88    | PscTransitionCurrentState                                           |         |                                                                       |
| 0x89    | PscTransitionPreviousState                                          |         |                                                                       |
| 0x8A    | PscInitializedList                                                  |         |                                                                       |
| 0x8B    | PscCurrentPmStateList                                               |         |                                                                       |
| 0x8C    | PscNextPmStateList                                                  |         |                                                                       |
| 0x8D    | PerformanceMode                                                     |         |                                                                       |
| 0x8E    | PerformanceConfiguration                                            |         |                                                                       |
| 0x8F    | Throttled                                                           |         |                                                                       |
| 0x90    | ThrottlingDuration                                                  |         |                                                                       |
| 0x91    | ThrottlingTimestamp                                                 | Integer | UTC unix timestamp                                                    |
| 0x92    | GameCardCrcErrorCount                                               |         |                                                                       |
| 0x93    | GameCardAsicCrcErrorCount                                           |         |                                                                       |
| 0x94    | GameCardRefreshCount                                                |         |                                                                       |
| 0x95    | GameCardReadRetryCount                                              |         |                                                                       |
| 0x96    | EdidBlock                                                           |         |                                                                       |
| 0x97    | EdidExtensionBlock                                                  |         |                                                                       |
| 0x98    | CreateProcessFailureFlag                                            |         |                                                                       |
| 0x99    | TemperaturePcb                                                      |         |                                                                       |
| 0x9A    | TemperatureSoc                                                      |         |                                                                       |
| 0x9B    | CurrentFanDuty                                                      |         |                                                                       |
| 0x9C    | LastDvfsThresholdTripped                                            |         |                                                                       |
| 0x9D    | CradlePdcHFwVersion                                                 |         |                                                                       |
| 0x9E    | CradlePdcAFwVersion                                                 |         |                                                                       |
| 0x9F    | CradleMcuFwVersion                                                  |         |                                                                       |
| 0xA0    | CradleDp2HdmiFwVersion                                              |         |                                                                       |
| 0xA1    | RunningApplicationId                                                |         |                                                                       |
| 0xA2    | RunningApplicationTitle                                             |         |                                                                       |
| 0xA3    | RunningApplicationVersion                                           |         |                                                                       |
| 0xA4    | RunningApplicationStorageLocation                                   |         |                                                                       |
| 0xA5    | RunningAppletList                                                   |         |                                                                       |
| 0xA6    | FocusedAppletHistory                                                |         |                                                                       |
| 0xA7    | CompositorState                                                     |         |                                                                       |
| 0xA8    | CompositorLayerState                                                |         |                                                                       |
| 0xA9    | CompositorDisplayState                                              |         |                                                                       |
| 0xAA    | CompositorHWCState                                                  |         |                                                                       |
| 0xAB    | InputCurrentLimit                                                   |         |                                                                       |
| 0xAC    | BoostModeCurrentLimit                                               |         |                                                                       |
| 0xAD    | FastChargeCurrentLimit                                              |         |                                                                       |
| 0xAE    | ChargeVoltageLimit                                                  |         |                                                                       |
| 0xAF    | ChargeConfiguration                                                 |         |                                                                       |
| 0xB0    | HizMode                                                             |         |                                                                       |
| 0xB1    | ChargeEnabled                                                       |         |                                                                       |
| 0xB2    | PowerSupplyPath                                                     |         |                                                                       |
| 0xB3    | BatteryTemperature                                                  |         |                                                                       |
| 0xB4    | BatteryChargePercent                                                |         |                                                                       |
| 0xB5    | BatteryChargeVoltage                                                |         |                                                                       |
| 0xB6    | BatteryAge                                                          |         |                                                                       |
| 0xB7    | PowerRole                                                           |         |                                                                       |
| 0xB8    | PowerSupplyType                                                     |         |                                                                       |
| 0xB9    | PowerSupplyVoltage                                                  |         |                                                                       |
| 0xBA    | PowerSupplyCurrent                                                  |         |                                                                       |
| 0xBB    | FastBatteryChargingEnabled                                          |         |                                                                       |
| 0xBC    | ControllerPowerSupplyAcquired                                       |         |                                                                       |
| 0xBD    | OtgRequested                                                        |         |                                                                       |
| 0xBE    | NANDPreEolInfo                                                      |         |                                                                       |
| 0xBF    | NANDDeviceLifeTimeEstTypA                                           |         |                                                                       |
| 0xC0    | NANDDeviceLifeTimeEstTypB                                           |         |                                                                       |
| 0xC1    | NANDPatrolCount                                                     |         |                                                                       |
| 0xC2    | NANDNumActivationFailures                                           |         |                                                                       |
| 0xC3    | NANDNumActivationErrorCorrections                                   |         |                                                                       |
| 0xC4    | NANDNumReadWriteFailures                                            |         |                                                                       |
| 0xC5    | NANDNumReadWriteErrorCorrections                                    |         |                                                                       |
| 0xC6    | NANDErrorLog                                                        |         |                                                                       |
| 0xC7    | SdCardUserAreaSize                                                  |         |                                                                       |
| 0xC8    | SdCardProtectedAreaSize                                             |         |                                                                       |
| 0xC9    | SdCardNumActivationFailures                                         |         |                                                                       |
| 0xCA    | SdCardNumActivationErrorCorrections                                 |         |                                                                       |
| 0xCB    | SdCardNumReadWriteFailures                                          |         |                                                                       |
| 0xCC    | SdCardNumReadWriteErrorCorrections                                  |         |                                                                       |
| 0xCD    | SdCardErrorLog                                                      |         |                                                                       |
| 0xCE    | EncryptionKey                                                       |         |                                                                       |
| 0xCF    | EncryptedExceptionInfo                                              |         |                                                                       |
| 0xD0    | GameCardTimeoutRetryErrorCount                                      |         |                                                                       |
| 0xD1    | FsRemountForDataCorruptCount                                        |         |                                                                       |
| 0xD2    | FsRemountForDataCorruptRetryOutCount                                |         |                                                                       |
| 0xD3    | \[3.0.0+\] GameCardInsertionCount                                   |         |                                                                       |
| 0xD4    | \[3.0.0+\] GameCardRemovalCount                                     |         |                                                                       |
| 0xD5    | \[3.0.0+\] GameCardAsicInitializeCount                              |         |                                                                       |
| 0xD6    | \[3.0.0+\] TestU16                                                  |         |                                                                       |
| 0xD7    | \[3.0.0+\] TestU8                                                   |         |                                                                       |
| 0xD8    | \[3.0.0+\] TestI16                                                  |         |                                                                       |
| 0xD9    | \[3.0.0+\] TestI8                                                   |         |                                                                       |
| 0xDA    | \[3.0.0+\] SystemAppletScene                                        |         |                                                                       |
| 0xDB    | \[3.0.0+\] CodecType                                                |         |                                                                       |
| 0xDC    | \[3.0.0+\] DecodeBuffers                                            |         |                                                                       |
| 0xDD    | \[3.0.0+\] FrameWidth                                               |         |                                                                       |
| 0xDE    | \[3.0.0+\] FrameHeight                                              |         |                                                                       |
| 0xDF    | \[3.0.0+\] ColorPrimaries                                           |         |                                                                       |
| 0xE0    | \[3.0.0+\] TransferCharacteristics                                  |         |                                                                       |
| 0xE1    | \[3.0.0+\] MatrixCoefficients                                       |         |                                                                       |
| 0xE2    | \[3.0.0+\] DisplayWidth                                             |         |                                                                       |
| 0xE3    | \[3.0.0+\] DisplayHeight                                            |         |                                                                       |
| 0xE4    | \[3.0.0+\] DARWidth                                                 |         |                                                                       |
| 0xE5    | \[3.0.0+\] DARHeight                                                |         |                                                                       |
| 0xE6    | \[3.0.0+\] ColorFormat                                              |         |                                                                       |
| 0xE7    | \[3.0.0+\] ColorSpace                                               |         |                                                                       |
| 0xE8    | \[3.0.0+\] SurfaceLayout                                            |         |                                                                       |
| 0xE9    | \[3.0.0+\] BitStream                                                |         |                                                                       |
| 0xEA    | \[3.0.0+\] VideoDecState                                            |         |                                                                       |
| 0xEB    | \[3.0.0+\] GpuErrorChannelId                                        |         |                                                                       |
| 0xEC    | \[3.0.0+\] GpuErrorAruId                                            |         |                                                                       |
| 0xED    | \[3.0.0+\] GpuErrorType                                             |         |                                                                       |
| 0xEE    | \[3.0.0+\] GpuErrorFaultInfo                                        |         |                                                                       |
| 0xEF    | \[3.0.0+\] GpuErrorWriteAccess                                      |         |                                                                       |
| 0xF0    | \[3.0.0+\] GpuErrorFaultAddress                                     |         |                                                                       |
| 0xF1    | \[3.0.0+\] GpuErrorFaultUnit                                        |         |                                                                       |
| 0xF2    | \[3.0.0+\] GpuErrorFaultType                                        |         |                                                                       |
| 0xF3    | \[3.0.0+\] GpuErrorHwContextPointer                                 |         |                                                                       |
| 0xF4    | \[3.0.0+\] GpuErrorContextStatus                                    |         |                                                                       |
| 0xF5    | \[3.0.0+\] GpuErrorPbdmaIntr                                        |         |                                                                       |
| 0xF6    | \[3.0.0+\] GpuErrorPbdmaErrorType                                   |         |                                                                       |
| 0xF7    | \[3.0.0+\] GpuErrorPbdmaHeaderShadow                                |         |                                                                       |
| 0xF8    | \[3.0.0+\] GpuErrorPbdmaHeader                                      |         |                                                                       |
| 0xF9    | \[3.0.0+\] GpuErrorPbdmaGpShadow0                                   |         |                                                                       |
| 0xFA    | \[3.0.0+\] GpuErrorPbdmaGpShadow1                                   |         |                                                                       |
| 0xFB    | \[3.0.0+\] AccessPointChannel                                       |         |                                                                       |
| 0xFC    | \[3.0.0+\] ThreadName                                               |         |                                                                       |
| 0xFD    | \[3.0.0+\] AdspExceptionRegisters                                   |         |                                                                       |
| 0xFE    | \[3.0.0+\] AdspExceptionSpsr                                        |         |                                                                       |
| 0xFF    | \[3.0.0+\] AdspExceptionProgramCounter                              |         |                                                                       |
| 0x100   | \[3.0.0+\] AdspExceptionLinkRegister                                |         |                                                                       |
| 0x101   | \[3.0.0+\] AdspExceptionStackPointer                                |         |                                                                       |
| 0x102   | \[3.0.0+\] AdspExceptionArmModeRegisters                            |         |                                                                       |
| 0x103   | \[3.0.0+\] AdspExceptionStackAddress                                |         |                                                                       |
| 0x104   | \[3.0.0+\] AdspExceptionStackDump                                   |         |                                                                       |
| 0x105   | \[3.0.0+\] AdspExceptionReason                                      |         |                                                                       |
| 0x106   | \[3.0.0+\] OscillatorClock                                          |         |                                                                       |
| 0x107   | \[3.0.0+\] CpuDvfsTableClocks                                       |         |                                                                       |
| 0x108   | \[3.0.0+\] CpuDvfsTableVoltages                                     |         |                                                                       |
| 0x109   | \[3.0.0+\] GpuDvfsTableClocks                                       |         |                                                                       |
| 0x10A   | \[3.0.0+\] GpuDvfsTableVoltages                                     |         |                                                                       |
| 0x10B   | \[3.0.0+\] EmcDvfsTableClocks                                       |         |                                                                       |
| 0x10C   | \[3.0.0+\] EmcDvfsTableVoltages                                     |         |                                                                       |
| 0x10D   | \[3.0.0+\] ModuleClockFrequencies                                   |         |                                                                       |
| 0x10E   | \[3.0.0+\] ModuleClockEnableFlags                                   |         |                                                                       |
| 0x10F   | \[3.0.0+\] ModulePowerEnableFlags                                   |         |                                                                       |
| 0x110   | \[3.0.0+\] ModuleResetAssertFlags                                   |         |                                                                       |
| 0x111   | \[3.0.0+\] ModuleMinimumVoltageClockRates                           |         |                                                                       |
| 0x112   | \[3.0.0+\] PowerDomainEnableFlags                                   |         |                                                                       |
| 0x113   | \[3.0.0+\] PowerDomainVoltages                                      |         |                                                                       |
| 0x114   | \[3.0.0+\] AccessPointRssi                                          |         |                                                                       |
| 0x115   | \[3.0.0+\] FuseInfo                                                 |         |                                                                       |
| 0x116   | \[3.0.0+\] VideoLog                                                 |         |                                                                       |
| 0x117   | \[3.0.0+\] GameCardDeviceId                                         |         |                                                                       |
| 0x118   | \[3.0.0+\] GameCardAsicReinitializeCount                            |         |                                                                       |
| 0x119   | \[3.0.0+\] GameCardAsicReinitializeFailureCount                     |         |                                                                       |
| 0x11A   | \[3.0.0+\] GameCardAsicReinitializeFailureDetail                    |         |                                                                       |
| 0x11B   | \[3.0.0+\] GameCardRefreshSuccessCount                              |         |                                                                       |
| 0x11C   | \[3.0.0+\] GameCardAwakenCount                                      |         |                                                                       |
| 0x11D   | \[3.0.0+\] GameCardAwakenFailureCount                               |         |                                                                       |
| 0x11E   | \[3.0.0+\] GameCardReadCountFromInsert                              |         |                                                                       |
| 0x11F   | \[3.0.0+\] GameCardReadCountFromAwaken                              |         |                                                                       |
| 0x120   | \[3.0.0+\] GameCardLastReadErrorPageAddress                         |         |                                                                       |
| 0x121   | \[3.0.0+\] GameCardLastReadErrorPageCount                           |         |                                                                       |
| 0x122   | \[3.0.0+\] AppletManagerContextTrace                                |         |                                                                       |
| 0x123   | \[3.0.0+\] NvDispIsRegistered                                       |         |                                                                       |
| 0x124   | \[3.0.0+\] NvDispIsSuspend                                          |         |                                                                       |
| 0x125   | \[3.0.0+\] NvDispDC0SurfaceNum                                      |         |                                                                       |
| 0x126   | \[3.0.0+\] NvDispDC1SurfaceNum                                      |         |                                                                       |
| 0x127   | \[3.0.0+\] NvDispWindowSrcRectX                                     |         |                                                                       |
| 0x128   | \[3.0.0+\] NvDispWindowSrcRectY                                     |         |                                                                       |
| 0x129   | \[3.0.0+\] NvDispWindowSrcRectWidth                                 |         |                                                                       |
| 0x12A   | \[3.0.0+\] NvDispWindowSrcRectHeight                                |         |                                                                       |
| 0x12B   | \[3.0.0+\] NvDispWindowDstRectX                                     |         |                                                                       |
| 0x12C   | \[3.0.0+\] NvDispWindowDstRectY                                     |         |                                                                       |
| 0x12D   | \[3.0.0+\] NvDispWindowDstRectWidth                                 |         |                                                                       |
| 0x12E   | \[3.0.0+\] NvDispWindowDstRectHeight                                |         |                                                                       |
| 0x12F   | \[3.0.0+\] NvDispWindowIndex                                        |         |                                                                       |
| 0x130   | \[3.0.0+\] NvDispWindowBlendOperation                               |         |                                                                       |
| 0x131   | \[3.0.0+\] NvDispWindowAlphaOperation                               |         |                                                                       |
| 0x132   | \[3.0.0+\] NvDispWindowDepth                                        |         |                                                                       |
| 0x133   | \[3.0.0+\] NvDispWindowAlpha                                        |         |                                                                       |
| 0x134   | \[3.0.0+\] NvDispWindowHFilter                                      |         |                                                                       |
| 0x135   | \[3.0.0+\] NvDispWindowVFilter                                      |         |                                                                       |
| 0x136   | \[3.0.0+\] NvDispWindowOptions                                      |         |                                                                       |
| 0x137   | \[3.0.0+\] NvDispWindowSyncPointId                                  |         |                                                                       |
| 0x138   | \[3.0.0+\] NvDispDPSorPower                                         |         |                                                                       |
| 0x139   | \[3.0.0+\] NvDispDPClkType                                          |         |                                                                       |
| 0x13A   | \[3.0.0+\] NvDispDPEnable                                           |         |                                                                       |
| 0x13B   | \[3.0.0+\] NvDispDPState                                            |         |                                                                       |
| 0x13C   | \[3.0.0+\] NvDispDPEdid                                             |         |                                                                       |
| 0x13D   | \[3.0.0+\] NvDispDPEdidSize                                         |         |                                                                       |
| 0x13E   | \[3.0.0+\] NvDispDPEdidExtSize                                      |         |                                                                       |
| 0x13F   | \[3.0.0+\] NvDispDPFakeMode                                         |         |                                                                       |
| 0x140   | \[3.0.0+\] NvDispDPModeNumber                                       |         |                                                                       |
| 0x141   | \[3.0.0+\] NvDispDPPlugInOut                                        |         |                                                                       |
| 0x142   | \[3.0.0+\] NvDispDPAuxIntHandler                                    |         |                                                                       |
| 0x143   | \[3.0.0+\] NvDispDPForceMaxLinkBW                                   |         |                                                                       |
| 0x144   | \[3.0.0+\] NvDispDPIsConnected                                      |         |                                                                       |
| 0x145   | \[3.0.0+\] NvDispDPLinkValid                                        |         |                                                                       |
| 0x146   | \[3.0.0+\] NvDispDPLinkMaxBW                                        |         |                                                                       |
| 0x147   | \[3.0.0+\] NvDispDPLinkMaxLaneCount                                 |         |                                                                       |
| 0x148   | \[3.0.0+\] NvDispDPLinkDownSpread                                   |         |                                                                       |
| 0x149   | \[3.0.0+\] NvDispDPLinkSupportEnhancedFraming                       |         |                                                                       |
| 0x14A   | \[3.0.0+\] NvDispDPLinkBpp                                          |         |                                                                       |
| 0x14B   | \[3.0.0+\] NvDispDPLinkScaramberCap                                 |         |                                                                       |
| 0x14C   | \[3.0.0+\] NvDispDPLinkBW                                           |         |                                                                       |
| 0x14D   | \[3.0.0+\] NvDispDPLinkLaneCount                                    |         |                                                                       |
| 0x14E   | \[3.0.0+\] NvDispDPLinkEnhancedFraming                              |         |                                                                       |
| 0x14F   | \[3.0.0+\] NvDispDPLinkScrambleEnable                               |         |                                                                       |
| 0x150   | \[3.0.0+\] NvDispDPLinkActivePolarity                               |         |                                                                       |
| 0x151   | \[3.0.0+\] NvDispDPLinkActiveCount                                  |         |                                                                       |
| 0x152   | \[3.0.0+\] NvDispDPLinkTUSize                                       |         |                                                                       |
| 0x153   | \[3.0.0+\] NvDispDPLinkActiveFrac                                   |         |                                                                       |
| 0x154   | \[3.0.0+\] NvDispDPLinkWatermark                                    |         |                                                                       |
| 0x155   | \[3.0.0+\] NvDispDPLinkHBlank                                       |         |                                                                       |
| 0x156   | \[3.0.0+\] NvDispDPLinkVBlank                                       |         |                                                                       |
| 0x157   | \[3.0.0+\] NvDispDPLinkOnlyEnhancedFraming                          |         |                                                                       |
| 0x158   | \[3.0.0+\] NvDispDPLinkOnlyEdpCap                                   |         |                                                                       |
| 0x159   | \[3.0.0+\] NvDispDPLinkSupportFastLT                                |         |                                                                       |
| 0x15A   | \[3.0.0+\] NvDispDPLinkLTDataValid                                  |         |                                                                       |
| 0x15B   | \[3.0.0+\] NvDispDPLinkTsp3Support                                  |         |                                                                       |
| 0x15C   | \[3.0.0+\] NvDispDPLinkAuxInterval                                  |         |                                                                       |
| 0x15D   | \[3.0.0+\] NvDispHdcpCreated                                        |         |                                                                       |
| 0x15E   | \[3.0.0+\] NvDispHdcpUserRequest                                    |         |                                                                       |
| 0x15F   | \[3.0.0+\] NvDispHdcpPlugged                                        |         |                                                                       |
| 0x160   | \[3.0.0+\] NvDispHdcpState                                          |         |                                                                       |
| 0x161   | \[3.0.0+\] NvDispHdcpFailCount                                      |         |                                                                       |
| 0x162   | \[3.0.0+\] NvDispHdcpHdcp22                                         |         |                                                                       |
| 0x163   | \[3.0.0+\] NvDispHdcpMaxRetry                                       |         |                                                                       |
| 0x164   | \[3.0.0+\] NvDispHdcpHpd                                            |         |                                                                       |
| 0x165   | \[3.0.0+\] NvDispHdcpRepeater                                       |         |                                                                       |
| 0x166   | \[3.0.0+\] NvDispCecRxBuf                                           |         |                                                                       |
| 0x167   | \[3.0.0+\] NvDispCecRxLength                                        |         |                                                                       |
| 0x168   | \[3.0.0+\] NvDispCecTxBuf                                           |         |                                                                       |
| 0x169   | \[3.0.0+\] NvDispCecTxLength                                        |         |                                                                       |
| 0x16A   | \[3.0.0+\] NvDispCecTxRet                                           |         |                                                                       |
| 0x16B   | \[3.0.0+\] NvDispCecState                                           |         |                                                                       |
| 0x16C   | \[3.0.0+\] NvDispCecTxInfo                                          |         |                                                                       |
| 0x16D   | \[3.0.0+\] NvDispCecRxInfo                                          |         |                                                                       |
| 0x16E   | \[3.0.0+\] NvDispDCIndex                                            |         |                                                                       |
| 0x16F   | \[3.0.0+\] NvDispDCInitialize                                       |         |                                                                       |
| 0x170   | \[3.0.0+\] NvDispDCClock                                            |         |                                                                       |
| 0x171   | \[3.0.0+\] NvDispDCFrequency                                        |         |                                                                       |
| 0x172   | \[3.0.0+\] NvDispDCFailed                                           |         |                                                                       |
| 0x173   | \[3.0.0+\] NvDispDCModeWidth                                        |         |                                                                       |
| 0x174   | \[3.0.0+\] NvDispDCModeHeight                                       |         |                                                                       |
| 0x175   | \[3.0.0+\] NvDispDCModeBpp                                          |         |                                                                       |
| 0x176   | \[3.0.0+\] NvDispDCPanelFrequency                                   |         |                                                                       |
| 0x177   | \[3.0.0+\] NvDispDCWinDirty                                         |         |                                                                       |
| 0x178   | \[3.0.0+\] NvDispDCWinEnable                                        |         |                                                                       |
| 0x179   | \[3.0.0+\] NvDispDCVrr                                              |         |                                                                       |
| 0x17A   | \[3.0.0+\] NvDispDCPanelInitialize                                  |         |                                                                       |
| 0x17B   | \[3.0.0+\] NvDispDsiDataFormat                                      |         |                                                                       |
| 0x17C   | \[3.0.0+\] NvDispDsiVideoMode                                       |         |                                                                       |
| 0x17D   | \[3.0.0+\] NvDispDsiRefreshRate                                     |         |                                                                       |
| 0x17E   | \[3.0.0+\] NvDispDsiLpCmdModeFrequency                              |         |                                                                       |
| 0x17F   | \[3.0.0+\] NvDispDsiHsCmdModeFrequency                              |         |                                                                       |
| 0x180   | \[3.0.0+\] NvDispDsiPanelResetTimeout                               |         |                                                                       |
| 0x181   | \[3.0.0+\] NvDispDsiPhyFrequency                                    |         |                                                                       |
| 0x182   | \[3.0.0+\] NvDispDsiFrequency                                       |         |                                                                       |
| 0x183   | \[3.0.0+\] NvDispDsiInstance                                        |         |                                                                       |
| 0x184   | \[3.0.0+\] NvDispDcDsiHostCtrlEnable                                |         |                                                                       |
| 0x185   | \[3.0.0+\] NvDispDcDsiInit                                          |         |                                                                       |
| 0x186   | \[3.0.0+\] NvDispDcDsiEnable                                        |         |                                                                       |
| 0x187   | \[3.0.0+\] NvDispDcDsiHsMode                                        |         |                                                                       |
| 0x188   | \[3.0.0+\] NvDispDcDsiVendorId                                      |         |                                                                       |
| 0x189   | \[3.0.0+\] NvDispDcDsiLcdVendorNum                                  |         |                                                                       |
| 0x18A   | \[3.0.0+\] NvDispDcDsiHsClockControl                                |         |                                                                       |
| 0x18B   | \[3.0.0+\] NvDispDcDsiEnableHsClockInLpMode                         |         |                                                                       |
| 0x18C   | \[3.0.0+\] NvDispDcDsiTeFrameUpdate                                 |         |                                                                       |
| 0x18D   | \[3.0.0+\] NvDispDcDsiGangedType                                    |         |                                                                       |
| 0x18E   | \[3.0.0+\] NvDispDcDsiHbpInPktSeq                                   |         |                                                                       |
| 0x18F   | \[3.0.0+\] NvDispErrID                                              |         |                                                                       |
| 0x190   | \[3.0.0+\] NvDispErrData0                                           |         |                                                                       |
| 0x191   | \[3.0.0+\] NvDispErrData1                                           |         |                                                                       |
| 0x192   | \[3.0.0+\] SdCardMountStatus                                        |         |                                                                       |
| 0x193   | \[3.0.0+\] SdCardMountUnexpectedResult                              |         |                                                                       |
| 0x194   | \[3.0.0+\] NANDTotalSize                                            |         |                                                                       |
| 0x195   | \[3.0.0+\] SdCardTotalSize                                          |         |                                                                       |
| 0x196   | \[3.0.0+\] ElapsedTimeSinceInitialLaunch                            |         |                                                                       |
| 0x197   | \[3.0.0+\] ElapsedTimeSincePowerOn                                  |         |                                                                       |
| 0x198   | \[3.0.0+\] ElapsedTimeSinceLastAwake                                |         |                                                                       |
| 0x199   | \[3.0.0+\] OccurrenceTick                                           |         |                                                                       |
| 0x19A   | \[3.0.0+\] RetailInteractiveDisplayFlag                             |         |                                                                       |
| 0x19B   | \[3.0.0+\] FatFsError                                               |         |                                                                       |
| 0x19C   | \[3.0.0+\] FatFsExtraError                                          |         |                                                                       |
| 0x19D   | \[3.0.0+\] FatFsErrorDrive                                          |         |                                                                       |
| 0x19E   | \[3.0.0+\] FatFsErrorName                                           |         |                                                                       |
| 0x19F   | \[3.0.0+\] MonitorManufactureCode                                   |         |                                                                       |
| 0x1A0   | \[3.0.0+\] MonitorProductCode                                       |         |                                                                       |
| 0x1A1   | \[3.0.0+\] MonitorSerialNumber                                      |         |                                                                       |
| 0x1A2   | \[3.0.0+\] MonitorManufactureYear                                   |         |                                                                       |
| 0x1A3   | \[3.0.0+\] PhysicalAddress                                          |         |                                                                       |
| 0x1A4   | \[3.0.0+\] Is4k60Hz                                                 |         |                                                                       |
| 0x1A5   | \[3.0.0+\] Is4k30Hz                                                 |         |                                                                       |
| 0x1A6   | \[3.0.0+\] Is1080P60Hz                                              |         |                                                                       |
| 0x1A7   | \[3.0.0+\] Is720P60Hz                                               |         |                                                                       |
| 0x1A8   | \[3.0.0+\] PcmChannelMax                                            |         |                                                                       |
| 0x1A9   | \[3.0.0+\] CrashReportHash                                          |         |                                                                       |
| 0x1AA   | \[3.0.0+\] ErrorReportSharePermission                               |         |                                                                       |
| 0x1AB   | \[3.0.0+\] VideoCodecTypeEnum                                       |         |                                                                       |
| 0x1AC   | \[3.0.0+\] VideoBitRate                                             |         |                                                                       |
| 0x1AD   | \[3.0.0+\] VideoFrameRate                                           |         |                                                                       |
| 0x1AE   | \[3.0.0+\] VideoWidth                                               |         |                                                                       |
| 0x1AF   | \[3.0.0+\] VideoHeight                                              |         |                                                                       |
| 0x1B0   | \[3.0.0+\] AudioCodecTypeEnum                                       |         |                                                                       |
| 0x1B1   | \[3.0.0+\] AudioSampleRate                                          |         |                                                                       |
| 0x1B2   | \[3.0.0+\] AudioChannelCount                                        |         |                                                                       |
| 0x1B3   | \[3.0.0+\] AudioBitRate                                             |         |                                                                       |
| 0x1B4   | \[3.0.0+\] MultimediaContainerType                                  |         |                                                                       |
| 0x1B5   | \[3.0.0+\] MultimediaProfileType                                    |         |                                                                       |
| 0x1B6   | \[3.0.0+\] MultimediaLevelType                                      |         |                                                                       |
| 0x1B7   | \[3.0.0+\] MultimediaCacheSizeEnum                                  |         |                                                                       |
| 0x1B8   | \[3.0.0+\] MultimediaErrorStatusEnum                                |         |                                                                       |
| 0x1B9   | \[3.0.0+\] MultimediaErrorLog                                       |         |                                                                       |
| 0x1BA   | \[3.0.0+\] ServerFqdn                                               |         |                                                                       |
| 0x1BB   | \[3.0.0+\] ServerIpAddress                                          |         |                                                                       |
| 0x1BC   | \[3.0.0+\] TestStringEncrypt                                        |         |                                                                       |
| 0x1BD   | \[3.0.0+\] TestU8ArrayEncrypt                                       |         |                                                                       |
| 0x1BE   | \[3.0.0+\] TestU32ArrayEncrypt                                      |         |                                                                       |
| 0x1BF   | \[3.0.0+\] TestU64ArrayEncrypt                                      |         |                                                                       |
| 0x1C0   | \[3.0.0+\] TestI32ArrayEncrypt                                      |         |                                                                       |
| 0x1C1   | \[3.0.0+\] TestI64ArrayEncrypt                                      |         |                                                                       |
| 0x1C2   | \[3.0.0+\] CipherKey                                                |         |                                                                       |
| 0x1C3   | \[3.0.0+\] FileSystemPath                                           |         |                                                                       |
| 0x1C4   | \[3.0.0+\] WebMediaPlayerOpenUrl                                    |         |                                                                       |
| 0x1C5   | \[3.0.0+\] WebMediaPlayerLastSocketErrors                           |         |                                                                       |
| 0x1C6   | \[3.0.0+\] UnknownControllerCount                                   |         |                                                                       |
| 0x1C7   | \[3.0.0+\] AttachedControllerCount                                  |         |                                                                       |
| 0x1C8   | \[3.0.0+\] BluetoothControllerCount                                 |         |                                                                       |
| 0x1C9   | \[3.0.0+\] UsbControllerCount                                       |         |                                                                       |
| 0x1CA   | \[3.0.0+\] ControllerTypeList                                       |         |                                                                       |
| 0x1CB   | \[3.0.0+\] ControllerInterfaceList                                  |         |                                                                       |
| 0x1CC   | \[3.0.0+\] ControllerStyleList                                      |         |                                                                       |
| 0x1CD   | \[3.0.0+\] FsPooledBufferPeakFreeSize                               |         |                                                                       |
| 0x1CE   | \[3.0.0+\] FsPooledBufferRetriedCount                               |         |                                                                       |
| 0x1CF   | \[3.0.0+\] FsPooledBufferReduceAllocationCount                      |         |                                                                       |
| 0x1D0   | \[3.0.0+\] FsBufferManagerPeakFreeSize                              |         |                                                                       |
| 0x1D1   | \[3.0.0+\] FsBufferManagerRetriedCount                              |         |                                                                       |
| 0x1D2   | \[3.0.0+\] FsExpHeapPeakFreeSize                                    |         |                                                                       |
| 0x1D3   | \[3.0.0+\] FsBufferPoolPeakFreeSize                                 |         |                                                                       |
| 0x1D4   | \[3.0.0+\] FsPatrolReadAllocateBufferSuccessCount                   |         |                                                                       |
| 0x1D5   | \[3.0.0+\] FsPatrolReadAllocateBufferFailureCount                   |         |                                                                       |
| 0x1D6   | \[5.0.0+\] SteadyClockInternalOffset                                |         |                                                                       |
| 0x1D7   | \[5.0.0+\] SteadyClockCurrentTimePointValue                         |         |                                                                       |
| 0x1D8   | \[5.0.0+\] UserClockContextOffset                                   |         |                                                                       |
| 0x1D9   | \[5.0.0+\] UserClockContextTimeStampValue                           |         |                                                                       |
| 0x1DA   | \[5.0.0+\] NetworkClockContextOffset                                |         |                                                                       |
| 0x1DB   | \[5.0.0+\] NetworkClockContextTimeStampValue                        |         |                                                                       |
| 0x1DC   | \[5.0.0+\] SystemAbortFlag                                          |         |                                                                       |
| 0x1DD   | \[5.0.0+\] ApplicationAbortFlag                                     |         |                                                                       |
| 0x1DE   | \[5.0.0+\] NifmErrorCode                                            |         |                                                                       |
| 0x1DF   | \[5.0.0+\] LcsApplicationId                                         |         |                                                                       |
| 0x1E0   | \[5.0.0+\] LcsContentMetaKeyIdList                                  |         |                                                                       |
| 0x1E1   | \[5.0.0+\] LcsContentMetaKeyVersionList                             |         |                                                                       |
| 0x1E2   | \[5.0.0+\] LcsContentMetaKeyTypeList                                |         |                                                                       |
| 0x1E3   | \[5.0.0+\] LcsContentMetaKeyInstallTypeList                         |         |                                                                       |
| 0x1E4   | \[5.0.0+\] LcsSenderFlag                                            |         |                                                                       |
| 0x1E5   | \[5.0.0+\] LcsApplicationRequestFlag                                |         |                                                                       |
| 0x1E6   | \[5.0.0+\] LcsHasExFatDriverFlag                                    |         |                                                                       |
| 0x1E7   | \[5.0.0+\] LcsIpAddress                                             |         |                                                                       |
| 0x1E8   | \[5.0.0+\] AcpStartupUserAccount                                    |         |                                                                       |
| 0x1E9   | \[5.0.0+\] AcpAocRegistrationType                                   |         |                                                                       |
| 0x1EA   | \[5.0.0+\] AcpAttributeFlag                                         |         |                                                                       |
| 0x1EB   | \[5.0.0+\] AcpSupportedLanguageFlag                                 |         |                                                                       |
| 0x1EC   | \[5.0.0+\] AcpParentalControlFlag                                   |         |                                                                       |
| 0x1ED   | \[5.0.0+\] AcpScreenShot                                            |         |                                                                       |
| 0x1EE   | \[5.0.0+\] AcpVideoCapture                                          |         |                                                                       |
| 0x1EF   | \[5.0.0+\] AcpDataLossConfirmation                                  |         |                                                                       |
| 0x1F0   | \[5.0.0+\] AcpPlayLogPolicy                                         |         |                                                                       |
| 0x1F1   | \[5.0.0+\] AcpPresenceGroupId                                       |         |                                                                       |
| 0x1F2   | \[5.0.0+\] AcpRatingAge                                             |         |                                                                       |
| 0x1F3   | \[5.0.0+\] AcpAocBaseId                                             |         |                                                                       |
| 0x1F4   | \[5.0.0+\] AcpSaveDataOwnerId                                       |         |                                                                       |
| 0x1F5   | \[5.0.0+\] AcpUserAccountSaveDataSize                               |         |                                                                       |
| 0x1F6   | \[5.0.0+\] AcpUserAccountSaveDataJournalSize                        |         |                                                                       |
| 0x1F7   | \[5.0.0+\] AcpDeviceSaveDataSize                                    |         |                                                                       |
| 0x1F8   | \[5.0.0+\] AcpDeviceSaveDataJournalSize                             |         |                                                                       |
| 0x1F9   | \[5.0.0+\] AcpBcatDeliveryCacheStorageSize                          |         |                                                                       |
| 0x1FA   | \[5.0.0+\] AcpApplicationErrorCodeCategory                          |         |                                                                       |
| 0x1FB   | \[5.0.0+\] AcpLocalCommunicationId                                  |         |                                                                       |
| 0x1FC   | \[5.0.0+\] AcpLogoType                                              |         |                                                                       |
| 0x1FD   | \[5.0.0+\] AcpLogoHandling                                          |         |                                                                       |
| 0x1FE   | \[5.0.0+\] AcpRuntimeAocInstall                                     |         |                                                                       |
| 0x1FF   | \[5.0.0+\] AcpCrashReport                                           |         |                                                                       |
| 0x200   | \[5.0.0+\] AcpHdcp                                                  |         |                                                                       |
| 0x201   | \[5.0.0+\] AcpSeedForPseudoDeviceId                                 |         |                                                                       |
| 0x202   | \[5.0.0+\] AcpBcatPassphrase                                        |         |                                                                       |
| 0x203   | \[5.0.0+\] AcpUserAccountSaveDataSizeMax                            |         |                                                                       |
| 0x204   | \[5.0.0+\] AcpUserAccountSaveDataJournalSizeMax                     |         |                                                                       |
| 0x205   | \[5.0.0+\] AcpDeviceSaveDataSizeMax                                 |         |                                                                       |
| 0x206   | \[5.0.0+\] AcpDeviceSaveDataJournalSizeMax                          |         |                                                                       |
| 0x207   | \[5.0.0+\] AcpTemporaryStorageSize                                  |         |                                                                       |
| 0x208   | \[5.0.0+\] AcpCacheStorageSize                                      |         |                                                                       |
| 0x209   | \[5.0.0+\] AcpCacheStorageJournalSize                               |         |                                                                       |
| 0x20A   | \[5.0.0+\] AcpCacheStorageDataAndJournalSizeMax                     |         |                                                                       |
| 0x20B   | \[5.0.0+\] AcpCacheStorageIndexMax                                  |         |                                                                       |
| 0x20C   | \[5.0.0+\] AcpPlayLogQueryableApplicationId                         |         |                                                                       |
| 0x20D   | \[5.0.0+\] AcpPlayLogQueryCapability                                |         |                                                                       |
| 0x20E   | \[5.0.0+\] AcpRepairFlag                                            |         |                                                                       |
| 0x20F   | \[5.0.0+\] RunningApplicationPatchStorageLocation                   |         |                                                                       |
| 0x210   | \[5.0.0+\] RunningApplicationVersionNumber                          |         |                                                                       |
| 0x211   | \[5.0.0+\] FsRecoveredByInvalidateCacheCount                        |         |                                                                       |
| 0x212   | \[5.0.0+\] FsSaveDataIndexCount                                     |         |                                                                       |
| 0x213   | \[5.0.0+\] FsBufferManagerPeakTotalAllocatableSize                  |         |                                                                       |
| 0x214   | \[5.0.0+\] MonitorCurrentWidth                                      |         |                                                                       |
| 0x215   | \[5.0.0+\] MonitorCurrentHeight                                     |         |                                                                       |
| 0x216   | \[5.0.0+\] MonitorCurrentRefreshRate                                |         |                                                                       |
| 0x217   | \[5.0.0+\] RebootlessSystemUpdateVersion                            |         |                                                                       |
| 0x218   | \[5.0.0+\] EncryptedExceptionInfo1                                  |         |                                                                       |
| 0x219   | \[5.0.0+\] EncryptedExceptionInfo2                                  |         |                                                                       |
| 0x21A   | \[5.0.0+\] EncryptedExceptionInfo3                                  |         |                                                                       |
| 0x21B   | \[5.0.0+\] EncryptedDyingMessage                                    |         |                                                                       |
| 0x21C   | \[5.0.0+\] DramId                                                   |         |                                                                       |
| 0x21D   | \[6.0.0+\] NifmConnectionTestRedirectUrl                            |         |                                                                       |
| 0x21E   | \[6.0.0+\] AcpRequiredNetworkServiceLicenseOnLaunchFlag             |         |                                                                       |
| 0x21F   | \[6.0.0+\] PciePort0Flags                                           |         |                                                                       |
| 0x220   | \[6.0.0+\] PciePort0Speed                                           |         |                                                                       |
| 0x221   | \[6.0.0+\] PciePort0ResetTimeInUs                                   |         |                                                                       |
| 0x222   | \[6.0.0+\] PciePort0IrqCount                                        |         |                                                                       |
| 0x223   | \[6.0.0+\] PciePort0Statistics                                      |         |                                                                       |
| 0x224   | \[6.0.0+\] PciePort1Flags                                           |         |                                                                       |
| 0x225   | \[6.0.0+\] PciePort1Speed                                           |         |                                                                       |
| 0x226   | \[6.0.0+\] PciePort1ResetTimeInUs                                   |         |                                                                       |
| 0x227   | \[6.0.0+\] PciePort1IrqCount                                        |         |                                                                       |
| 0x228   | \[6.0.0+\] PciePort1Statistics                                      |         |                                                                       |
| 0x229   | \[6.0.0+\] PcieFunction0VendorId                                    |         |                                                                       |
| 0x22A   | \[6.0.0+\] PcieFunction0DeviceId                                    |         |                                                                       |
| 0x22B   | \[6.0.0+\] PcieFunction0PmState                                     |         |                                                                       |
| 0x22C   | \[6.0.0+\] PcieFunction0IsAcquired                                  |         |                                                                       |
| 0x22D   | \[6.0.0+\] PcieFunction1VendorId                                    |         |                                                                       |
| 0x22E   | \[6.0.0+\] PcieFunction1DeviceId                                    |         |                                                                       |
| 0x22F   | \[6.0.0+\] PcieFunction1PmState                                     |         |                                                                       |
| 0x230   | \[6.0.0+\] PcieFunction1IsAcquired                                  |         |                                                                       |
| 0x231   | \[6.0.0+\] PcieGlobalRootComplexStatistics                          |         |                                                                       |
| 0x232   | \[6.0.0+\] PciePllResistorCalibrationValue                          |         |                                                                       |
| 0x233   | \[6.0.0+\] CertificateRequestedHostName                             |         |                                                                       |
| 0x234   | \[6.0.0+\] CertificateCommonName                                    |         |                                                                       |
| 0x235   | \[6.0.0+\] CertificateSANCount                                      |         |                                                                       |
| 0x236   | \[6.0.0+\] CertificateSANs                                          |         |                                                                       |
| 0x237   | \[6.0.0+\] FsBufferPoolMaxAllocateSize                              |         |                                                                       |
| 0x238   | \[6.0.0+\] CertificateIssuerName                                    |         |                                                                       |
| 0x239   | \[6.0.0+\] ApplicationAliveTime                                     |         |                                                                       |
| 0x23A   | \[6.0.0+\] ApplicationInFocusTime                                   |         |                                                                       |
| 0x23B   | \[6.0.0+\] ApplicationOutOfFocusTime                                |         |                                                                       |
| 0x23C   | \[6.0.0+\] ApplicationBackgroundFocusTime                           |         |                                                                       |
| 0x23D   | \[6.0.0+\] AcpUserAccountSwitchLock                                 |         |                                                                       |
| 0x23E   | \[6.0.0+\] USB3HostAvailableFlag                                    |         |                                                                       |
| 0x23F   | \[6.0.0+\] USB3DeviceAvailableFlag                                  |         |                                                                       |
| 0x240   | \[7.0.0+\] AcpNeighborDetectionClientConfigurationSendDataId        |         |                                                                       |
| 0x241   | \[7.0.0+\] AcpNeighborDetectionClientConfigurationReceivableDataIds |         |                                                                       |
| 0x242   | \[7.0.0+\] AcpStartupUserAccountOptionFlag                          |         |                                                                       |
| 0x243   | \[7.0.0+\] ServerErrorCode                                          |         |                                                                       |
| 0x244   | \[7.0.0+\] AppletManagerMetaLogTrace                                |         |                                                                       |
| 0x245   | \[7.0.0+\] ServerCertificateSerialNumber                            |         |                                                                       |
| 0x246   | \[7.0.0+\] ServerCertificatePublicKeyAlgorithm                      |         |                                                                       |
| 0x247   | \[7.0.0+\] ServerCertificateSignatureAlgorithm                      |         |                                                                       |
| 0x248   | \[7.0.0+\] ServerCertificateNotBefore                               |         |                                                                       |
| 0x249   | \[7.0.0+\] ServerCertificateNotAfter                                |         |                                                                       |
| 0x24A   | \[7.0.0+\] CertificateAlgorithmInfoBits                             |         |                                                                       |
| 0x24B   | \[7.0.0+\] TlsConnectionPeerIpAddress                               |         |                                                                       |
| 0x24C   | \[7.0.0+\] TlsConnectionLastHandshakeState                          |         |                                                                       |
| 0x24D   | \[7.0.0+\] TlsConnectionInfoBits                                    |         |                                                                       |
| 0x24E   | \[7.0.0+\] SslStateBits                                             |         |                                                                       |
| 0x24F   | \[7.0.0+\] SslProcessInfoBits                                       |         |                                                                       |
| 0x250   | \[7.0.0+\] SslProcessHeapSize                                       |         |                                                                       |
| 0x251   | \[7.0.0+\] SslBaseErrorCode                                         |         |                                                                       |
| 0x252   | \[7.0.0+\] GpuCrashDumpSize                                         |         |                                                                       |
| 0x253   | \[7.0.0+\] GpuCrashDump                                             |         |                                                                       |
| 0x254   | \[7.0.0+\] RunningApplicationProgramIndex                           |         |                                                                       |
| 0x255   | \[8.0.0+\] UsbTopology                                              |         |                                                                       |
| 0x256   | \[8.0.0+\] AkamaiReferenceId                                        |         |                                                                       |
| 0x257   | \[9.0.0+\] NvHostErrID                                              |         |                                                                       |
| 0x258   | \[9.0.0+\] NvHostErrDataArrayU32                                    |         |                                                                       |
| 0x259   | \[9.0.0+\] HasSyslogFlag                                            |         |                                                                       |
| 0x25A   | \[9.0.0+\] AcpRuntimeParameterDelivery                              |         |                                                                       |
| 0x25B   | \[9.0.0+\] PlatformRegion                                           |         |                                                                       |
| 0x25C   | \[9.0.0+\] RunningUlaApplicationId                                  |         |                                                                       |
| 0x25D   | \[9.0.0+\] RunningUlaAppletId                                       |         |                                                                       |
| 0x25E   | \[9.0.0+\] RunningUlaVersion                                        |         |                                                                       |
| 0x25F   | \[9.0.0+\] RunningUlaApplicationStorageLocation                     |         |                                                                       |
| 0x260   | \[9.0.0+\] RunningUlaPatchStorageLocation                           |         |                                                                       |

[Category:Services](Category:Services "wikilink")
