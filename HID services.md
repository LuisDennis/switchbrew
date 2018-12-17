See [here](HID%20Shared%20Memory.md "wikilink") for the HID
shared-memory.

# hid

This is
"nn::hid::IHidServer".

| Cmd  | Name                                                                                             |
| ---- | ------------------------------------------------------------------------------------------------ |
| 0    | [\#CreateAppletResource](#CreateAppletResource "wikilink")                                       |
| 1    | ActivateDebugPad                                                                                 |
| 11   | ActivateTouchScreen                                                                              |
| 21   | ActivateMouse                                                                                    |
| 31   | ActivateKeyboard                                                                                 |
| 32   | \[6.0.0+\] SendKeyboardLockKeyEvent                                                              |
| 40   | AcquireXpadIdEventHandle                                                                         |
| 41   | ReleaseXpadIdEventHandle                                                                         |
| 51   | ActivateXpad                                                                                     |
| 55   | GetXpadIds                                                                                       |
| 56   | ActivateJoyXpad                                                                                  |
| 58   | GetJoyXpadLifoHandle                                                                             |
| 59   | GetJoyXpadIds                                                                                    |
| 60   | ActivateSixAxisSensor                                                                            |
| 61   | DeactivateSixAxisSensor                                                                          |
| 62   | GetSixAxisSensorLifoHandle                                                                       |
| 63   | ActivateJoySixAxisSensor                                                                         |
| 64   | DeactivateJoySixAxisSensor                                                                       |
| 65   | GetJoySixAxisSensorLifoHandle                                                                    |
| 66   | StartSixAxisSensor                                                                               |
| 67   | StopSixAxisSensor                                                                                |
| 68   | IsSixAxisSensorFusionEnabled                                                                     |
| 69   | EnableSixAxisSensorFusion                                                                        |
| 70   | SetSixAxisSensorFusionParameters                                                                 |
| 71   | GetSixAxisSensorFusionParameters                                                                 |
| 72   | ResetSixAxisSensorFusionParameters                                                               |
| 73   | SetAccelerometerParameters                                                                       |
| 74   | GetAccelerometerParameters                                                                       |
| 75   | ResetAccelerometerParameters                                                                     |
| 76   | SetAccelerometerPlayMode                                                                         |
| 77   | GetAccelerometerPlayMode                                                                         |
| 78   | ResetAccelerometerPlayMode                                                                       |
| 79   | SetGyroscopeZeroDriftMode                                                                        |
| 80   | GetGyroscopeZeroDriftMode                                                                        |
| 81   | ResetGyroscopeZeroDriftMode                                                                      |
| 82   | IsSixAxisSensorAtRest                                                                            |
| 83   | \[6.0.0+\] IsFirmwareUpdateAvailableForSixAxisSensor                                             |
| 91   | ActivateGesture                                                                                  |
| 100  | [\#SetSupportedNpadStyleSet](#SetSupportedNpadStyleSet "wikilink")                               |
| 101  | [\#GetSupportedNpadStyleSet](#GetSupportedNpadStyleSet "wikilink")                               |
| 102  | [\#SetSupportedNpadIdType](#SetSupportedNpadIdType "wikilink")                                   |
| 103  | ActivateNpad                                                                                     |
| 104  | DeactivateNpad                                                                                   |
| 106  | [\#AcquireNpadStyleSetUpdateEventHandle](#AcquireNpadStyleSetUpdateEventHandle "wikilink")       |
| 107  | DisconnectNpad                                                                                   |
| 108  | GetPlayerLedPattern                                                                              |
| 109  | \[5.0.0+\] ActivateNpadWithRevision                                                              |
| 120  | SetNpadJoyHoldType                                                                               |
| 121  | GetNpadJoyHoldType                                                                               |
| 122  | [\#SetNpadJoyAssignmentModeSingleByDefault](#SetNpadJoyAssignmentModeSingleByDefault "wikilink") |
| 123  | [\#SetNpadJoyAssignmentModeSingle](#SetNpadJoyAssignmentModeSingle "wikilink")                   |
| 124  | [\#SetNpadJoyAssignmentModeDual](#SetNpadJoyAssignmentModeDual "wikilink")                       |
| 125  | [\#MergeSingleJoyAsDualJoy](#MergeSingleJoyAsDualJoy "wikilink")                                 |
| 126  | StartLrAssignmentMode                                                                            |
| 127  | StopLrAssignmentMode                                                                             |
| 128  | SetNpadHandheldActivationMode                                                                    |
| 129  | [\#GetNpadHandheldActivationMode](#GetNpadHandheldActivationMode "wikilink")                     |
| 130  | SwapNpadAssignment                                                                               |
| 131  | IsUnintendedHomeButtonInputProtectionEnabled                                                     |
| 132  | EnableUnintendedHomeButtonInputProtection                                                        |
| 133  | \[5.0.0+\] SetNpadJoyAssignmentModeSingleWithDestination                                         |
| 134  | \[6.1.0+\]                                                                                       |
| 200  | [\#GetVibrationDeviceInfo](#GetVibrationDeviceInfo "wikilink")                                   |
| 201  | [\#SendVibrationValue](#SendVibrationValue "wikilink")                                           |
| 202  | [\#GetActualVibrationValue](#GetActualVibrationValue "wikilink")                                 |
| 203  | [\#CreateActiveVibrationDeviceList](#CreateActiveVibrationDeviceList "wikilink")                 |
| 204  | [\#PermitVibration](#PermitVibration "wikilink")                                                 |
| 205  | [\#IsVibrationPermitted](#IsVibrationPermitted "wikilink")                                       |
| 206  | [\#SendVibrationValues](#SendVibrationValues "wikilink")                                         |
| 207  | \[4.0.0+\] SendVibrationGcErmCommand                                                             |
| 208  | \[4.0.0+\] GetActualVibrationGcErmCommand                                                        |
| 209  | \[4.0.0+\] BeginPermitVibrationSession                                                           |
| 210  | \[4.0.0+\] EndPermitVibrationSession                                                             |
| 300  | ActivateConsoleSixAxisSensor                                                                     |
| 301  | StartConsoleSixAxisSensor                                                                        |
| 302  | StopConsoleSixAxisSensor                                                                         |
| 303  | \[5.0.0+\] ActivateSevenSixAxisSensor                                                            |
| 304  | \[5.0.0+\] StartSevenSixAxisSensor                                                               |
| 305  | \[5.0.0+\] StopSevenSixAxisSensor                                                                |
| 306  | \[5.0.0+\] InitializeSevenSixAxisSensor                                                          |
| 307  | \[5.0.0+\] FinalizeSevenSixAxisSensor                                                            |
| 308  | \[5.0.0+\] SetSevenSixAxisSensorFusionStrength                                                   |
| 309  | \[5.0.0+\] GetSevenSixAxisSensorFusionStrength                                                   |
| 310  | \[6.0.0+\] ResetSevenSixAxisSensorTimestamp                                                      |
| 400  | IsUsbFullKeyControllerEnabled                                                                    |
| 401  | EnableUsbFullKeyController                                                                       |
| 402  | IsUsbFullKeyControllerConnected                                                                  |
| 403  | \[4.0.0+\] HasBattery                                                                            |
| 404  | \[4.0.0+\] HasLeftRightBattery                                                                   |
| 405  | \[4.0.0+\] GetNpadInterfaceType                                                                  |
| 406  | \[4.0.0+\] GetNpadLeftRightInterfaceType                                                         |
| 500  | \[5.0.0+\] GetPalmaConnectionHandle                                                              |
| 501  | \[5.0.0+\] InitializePalma                                                                       |
| 502  | \[5.0.0+\] AcquirePalmaOperationCompleteEvent                                                    |
| 503  | \[5.0.0+\] GetPalmaOperationInfo                                                                 |
| 504  | \[5.0.0+\] PlayPalmaActivity                                                                     |
| 505  | \[5.0.0+\] SetPalmaFrModeType                                                                    |
| 506  | \[5.0.0+\] ReadPalmaStep                                                                         |
| 507  | \[5.0.0+\] EnablePalmaStep                                                                       |
| 508  | \[6.0.0+\] ResetPalmaStep (\[5.0.0-6.0.0\] SuspendPalmaStep)                                     |
| 509  | \[6.0.0+\] ReadPalmaApplicationSection (\[5.0.0-6.0.0\] ResetPalmaStep)                          |
| 510  | \[6.0.0+\] WritePalmaApplicationSection (\[5.0.0-6.0.0\] ReadPalmaApplicationSection)            |
| 511  | \[6.0.0+\] ReadPalmaUniqueCode (\[5.0.0-6.0.0\] WritePalmaApplicationSection)                    |
| 512  | \[6.0.0+\] SetPalmaUniqueCodeInvalid (\[5.0.0-6.0.0\] ReadPalmaUniqueCode)                       |
| 513  | \[6.0.0+\] WritePalmaActivityEntry (\[5.0.0-6.0.0\] SetPalmaUniqueCodeInvalid)                   |
| 514  | \[6.0.0+\] WritePalmaRgbLedPatternEntry                                                          |
| 515  | \[6.0.0+\] WritePalmaWaveEntry                                                                   |
| 516  | \[6.0.0+\] SetPalmaDataBaseIdentificationVersion                                                 |
| 517  | \[6.0.0+\] GetPalmaDataBaseIdentificationVersion                                                 |
| 518  | \[6.0.0+\] SuspendPalmaFeature                                                                   |
| 519  | \[6.0.0+\] GetPalmaOperationResult                                                               |
| 520  | \[6.0.0+\] ReadPalmaPlayLog (\[5.1.0-6.0.0\] WritePalmaActivityEntry)                            |
| 521  | \[6.0.0+\] ResetPalmaPlayLog (\[5.1.0-6.0.0\] WritePalmaRgbLedPatternEntry)                      |
| 522  | \[6.0.0+\] SetIsPalmaAllConnectable                                                              |
| 523  | \[6.0.0+\] SetIsPalmaPairedConnectable                                                           |
| 524  | \[6.0.0+\] PairPalma                                                                             |
| 525  | \[6.0.0+\] SetPalmaBoostMode                                                                     |
| 1000 | SetNpadCommunicationMode                                                                         |
| 1001 | GetNpadCommunicationMode                                                                         |

## CreateAppletResource

Takes a PID and an u64
[AppletResourceUserId](AM%20services.md "wikilink"). Returns an
[\#IAppletResource](#IAppletResource "wikilink").

## SetSupportedNpadStyleSet

Takes an u32 [\#NpadStyleTag](#NpadStyleTag "wikilink").

## GetSupportedNpadStyleSet

Returns an u32 [\#NpadStyleTag](#NpadStyleTag "wikilink").

## SetSupportedNpadIdType

Takes a PID-descriptor, a type-0x9 input buffer, and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

The input buffer contains an array of u32
[\#NpadIdType](#NpadIdType "wikilink").

## AcquireNpadStyleSetUpdateEventHandle

Takes an input u32, an u64
[AppletResourceUserId](AM%20services.md "wikilink"), and an u64. Returns
an output event handle, autoclear for this is user-specified.

The value for the last u64 doesn't seem to matter (?): official sw sets
this to the address of the structure used for storing the event which is
initialized after using this cmd.

## SetNpadJoyAssignmentModeSingleByDefault

Takes a PID-descriptor, an u32, and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## SetNpadJoyAssignmentModeSingle

Takes a PID-descriptor, an u32,
[AppletResourceUserId](AM%20services.md "wikilink"), and s64
**NpadJoyDeviceType**. No output.

## SetNpadJoyAssignmentModeDual

Takes a PID-descriptor, an u32, and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## MergeSingleJoyAsDualJoy

Takes a PID-descriptor, two u32s, and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## GetNpadHandheldActivationMode

Takes a PID and an u64
[AppletResourceUserId](AM%20services.md "wikilink"). Returns an output
u64. Official user-processes panic if the output u64 is not 0-2.

## GetVibrationDeviceInfo

Takes a [\#VibrationDeviceHandle](#VibrationDeviceHandle "wikilink").
Returns an output
[\#VibrationDeviceInfo](#VibrationDeviceInfo "wikilink").

## SendVibrationValue

Takes a PID-descriptor, a
[\#VibrationDeviceHandle](#VibrationDeviceHandle "wikilink"), a
[\#VibrationValue](#VibrationValue "wikilink") immediately after that,
and an u64 [AppletResourceUserId](AM%20services.md "wikilink"). No
output.

## GetActualVibrationValue

Takes a PID-descriptor, a
[\#VibrationDeviceHandle](#VibrationDeviceHandle "wikilink"), and an u64
[AppletResourceUserId](AM%20services.md "wikilink"). Returns an output
[\#VibrationValue](#VibrationValue "wikilink").

## CreateActiveVibrationDeviceList

No input. Returns an
[\#IActiveVibrationDeviceList](#IActiveVibrationDeviceList "wikilink").

## PermitVibration

Takes an input u8 bool. No output.

This affects the config displayed by System Settings.

## IsVibrationPermitted

No input. Returns an output u8 bool.

## SendVibrationValues

Takes an u64 [AppletResourceUserId](AM%20services.md "wikilink"), and
two type-0x9 input buffers containing an array of:
[\#VibrationDeviceHandle](#VibrationDeviceHandle "wikilink") for first
buffer, and [\#VibrationValue](#VibrationValue "wikilink") for the
second buffer.

Official sw uses the same entry-count for each array.

## VibrationDeviceHandle

This is an u32.

## VibrationDeviceInfo

This is a 0x8-byte struct.

## VibrationValue

This is a 0x10-byte struct, which contains 4 float values.

## IAppletResource

| Cmd | Name                                                         |
| --- | ------------------------------------------------------------ |
| 0   | [\#GetSharedMemoryHandle](#GetSharedMemoryHandle "wikilink") |

### GetSharedMemoryHandle

No input. Returned a [sharedmem](HID%20Shared%20Memory.md "wikilink")
handle.

## IActiveVibrationDeviceList

This is
"nn::hid::IActiveVibrationDeviceList".

| Cmd | Name                                                             |
| --- | ---------------------------------------------------------------- |
| 0   | [\#ActivateVibrationDevice](#ActivateVibrationDevice "wikilink") |

### ActivateVibrationDevice

Takes an input
[\#VibrationDeviceHandle](#VibrationDeviceHandle "wikilink"). No output.

## NpadStyleTag

This is a bitfield describing which controller styles are supported.

| Bits | Description      | Notes                                   |
| ---- | ---------------- | --------------------------------------- |
| 0    | NpadFullKey      | Pro Controller.                         |
| 1    | NpadHandheld     | JoyCon controller in handheld mode.     |
| 2    | NpadJoyDual      | JoyCon controller in dual mode.         |
| 3    | NpadJoyLeft      | JoyCon left controller in single mode.  |
| 4    | NpadJoyRight     | JoyCon right controller in single mode. |
| 5    | NpadGc           | GameCube controller.                    |
| 6    | NpadPalma        | Poké Ball Plus controller.              |
| 7    | NpadLark         | NES controller.                         |
| 8    | NpadHandheldLark | NES controller in handheld mode.        |
| 9-28 | Reserved         |                                         |
| 29   | NpadSystemExt    |                                         |
| 30   | NpadSystem       |                                         |
| 31   | Reserved         |                                         |

## NpadIdType

This is an u32. This is the controller index used in
[sharedmem](HID%20Shared%20Memory#Controllers.md##Controllers "wikilink").
0x20 is handheld.

# hid:dbg

This is "nn::hid::IHidDebugServer".

| Cmd | Name                                                |
| --- | --------------------------------------------------- |
| 0   | DeactivateDebugPad                                  |
| 1   | SetDebugPadAutoPilotState                           |
| 2   | UnsetDebugPadAutoPilotState                         |
| 10  | DeactivateTouchScreen                               |
| 11  | SetTouchScreenAutoPilotState                        |
| 12  | UnsetTouchScreenAutoPilotState                      |
| 20  | DeactivateMouse                                     |
| 21  | SetMouseAutoPilotState                              |
| 22  | UnsetMouseAutoPilotState                            |
| 30  | DeactivateKeyboard                                  |
| 31  | SetKeyboardAutoPilotState                           |
| 32  | UnsetKeyboardAutoPilotState                         |
| 50  | DeactivateXpad                                      |
| 51  | SetXpadAutoPilotState                               |
| 52  | UnsetXpadAutoPilotState                             |
| 60  | DeactivateJoyXpad                                   |
| 91  | DeactivateGesture                                   |
| 110 | DeactivateHomeButton                                |
| 111 | SetHomeButtonAutoPilotState                         |
| 112 | UnsetHomeButtonAutoPilotState                       |
| 120 | DeactivateSleepButton                               |
| 121 | SetSleepButtonAutoPilotState                        |
| 122 | UnsetSleepButtonAutoPilotState                      |
| 123 | DeactivateInputDetector                             |
| 130 | DeactivateCaptureButton                             |
| 131 | SetCaptureButtonAutoPilotState                      |
| 132 | UnsetCaptureButtonAutoPilotState                    |
| 133 | SetShiftAccelerometerCalibrationValue               |
| 134 | GetShiftAccelerometerCalibrationValue               |
| 135 | SetShiftGyroscopeCalibrationValue                   |
| 136 | GetShiftGyroscopeCalibrationValue                   |
| 140 | DeactivateConsoleSixAxisSensor                      |
| 141 | \[5.0.0+\] GetConsoleSixAxisSensorSamplingFrequency |
| 142 | \[5.0.0+\] DeactivateSevenSixAxisSensor             |
| 143 | \[6.0.0+\] GetConsoleSixAxisSensorCountStates       |
| 201 | ActivateFirmwareUpdate                              |
| 202 | DeactivateFirmwareUpdate                            |
| 203 | StartFirmwareUpdate                                 |
| 204 | GetFirmwareUpdateStage                              |
| 205 | GetFirmwareVersion                                  |
| 206 | GetDestinationFirmwareVersion                       |
| 207 | DiscardFirmwareInfoCacheForRevert                   |
| 208 | StartFirmwareUpdateForRevert                        |
| 209 | GetAvailableFirmwareVersionForRevert                |
| 210 | \[4.0.0+\] IsFirmwareUpdatingDevice                 |
| 211 | \[6.0.0+\] StartFirmwareUpdateIndividual            |
| 215 | \[6.0.0+\] SetUsbFirmwareForceUpdateEnabled         |
| 216 | \[6.0.0+\] SetAllKuinaDevicesToFirmwareUpdateMode   |
| 221 | UpdateControllerColor                               |
| 222 | \[4.0.0+\] ConnectUsbPadsAsync                      |
| 223 | \[4.0.0+\] DisconnectUsbPadsAsync                   |
| 224 | \[5.0.0+\] UpdateDesignInfo                         |
| 225 | \[5.0.0+\] GetUniquePadDriverState                  |
| 226 | \[5.0.0+\] GetSixAxisSensorDriverStates             |
| 227 | \[6.0.0+\] GetRxPacketHistory                       |
| 228 | \[6.0.0+\] AcquireOperationEventHandle              |
| 229 | \[6.0.0+\] ReadSerialFlash                          |
| 230 | \[6.0.0+\] WriteSerialFlash                         |
| 231 | \[6.0.0+\] GetOperationResult                       |
| 232 | \[6.0.0+\] EnableShipmentMode                       |
| 233 | \[6.0.0+\] ClearPairingInfo                         |
| 234 | \[6.0.0+\] GetUniquePadDeviceTypeSetInternal        |
| 301 | \[5.0.0+\] GetAbstractedPadHandles                  |
| 302 | \[5.0.0+\] GetAbstractedPadState                    |
| 303 | \[5.0.0+\] GetAbstractedPadsState                   |
| 321 | \[5.0.0+\] SetAutoPilotVirtualPadState              |
| 322 | \[5.0.0+\] UnsetAutoPilotVirtualPadState            |
| 323 | \[5.0.0+\] UnsetAllAutoPilotVirtualPadState         |
| 350 | \[5.0.0+\] AddRegisteredDevice                      |
| 400 | \[6.0.0+\] DisableExternalMcuOnNxDevice             |
| 401 | \[6.0.0+\] DisableRailDeviceFiltering               |

# hid:sys

This is
"nn::hid::IHidSystemServer".

| Cmd  | Name                                                               |
| ---- | ------------------------------------------------------------------ |
| 31   | SendKeyboardLockKeyEvent                                           |
| 101  | AcquireHomeButtonEventHandle                                       |
| 111  | ActivateHomeButton                                                 |
| 121  | AcquireSleepButtonEventHandle                                      |
| 131  | ActivateSleepButton                                                |
| 141  | AcquireCaptureButtonEventHandle                                    |
| 151  | ActivateCaptureButton                                              |
| 210  | AcquireNfcDeviceUpdateEventHandle                                  |
| 211  | GetNpadsWithNfc                                                    |
| 212  | AcquireNfcActivateEventHandle                                      |
| 213  | ActivateNfc                                                        |
| 214  | \[4.0.0+\] GetXcdHandleForNpadWithNfc                              |
| 215  | \[4.0.0+\] IsNfcActivated                                          |
| 230  | AcquireIrSensorEventHandle                                         |
| 231  | ActivateIrSensor                                                   |
| 301  | ActivateNpadSystem                                                 |
| 303  | ApplyNpadSystemCommonPolicy                                        |
| 304  | EnableAssigningSingleOnSlSrPress                                   |
| 305  | DisableAssigningSingleOnSlSrPress                                  |
| 306  | GetLastActiveNpad                                                  |
| 307  | GetNpadSystemExtStyle                                              |
| 308  | \[5.0.0+\] ApplyNpadSystemCommonPolicyFull                         |
| 309  | \[5.0.0+\] GetNpadFullKeyGripColor                                 |
| 310  | \[6.0.0+\] GetMaskedSupportedNpadStyleSet                          |
| 311  | SetNpadPlayerLedBlinkingDevice                                     |
| 312  | \[6.0.0+\] SetSupportedNpadStyleSetAll                             |
| 321  | GetUniquePadsFromNpad                                              |
| 322  | GetIrSensorState                                                   |
| 323  | GetXcdHandleForNpadWithIrSensor                                    |
| 500  | SetAppletResourceUserId                                            |
| 501  | RegisterAppletResourceUserId                                       |
| 502  | UnregisterAppletResourceUserId                                     |
| 503  | EnableAppletToGetInput                                             |
| 504  | SetAruidValidForVibration                                          |
| 505  | EnableAppletToGetSixAxisSensor                                     |
| 510  | [\#SetVibrationMasterVolume](#SetVibrationMasterVolume "wikilink") |
| 511  | GetVibrationMasterVolume                                           |
| 512  | BeginPermitVibrationSession                                        |
| 513  | EndPermitVibrationSession                                          |
| 520  | EnableHandheldHids                                                 |
| 521  | DisableHandheldHids                                                |
| 540  | AcquirePlayReportControllerUsageUpdateEvent                        |
| 541  | GetPlayReportControllerUsages                                      |
| 542  | AcquirePlayReportRegisteredDeviceUpdateEvent                       |
| 543  | GetRegisteredDevicesOld (\[1.0.0-4.1.0\] GetRegisteredDevices)     |
| 544  | AcquireConnectionTriggerTimeoutEvent                               |
| 545  | SendConnectionTrigger                                              |
| 546  | AcquireDeviceRegisteredEventForControllerSupport                   |
| 547  | GetAllowedBluetoothLinksCount                                      |
| 548  | \[5.0.0+\] GetRegisteredDevices                                    |
| 549  | \[6.0.0+\] GetConnectableRegisteredDevices                         |
| 700  | ActivateUniquePad                                                  |
| 702  | AcquireUniquePadConnectionEventHandle                              |
| 703  | GetUniquePadIds                                                    |
| 751  | AcquireJoyDetachOnBluetoothOffEventHandle                          |
| 800  | ListSixAxisSensorHandles                                           |
| 801  | IsSixAxisSensorUserCalibrationSupported                            |
| 802  | ResetSixAxisSensorCalibrationValues                                |
| 803  | StartSixAxisSensorUserCalibration                                  |
| 804  | CancelSixAxisSensorUserCalibration                                 |
| 805  | GetUniquePadBluetoothAddress                                       |
| 806  | DisconnectUniquePad                                                |
| 807  | \[5.0.0+\] GetUniquePadType                                        |
| 808  | \[5.0.0+\] GetUniquePadInterface                                   |
| 809  | \[5.0.0+\] GetUniquePadSerialNumber                                |
| 810  | \[5.0.0+\] GetUniquePadControllerNumber                            |
| 811  | \[5.0.0+\] GetSixAxisSensorUserCalibrationStage                    |
| 821  | StartAnalogStickManualCalibration                                  |
| 822  | RetryCurrentAnalogStickManualCalibrationStage                      |
| 823  | CancelAnalogStickManualCalibration                                 |
| 824  | ResetAnalogStickManualCalibration                                  |
| 825  | \[5.0.0+\] GetAnalogStickState                                     |
| 826  | \[5.0.0+\] GetAnalogStickManualCalibrationStage                    |
| 827  | \[5.0.0+\] IsAnalogStickButtonPressed                              |
| 828  | \[5.0.0+\] IsAnalogStickInReleasePosition                          |
| 829  | \[5.0.0+\] IsAnalogStickInCircumference                            |
| 850  | IsUsbFullKeyControllerEnabled                                      |
| 851  | EnableUsbFullKeyController                                         |
| 852  | IsUsbConnected                                                     |
| 870  | \[6.0.0+\] IsHandheldButtonPressedOnConsoleMode                    |
| 900  | ActivateInputDetector                                              |
| 901  | [\#NotifyInputDetector](#NotifyInputDetector "wikilink")           |
| 1000 | InitializeFirmwareUpdate                                           |
| 1001 | GetFirmwareVersion                                                 |
| 1002 | GetAvailableFirmwareVersion                                        |
| 1003 | IsFirmwareUpdateAvailable                                          |
| 1004 | CheckFirmwareUpdateRequired                                        |
| 1005 | StartFirmwareUpdate                                                |
| 1006 | AbortFirmwareUpdate                                                |
| 1007 | GetFirmwareUpdateState                                             |
| 1008 | \[4.0.0+\] ActivateAudioControl                                    |
| 1009 | \[4.0.0+\] AcquireAudioControlEventHandle                          |
| 1010 | \[4.0.0+\] GetAudioControlStates                                   |
| 1011 | \[4.0.0+\] DeactivateAudioControl                                  |
| 1050 | \[5.0.0+\] IsSixAxisSensorAccurateUserCalibrationSupported         |
| 1051 | \[5.0.0+\] StartSixAxisSensorAccurateUserCalibration               |
| 1052 | \[5.0.0+\] CancelSixAxisSensorAccurateUserCalibration              |
| 1053 | \[5.0.0+\] GetSixAxisSensorAccurateUserCalibrationState            |
| 1100 | \[5.0.0+\] GetHidbusSystemServiceObject                            |
| 1120 | \[6.0.0+\] SetFirmwareHotfixUpdateSkipEnabled                      |
| 1130 | \[6.0.0+\] InitializeUsbFirmwareUpdate                             |
| 1131 | \[6.0.0+\] FinalizeUsbFirmwareUpdate                               |
| 1132 | \[6.0.0+\] CheckUsbFirmwareUpdateRequired                          |
| 1133 | \[6.0.0+\] StartUsbFirmwareUpdate                                  |
| 1134 | \[6.0.0+\] GetUsbFirmwareUpdateState                               |

## SetVibrationMasterVolume

Takes an input 32bit float.

## NotifyInputDetector

Takes an input u32 bitmask InputSourceId, no output.

This is the only hid:sys command used by USB-sysmodule (with value
0x40).

# hid:tmp

This is "nn::hid::IHidTemporaryServer".

| Cmd | Name                                     |
| --- | ---------------------------------------- |
| 0   | GetConsoleSixAxisSensorCalibrationValues |

# irs

This is
"nn::irsensor::IIrSensorServer".

| Cmd | Name                                                                           |
| --- | ------------------------------------------------------------------------------ |
| 302 | [\#ActivateIrsensor](#ActivateIrsensor "wikilink")                             |
| 303 | [\#DeactivateIrsensor](#DeactivateIrsensor "wikilink")                         |
| 304 | [\#GetIrsensorSharedMemoryHandle](#GetIrsensorSharedMemoryHandle "wikilink")   |
| 305 | [\#StopImageProcessor](#StopImageProcessor "wikilink")                         |
| 306 | [\#RunMomentProcessor](#RunMomentProcessor "wikilink")                         |
| 307 | [\#RunClusteringProcessor](#RunClusteringProcessor "wikilink")                 |
| 308 | [\#RunImageTransferProcessor](#RunImageTransferProcessor "wikilink")           |
| 309 | [\#GetImageTransferProcessorState](#GetImageTransferProcessorState "wikilink") |
| 310 | [\#RunTeraPluginProcessor](#RunTeraPluginProcessor "wikilink")                 |
| 311 | [\#GetNpadIrCameraHandle](#GetNpadIrCameraHandle "wikilink")                   |
| 312 | [\#RunPointingProcessor](#RunPointingProcessor "wikilink")                     |
| 313 | [\#SuspendImageProcessor](#SuspendImageProcessor "wikilink")                   |
| 314 | \[3.0.0+\] [\#CheckFirmwareVersion](#CheckFirmwareVersion "wikilink")          |
| 315 | \[5.0.0+\] SetFunctionLevel                                                    |
| 316 | \[5.0.0+\] RunImageTransferExProcessor                                         |
| 317 | \[5.0.0+\] RunIrLedProcessor                                                   |
| 318 | \[5.0.0+\] StopImageProcessorAsync                                             |
| 319 | \[5.0.0+\] ActivateIrsensorWithFunctionLevel                                   |

## ActivateIrsensor

Takes a PID-descriptor and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## DeactivateIrsensor

Takes a PID-descriptor and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## GetIrsensorSharedMemoryHandle

Takes a PID-descriptor and an
[AppletResourceUserId](AM%20services.md "wikilink"). Returns a
SharedMemory handle.

The SharedMemory is mapped with permissions=read-only and size=0x8000.

## StopImageProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## RunMomentProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), an
[AppletResourceUserId](AM%20services.md "wikilink"), and a
[\#PackedMomentProcessorConfig](#PackedMomentProcessorConfig "wikilink").
No output.

## RunClusteringProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), an
[AppletResourceUserId](AM%20services.md "wikilink"), and a
[\#PackedClusteringProcessorConfig](#PackedClusteringProcessorConfig "wikilink").
No output.

## RunImageTransferProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), an
[AppletResourceUserId](AM%20services.md "wikilink"), a
[\#PackedImageTransferProcessorConfig](#PackedImageTransferProcessorConfig "wikilink"),
an u64 for the TransferMemory\_size, and a TransferMemory handle. No
output.

Official sw creates the TransferMemory with an user-specified buffer and
permissions=0.

## GetImageTransferProcessorState

Takes a PID-descriptor, a type-0x6 output buffer, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), and an
[AppletResourceUserId](AM%20services.md "wikilink"). Returns an
[\#ImageTransferProcessorState](#ImageTransferProcessorState "wikilink").
No output.

## RunTeraPluginProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), a
[\#PackedTeraPluginProcessorConfig](#PackedTeraPluginProcessorConfig "wikilink")
(immediately after the previous word), and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## GetNpadIrCameraHandle

Takes an input u32. Returns an output
[\#IrCameraHandle](#IrCameraHandle "wikilink").

## RunPointingProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), a
[\#PackedDpdProcessorConfig](#PackedDpdProcessorConfig "wikilink")
(immediately after the previous word), and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## SuspendImageProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## CheckFirmwareVersion

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), a
[\#PackedMcuVersion](#PackedMcuVersion "wikilink"), and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## IrCameraHandle

This is an u32.

## PackedMomentProcessorConfig

This is a 0x20-byte struct. This is converted from another structure by
the official
user-process.

| Offset | Size | Description            | DefaultConfig                  |
| ------ | ---- | ---------------------- | ------------------------------ |
| 0x0    | 0x8  | ?                      | 0x493E0                        |
| 0x8    | 0x1  | ?                      | 0x0                            |
| 0x9    | 0x1  | ?                      | 0x8                            |
| 0xA    | 0x1  | ?                      | 0x0                            |
| 0xB    | 0x5  | Padding                |                                |
| 0x10   | 0x8  | u16, u32, u16          | {Not written}, 0x1400000, 0xF0 |
| 0x18   | 0x4  | Hard-coded to 0xA0003. |                                |
| 0x1C   | 0x1  | ?                      | 0x1                            |
| 0x1D   | 0x1  | ?                      | 0x50                           |
| 0x1E   | 0x2  | Padding                |                                |

## PackedClusteringProcessorConfig

This is a 0x28-byte struct.

## PackedImageTransferProcessorConfig

This is a 0x18-byte struct. This is converted from another structure by
the official user-process. The conversion is the same as
PackedMomentProcessorConfig, except the code using out +0x1C/+0x1D was
removed, and the constant is now located at out+0x10. The code which
wrote to out u64 +0x10 from in+0x24 was replaced with code which writes
an u8 to out+0x14.

## ImageTransferProcessorState

This is a 0x10-byte struct.

## PackedTeraPluginProcessorConfig

This is an u64.

## PackedDpdProcessorConfig

This is a 0x10-byte struct.

## PackedMcuVersion

This is an u32.

# irs:sys

This is "nn::irsensor::IIrSensorSystemServer".

| Cmd | Name                           |
| --- | ------------------------------ |
| 500 | SetAppletResourceUserId        |
| 501 | RegisterAppletResourceUserId   |
| 502 | UnregisterAppletResourceUserId |
| 503 | EnableAppletToGetInput         |

# ahid:cd

This is "nn::ahid::IServerSession".

Used for USB HID
devices.

| Cmd | Name | Notes                                                                        |
| --- | ---- | ---------------------------------------------------------------------------- |
| 0   |      | Takes an input s32, no output.                                               |
| 1   |      | Takes an input s32, no output.                                               |
| 2   |      | Takes an input u32, returns an [\#ICtrlSession](#ICtrlSession "wikilink").   |
| 3   |      | Takes an input u32, returns an [\#IReadSession](#IReadSession "wikilink").   |
| 4   |      | Takes an input u32, returns an [\#IWriteSession](#IWriteSession "wikilink"). |

## ICtrlSession

This is "nn::ahid::ICtrlSession".

| Cmd | Name | Notes |
| --- | ---- | ----- |
| 0   |      |       |
| 1   |      |       |
| 2   |      |       |
| 3   |      |       |
| 4   |      |       |
| 5   |      |       |
| 6   |      |       |
| 7   |      |       |
| 8   |      |       |
| 9   |      |       |
| 10  |      |       |
| 11  |      |       |

All of these use USB [CtrlXfer](USB%20services.md "wikilink"), except
for cmd10-11 which are event(?) related, and cmd1 which copies
0x4000-bytes from state to output.

## IReadSession

This is "nn::ahid::IReadSession".

| Cmd | Name | Notes |
| --- | ---- | ----- |
| 0   |      |       |

Cmd0 uses [PostBufferAsync](USB%20services.md "wikilink") etc with the
INPUT endpoint. The size must be \<=0x1000. The actual transfer size is
returned in an output u64. The data is copied from the tmpbuf to the
output buffer using the actual-transfer-size.

## IWriteSession

This is
"nn::ahid::IWriteSession".

| Cmd | Name | Notes                                                                                                                  |
| --- | ---- | ---------------------------------------------------------------------------------------------------------------------- |
| 0   |      | This is the inverse of [\#IReadSession](#IReadSession "wikilink") cmd0. Uses the OUTPUT endpoint with an input buffer. |

# ahid:hdr

This is "nn::ahid::hdr::ISession".

Used internally for USB HID devices.

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |
| 4   |      |

# xcd:sys

This is "nn::xcd::detail::ISystemServer".

| Cmd | Name                              |
| --- | --------------------------------- |
| 0   | GetDataFormat                     |
| 1   | SetDataFormat                     |
| 2   | GetMcuState                       |
| 3   | SetMcuState                       |
| 4   | GetMcuVersionForNfc               |
| 5   | CheckNfcDevicePower               |
| 10  | SetNfcEvent                       |
| 11  | GetNfcInfo                        |
| 12  | StartNfcDiscovery                 |
| 13  | StopNfcDiscovery                  |
| 14  | StartNtagRead                     |
| 15  | StartNtagWrite                    |
| 16  | SendNfcRawData                    |
| 17  | RegisterMifareKey                 |
| 18  | ClearMifareKey                    |
| 19  | StartMifareRead                   |
| 20  | StartMifareWrite                  |
| 101 | GetAwakeTriggerReasonForLeftRail  |
| 102 | GetAwakeTriggerReasonForRightRail |

# hidbus

This is "nn::hidbus::IHidbusServer".

| Cmd | Name                             |
| --- | -------------------------------- |
| 1   | GetBusHandle                     |
| 2   | IsExternalDeviceConnected        |
| 3   | Initialize                       |
| 4   | Finalize                         |
| 5   | EnableExternalDevice             |
| 6   | GetExternalDeviceId              |
| 7   | SendCommandAsync                 |
| 8   | GetSendCommandAsynceResult       |
| 9   | SetEventForSendCommandAsycResult |
| 10  | GetSharedMemoryHandle            |
| 11  | EnableJoyPollingReceiveMode      |
| 12  | DisableJoyPollingReceiveMode     |
| 13  | GetPollingData                   |
| 14  | \[6.0.0+\] SetStatusManagerType  |

# RomFS

The hid-sysmodule RomFS contains:

` ftmFwUpdate`  
`   ├── NTD_4CD_1801.fts256`  
`   ├── NTD_4CD_2602.fts256`  
`   └── NTD_4CD_3801.fts256`

These are firmware files for the touchscreen controller.

# Firmware update

Starting with [3.0.0](3.0.0.md "wikilink") HID-sysmodule now contains
strings for data stored in title
[0100000000000822](Title%20list.md "wikilink").

[Category:Services](Category:Services "wikilink")
