# btm

This is "nn::btm::IBtm".

| Cmd | Name                                       |
| --- | ------------------------------------------ |
| 0   | GetState                                   |
| 1   | GetHostDeviceProperty                      |
| 2   | AcquireDeviceConditionEvent                |
| 3   | GetDeviceCondition                         |
| 4   | SetBurstMode                               |
| 5   | SetSlotMode                                |
| 6   | \[1.0.0-8.1.0\] SetBluetoothMode           |
| 7   | SetWlanMode                                |
| 8   | AcquireDeviceInfoEvent                     |
| 9   | GetDeviceInfo                              |
| 10  | AddDeviceInfo                              |
| 11  | RemoveDeviceInfo                           |
| 12  | IncreaseDeviceInfoOrder                    |
| 13  | LlrNotify                                  |
| 14  | EnableRadio                                |
| 15  | DisableRadio                               |
| 16  | HidDisconnect                              |
| 17  | HidSetRetransmissionMode                   |
| 18  | \[2.0.0+\] AcquireAwakeReqEvent            |
| 19  | \[4.0.0+\] AcquireLlrStateEvent            |
| 20  | \[4.0.0+\] IsLlrStarted                    |
| 21  | \[4.0.0+\] EnableSlotSaving                |
| 22  | \[5.0.0+\] ProtectDeviceInfo               |
| 23  | \[5.0.0+\] AcquireBleScanEvent             |
| 24  | \[5.0.0+\] GetBleScanParameterGeneral      |
| 25  | \[5.0.0+\] GetBleScanParameterSmartDevice  |
| 26  | \[5.0.0+\] StartBleScanForGeneral          |
| 27  | \[5.0.0+\] StopBleScanForGeneral           |
| 28  | \[5.0.0+\] GetBleScanResultsForGeneral     |
| 29  | \[5.0.0+\] StartBleScanForPairedDevice     |
| 30  | \[5.0.0+\] StopBleScanForPairedDevice      |
| 31  | \[5.0.0+\] StartBleScanForSmartDevice      |
| 32  | \[5.0.0+\] StopBleScanForSmartDevice       |
| 33  | \[5.0.0+\] GetBleScanResultsForSmartDevice |
| 34  | \[5.0.0+\] AcquireBleConnectionEvent       |
| 35  | \[5.0.0+\] BleConnect                      |
| 36  | \[5.0.0+\] BleOverrideConnection           |
| 37  | \[5.0.0+\] BleDisconnect                   |
| 38  | \[5.0.0+\] BleGetConnectionState           |
| 39  | \[5.0.0+\] BleGetGattClientConditionList   |
| 40  | \[5.0.0+\] AcquireBlePairingEvent          |
| 41  | \[5.0.0+\] BlePairDevice                   |
| 42  | \[5.0.0+\] BleUnpairDeviceOnBoth           |
| 43  | \[5.1.0+\] BleUnpairDevice                 |
| 44  | \[5.1.0+\] BleGetPairedAddresses           |
| 45  | \[5.1.0+\] AcquireBleServiceDiscoveryEvent |
| 46  | \[5.1.0+\] GetGattServices                 |
| 47  | \[5.1.0+\] GetGattService                  |
| 48  | \[5.1.0+\] GetGattIncludedServices         |
| 49  | \[5.1.0+\] GetBelongingService             |
| 50  | \[5.1.0+\] GetGattCharacteristics          |
| 51  | \[5.1.0+\] GetGattDescriptors              |
| 52  | \[5.1.0+\] AcquireBleMtuConfigEvent        |
| 53  | \[5.1.0+\] ConfigureBleMtu                 |
| 54  | \[5.1.0+\] GetBleMtu                       |
| 55  | \[5.1.0+\] RegisterBleGattDataPath         |
| 56  | \[5.1.0+\] UnregisterBleGattDataPath       |
| 57  | \[5.1.0+\] RegisterAppletResourceUserId    |
| 58  | \[5.1.0+\] UnregisterAppletResourceUserId  |
| 59  | \[5.1.0+\] SetAppletResourceUserId         |
| 60  | \[8.0.0+\]                                 |
| 61  | \[8.0.0+\]                                 |
| 62  | \[9.0.0+\]                                 |
| 63  | \[9.0.0+\]                                 |

\[3.0.0+\] RegisterSystemEventForConnectedDeviceCondition,
RegisterSystemEventForRegisteredDeviceInfo, and cmd18 now returns an
output u8.

With \[5.1.0+\] cmds 24-42 were moved/replaced/etc (input/output
changed).

\[9.0.0+\] Cmd13 now takes 0xC-bytes of input and no output, instead of
0x6-bytes of input.

# btm:dbg

This is "nn::btm::IBtmDebug".

| Cmd | Name                                        |
| --- | ------------------------------------------- |
| 0   | AcquireDiscoveryEvent                       |
| 1   | StartDiscovery                              |
| 2   | CancelDiscovery                             |
| 3   | GetDeviceProperty                           |
| 4   | CreateBond                                  |
| 5   | CancelBond                                  |
| 6   | SetTsiMode                                  |
| 7   | GeneralTest                                 |
| 8   | HidConnect                                  |
| 9   | \[5.0.0+\] GeneralGet                       |
| 10  | \[5.1.0+\] GetGattClientDisconnectionReason |
| 11  | \[5.1.0+\] GetBleConnectionParameter        |
| 12  | \[5.1.0+\] GetBleConnectionParameterRequest |

\[3.0.0+\] RegisterSystemEventForDiscovery now returns an output u8.

# btm:sys

This is "nn::btm::IBtmSystem".

| Cmd | Name    |
| --- | ------- |
| 0   | GetCore |

## IBtmSystemCore

This is "nn::btm::IBtmSystemCore".

| Cmd | Name                                  |
| --- | ------------------------------------- |
| 0   | StartGamepadPairing                   |
| 1   | CancelGamepadPairing                  |
| 2   | ClearGamepadPairingDatabase           |
| 3   | GetPairedGamepadCount                 |
| 4   | EnableRadio                           |
| 5   | DisableRadio                          |
| 6   | GetRadioOnOff                         |
| 7   | \[3.0.0+\] AcquireRadioEvent          |
| 8   | \[3.0.0+\] AcquireGamepadPairingEvent |
| 9   | \[3.0.0+\] IsGamepadPairingStarted    |

# btm:u

This is "nn::btm::IBtmUser".

| Cmd | Name    |
| --- | ------- |
| 0   | GetCore |

## IBtmUserCore

This is "nn::btm::IBtmUserCore".

| Cmd | Name                            |
| --- | ------------------------------- |
| 0   | AcquireBleScanEvent             |
| 1   | GetBleScanFilterParameter       |
| 2   | GetBleScanFilterParameter2      |
| 3   | StartBleScanForGeneral          |
| 4   | StopBleScanForGeneral           |
| 5   | GetBleScanResultsForGeneral     |
| 6   | StartBleScanForPaired           |
| 7   | StopBleScanForPaired            |
| 8   | StartBleScanForSmartDevice      |
| 9   | StopBleScanForSmartDevice       |
| 10  | GetBleScanResultsForSmartDevice |
| 17  | AcquireBleConnectionEvent       |
| 18  | BleConnect                      |
| 19  | BleDisconnect                   |
| 20  | BleGetConnectionState           |
| 21  | AcquireBlePairingEvent          |
| 22  | BlePairDevice                   |
| 23  | BleUnPairDevice                 |
| 24  | BleUnPairDevice2                |
| 25  | BleGetPairedDevices             |
| 26  | AcquireBleServiceDiscoveryEvent |
| 27  | GetGattServices                 |
| 28  | GetGattService                  |
| 29  | GetGattIncludedServices         |
| 30  | GetBelongingGattService         |
| 31  | GetGattCharacteristics          |
| 32  | GetGattDescriptors              |
| 33  | AcquireBleMtuConfigEvent        |
| 34  | ConfigureBleMtu                 |
| 35  | GetBleMtu                       |
| 36  | RegisterBleGattDataPath         |
| 37  | UnregisterBleGattDataPath       |

[Category:Services](Category:Services "wikilink")
