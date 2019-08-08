\_\_NOTOC\_\_

# System calls

| Id   | Name                                                                               | In                                                                                                                                                                                                                                                                                 | Out                                                           |
| ---- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| 0x1  | [\#svcSetHeapSize](#svcSetHeapSize "wikilink")                                     | W1=size                                                                                                                                                                                                                                                                            | W0=result, X1=outaddr                                         |
| 0x2  | [\#svcSetMemoryPermission](#svcSetMemoryPermission "wikilink")                     | X0=addr, X1=size, W2=prot                                                                                                                                                                                                                                                          | W0=result                                                     |
| 0x3  | [\#svcSetMemoryAttribute](#svcSetMemoryAttribute "wikilink")                       | X0=addr, X1=size, W2=state0, W3=state1                                                                                                                                                                                                                                             | W0=result                                                     |
| 0x4  | [\#svcMapMemory](#svcMapMemory "wikilink")                                         | X0=dstaddr, X1=srcaddr, X2=size                                                                                                                                                                                                                                                    | W0=result                                                     |
| 0x5  | [\#svcUnmapMemory](#svcUnmapMemory "wikilink")                                     | X0=dstaddr, X1=srcaddr, X2=size                                                                                                                                                                                                                                                    | W0=result                                                     |
| 0x6  | [\#svcQueryMemory](#svcQueryMemory "wikilink")                                     | X0=MemoryInfo\*, X2=addr                                                                                                                                                                                                                                                           | W0=result, W1=PageInfo                                        |
| 0x7  | [\#svcExitProcess](#svcExitProcess "wikilink")                                     | None                                                                                                                                                                                                                                                                               |                                                               |
| 0x8  | [\#svcCreateThread](#svcCreateThread "wikilink")                                   | X1=entry, X2=thread\_context, X3=stacktop, W4=prio, W5=processor\_id                                                                                                                                                                                                               | W0=result, W1=handle                                          |
| 0x9  | [\#svcStartThread](#svcStartThread "wikilink")                                     | W0=thread\_handle                                                                                                                                                                                                                                                                  | W0=result                                                     |
| 0xA  | [\#svcExitThread](#svcExitThread "wikilink")                                       | None                                                                                                                                                                                                                                                                               |                                                               |
| 0xB  | [\#svcSleepThread](#svcSleepThread "wikilink")                                     | X0=nano                                                                                                                                                                                                                                                                            |                                                               |
| 0xC  | [\#svcGetThreadPriority](#svcGetThreadPriority "wikilink")                         | W1=thread\_handle                                                                                                                                                                                                                                                                  | W0=result, W1=prio                                            |
| 0xD  | [\#svcSetThreadPriority](#svcSetThreadPriority "wikilink")                         | W0=thread\_handle, W1=prio                                                                                                                                                                                                                                                         | W0=result                                                     |
| 0xE  | [\#svcGetThreadCoreMask](#svcGetThreadCoreMask "wikilink")                         | W2=thread\_handle                                                                                                                                                                                                                                                                  | W0=result, W1=out, X2=out                                     |
| 0xF  | [\#svcSetThreadCoreMask](#svcSetThreadCoreMask "wikilink")                         | W0=thread\_handle, W1=in, X2=in2                                                                                                                                                                                                                                                   | W0=result                                                     |
| 0x10 | [\#svcGetCurrentProcessorNumber](#svcGetCurrentProcessorNumber "wikilink")         | None                                                                                                                                                                                                                                                                               | W0/X0=cpuid                                                   |
| 0x11 | svcSignalEvent                                                                     | W0=wevent\_handle                                                                                                                                                                                                                                                                  | W0=result                                                     |
| 0x12 | svcClearEvent                                                                      | W0=wevent\_or\_revent\_handle                                                                                                                                                                                                                                                      | W0=result                                                     |
| 0x13 | [\#svcMapSharedMemory](#svcMapSharedMemory "wikilink")                             | W0=shmem\_handle, X1=addr, X2=size, W3=perm                                                                                                                                                                                                                                        | W0=result                                                     |
| 0x14 | svcUnmapSharedMemory                                                               | W0=shmem\_handle, X1=addr, X2=size                                                                                                                                                                                                                                                 | W0=result                                                     |
| 0x15 | [\#svcCreateTransferMemory](#svcCreateTransferMemory "wikilink")                   | X1=addr, X2=size, W3=perm                                                                                                                                                                                                                                                          | W0=result, W1=tmem\_handle                                    |
| 0x16 | svcCloseHandle                                                                     | W0=handle                                                                                                                                                                                                                                                                          | W0=result                                                     |
| 0x17 | svcResetSignal                                                                     | W0=revent\_or\_process\_handle                                                                                                                                                                                                                                                     | W0=result                                                     |
| 0x18 | [\#svcWaitSynchronization](#svcWaitSynchronization "wikilink")                     | X1=handles\_ptr, W2=num\_handles. X3=timeout                                                                                                                                                                                                                                       | W0=result, W1=handle\_idx                                     |
| 0x19 | [\#svcCancelSynchronization](#svcCancelSynchronization "wikilink")                 | W0=thread\_handle                                                                                                                                                                                                                                                                  | W0=result                                                     |
| 0x1A | svcArbitrateLock                                                                   | W0=cur\_thread\_handle, X1=ptr, W2=req\_thread\_handle                                                                                                                                                                                                                             |                                                               |
| 0x1B | svcArbitrateUnlock                                                                 | X0=ptr                                                                                                                                                                                                                                                                             |                                                               |
| 0x1C | svcWaitProcessWideKeyAtomic                                                        | X0=ptr0, X1=ptr, W2=thread\_handle, X3=timeout                                                                                                                                                                                                                                     | W0=result                                                     |
| 0x1D | svcSignalProcessWideKey                                                            | X0=ptr, W1=value                                                                                                                                                                                                                                                                   | W0=result                                                     |
| 0x1E | [\#svcGetSystemTick](#svcGetSystemTick "wikilink")                                 | None                                                                                                                                                                                                                                                                               | X0={value of cntpct\_el0}                                     |
| 0x1F | svcConnectToNamedPort                                                              | X1=port\_name\_str                                                                                                                                                                                                                                                                 | W0=result, W1=handle                                          |
| 0x20 | svcSendSyncRequestLight                                                            | W0=light\_session\_handle, X1=?                                                                                                                                                                                                                                                    | W0=result                                                     |
| 0x21 | svcSendSyncRequest                                                                 | X0=normal\_session\_handle                                                                                                                                                                                                                                                         | W0=result                                                     |
| 0x22 | [\#svcSendSyncRequestWithUserBuffer](#svcSendSyncRequestWithUserBuffer "wikilink") | X0=cmdbufptr, X1=size, X2=handle                                                                                                                                                                                                                                                   | W0=result                                                     |
| 0x23 | svcSendAsyncRequestWithUserBuffer                                                  | X1=cmdbufptr, X2=size, X3=handle                                                                                                                                                                                                                                                   | W0=result, W1=revent\_handle                                  |
| 0x24 | svcGetProcessId                                                                    | W1=thread\_or\_process\_or\_debug\_handle                                                                                                                                                                                                                                          | W0=result, X1=pid                                             |
| 0x25 | svcGetThreadId                                                                     | W1=thread\_handle                                                                                                                                                                                                                                                                  | W0=result, X1=out                                             |
| 0x26 | [\#svcBreak](#svcBreak "wikilink")                                                 | X0=break\_reason,X1,X2=info                                                                                                                                                                                                                                                        | W0=result = 0                                                 |
| 0x27 | svcOutputDebugString                                                               | X0=str, X1=size                                                                                                                                                                                                                                                                    | W0=result                                                     |
| 0x28 | svcReturnFromException                                                             | X0=result                                                                                                                                                                                                                                                                          |                                                               |
| 0x29 | [\#svcGetInfo](#svcGetInfo "wikilink")                                             | W1=info\_id, X2=handle, X3=info\_sub\_id R0=info\_sub\_id\_lower32, R1=info\_id, R2=handle, R3=info\_sub\_id\_upper32                                                                                                                                                              | W0=result, X1=out R0=result, R1=out\_lower32, R2=out\_upper32 |
| 0x2A | svcFlushEntireDataCache                                                            | None                                                                                                                                                                                                                                                                               | None                                                          |
| 0x2B | svcFlushDataCache                                                                  | X0=addr, X1=size                                                                                                                                                                                                                                                                   | W0=result                                                     |
| 0x2C | \[3.0.0+\] [\#svcMapPhysicalMemory](#svcMapPhysicalMemory "wikilink")              | X0=addr, X1=size                                                                                                                                                                                                                                                                   | W0=result                                                     |
| 0x2D | \[3.0.0+\] svcUnmapPhysicalMemory                                                  | X0=addr, X1=size                                                                                                                                                                                                                                                                   | W0=result                                                     |
| 0x2E | \[5.0.0+\] svcGetFutureThreadInfo                                                  | X3=timeout                                                                                                                                                                                                                                                                         | W0=result, bunch of crap                                      |
| 0x2F | svcGetLastThreadInfo                                                               | None                                                                                                                                                                                                                                                                               | W0=result, W1,W2,W3,W4=unk, W5=truncated\_u64, W6=bool        |
| 0x30 | svcGetResourceLimitLimitValue                                                      | W1=reslimit\_handle, W2=[\#LimitableResource](#LimitableResource "wikilink")                                                                                                                                                                                                       | W0=result, X1=value                                           |
| 0x31 | svcGetResourceLimitCurrentValue                                                    | W1=reslimit\_handle, W2=[\#LimitableResource](#LimitableResource "wikilink")                                                                                                                                                                                                       | W0=result, X1=value                                           |
| 0x32 | svcSetThreadActivity                                                               | W0=thread\_handle, W1=bool                                                                                                                                                                                                                                                         | W0=result                                                     |
| 0x33 | svcGetThreadContext3                                                               | X0=[\#ThreadContext](#ThreadContext "wikilink")\*, W1=thread\_handle                                                                                                                                                                                                               | W0=result                                                     |
| 0x34 | \[4.0.0+\] svcWaitForAddress                                                       | X0=ptr, W1=[\#ArbitrationType](#ArbitrationType "wikilink"), X2=value X3=timeout                                                                                                                                                                                                   |                                                               |
| 0x35 | \[4.0.0+\] svcSignalToAddress                                                      | X0=ptr, W1=[\#SignalType](#SignalType "wikilink"), X2=value W3=num\_to\_signal                                                                                                                                                                                                     |                                                               |
| 0x36 | \[8.0.0+\] svcSynchronizePreemptionState                                           | None                                                                                                                                                                                                                                                                               | W0=result                                                     |
| 0x3C | [\#svcDumpInfo](#svcDumpInfo "wikilink")                                           |                                                                                                                                                                                                                                                                                    |                                                               |
| 0x3D | \[4.0.0+\] svcDumpInfoNew                                                          |                                                                                                                                                                                                                                                                                    |                                                               |
| 0x40 | svcCreateSession                                                                   | W2=is\_light, X3=?                                                                                                                                                                                                                                                                 | W0=result, W1=server\_handle, W2=client\_handle               |
| 0x41 | [\#svcAcceptSession](#svcAcceptSession "wikilink")                                 | W1=port\_handle                                                                                                                                                                                                                                                                    | W0=result, W1=session\_handle                                 |
| 0x42 | svcReplyAndReceiveLight                                                            | W0=light\_session\_handle                                                                                                                                                                                                                                                          | W0=result, W1,W2,W3,W4,W5,W6,W7=out                           |
| 0x43 | [\#svcReplyAndReceive](#svcReplyAndReceive "wikilink")                             | X1=ptr\_handles, W2=num\_handles, X3=replytarget\_handle(0=none), X4=timeout                                                                                                                                                                                                       | W0=result, W1=handle\_idx                                     |
| 0x44 | svcReplyAndReceiveWithUserBuffer                                                   | X1=buf, X2=sz, X3=ptr\_handles, W4=num\_handles, X5=replytarget\_handle(0=none), X6=timeout                                                                                                                                                                                        | W0=result, W1=handle\_idx                                     |
| 0x45 | svcCreateEvent                                                                     | None                                                                                                                                                                                                                                                                               | W0=result, W1=wevent\_handle, W2=revent\_handle               |
| 0x48 | \[5.0.0+\] [\#svcMapPhysicalMemoryUnsafe](#svcMapPhysicalMemoryUnsafe "wikilink")  | X0=addr, X1=size                                                                                                                                                                                                                                                                   | W0=result                                                     |
| 0x49 | \[5.0.0+\] svcUnmapPhysicalMemoryUnsafe                                            | X0=addr, X1=size                                                                                                                                                                                                                                                                   | W0=result                                                     |
| 0x4A | \[5.0.0+\] svcSetUnsafeLimit                                                       | X0=size                                                                                                                                                                                                                                                                            | W0=result                                                     |
| 0x4B | \[4.0.0+\] [\#svcCreateCodeMemory](#svcCreateCodeMemory "wikilink")                | X1=addr, X2=size                                                                                                                                                                                                                                                                   | W0=result, W1=code\_memory\_handle                            |
| 0x4C | \[4.0.0+\] [\#svcControlCodeMemory](#svcControlCodeMemory "wikilink")              | W0=code\_memory\_handle, W1=[\#CodeMemoryOperation](#CodeMemoryOperation "wikilink"), X2=dstaddr, X3=size, W4=perm                                                                                                                                                                 | W0=result                                                     |
| 0x4D | svcSleepSystem                                                                     | None                                                                                                                                                                                                                                                                               | None                                                          |
| 0x4E | [\#svcReadWriteRegister](#svcReadWriteRegister "wikilink")                         | X1=reg\_addr, W2=rw\_mask, W3=in\_val                                                                                                                                                                                                                                              | W0=result, W1=out\_val                                        |
| 0x4F | svcSetProcessActivity                                                              | W0=process\_handle, W1=bool                                                                                                                                                                                                                                                        | W0=result                                                     |
| 0x50 | [\#svcCreateSharedMemory](#svcCreateSharedMemory "wikilink")                       | W1=size, W2=myperm, W3=otherperm                                                                                                                                                                                                                                                   | W0=result, W1=shmem\_handle                                   |
| 0x51 | [\#svcMapTransferMemory](#svcMapTransferMemory "wikilink")                         | X0=tmem\_handle, X1=addr, X2=size, W3=perm                                                                                                                                                                                                                                         | W0=result                                                     |
| 0x52 | [\#svcUnmapTransferMemory](#svcUnmapTransferMemory "wikilink")                     | W0=tmemhandle, X1=addr, X2=size                                                                                                                                                                                                                                                    | W0=result                                                     |
| 0x53 | [\#svcCreateInterruptEvent](#svcCreateInterruptEvent "wikilink")                   | X1=irq\_num, W2=flag                                                                                                                                                                                                                                                               | W0=result, W1=handle                                          |
| 0x54 | [\#svcQueryPhysicalAddress](#svcQueryPhysicalAddress "wikilink")                   | X1=addr                                                                                                                                                                                                                                                                            | W0=result, X1=physaddr, X2=kerneladdr, X3=size                |
| 0x55 | [\#svcQueryIoMapping](#svcQueryIoMapping "wikilink")                               | X1=physaddr, X2=size                                                                                                                                                                                                                                                               | W0=result, X1=virtaddr                                        |
| 0x56 | [\#svcCreateDeviceAddressSpace](#svcCreateDeviceAddressSpace "wikilink")           | X1=dev\_as\_start\_addr, X2=dev\_as\_end\_addr                                                                                                                                                                                                                                     | W0=result, W1=dev\_as\_handle                                 |
| 0x57 | [\#svcAttachDeviceAddressSpace](#svcAttachDeviceAddressSpace "wikilink")           | W0=device, X1=dev\_as\_handle                                                                                                                                                                                                                                                      | W0=result                                                     |
| 0x58 | [\#svcDetachDeviceAddressSpace](#svcDetachDeviceAddressSpace "wikilink")           | W0=device, X1=dev\_as\_handle                                                                                                                                                                                                                                                      | W0=result                                                     |
| 0x59 | [\#svcMapDeviceAddressSpaceByForce](#svcMapDeviceAddressSpaceByForce "wikilink")   | W0=dev\_as\_handle, W1=proc\_handle, X2=dev\_map\_addr, X3=dev\_as\_size, X4=dev\_as\_addr, W5=perm                                                                                                                                                                                | W0=result                                                     |
| 0x5A | [\#svcMapDeviceAddressSpaceAligned](#svcMapDeviceAddressSpaceAligned "wikilink")   | W0=dev\_as\_handle, W1=proc\_handle, X2=dev\_map\_addr, X3=dev\_as\_size, X4=dev\_as\_addr, W5=perm                                                                                                                                                                                | W0=result                                                     |
| 0x5B | svcMapDeviceAddressSpace                                                           |                                                                                                                                                                                                                                                                                    |                                                               |
| 0x5C | [\#svcUnmapDeviceAddressSpace](#svcUnmapDeviceAddressSpace "wikilink")             | W0=dev\_as\_handle, W1=proc\_handle, X2=dev\_map\_addr, X3=dev\_as\_size, X4=dev\_as\_addr                                                                                                                                                                                         | W0=result                                                     |
| 0x5D | svcInvalidateProcessDataCache                                                      | W0=process\_handle, X1=addr, X2=size                                                                                                                                                                                                                                               | W0=size                                                       |
| 0x5E | svcStoreProcessDataCache                                                           | W0=process\_handle, X1=addr, X2=size                                                                                                                                                                                                                                               | W0=size                                                       |
| 0x5F | svcFlushProcessDataCache                                                           | W0=process\_handle, X1=addr, X2=size                                                                                                                                                                                                                                               | W0=size                                                       |
| 0x60 | svcDebugActiveProcess                                                              | X1=pid                                                                                                                                                                                                                                                                             | W0=result, W1=debug\_handle                                   |
| 0x61 | svcBreakDebugProcess                                                               | W0=debug\_handle                                                                                                                                                                                                                                                                   | W0=result                                                     |
| 0x62 | svcTerminateDebugProcess                                                           | W0=debug\_handle                                                                                                                                                                                                                                                                   | W0=result                                                     |
| 0x63 | svcGetDebugEvent                                                                   | X0=[\#DebugEventInfo](#DebugEventInfo "wikilink")\*, W1=debug\_handle                                                                                                                                                                                                              | W0=result                                                     |
| 0x64 | [\#svcContinueDebugEvent](#svcContinueDebugEvent "wikilink")                       | \[1.0.0-2.3.0\] W0=debug\_handle, W1=[\#ContinueDebugFlagsOld](#ContinueDebugFlagsOld "wikilink"), X2=thread\_id \[3.0.0+\] W0=debug\_handle, W1=[\#ContinueDebugFlags](#ContinueDebugFlags "wikilink"), X2=thread\_id\_list(u64 \*), W3=num\_tids (max 64, 0 means "all threads") | W0=result                                                     |
| 0x65 | svcGetProcessList                                                                  | X1=pids\_out\_ptr, W2=max\_out                                                                                                                                                                                                                                                     | W0=result, W1=num\_out                                        |
| 0x66 | svcGetThreadList                                                                   | X1=tids\_out\_ptr, W2=max\_out, W3=debug\_handle\_or\_zero                                                                                                                                                                                                                         | W0=result, X1=num\_out                                        |
| 0x67 | svcGetDebugThreadContext                                                           | X0=ThreadContext\*, X1=debug\_handle, X2=thread\_id, W3=[\#ThreadContextFlags](#ThreadContextFlags "wikilink")                                                                                                                                                                     | W0=result                                                     |
| 0x68 | svcSetDebugThreadContext                                                           | W0=debug\_handle, X1=thread\_id, X2=ThreadContext\*, W3=[\#ThreadContextFlags](#ThreadContextFlags "wikilink")                                                                                                                                                                     | W0=result                                                     |
| 0x69 | svcQueryDebugProcessMemory                                                         | X0=[\#MemoryInfo](#MemoryInfo "wikilink")\*, X2=debug\_handle, X3=addr                                                                                                                                                                                                             | W0=result, W1=PageInfo                                        |
| 0x6A | svcReadDebugProcessMemory                                                          | X0=buffer\*, X1=debug\_handle, X2=src\_addr, X3=size                                                                                                                                                                                                                               | W0=result                                                     |
| 0x6B | svcWriteDebugProcessMemory                                                         | X0=debug\_handle, X1=buffer\*, X2=dst\_addr, X3=size                                                                                                                                                                                                                               | W0=result                                                     |
| 0x6C | [\#svcSetHardwareBreakPoint](#svcSetHardwareBreakPoint "wikilink")                 | W0=HardwareBreakpointId, X1=watchpoint\_flags/breakpoint\_flags, X2=watchpoint\_value/debug\_handle                                                                                                                                                                                |                                                               |
| 0x6D | svcGetDebugThreadParam                                                             | X2=debug\_handle, X3=thread\_id, W4=[\#DebugThreadParam](#DebugThreadParam "wikilink")                                                                                                                                                                                             | W0=result, X1=out0, W2=out1                                   |
| 0x6F | \[5.0.0+\] [\#svcGetSystemInfo](#svcGetSystemInfo "wikilink")                      | X1=info\_id, X2=handle, X3=info\_sub\_id                                                                                                                                                                                                                                           | W0=result, X1=out                                             |
| 0x70 | svcCreatePort                                                                      | W2=max\_sessions, W3=is\_light, X4=name\_ptr                                                                                                                                                                                                                                       | W0=result, W1=serverport\_handle, W2=clientport\_handle       |
| 0x71 | svcManageNamedPort                                                                 | X1=name\_ptr, W2=max\_sessions                                                                                                                                                                                                                                                     | W0=result, W1=serverport\_handle                              |
| 0x72 | svcConnectToPort                                                                   | W1=clientport\_handle                                                                                                                                                                                                                                                              | W0=result, W1=session\_handle                                 |
| 0x73 | [\#svcSetProcessMemoryPermission](#svcSetProcessMemoryPermission "wikilink")       | W0=process\_handle, X1=addr, X2=size, W3=perm                                                                                                                                                                                                                                      | W0=result                                                     |
| 0x74 | [\#svcMapProcessMemory](#svcMapProcessMemory "wikilink")                           | X0=dstaddr, W1=process\_handle, X2=srcaddr, X3=size                                                                                                                                                                                                                                | W0=result                                                     |
| 0x75 | [\#svcUnmapProcessMemory](#svcUnmapProcessMemory "wikilink")                       | X0=dstaddr, W1=process\_handle, X2=srcaddr, X3=size                                                                                                                                                                                                                                | W0=result                                                     |
| 0x76 | [\#svcQueryProcessMemory](#svcQueryProcessMemory "wikilink")                       | X0=meminfo\_ptr, W2=process\_handle, X3=addr                                                                                                                                                                                                                                       | W0=result, W1=pageinfo                                        |
| 0x77 | [\#svcMapProcessCodeMemory](#svcMapProcessCodeMemory "wikilink")                   | W0=process\_handle, X1=dstaddr, X2=srcaddr, X3=size                                                                                                                                                                                                                                | W0=result                                                     |
| 0x78 | [\#svcUnmapProcessCodeMemory](#svcUnmapProcessCodeMemory "wikilink")               | W0=process\_handle, X1=dstaddr, X2=srcaddr, X3=size                                                                                                                                                                                                                                | W0=result                                                     |
| 0x79 | [\#svcCreateProcess](#svcCreateProcess "wikilink")                                 | X1=procinfo\_ptr, X2=caps\_ptr, W3=cap\_num                                                                                                                                                                                                                                        | W0=result, W1=process\_handle                                 |
| 0x7A | svcStartProcess                                                                    | W0=process\_handle, W1=main\_thread\_prio, W2=default\_cpuid, W3=main\_thread\_stacksz                                                                                                                                                                                             | W0=result                                                     |
| 0x7B | svcTerminateProcess                                                                | W0=process\_handle                                                                                                                                                                                                                                                                 | W0=result                                                     |
| 0x7C | [\#svcGetProcessInfo](#svcGetProcessInfo "wikilink")                               | W0=process\_handle, W1=[\#ProcessInfoType](#ProcessInfoType "wikilink")                                                                                                                                                                                                            | W0=result, X1=[\#ProcessState](#ProcessState "wikilink")      |
| 0x7D | svcCreateResourceLimit                                                             | None                                                                                                                                                                                                                                                                               | W0=result, W1=reslimit\_handle                                |
| 0x7E | svcSetResourceLimitLimitValue                                                      | W0=reslimit\_handle, W1=[\#LimitableResource](#LimitableResource "wikilink"), X2=value                                                                                                                                                                                             | W0=result                                                     |
| 0x7F | [\#svcCallSecureMonitor](#svcCallSecureMonitor "wikilink")                         | X0=smc\_sub\_id, X1,X2,X3,X4,X5,X6,X7=smc\_args                                                                                                                                                                                                                                    | X0,X1,X2,X3,X4,X5,X6,X7=result                                |

## svcSetHeapSize

<div style="display: inline-block;">

| Argument | Type                           | Name    |
| -------- | ------------------------------ | ------- |
| (In) W1  | u64                            | Size    |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret     |
| (Out) X1 | u64                            | OutAddr |

</div>

**Description:** Set the process heap to a given Size. It can both
extend and shrink the heap.

Size must be a multiple of 0x200000 (2MB).

On success, the heap base-address (which is fixed by kernel, aslr'd) is
written to OutAddr.

Uses current process pool partition.

\[2.0.0+\] Size must be less than or equal to 4GB.

## svcSetMemoryPermission

<div style="display: inline-block;">

| Argument | Type                                   | Name |
| -------- | -------------------------------------- | ---- |
| (In) X0  | void\*                                 | Addr |
| (In) X1  | u64                                    | Size |
| (In) W2  | [\#Permission](#Permission "wikilink") | Prot |
| (Out) W0 | [\#Result](#Result "wikilink")         | Ret  |

</div>

**Description:** Change permission of page-aligned memory region.

Bit2 of permission (exec) is not allowed. Setting write-only is not
allowed either (bit1).

This can be used to move back and forth between ---, r-- and rw-.

## svcSetMemoryAttribute

<div style="display: inline-block;">

| Argument | Type                           | Name   |
| -------- | ------------------------------ | ------ |
| (In) X0  | void\*                         | Addr   |
| (In) X1  | u64                            | Size   |
| (In) W2  | u32                            | State0 |
| (In) W3  | u32                            | State1 |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret    |

</div>

**Description:** Change attribute of page-aligned memory region.

This is used to turn on/off caching for a given memory area. Useful when
talking to devices such as the GPU.

What happens "under the hood" is the "Memory Attribute Indirection
Register" index is changed from 2 to 3 in the MMU descriptor.

| State0 | State1 | Action                                                          |
| ------ | ------ | --------------------------------------------------------------- |
| 0      | 0      | Clear bit3 in [\#MemoryAttribute](#MemoryAttribute "wikilink"). |
| 8      | 0      | Clear bit3 in [\#MemoryAttribute](#MemoryAttribute "wikilink"). |
| 8      | 8      | Set bit3 in [\#MemoryAttribute](#MemoryAttribute "wikilink").   |

## svcMapMemory

<div style="display: inline-block;">

| Argument | Type                           | Name    |
| -------- | ------------------------------ | ------- |
| (In) X0  | void\*                         | DstAddr |
| (In) X1  | void\*                         | SrcAddr |
| (In) X2  | u64                            | Size    |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret     |

</div>

**Description:** Maps a memory range into a different range.

Mainly used for adding guard pages around stack.

Source range gets reprotected to --- (it can no longer be accessed), and
bit0 is set in the source
[\#MemoryAttribute](#MemoryAttribute "wikilink").

\[1.0.0\] This could be used to map into either the Alias Region or the
Stack region.

\[2.0.0+\] This can only be used to map into the Stack region.

Code can get the range of the Alias region from
[\#svcGetInfo](#svcGetInfo "wikilink") id0=2,3, and on 2.0.0+ the range
of the Stack region via [\#svcGetInfo](#svcGetInfo "wikilink") id0=14,
15 (on 1.0.0, the Stack region had hardcoded limits).

When mapped into the Alias region, the mapped memory will have state
0x482907.

When mapped into the Stack region, the mapped memory will have state
0x5C3C0B.

## svcUnmapMemory

<div style="display: inline-block;">

| Argument | Type                           | Name    |
| -------- | ------------------------------ | ------- |
| (In) X0  | void\*                         | DstAddr |
| (In) X1  | void\*                         | SrcAddr |
| (In) X2  | u64                            | Size    |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret     |

</div>

**Description:** Unmaps a region that was previously mapped with
[\#svcMapMemory](#svcMapMemory "wikilink").

It's possible to unmap ranges partially, you don't need to unmap the
entire range "in one go".

The srcaddr/dstaddr must match what was given when the pages were
originally mapped.

## svcQueryMemory

<div style="display: inline-block;">

| Argument | Type                                     | Name     |
| -------- | ---------------------------------------- | -------- |
| (In) X0  | [\#MemoryInfo](#MemoryInfo "wikilink")\* | MemInfo  |
| (In) X2  | void\*                                   | Addr     |
| (Out) W0 | [\#Result](#Result "wikilink")           | Ret      |
| (Out) W1 | PageInfo                                 | PageInfo |

</div>

**Description:** Query information about an address. Will always fetch
the lowest page-aligned mapping that contains the provided address.

Outputs a [\#MemoryInfo](#MemoryInfo "wikilink") struct.

## svcExitProcess

<div style="display: inline-block;">

| Argument   | Type | Name |
| ---------- | ---- | ---- |
| (In) None  |      |      |
| (Out) None |      |      |

</div>

**Description:** Exits the current process.

## svcCreateThread

<div style="display: inline-block;">

| Argument | Type                           | Name          |
| -------- | ------------------------------ | ------------- |
| (In) X1  | void(\*)(void\*)               | Entry         |
| (In) X2  | void\*                         | ThreadContext |
| (In) X3  | void\*                         | StackTop      |
| (In) W4  | u32                            | Priority      |
| (In) W5  | u32                            | ProcessorId   |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret           |
| (Out) W1 | Handle<Thread>                 | Handle        |

</div>

**Description:** Create a thread in the current process.

Processor\_id must be 0,1,2,3 or -2, where -2 uses the default cpuid for
process.

## svcStartThread

<div style="display: inline-block;">

| Argument   | Type           | Name   |
| ---------- | -------------- | ------ |
| (In) W0    | Handle<Thread> | Handle |
| (Out) None |                |        |

</div>

**Description:** Starts the thread for the provided handle.

## svcExitThread

<div style="display: inline-block;">

| Argument   | Type | Name |
| ---------- | ---- | ---- |
| (In) None  |      |      |
| (Out) None |      |      |

</div>

**Description:** Exits the current thread.

## svcSleepThread

<div style="display: inline-block;">

| Argument | Type | Name        |
| -------- | ---- | ----------- |
| (In) X0  | s64  | Nanoseconds |
|          |      |             |

</div>

**Description:** Sleep for a specified amount of time, or yield thread.

Setting nanoseconds to 0, -1, or -2 indicates a yielding type.

<div style="display: inline-block;">

| Value | Type                            |
| ----- | ------------------------------- |
| 0     | Yielding without core migration |
| \-1   | Yielding with core migration    |
| \-2   | Yielding to any other thread    |
|       |                                 |

</div>

## svcGetThreadPriority

<div style="display: inline-block;">

| Argument | Type                           | Name     |
| -------- | ------------------------------ | -------- |
| (In) W1  | Handle<Thread>                 | Handle   |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret      |
| (Out) W1 | u64                            | Priority |

</div>

**Description:** Get priority of provided thread handle.

## svcSetThreadPriority

<div style="display: inline-block;">

| Argument | Type                           | Name     |
| -------- | ------------------------------ | -------- |
| (In) W0  | Handle<Thread>                 | Handle   |
| (In) W1  | u32                            | Priority |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret      |

</div>

**Description:** Set priority of provided thread handle.

Priority is a number 0-0x3F. Lower value means higher priority.

## svcGetThreadCoreMask

<div style="display: inline-block;">

| Argument | Type                           | Name   |
| -------- | ------------------------------ | ------ |
| (In) W2  | Handle<Thread>                 | Handle |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret    |
| (Out) W1 | u32                            | Out0   |
| (Out) X2 | u64                            | Out1   |

</div>

**Description:** Get affinity mask of provided thread handle.

## svcSetThreadCoreMask

<div style="display: inline-block;">

| Argument | Type                           | Name   |
| -------- | ------------------------------ | ------ |
| (In) W0  | Handle<Thread>                 | Handle |
| (In) W1  | u32                            | In0    |
| (In) X2  | u64                            | In1    |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret    |

</div>

**Description:** Set affinity mask of provided thread handle.

## svcGetCurrentProcessorNumber

<div style="display: inline-block;">

| Argument    | Type | Name  |
| ----------- | ---- | ----- |
| (In) None   |      |       |
| (Out) W0/X0 | u64  | CpuId |

</div>

**Description:** Get which cpu is executing the current thread.

Cpu-id is an integer in the range 0-3.

## svcMapSharedMemory

<div style="display: inline-block;">

| Argument | Type                                   | Name        |
| -------- | -------------------------------------- | ----------- |
| (In) W0  | Handle<SharedMemory>                   | MemHandle   |
| (In) X1  | void\*                                 | Addr        |
| (In) X2  | u64                                    | Size        |
| (In) W3  | [\#Permission](#Permission "wikilink") | Permissions |
| (Out) W0 | [\#Result](#Result "wikilink")         | Ret         |

</div>

Maps the block supplied by the handle. The required permissions are
different for the process that created the handle and all other
processes.

Increases reference count for the KSharedMemory object. Thus in order to
release the memory associated with the object, all handles to it must be
closed and all mappings must be unmapped.

## svcCreateTransferMemory

<div style="display: inline-block;">

| Argument | Type                                   | Name        |
| -------- | -------------------------------------- | ----------- |
| (In) X1  | void\*                                 | Addr        |
| (In) X2  | u64                                    | Size        |
| (In) W3  | [\#Permission](#Permission "wikilink") | Permissions |
| (Out) W0 | [\#Result](#Result "wikilink")         | Ret         |
| (Out) W1 | Handle<TransferMemory>                 | Handle      |

</div>

This one reprotects the src block with perms you give it. It also sets
bit0 into [\#MemoryAttribute](#MemoryAttribute "wikilink").

Executable bit perm not allowed.

Closing all handles automatically causes the bit0 in
[\#MemoryAttribute](#MemoryAttribute "wikilink") to clear, and the
permission to reset.

## svcWaitSynchronization

<div style="display: inline-block;">

| Argument | Type                           | Name        |
| -------- | ------------------------------ | ----------- |
| (In) X1  | Handle\*                       | HandlesPtr  |
| (In) W2  | u64                            | HandlesNum  |
| (In) X3  | u64                            | Timeout     |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret         |
| (Out) W1 | u64                            | HandleIndex |

</div>

Works with num\_handles \<= 0x40.

When zero handles are passed, this will wait forever until either
timeout or cancellation occurs.

Does not accept 0xFFFF8001 or 0xFFFF8000 as handles.

### Object types

**KDebug:** signals when there is a new
[DebugEvent](#DebugEventInfo "wikilink") (retrievable via
[\#svcGetDebugEvent](#svcGetDebugEvent "wikilink")).

**KClientPort:** signals when the number of sessions is less than the
maximum allowed.

**KProcess:** signals when the process undergoes a state change
(retrievable via [\#svcGetProcessInfo](#svcGetProcessInfo "wikilink")).

**KReadableEvent:** signals when the event's corresponding
KWritableEvent has been signaled via svcSignalEvent.

**KServerPort:** signals when there is an incoming connection waiting to
be [accepted](#svcAcceptSession "wikilink").

**KServerSession:** signals when there is an incoming message waiting to
be [received](#svcReplyAndReceive "wikilink") or the pipe is closed.

**KThread:** signals when the thread has exited.

### Result codes

**0x0:** Success. One of the objects was signaled before the timeout
expired, or one of the objects is a Session with a closed remote. Handle
index is updated to indicate which object signaled.

**0x7601:** Thread termination requested. Handle index is not updated.

**0xe401:** Invalid handle. Returned when one of the handles passed is
invalid. Handle index is not updated.

**0xe601:** Invalid address. Returned when the handles pointer is not a
readable address. Handle index is not updated.

**0xea01:** Timeout. Returned when no objects have been signaled within
the timeout. Handle index is not updated.

**0xec01:** Interrupted. Returned when another thread uses
[\#svcCancelSynchronization](#svcCancelSynchronization "wikilink") to
cancel this thread. Handle index is not updated.

**0xee01:** Too many handles. Returned when the number of handles passed
is \> 0x40.

## svcCancelSynchronization

<div style="display: inline-block;">

| Argument | Type                           | Name   |
| -------- | ------------------------------ | ------ |
| (In) W0  | Handle<Thread>                 | Handle |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret    |

</div>

If the referenced thread is currently in a synchronization call
([\#svcWaitSynchronization](#svcWaitSynchronization "wikilink"),
[\#svcReplyAndReceive](#svcReplyAndReceive "wikilink") or
[\#svcReplyAndReceiveLight](#svcReplyAndReceiveLight "wikilink")), that
call will be interrupted and return 0xec01. If that thread is not
currently executing such a synchronization call, the next call to a
synchronization call will return 0xec01.

This doesn't take force-pause (activity/debug pause) into account.

### Result codes

**0x0:** Success. The thread was either interrupted or has had its flag
set.

**0xe401:** Invalid handle. The handle given was either invalid or not a
thread handle.

## svcGetSystemTick

<div style="display: inline-block;">

| Argument | Type | Name  |
| -------- | ---- | ----- |
| (Out) X0 | u64  | Ticks |

</div>

Returns the value of cntpct\_el0.

The frequency is 19200000 Hz (constant from official sw).

Official sw reads cntpct\_el0 directly from usermode without using this
SVC. [sdk-nso](ExeFS.md "wikilink") has this SVC, but it's not known to
be called anywhere.

## svcSendSyncRequestWithUserBuffer

<div style="display: inline-block;">

| Argument | Type                           | Name   |
| -------- | ------------------------------ | ------ |
| (In) X0  | void\*                         | CmdPtr |
| (In) X1  | u64                            | Size   |
| (In) W2  | Handle<Session>                | Handle |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret    |

</div>

Size and CmdPtr must be 0x1000-aligned.

### Result codes

**0x0:** Success.

**0xcc01:** CmdPtr is not 0x1000-aligned.

**0xca01:** Size is not 0x1000-aligned.

**0xce01:** KSessionRequest allocation failed (unlikely) or pointer
buffer size exceeded.

**0xe401:** Handles does not exist, or handle is not an instance of
KClientSession.

## svcBreak

<div style="display: inline-block;">

| Argument | Type   | Name         |
| -------- | ------ | ------------ |
| (In) X0  | u64    | Break Reason |
| (In) X1  | u64    |              |
| (In) X2  | u64    | Info         |
| (Out) W0 | Result | 0 (Success)  |

</div>

If the process is attached, report the Break event. Then, if
svcContinueDebugEvent didn't apply IgnoreException on the thread: if
TPIDR\_EL0 is 0, adjust ELR\_EL1 to retry to svc instruction (and set
TPIDR\_EL0 to 1).

Otherwise, if bit31 in reason isn't set, perform crash reporting (see
Exception Handling section below), if it doesn't terminate the process
adjust ELR\_EL1 as well.

Otherwise just return 0.

## svcGetInfo

<div style="display: inline-block;">

| Argument | Type                           | Name      |
| -------- | ------------------------------ | --------- |
| (In) W1  | u32                            | InfoId    |
| (In) W2  | Handle                         | Handle    |
| (In) X3  | u64                            | InfoSubId |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret       |
| (Out) X1 | u64                            | Out       |

</div>

<div style="display: inline-block; vertical-align:top;">

| Argument | Type                           | Name             |
| -------- | ------------------------------ | ---------------- |
| (In) R0  | u32                            | InfoSubIdLower32 |
| (In) R1  | u32                            | InfoId           |
| (In) R2  | Handle                         | Handle           |
| (In) R3  | u32                            | InfoSubIdUpper32 |
| (Out) R0 | [\#Result](#Result "wikilink") | Ret              |
| (Out) R1 | u32                            | OutLower32       |
| (Out) R2 | u32                            | OutUpper32       |

</div>

| Handle type | Id0        | Id1                   | Description                                                                                                                               |
| ----------- | ---------- | --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Process     | 0          | 0                     | AllowedCpuIdBitmask                                                                                                                       |
| Process     | 1          | 0                     | AllowedThreadPrioBitmask                                                                                                                  |
| Process     | 2          | 0                     | AliasRegionBaseAddr                                                                                                                       |
| Process     | 3          | 0                     | AliasRegionSize                                                                                                                           |
| Process     | 4          | 0                     | HeapRegionBaseAddr                                                                                                                        |
| Process     | 5          | 0                     | HeapRegionSize                                                                                                                            |
| Process     | 6          | 0                     | TotalMemoryAvailable. Total memory available(free+used).                                                                                  |
| Process     | 7          | 0                     | TotalMemoryUsage. Total used size of codebin memory + main-thread stack + allocated heap.                                                 |
| Zero        | 8          | 0                     | IsCurrentProcessBeingDebugged                                                                                                             |
| Zero        | 9          | 0                     | Returns ResourceLimit handle for current process. Used by [PM](Process%20Manager%20services.md "wikilink").                               |
| Zero        | 10         | \-1, {current coreid} | IdleTickCount                                                                                                                             |
| Zero        | 11         | 0-3                   | RandomEntropy from current process. TRNG. Used to seed usermode PRNGs.                                                                    |
| Process     | 12         | 0                     | \[2.0.0+\] AddressSpaceBaseAddr                                                                                                           |
| Process     | 13         | 0                     | \[2.0.0+\] AddressSpaceSize                                                                                                               |
| Process     | 14         | 0                     | \[2.0.0+\] StackRegionBaseAddr                                                                                                            |
| Process     | 15         | 0                     | \[2.0.0+\] StackRegionSize                                                                                                                |
| Process     | 16         | 0                     | \[3.0.0+\] PersonalMmHeapSize                                                                                                             |
| Process     | 17         | 0                     | \[3.0.0+\] PersonalMmHeapUsage                                                                                                            |
| Process     | 18         | 0                     | \[3.0.0+\] TitleId                                                                                                                        |
| Zero        | 19         | 0                     | \[4.0.0-4.1.0\] PrivilegedProcessId\_LowerBound                                                                                           |
| Zero        | 19         | 1                     | \[4.0.0-4.1.0\] PrivilegedProcessId\_UpperBound                                                                                           |
| Process     | 20         | 0                     | \[5.0.0+\] UserExceptionContextAddr                                                                                                       |
| Process     | 21         | 0                     | \[6.0.0+\] TotalMemoryAvailableWithoutMmHeap                                                                                              |
| Process     | 22         | 0                     | \[6.0.0+\] TotalMemoryUsedWithoutMmHeap                                                                                                   |
| Thread      | 0xF0000002 | 0-3, -1               | Thread Ticks. When 0-3 are passed, gets specific core CPU ticks spent on thread. When -1 is passed, gets total CPU ticks spent on thread. |

## svcMapPhysicalMemory

This is like svcSetHeapSize except you can allocate heap at any address
you'd like.

Uses current process pool partition.

## svcDumpInfo

<div style="display: inline-block;">

| Argument   | Type | Name |
| ---------- | ---- | ---- |
| (In) None  |      |      |
| (Out) None |      |      |

</div>

Does nothing, just returns with registers set to all-zero.

## svcAcceptSession

<div style="display: inline-block;">

| Argument | Type                           | Name    |
| -------- | ------------------------------ | ------- |
| (In) W1  | Handle<Port>                   | Port    |
| (Out) W0 | [\#Result](#Result "wikilink") | Result  |
| (Out) W1 | Handle<ServerSession>          | Session |

</div>

### Result codes

**0xf201:** No session waiting to be accepted

## svcReplyAndReceive

<div style="display: inline-block;">

| Argument | Type                            | Name        |
| -------- | ------------------------------- | ----------- |
| (In) W1  | \*Handle<Port or ServerSession> | Handles     |
| (In) W2  | u32                             | NumHandles  |
| (In) W3  | Handle<ServerSession>           | ReplyTarget |
| (In) X4  | u64 (nanoseconds)               | Timeout     |
| (Out) W0 | [\#Result](#Result "wikilink")  | Result      |
| (Out) W1 | u32                             | HandleIndex |

</div>

If ReplyTarget is not zero, a reply from the TLS will be sent to that
session. Then it will wait until either of the passed sessions has an
incoming message, is closed, a passed port has an incoming connection,
or the timeout expires. If there is an incoming message, it is copied to
the TLS.

If ReplyTarget is zero, the TLS should contain a blank message. If this
message has a C descriptor, the buffer it points to will be used as the
pointer buffer. See
[IPC\_Marshalling\#IPC\_buffers](IPC%20Marshalling#IPC%20buffers.md##IPC_buffers "wikilink").
Note that a pointer buffer cannot be specified if ReplyTarget is not
zero.

After being validated, passed handles will be enumerated in order; even
if a session has been closed, if one that appears earlier in the list
has an incoming message, it will take priority and a result code of 0x0
will be returned.

### Result codes

**0x0:** Success. Either a session has an incoming message or a port has
an incoming connection. HandleIndex is set appropriately.

**0xea01:** Timeout. No handles were signalled before the timeout
expired. HandleIndex is not updated.

**0xf601:** Port remote dead. One of the sessions has been closed.
HandleIndex is set appropriately.

## svcMapPhysicalMemoryUnsafe

Same as [\#svcMapPhysicalMemory](#svcMapPhysicalMemory "wikilink")
except it always uses pool partition 0.

## svcCreateCodeMemory

Takes an address range with backing memory to create the code memory
object.

The memory is initially memset to 0xFF after being locked.

## svcControlCodeMemory

Maps the backing memory for a Code memory object into the current
process.

For [CodeMemoryOperation\_MapOwner](#CodeMemoryOperation "wikilink"),
memory permission must be RW-.

For [CodeMemoryOperation\_MapSlave](#CodeMemoryOperation "wikilink"),
memory permission must be R-- or R-X.

Operations
[CodeMemoryOperation\_UnmapOwner/CodeMemoryOperation\_UnmapSlave](#CodeMemoryOperation "wikilink")
unmap memory that was previously mapped this way.

This allows one "secure JIT" process to map the code memory as RW-, and
the other "slave" process to map it R-X.

\[5.0.0+\] Error 0xE401 is now returned when the process owner of the
Code memory object is the same as the current process.

## svcReadWriteRegister

<div style="display: inline-block;">

| Argument | Type                           | Name     |
| -------- | ------------------------------ | -------- |
| (In) X1  | u64                            | RegAddr  |
| (In) W2  | u64                            | RwMask   |
| (In) W3  | u64                            | InValue  |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret      |
| (Out) W1 | u64                            | OutValue |

</div>

Read/write IO registers with a hardcoded whitelist. Input address is
physical-address and must be aligned to 4.

rw\_mask is 0 for reading and 0xffffffff for writing. You can also write
individual bits by using a mask value.

You can only write to registers inside physical pages 0x70019000 (MC),
0x7001C000 (MC0), 0x7001D000 (MC1), and they all share the same
whitelist.

The whitelist is same for writing as for reading.

The whitelist is:

0x054, 0x090, 0x094, 0x098, 0x09c, 0x0a0, 0x0a4, 0x0a8, 0x0ac, 0x0b0,
0x0b4, 0x0b8, 0x0bc, 0x0c0, 0x0c4, 0x0c8, 0x0d0, 0x0d4, 0x0d8, 0x0dc,
0x0e0, 0x100, 0x108, 0x10c, 0x118, 0x11c, 0x124, 0x128, 0x12c, 0x130,
0x134, 0x138, 0x13c, 0x158, 0x15c, 0x164, 0x168, 0x16c, 0x170, 0x174,
0x178, 0x17c, 0x200, 0x204, 0x2e4, 0x2e8, 0x2ec, 0x2f4, 0x2f8, 0x310,
0x314, 0x320, 0x328, 0x344, 0x348, 0x370, 0x374, 0x37c, 0x380, 0x390,
0x394, 0x398, 0x3ac, 0x3b8, 0x3bc, 0x3c0, 0x3c4, 0x3d8, 0x3e8, 0x41c,
0x420, 0x424, 0x428, 0x42c, 0x430, 0x44c, 0x47c, 0x480, 0x484, 0x50c,
0x554, 0x558, 0x55c, 0x670, 0x674, 0x690, 0x694, 0x698, 0x69c, 0x6a0,
0x6a4, 0x6c0, 0x6c4, 0x6f0, 0x6f4, 0x960, 0x970, 0x974, 0xa20, 0xa24,
0xb88, 0xb8c, 0xbc4, 0xbc8, 0xbcc, 0xbd0, 0xbd4, 0xbd8, 0xbdc, 0xbe0,
0xbe4, 0xbe8, 0xbec, 0xc00, 0xc5c, 0xcac

\[2.0.0+\] Whitelist was extended with 0x4c4, 0x4c8, 0x4cc, 0x584,
0x588, 0x58c.

\[2.0.0+\] The IO registers in range 0x7000E400 (PMC) size 0xC00 skip
the whitelist, and do a TrustZone call using [SMC](SMC.md "wikilink")
Id1 0xC3000008(ReadWriteRegister).

\[4.0.0+\] Access to the Memory Controller (0x70019000) also uses
smcReadWriteRegister.

Here is the whitelist imposed by that SMC, relative to the start of the
PMC registers:

0x000, 0x00c, 0x010, 0x014, 0x01c, 0x020, 0x02c, 0x030, 0x034, 0x038,
0x03c, 0x040, 0x044, 0x048, 0x0dc, 0x0e0, 0x0e4, 0x160, 0x164, 0x168,
0x170, 0x1a8, 0x1b8, 0x1bc, 0x1c0, 0x1c4, 0x1c8, 0x2b4, 0x2d4, 0x440,
0x4d8

Here is the whitelist imposed by smcReadWriteRegister (checked in
addition to the whitelist in svcReadWriteRegister), relative to the
start of the MC registers:

0x000, 0x004, 0x008, 0x00C, 0x010, 0x01C, 0x020, 0x030, 0x034, 0x050,
0x054, 0x090, 0x094, 0x098, 0x09C, 0x0A0, 0x0A4, 0x0A8, 0x0AC, 0x0B0,
0x0B4, 0x0B8, 0x0BC, 0x0C0, 0x0C4, 0x0C8, 0x0D0, 0x0D4, 0x0D8, 0x0DC,
0x0E0, 0x100, 0x108, 0x10C, 0x118, 0x11C, 0x124, 0x128, 0x12C, 0x130,
0x134, 0x138, 0x13C, 0x158, 0x15C, 0x164, 0x168, 0x16C, 0x170, 0x174,
0x178, 0x17C, 0x200, 0x204, 0x238, 0x240, 0x244, 0x250, 0x254, 0x258,
0x264, 0x268, 0x26C, 0x270, 0x274, 0x280, 0x284, 0x288, 0x28C, 0x294,
0x2E4, 0x2E8, 0x2EC, 0x2F4, 0x2F8, 0x310, 0x314, 0x320, 0x328, 0x344,
0x348, 0x370, 0x374, 0x37C, 0x380, 0x390, 0x394, 0x398, 0x3AC, 0x3B8,
0x3BC, 0x3C0, 0x3C4, 0x3D8, 0x3E8, 0x41C, 0x420, 0x424, 0x428, 0x42C,
0x430, 0x44C, 0x47C, 0x480, 0x484, 0x4C4, 0x4C8, 0x4CC, 0x50C, 0x554,
0x558, 0x55C, 0x584, 0x588, 0x58C, 0x670, 0x674, 0x690, 0x694, 0x698,
0x69C, 0x6A0, 0x6A4, 0x6C0, 0x6C4, 0x6F0, 0x6F4, 0x960, 0x970, 0x974,
0x9B8, 0xA20, 0xA24, 0xA88, 0xA94, 0xA98, 0xA9C, 0xAA0, 0xAA4, 0xAA8,
0xAAC, 0xAB0, 0xAB4, 0xAB8, 0xABC, 0xAC0, 0xAC4, 0xAC8, 0xACC, 0xAD0,
0xAD4, 0xAD8, 0xADC, 0xAE0, 0xB88, 0xB8C, 0xBC4, 0xBC8, 0xBCC, 0xBD0,
0xBD4, 0xBD8, 0xBDC, 0xBE0, 0xBE4, 0xBE8, 0xBEC, 0xC00, 0xC5C, 0xCAC

## svcCreateSharedMemory

<div style="display: inline-block;">

| Argument | Type                                   | Name       |
| -------- | -------------------------------------- | ---------- |
| (In) W1  | u64                                    | Size       |
| (In) W2  | [\#Permission](#Permission "wikilink") | LocalPerm  |
| (In) W3  | [\#Permission](#Permission "wikilink") | RemotePerm |
| (Out) W0 | [\#Result](#Result "wikilink")         | Ret        |
| (Out) W1 | Handle<SharedMemory>                   | MemHandle  |

</div>

Other perm can be used to enforce permission 1, 3, or 0x10000000 if
don't care.

Allocates memory from the current process' pool partition.

## svcMapTransferMemory

<div style="display: inline-block;">

| Argument | Type                                   | Name        |
| -------- | -------------------------------------- | ----------- |
| (In) X0  | Handle<TransferMemory>                 | MemHandle   |
| (In) X1  | void\*                                 | Addr        |
| (In) X2  | u64                                    | Size        |
| (In) W3  | [\#Permission](#Permission "wikilink") | Permissions |
| (Out) W0 | [\#Result](#Result "wikilink")         | Ret         |

</div>

The newly mapped pages will have
[\#MemoryState](#MemoryState "wikilink") type 0xE.

You must pass same size and permissions as given in
svcCreateMemoryMirror, otherwise error.

## svcUnmapTransferMemory

<div style="display: inline-block;">

| Argument | Type                           | Name      |
| -------- | ------------------------------ | --------- |
| (In) X0  | Handle<TransferMemory>         | MemHandle |
| (In) X1  | void\*                         | Addr      |
| (In) X2  | u64                            | Size      |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret       |

</div>

Size must match size given in map syscall, otherwise there's an
invalid-size error.

## svcCreateInterruptEvent

<div style="display: inline-block;">

| Argument | Type                           | Name                |
| -------- | ------------------------------ | ------------------- |
| (In) X1  | u64                            | IrqNum              |
| (In) W2  | bool                           | Flags               |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret                 |
| (Out) W1 | Handle<ReadableEvent>          | ReadableEventHandle |

</div>

Create an event handle for the given IRQ number. Waiting on this handle
will wait until the IRQ is triggered. The flags argument configures the
triggering. If it is false, the IRQ is active HIGH level sensitive, if
it is true it is rising-edge sensitive.

### Result codes

**0x0:** Success.

**0xF001:** Flags was \> 1

**0xF201:** IRQ above 0x3FF or outside the [IRQ access
mask](NPDM#Kernel%20Access%20Control.md##Kernel_Access_Control "wikilink")
was given.

**0xCE01:** A SlabHeap was exhausted (too many interrupts created).

**0xF401:** IRQ already has an event registered.

**0xD201:** The handle table is full. Try closing some handles.

## svcQueryPhysicalAddress

<div style="display: inline-block;">

| Argument | Type                           | Name       |
| -------- | ------------------------------ | ---------- |
| (In) X1  | u64                            | Addr       |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret        |
| (Out) X1 | u64                            | PhysAddr   |
| (Out) X2 | u64                            | KernelAddr |
| (Out) X3 | u64                            | Size       |

</div>

## svcQueryIoMapping

<div style="display: inline-block;">

| Argument | Type                           | Name     |
| -------- | ------------------------------ | -------- |
| (In) X1  | u64                            | PhysAddr |
| (In) X2  | u64                            | Size     |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret      |
| (Out) X1 | void\*                         | VirtAddr |

</div>

**Description:** Returns a virtual address mapped to a given IO range.

## svcCreateDeviceAddressSpace

<div style="display: inline-block;">

| Argument | Type                           | Name               |
| -------- | ------------------------------ | ------------------ |
| (In) X1  | u64                            | StartAddr          |
| (In) X2  | u64                            | EndAddr            |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret                |
| (Out) W1 | Handle<DeviceAddressSpace>     | AddressSpaceHandle |

</div>

**Description:** Creates a virtual address space for binding device
address spaces and returns a handle.

dev\_as\_start\_addr is normally set to 0 and dev\_as\_end\_addr is
normally set to 0xFFFFFFFF.

## svcAttachDeviceAddressSpace

<div style="display: inline-block;">

| Argument | Type                                   | Name           |
| -------- | -------------------------------------- | -------------- |
| (In) W0  | [\#DeviceName](#DeviceName "wikilink") | DeviceId       |
| (In) X1  | Handle<DeviceAddressSpace>             | DeviceAsHandle |
| (Out) W0 | [\#Result](#Result "wikilink")         | Ret            |

</div>

**Description:** Attaches a device address space to a
[device](#DeviceName "wikilink").

## svcDetachDeviceAddressSpace

<div style="display: inline-block;">

| Argument | Type                                   | Name           |
| -------- | -------------------------------------- | -------------- |
| (In) W0  | [\#DeviceName](#DeviceName "wikilink") | DeviceId       |
| (In) X1  | Handle<DeviceAddressSpace>             | DeviceAsHandle |
| (Out) W0 | [\#Result](#Result "wikilink")         | Ret            |

</div>

**Description:** Detaches a device address space from a
[device](#DeviceName "wikilink").

## svcMapDeviceAddressSpaceByForce

<div style="display: inline-block;">

| Argument | Type                                   | Name           |
| -------- | -------------------------------------- | -------------- |
| (In) W0  | Handle<DeviceAddressSpace>             | DeviceAsHandle |
| (In) W1  | Handle<Process>                        | ProcessHandle  |
| (In) X2  | void\*                                 | SrcAddr        |
| (In) X3  | u64                                    | DeviceAsSize   |
| (In) X4  | u64                                    | DeviceAsAddr   |
| (In) W5  | [\#Permission](#Permission "wikilink") | Permissions    |
| (Out) W0 | [\#Result](#Result "wikilink")         | Ret            |

</div>

**Description:** Maps an attached device address space to an userspace
address.

dev\_map\_addr is the userspace destination address, while dev\_as\_addr
is the source address between dev\_as\_start\_addr and
dev\_as\_end\_addr (passed to
[\#svcCreateDeviceAddressSpace](#svcCreateDeviceAddressSpace "wikilink")).

The userspace destination address must have the
[MapDeviceAllowed](SVC#MemoryState.md##MemoryState "wikilink") bit set.
Bit [IsDeviceMapped](SVC#MemoryAttribute.md##MemoryAttribute "wikilink")
will be set after mapping.

## svcMapDeviceAddressSpaceAligned

<div style="display: inline-block;">

| Argument | Type                                   | Name           |
| -------- | -------------------------------------- | -------------- |
| (In) W0  | Handle<DeviceAddressSpace>             | DeviceAsHandle |
| (In) W1  | Handle<Process>                        | ProcessHandle  |
| (In) X2  | void\*                                 | SrcAddr        |
| (In) X3  | u64                                    | DeviceAsSize   |
| (In) X4  | u64                                    | DeviceAsAddr   |
| (In) W5  | [\#Permission](#Permission "wikilink") | Permissions    |
| (Out) W0 | [\#Result](#Result "wikilink")         | Ret            |

</div>

**Description:** Maps an attached device address space to an userspace
address.

Same as
[\#svcMapDeviceAddressSpaceByForce](#svcMapDeviceAddressSpaceByForce "wikilink"),
but the userspace destination address must have the
[MapDeviceAlignedAllowed](SVC#MemoryState.md##MemoryState "wikilink")
bit set instead.

## svcUnmapDeviceAddressSpace

<div style="display: inline-block;">

| Argument | Type                           | Name           |
| -------- | ------------------------------ | -------------- |
| (In) W0  | Handle<DeviceAddressSpace>     | DeviceAsHandle |
| (In) W1  | Handle<Process>                | ProcessHandle  |
| (In) X2  | void\*                         | SrcAddr        |
| (In) X3  | u64                            | DeviceAsSize   |
| (In) X4  | u64                            | DeviceAsAddr   |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret            |

</div>

**Description:** Unmaps an attached device address space from an
userspace address.

## svcContinueDebugEvent

### Result codes

**0x0:** Success. The process has been resumed.

**0xe401:** Invalid debug handle.

**0xf401:** Process has debug events queued or is already running.

## svcGetSystemInfo

<div style="display: inline-block;">

| Argument | Type                           | Name      |
| -------- | ------------------------------ | --------- |
| (In) X1  | u64                            | InfoId    |
| (In) W2  | Handle                         | Handle    |
| (In) X3  | u64                            | InfoSubId |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret       |
| (Out) X1 | u64                            | Out       |

</div>

| Handle type | Id0 | Id1 | Description                     |
| ----------- | --- | --- | ------------------------------- |
| Zero        | 0   | 0   | TotalMemorySize\_Application    |
| Zero        | 0   | 1   | TotalMemorySize\_Applet         |
| Zero        | 0   | 2   | TotalMemorySize\_System         |
| Zero        | 0   | 3   | TotalMemorySize\_SystemUnsafe   |
| Zero        | 1   | 0   | CurrentMemorySize\_Application  |
| Zero        | 1   | 1   | CurrentMemorySize\_Applet       |
| Zero        | 1   | 2   | CurrentMemorySize\_System       |
| Zero        | 1   | 3   | CurrentMemorySize\_SystemUnsafe |
| Zero        | 2   | 0   | PrivilegedProcessId\_LowerBound |
| Zero        | 2   | 1   | PrivilegedProcessId\_UpperBound |
|             |     |     |                                 |

## svcSetProcessMemoryPermission

<div style="display: inline-block;">

| Argument | Type                           | Name          |
| -------- | ------------------------------ | ------------- |
| (In) W0  | Handle<Process>                | ProcessHandle |
| (In) X1  | u64                            | Addr          |
| (In) X2  | u64                            | Size          |
| (In) W3  | void\*                         | Perm          |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret           |

</div>

This sets the memory permissions for the specified memory with the
supplied process handle.

This throws an error(0xD801) when the input perm is \>0x5, hence -WX and
RWX are not allowed.

## svcMapProcessMemory

<div style="display: inline-block;">

| Argument | Type                           | Name          |
| -------- | ------------------------------ | ------------- |
| (In) X0  | u64                            | DstAddr       |
| (In) W1  | Handle<Process>                | ProcessHandle |
| (In) X2  | void\*                         | SrcAddr       |
| (In) X3  | u64                            | Size          |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret           |

</div>

Maps the src address from the supplied process handle into the current
process.

This allows mapping code and rodata with RW- permission.

## svcUnmapProcessMemory

<div style="display: inline-block;">

| Argument | Type                           | Name          |
| -------- | ------------------------------ | ------------- |
| (In) X0  | void\*                         | DstAddr       |
| (In) W1  | Handle<Process>                | ProcessHandle |
| (In) X2  | u64                            | SrcAddr       |
| (In) X3  | u64                            | Size          |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret           |

</div>

Unmaps what was mapped by
[\#svcMapProcessMemory](#svcMapProcessMemory "wikilink").

## svcQueryProcessMemory

<div style="display: inline-block;">

| Argument | Type                                     | Name          |
| -------- | ---------------------------------------- | ------------- |
| (In) X0  | [\#MemoryInfo](#MemoryInfo "wikilink")\* | MemInfoPtr    |
| (In) W2  | Handle<Process>                          | ProcessHandle |
| (In) X3  | u64                                      | Addr          |
| (Out) W0 | [\#Result](#Result "wikilink")           | Ret           |
| (Out) W1 | PageInfo                                 | PageInfo      |

</div>

Equivalent to [\#svcQueryMemory](#svcQueryMemory "wikilink") except
takes a process handle.

## svcMapProcessCodeMemory

<div style="display: inline-block;">

| Argument | Type                           | Name          |
| -------- | ------------------------------ | ------------- |
| (In) W0  | Handle<Process>                | ProcessHandle |
| (In) X1  | u64                            | DstAddr       |
| (In) X2  | u64                            | SrcAddr       |
| (In) X3  | u64                            | Size          |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret           |

</div>

Takes a process handle, and maps normal heap in that process as
executable code in that process. Used when loading NROs. This does not
support using the current-process handle alias.

## svcUnmapProcessCodeMemory

<div style="display: inline-block;">

| Argument | Type                           | Name          |
| -------- | ------------------------------ | ------------- |
| (In) W0  | Handle<Process>                | ProcessHandle |
| (In) X1  | u64                            | DstAddr       |
| (In) X2  | u64                            | SrcAddr       |
| (In) X3  | u64                            | Size          |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret           |

</div>

Unmaps what was mapped by
[\#svcMapProcessCodeMemory](#svcMapProcessCodeMemory "wikilink").

## svcCreateProcess

<div style="display: inline-block;">

| Argument | Type                                                   | Name            |
| -------- | ------------------------------------------------------ | --------------- |
| (In) X1  | [\#CreateProcessInfo](#CreateProcessInfo "wikilink")\* | InfoPtr         |
| (In) X2  | u32\*                                                  | CapabilitiesPtr |
| (In) X3  | u64                                                    | CapabilitiesNum |
| (Out) W0 | [\#Result](#Result "wikilink")                         | Ret             |
| (Out) W1 | Handle<Process>                                        | ProcessHandle   |

</div>

Takes a [\#CreateProcessInfo](#CreateProcessInfo "wikilink") as input.
CapabilitiesPtr points to an array of [kernel
capabilities](NPDM#Kernel%20Access%20Control.md##Kernel_Access_Control "wikilink").
CapabilitiesNum is a number of capabilities in the CapabilitiesPtr array
(number of element, not number of bytes).

### Result codes

**0x0:** Success.

**0xCA01:** Attempted to map more code pages than available in address
space.

**0xCC01:** Provided CodeAddr is invalid (make sure it's in range?)

**0xE401:** The resource handle passed is invalid.

**0xE601:** Attempt to copy procinfo from user-supplied pointer failed.
Attempt to copy capabilities\_num from user-supplied pointer failed.

**0xE801:** Attempted to create a 32-bit process with a 36-bit address
space.

**0xF001:** Unused bits are set in mmuflags. Unknown address space type
used.

## svcGetProcessInfo

<div style="display: inline-block;">

| Argument | Type                                       | Name          |
| -------- | ------------------------------------------ | ------------- |
| (In) W0  | Handle<Process>                            | ProcessHandle |
| (Out) W0 | [\#Result](#Result "wikilink")             | Ret           |
| (Out) W1 | [\#ProcessState](#ProcessState "wikilink") | State         |

</div>

Returns an enum with value 0-7.

## svcCallSecureMonitor

<div style="display: inline-block;">

| Argument    | Type                                           | Name                                          |
| ----------- | ---------------------------------------------- | --------------------------------------------- |
| (In) X0     | u64                                            | [Function ID](SMC#ID%200.md##ID_0 "wikilink") |
| (In) X1-X7  | u64                                            | SMC sub-arguments                             |
| (Out) X0    | [SMC Result](SMC#Errors.md##Errors "wikilink") | Result of SMC                                 |
| (Out) X1-X7 | u64                                            | SMC sub-output                                |

</div>

Takes in a SMC function ID in X0, and arguments for that SMC function in
X1-X7.

Passing an invalid SMC function ID or calling from a core other than
core 3 will result in a secure monitor panic.

The kernel parses bits 9-15 in the passed SMC function ID (per the ARM
SMC calling convention), and when set uses as an indicator to translate
a pointer in the associated register (X1-X7) to a physical address. The
kernel will translate any address mapped as R-W, other addresses (R--,
R-X, or invalid pointers) will be translated as 0/NULL.

Output is returned raw from the Secure Monitor; X0 will be the
untranslated SMC result and X1-X7 will contain other SMC output (or be
unchanged, depending on the SMC).

## Debugging

\[2.0.0+\] Exactly 6 debug SVCs require that
[IsDebugMode](SPL%20services#GetConfig.md##GetConfig "wikilink") is
non-zero. Error 0x4201 is returned otherwise.

  - svcBreakDebugProcess
  - svcContinueDebugEvent
  - svcWriteDebugProcessMemory
  - svcSetDebugThreadContext
  - svcTerminateDebugProcess
  - svcSetHardwareBreakPoint

svcDebugActiveProcess stops execution of the target process, the normal
method for resuming it requires svcContinueDebugEvent(see above).
Closing the debug handle also results in execution being resumed.

## svcSetHardwareBreakPoint

<div style="display: inline-block;">

| Argument | Type                           | Name                     |
| -------- | ------------------------------ | ------------------------ |
| (In) W0  | u32                            | hardware\_breakpoint\_id |
| (In) W1  | u64                            | flags                    |
| (In) W2  | u64                            | value                    |
| (Out) W0 | [\#Result](#Result "wikilink") | Ret                      |

</div>

Sets one of the AArch64 hardware breakpoints. The nintendo switch has 6
hardware breakpoints, and 4 hardware watchpoints. The syscall has two
behaviors depending on the value of hardware\_breakpoint\_id:

If hardware\_breakpoint\_id \< 0x10, then it sets one of the AArch64
hardware breakpoints. Flags will go to DBGBCRn\_EL1, and value to
DBGBVRn\_EL1. The only flags the user is allowed to set are those in the
bitmask 0x7F01E1. Furthermore, the kernel will or it with 0x4004, in
order to set various security flags to guarantee the watchpoints only
triggers for code in EL0. If the user asks for a Breakpoint Type of
ContextIDR match, the kernel shall use the given debug\_handle to set
DBGBVRn\_EL1 to the ContextID of the debugged process.

If hardware\_breakpoint\_id is between 0x10 and 0x20 (exclusive), then
it sets one of the AArch64 hardware watchpoints. Flags will go to
DBGWCRn\_EL1, and the value to DBGWVRn\_EL1. The only flags the user is
allowed to set are those in the bitmask 0xFF0F1FF9. Furthermore, the
kernel will or it with 0x104004. This will set various security flags,
and set the watchpoint type to be a Linked Watchpoint. This means that
you need to link it to a Linked ContextIDR breakpoint. Check the ARM
documentation for more information.

Note that hardware\_breakpoint\_id 0 to 4 match only to Virtual Address,
while hardware\_breakpoint\_id 5 and 6 match against either Virtual
Address, ContextID, or VMID. As such, if you are configuring a
breakpoint to link for a watchpoint, make sure you use
hardware\_breakpoint\_id 5 or 6.

For more documentation for hardware breakpoints, check out the AArch64
documentation for the [DBGBCRn\_EL1
register](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.ddi0488h/way1382455558968.html)
and the [DBGWCRn\_EL1
register](http://infocenter.arm.com/help/topic/com.arm.doc.ddi0488h/way1382455560629.html)

# Enum/Structures

## ThreadContextFlags

Bitfield of one of more of these:

| Bit | Bitmask | Name                             | Description                                                                                           |
| --- | ------- | -------------------------------- | ----------------------------------------------------------------------------------------------------- |
| 0   | 1       | General-purpose registers        | If in 64-bit mode, GPRs 0–28 will be read/written. If in 32-bit mode, GPRs 0–12 will be read/written. |
| 1   | 2       | Control registers                | Reads/writes the FP, LR, PC, SP, PSTATE, and TPIDR registers.                                         |
| 2   | 4       | Floating-point registers         | Reads/writes the floating-point vector registers.                                                     |
| 3   | 8       | Floating-point control registers | Reads/writes the FPCR and FPSR registers.                                                             |

## DeviceName

| Value | Name                   |
| ----- | ---------------------- |
| 0     | DeviceName\_AFI        |
| 1     | DeviceName\_AVPC       |
| 2     | DeviceName\_DC         |
| 3     | DeviceName\_DCB        |
| 4     | DeviceName\_HC         |
| 5     | DeviceName\_HDA        |
| 6     | DeviceName\_ISP2       |
| 7     | DeviceName\_MSENCNVENC |
| 8     | DeviceName\_NV         |
| 9     | DeviceName\_NV2        |
| 10    | DeviceName\_PPCS       |
| 11    | DeviceName\_SATA       |
| 12    | DeviceName\_VI         |
| 13    | DeviceName\_VIC        |
| 14    | DeviceName\_XUSB\_HOST |
| 15    | DeviceName\_XUSB\_DEV  |
| 16    | DeviceName\_TSEC       |
| 17    | DeviceName\_PPCS1      |
| 18    | DeviceName\_DC1        |
| 19    | DeviceName\_SDMMC1A    |
| 20    | DeviceName\_SDMMC2A    |
| 21    | DeviceName\_SDMMC3A    |
| 22    | DeviceName\_SDMMC4A    |
| 23    | DeviceName\_ISP2B      |
| 24    | DeviceName\_GPU        |
| 25    | DeviceName\_GPUB       |
| 26    | DeviceName\_PPCS2      |
| 27    | DeviceName\_NVDEC      |
| 28    | DeviceName\_APE        |
| 29    | DeviceName\_SE         |
| 30    | DeviceName\_NVJPG      |
| 31    | DeviceName\_HC1        |
| 32    | DeviceName\_SE1        |
| 33    | DeviceName\_AXIAP      |
| 34    | DeviceName\_ETR        |
| 35    | DeviceName\_TSECB      |
| 36    | DeviceName\_TSEC1      |
| 37    | DeviceName\_TSECB1     |
| 38    | DeviceName\_NVDEC1     |

## CodeMemoryOperation

| Value | Name                            |
| ----- | ------------------------------- |
| 0     | CodeMemoryOperation\_MapOwner   |
| 1     | CodeMemoryOperation\_MapSlave   |
| 2     | CodeMemoryOperation\_UnmapOwner |
| 3     | CodeMemoryOperation\_UnmapSlave |

## LimitableResource

| Value | Name                                | Note                                                                                                        |
| ----- | ----------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| 0     | LimitableResource\_Memory           | Bytes of memory a process may allocate.                                                                     |
| 1     | LimitableResource\_Threads          | Amount of threads a process can create.                                                                     |
| 2     | LimitableResource\_Events           | Amount of events a process can create through svcCreateEvent or svcSendAsyncRequestWithUserBuffer.          |
| 3     | LimitableResource\_TransferMemories | Amount of TransferMemory a process can create through svcCreateTransferMemory.                              |
| 4     | LimitableResource\_Sessions         | Amount of session a process can create through svcCreateSession, svcConnectToPort or svcConnectToNamedPort. |

## ProcessInfoType

| Value | Name                                                      |
| ----- | --------------------------------------------------------- |
| 0     | [ProcessInfoType\_ProcessState](#ProcessState "wikilink") |
|       |                                                           |

## ProcessState

| Value | Name                          | Notes                                                                                                           |
| ----- | ----------------------------- | --------------------------------------------------------------------------------------------------------------- |
| 0     | ProcessState\_Created         |                                                                                                                 |
| 1     | ProcessState\_CreatedAttached |                                                                                                                 |
| 2     | ProcessState\_Started         |                                                                                                                 |
| 3     | ProcessState\_Crashed         | Processes will not enter this state unless they were created with [EnableDebug](#CreateProcessInfo "wikilink"). |
| 4     | ProcessState\_StartedAttached |                                                                                                                 |
| 5     | ProcessState\_Exiting         |                                                                                                                 |
| 6     | ProcessState\_Exited          |                                                                                                                 |
| 7     | ProcessState\_DebugSuspended  |                                                                                                                 |

## DebugThreadParam

| Value | Name                               |
| ----- | ---------------------------------- |
| 0     | DebugThreadParam\_DynamicPriority  |
| 1     | DebugThreadParam\_SchedulingStatus |
| 2     | DebugThreadParam\_PreferredCpuCore |
| 3     | DebugThreadParam\_CurrentCpuCore   |
| 4     | DebugThreadParam\_AffinityMask     |

Dynamic priority: output in out2

Scheduling status: out1 contains bit0: is debug-suspended, bit1: is
user-suspended (svcSetThreadActivity 1 or svcSetProcessActivity 1). Out2
contains {suspended, idle, running, terminating} =\> {5, 0, 1, 4}

DebugThreadParam\_PreferredCpuCore: output in out2

DebugThreadParam\_CurrentCpuCore: output in out2

DebugThreadParam\_AffinityMask: output in out1

## CreateProcessInfo

| Offset | Length | Bits    | Description                                                                           |
| ------ | ------ | ------- | ------------------------------------------------------------------------------------- |
| 0      | 12     |         | ProcessName (doesn't have to be null-terminated)                                      |
| 0x0C   | 4      |         | ProcessCategory (0: regular title, 1: kernel built-in)                                |
| 0x10   | 8      |         | TitleId                                                                               |
| 0x18   | 8      |         | CodeAddr                                                                              |
| 0x20   | 4      |         | CodeNumPages                                                                          |
| 0x24   | 4      |         | Flags                                                                                 |
|        |        | Bit0    | IsAarch64                                                                             |
|        |        | Bit3-1  | [\#AddressSpaceType](#AddressSpaceType "wikilink")                                    |
|        |        | Bit4    | \[2.0.0+\] EnableDebug                                                                |
|        |        | Bit5    | EnableAslr                                                                            |
|        |        | Bit6    | IsApplication                                                                         |
|        |        | Bit7    | \[4.0.0\] UseSecureMemory                                                             |
|        |        | Bit10-7 | \[5.0.0+\] PoolPartition (0=Application, 1=Applet, 2=Sysmodule, 3=Nvservices)         |
|        |        | Bit11   | \[7.0.0+\] OptimizeMemoryAllocation (Only allowed in combination with IsApplication). |
| 0x28   | 4      |         | ResourceLimitHandle or zero                                                           |
| 0x2C   | 4      |         | \[3.0.0+\] SystemResourceNumPages                                                     |

On \[1.0.0\] there's only one pool.

On \[2.0.0-4.0.0\] PoolPartition is 1 for built-ins and 0 for rest.

On \[5.0.0\] PoolPartition is specified in CreateProcessArgs. There are
now 4 pool partitions.

On \[5.0.0\] (maybe lower?) a zero ResourceLimitHandle defaults to
sysmodule limits and 0x12300000 bytes of memory.

The PersonalMmHeap are allocated as follows:

  - For the application, normal insecure pool is used. Carveout 5 is
    used to provide protection.
  - For the applet, a pre-allocated secure pool segment of size 0x400000
    is used.
  - For sysmodules, secure pool is allocated.

### AddressSpaceType

| Type | Name                     | Width | Description                            |
| ---- | ------------------------ | ----- | -------------------------------------- |
| 0    | Normal\_32Bit            | 32    |                                        |
| 1    | Normal\_36Bit            | 36    |                                        |
| 2    | WithoutMap\_32Bit        | 32    | Appears to be missing map region \[?\] |
| 3    | \[2.0.0+\] Normal\_39Bit | 39    |                                        |

## MemoryInfo

| Offset | Length | Description                                                          |
| ------ | ------ | -------------------------------------------------------------------- |
| 0      | 8      | BaseAddress                                                          |
| 8      | 8      | Size                                                                 |
| 0x10   | 4      | MemoryType: lower 8 bits of [\#MemoryState](#MemoryState "wikilink") |
| 0x14   | 4      | [\#MemoryAttribute](#MemoryAttribute "wikilink")                     |
| 0x18   | 4      | Permission (bit0: R, bit1: W, bit2: X)                               |
| 0x1C   | 4      | IpcRefCount                                                          |
| 0x20   | 4      | DeviceRefCount                                                       |
| 0x24   | 4      | Padding: always zero                                                 |

## MemoryAttribute

| Bits | Description                               |
| ---- | ----------------------------------------- |
| 0    | IsBorrowed                                |
| 1    | IsIpcLocked (when IpcRefCount \> 0)       |
| 2    | IsDeviceShared (when DeviceRefCount \> 0) |
| 3    | IsUncached                                |

## MemoryState

| Bits | Description                                                                                                                                                                |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 7-0  | Type                                                                                                                                                                       |
| 8    | [PermissionChangeAllowed](#svcSetMemoryPermission "wikilink")                                                                                                              |
| 9    | ForceReadWritableByDebugSyscalls                                                                                                                                           |
| 10   | IpcSendAllowed                                                                                                                                                             |
| 11   | NonDeviceIpcSendAllowed                                                                                                                                                    |
| 12   | NonSecureIpcSendAllowed                                                                                                                                                    |
| 14   | [ProcessPermissionChangeAllowed](#svcSetProcessMemoryPermission "wikilink")                                                                                                |
| 15   | [MapAllowed](#svcMapMemory "wikilink")                                                                                                                                     |
| 16   | [UnmapProcessCodeMemoryAllowed](#svcUnmapProcessCodeMemory "wikilink")                                                                                                     |
| 17   | [TransferMemoryAllowed](#svcCreateTransferMemory "wikilink")                                                                                                               |
| 18   | [QueryPhysicalAddressAllowed](#svcQueryPhysicalAddress "wikilink")                                                                                                         |
| 19   | MapDeviceAllowed ([\#svcMapDeviceAddressSpace](#svcMapDeviceAddressSpace "wikilink") and [\#svcMapDeviceAddressSpaceByForce](#svcMapDeviceAddressSpaceByForce "wikilink")) |
| 20   | [MapDeviceAlignedAllowed](#svcMapDeviceAddressSpaceAligned "wikilink")                                                                                                     |
| 21   | [IpcBufferAllowed](#svcSendSyncRequestWithUserBuffer "wikilink")                                                                                                           |
| 22   | IsPoolAllocated/IsReferenceCounted                                                                                                                                         |
| 23   | [MapProcessAllowed](#svcMapProcessMemory "wikilink")                                                                                                                       |
| 24   | [AttributeChangeAllowed](#svcSetMemoryAttribute "wikilink")                                                                                                                |
| 25   | \[4.0.0+\] CodeMemoryAllowed                                                                                                                                               |

<table>
<thead>
<tr class="header">
<th><p>Value</p></th>
<th><p>Type</p></th>
<th><p>Meaning</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x00000000</p></td>
<td><p>MemoryType_Unmapped</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0x00002001</p></td>
<td><p>MemoryType_Io</p></td>
<td><p>Mapped by kernel capability parsing in <a href="#svcCreateProcess" title="wikilink">#svcCreateProcess</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x00042002</p></td>
<td><p>MemoryType_Normal</p></td>
<td><p>Mapped by kernel capability parsing in <a href="#svcCreateProcess" title="wikilink">#svcCreateProcess</a>.</p></td>
</tr>
<tr class="even">
<td><p>0x00DC7E03</p></td>
<td><p>MemoryType_CodeStatic</p></td>
<td><p>Mapped during <a href="#svcCreateProcess" title="wikilink">#svcCreateProcess</a>.</p></td>
</tr>
<tr class="odd">
<td><p>[1.0.0+]</p>
<p>0x01FEBD04</p>
<p>[4.0.0+]</p>
<p>0x03FEBD04</p></td>
<td><p>MemoryType_CodeMutable</p></td>
<td><p>Transition from 0xDC7E03 performed by <a href="#svcSetProcessMemoryPermission" title="wikilink">#svcSetProcessMemoryPermission</a>.</p></td>
</tr>
<tr class="even">
<td><p>[1.0.0+] 0x017EBD05</p>
<p>[4.0.0+]</p>
<p>0x037EBD05</p></td>
<td><p>MemoryType_Heap</p></td>
<td><p>Mapped using <a href="#svcSetHeapSize" title="wikilink">#svcSetHeapSize</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x00402006</p></td>
<td><p>MemoryType_SharedMemory</p></td>
<td><p>Mapped using <a href="#svcMapSharedMemory" title="wikilink">#svcMapSharedMemory</a>.</p></td>
</tr>
<tr class="even">
<td><p>0x00482907</p></td>
<td><p>[1.0.0] MemoryType_Alias</p></td>
<td><p>Mapped using <a href="#svcMapMemory" title="wikilink">#svcMapMemory</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x00DD7E08</p></td>
<td><p>MemoryType_ModuleCodeStatic</p></td>
<td><p>Mapped using <a href="#svcMapProcessCodeMemory" title="wikilink">#svcMapProcessCodeMemory</a>.</p></td>
</tr>
<tr class="even">
<td><p>[1.0.0+]</p>
<p>0x01FFBD09</p>
<p>[4.0.0+]</p>
<p>0x03FFBD09</p></td>
<td><p>MemoryType_ModuleCodeMutable</p></td>
<td><p>Transition from 0xDD7E08 performed by <a href="#svcSetProcessMemoryPermission" title="wikilink">#svcSetProcessMemoryPermission</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x005C3C0A</p></td>
<td><p><a href="IPC Marshalling.md" title="wikilink">MemoryType_Ipc</a></p></td>
<td><p>IPC buffers with descriptor flags=0.</p></td>
</tr>
<tr class="even">
<td><p>0x005C3C0B</p></td>
<td><p>MemoryType_Stack</p></td>
<td><p>Mapped using <a href="#svcMapMemory" title="wikilink">#svcMapMemory</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x0040200C</p></td>
<td><p><a href="Thread Local Storage.md" title="wikilink">MemoryType_ThreadLocal</a></p></td>
<td><p>Mapped during <a href="#svcCreateThread" title="wikilink">#svcCreateThread</a>.</p></td>
</tr>
<tr class="even">
<td><p>0x015C3C0D</p></td>
<td><p>MemoryType_TransferMemoryIsolated</p></td>
<td><p>Mapped using <a href="#svcMapTransferMemory" title="wikilink">#svcMapTransferMemory</a> when the owning process has perm=0.</p></td>
</tr>
<tr class="odd">
<td><p>0x005C380E</p></td>
<td><p>MemoryType_TransferMemory</p></td>
<td><p>Mapped using <a href="#svcMapTransferMemory" title="wikilink">#svcMapTransferMemory</a> when the owning process has perm!=0.</p></td>
</tr>
<tr class="even">
<td><p>0x0040380F</p></td>
<td><p>MemoryType_ProcessMemory</p></td>
<td><p>Mapped using <a href="#svcMapProcessMemory" title="wikilink">#svcMapProcessMemory</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x00000010</p></td>
<td><p>MemoryType_Reserved</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0x005C3811</p></td>
<td><p><a href="IPC Marshalling.md" title="wikilink">MemoryType_NonSecureIpc</a></p></td>
<td><p>IPC buffers with descriptor flags=1.</p></td>
</tr>
<tr class="odd">
<td><p>0x004C2812</p></td>
<td><p><a href="IPC Marshalling.md" title="wikilink">MemoryType_NonDeviceIpc</a></p></td>
<td><p>IPC buffers with descriptor flags=3.</p></td>
</tr>
<tr class="even">
<td><p>0x00002013</p></td>
<td><p>MemoryType_KernelStack</p></td>
<td><p>Mapped in kernel during <a href="#svcCreateThread" title="wikilink">#svcCreateThread</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x00402214</p></td>
<td><p>[4.0.0+] MemoryType_CodeReadOnly</p></td>
<td><p>Mapped in kernel during <a href="#svcControlCodeMemory" title="wikilink">#svcControlCodeMemory</a>.</p></td>
</tr>
<tr class="even">
<td><p>0x00402015</p></td>
<td><p>[4.0.0+] MemoryType_CodeWritable</p></td>
<td><p>Mapped in kernel during <a href="#svcControlCodeMemory" title="wikilink">#svcControlCodeMemory</a>.</p></td>
</tr>
</tbody>
</table>

## ArbitrationType

| Value | Type                       |
| ----- | -------------------------- |
| 0x0   | WaitIfLessThan             |
| 0x1   | DecrementAndWaitIfLessThan |
| 0x2   | WaitIfEqual                |
|       |                            |

## SignalType

| Value | Type                                            |
| ----- | ----------------------------------------------- |
| 0x0   | Signal                                          |
| 0x1   | SignalAndIncrementIfEqual                       |
| 0x2   | SignalAndModifyBasedOnWaitingThreadCountIfEqual |
|       |                                                 |

## ContinueDebugFlagsOld

\[1.0.0-2.3.0\]

| Bit | Bitmask | Description                                                                  |
| --- | ------- | ---------------------------------------------------------------------------- |
| 0   | 1       | IgnoreException (note: ResumeAllThreads or debug-suspended-thread-id needed) |
| 1   | 2       | SwallowException                                                             |
| 2   | 4       | ResumeAllThreads                                                             |

## ContinueDebugFlags

\[3.0.0+\]

| Bit | Bitmask | Description                                                                 |
| --- | ------- | --------------------------------------------------------------------------- |
| 0   | 1       | IgnoreException (note: doesn't need to be set in the same call than Resume) |
| 1   | 2       | DontCatchExceptions                                                         |
| 2   | 4       | Resume                                                                      |
| 3   | 8       | IgnoreOtherThreadsExceptions                                                |

IgnoreExceptionsOfOthers is like IgnoreException but acts on all threads
that aren't in the input list. The affected threads are resumed.

Only one of of Resume and IgnoreOtherThreadsExceptions can be set at a
time.

If the input number of threads is 0, this means "all threads".

## DebugEventInfo

The below table is for the Aarch64 version of the system call. For A32,
all u64 fields but title/process/thread id are actually u32, making the
structure 0x28-byte-big (0x40 for a64).

Size: 0x40

| Offset | Length | Description                 |
| ------ | ------ | --------------------------- |
| 0      | u32    | EventType                   |
| 4      | u32    | Flags (bit0: NeedsContinue) |
| 8      | u64    | ThreadId                    |
| 0x10   |        | PerTypeSpecifics            |

AttachProcess specific:

| Offset | Length     | Description                         |
| ------ | ---------- | ----------------------------------- |
| 0x10   | u64        | TitleId                             |
| 0x18   | u64        | ProcessId                           |
| 0x20   | char\[12\] | ProcessName                         |
| 0x2C   | u32        | MmuFlags                            |
| 0x30   | u64        | \[5.0.0+\] UserExceptionContextAddr |

AttachThread specific:

| Offset | Length | Description |
| ------ | ------ | ----------- |
| 0x10   | u64    | ThreadId    |
| 0x18   | u64    | TlsPtr      |
| 0x20   | u64    | Entrypoint  |

Exit specific:

| Offset | Length | Description                                                                  |
| ------ | ------ | ---------------------------------------------------------------------------- |
| 0x10   | u32    | Type (0=PausedThread, 1=RunningThread, 2=ExitedProcess, 3=TerminatedProcess) |

Exception specific:

| Offset | Length | Description           |
| ------ | ------ | --------------------- |
| 0x10   | u32    | ExceptionType         |
| 0x18   | u64    | FaultRegister         |
| 0x20   |        | PerExceptionSpecifics |

### DebugEventType

| Value | Name                      |
| ----- | ------------------------- |
| 0     | DebugEvent\_AttachProcess |
| 1     | DebugEvent\_AttachThread  |
| 2     | DebugEvent\_ExitProcess   |
| 3     | DebugEvent\_ExitThread    |
| 4     | DebugEvent\_Exception     |

### DebugExceptionType

| Value | Name                               |
| ----- | ---------------------------------- |
| 0     | Exception\_Trap (\*)               |
| 1     | Exception\_InstructionAbort        |
| 2     | Exception\_DataAbortMisc (\*\*)    |
| 3     | Exception\_PcSpAlignmentFault      |
| 4     | Exception\_DebuggerAttached        |
| 5     | Exception\_BreakPoint              |
| 6     | Exception\_UserBreak               |
| 7     | Exception\_DebuggerBreak           |
| 8     | Exception\_BadSvcId                |
| 9     | Exception\_SError \[not in 1.0.0\] |

\* Undefined instructions, software breakpoints, some other traps.

\*\* Data aborts, FP traps, and everything else that doesn't belong to
any of the above.

Trap specifics:

| Offset | Length | Description |
| ------ | ------ | ----------- |
| 0x20   | u32    | Opcode      |

BreakPoint specifics:

| Offset | Length | Description  |
| ------ | ------ | ------------ |
| 0x20   | u32    | IsWatchpoint |

UserBreak specifics:

| Offset | Length | Description |
| ------ | ------ | ----------- |
| 0x20   | u32    | Info0       |
| 0x28   | u64    | Info1       |
| 0x30   | u64    | Info2       |

BadSvcId specifics:

| Offset | Length | Description |
| ------ | ------ | ----------- |
| 0x20   | u32    | SvcId       |

# Exception handling

First of all, a function that might be called by synchronous exception
handler and that is called by the SError handler fetches the exception
info, adjusts PC, panics on exceptions taken from EL1, then dispatches
the exception.

The dispatcher has two mutually exclusive exception reporting methods:

  - by storing information at the start of the process's TLS memregion
    (TPIDRRO\_EL0) and jumping back to the crt0
  - by using KDebug

KDebug dispatching is used when at least one of the following conditions
are met:

  - SMC ConfigItem KernelMemConfig bit 1 is NOT set (it isn't on
    retail), unless: this is a software or hardware breakpoint, or a
    watchpoint, or \[4.0.0+?\] the process is attached and this is a
    Google PNaCl trap instruction (see LLVM source)
  - FAR doesn't point to a valid address in mapped-readable CodeStatic
    memory (i.e. this is the case for NRO and JIT memory) or this is one
    of the following exceptions (it particular, that doesn't include FP
    exceptions occurring in CodeStatic memory):
      - Uncategorized
      - IllegalState
      - SupervisorCallA32
      - SupervisorCallA64
      - PCAlignment
      - SPAlignment
      - SError
      - BreakpointLowerEl
      - SoftwareStepLowerEl (note: no way set single-step flag; not
        parsed)
      - WatchpointLowerEl
      - SoftwareBreakpointA32 (note: not parsed)
      - SoftwareBreakpointA64 (note: not parsed)

In all other cases the userland-handled exception path is taken.

KDebug path:

If the process is attached, the exception is reported to the KDebug. If
the thread was continued using flag IgnoreExceptions, it returns from
the exception as if nothing happened.

If the latter is not the case, or if the process isn't attached, proceed
to \[2.0.0+\] crash reporting (or in \[1.0.0\] just terminate the
process): if EnableDebug is set, and depending on the process state
(more than one crash per process isn't permitted) it may signal itself
with ProcessState\_Crashed so that PM asks NS to start creport so that
creport attaches to it and reports the crashes. Otherwise, just
terminate.

Userland reporting path and svcReturnFromException:

TLS region start (A64):

| Offset | Length | Description       |
| ------ | ------ | ----------------- |
| 0x0    | 0x148  | Exception stack   |
| 0x148  | 0x78   | ExceptionFrameA64 |

ExceptionFrameA64:

| Offset | Length      | Description         |
| ------ | ----------- | ------------------- |
| 0x0    | 0x48 (8\*9) | GPRs 0..8.          |
| 0x48   | 0x8         | lr                  |
| 0x50   | 0x8         | sp                  |
| 0x58   | 0x8         | pc (elr\_el1)       |
| 0x60   | 0x4         | pstate & 0xFF0FFE20 |
| 0x64   | 0x4         | afsr0               |
| 0x68   | 0x4         | afsr1               |
| 0x6C   | 0x4         | esr                 |
| 0x70   | 0x8         | far                 |

TLS region start (A32):

| Offset | Length | Description       |
| ------ | ------ | ----------------- |
| 0x0    | 0x178  | Exception stack   |
| 0x148  | 0x44   | ExceptionFrameA32 |

ExceptionFrameA32:

| Offset | Length      | Description       |
| ------ | ----------- | ----------------- |
| 0x0    | 0x20 (8\*4) | GPRs 0..7.        |
| 0x20   | 0x4         | sp                |
| 0x24   | 0x4         | lr                |
| 0x28   | 0x4         | pc (elr\_el1)     |
| 0x2C   | 0x4         | tpidr\_el0 = 1    |
| 0x30   | 0x4         | cpsr & 0xFF0FFE20 |
| 0x34   | 0x4         | afsr0             |
| 0x38   | 0x4         | afsr1             |
| 0x3C   | 0x4         | esr               |
| 0x40   | 0x4         | far               |

In that case, after storing the regs in the TLS, the exception handler
returns to the application's crt0 (entrypoint), with
X0=<error description code> (see below) and X1=SP=frame=<stack top> (see
above)

| Desc. code | Meaning                                                                                           |
| ---------- | ------------------------------------------------------------------------------------------------- |
| 0x100      | Instruction abort                                                                                 |
| 0x102      | Misaligned PC                                                                                     |
| 0x103      | Misaligned SP                                                                                     |
| 0x106      | SError \[not in 1.0.0?\]                                                                          |
| 0x301      | Bad SVC                                                                                           |
| 0x104      | Uncategorized, CP15RTTrap, CP15RRTTrap, CP14RTTrap, CP14RRTTrap, IllegalState, SystemRegisterTrap |
| 0x101      | None of the above, EC \<= 0x34 and not a breakpoint                                               |
|            |                                                                                                   |

(During normal app boot the process is invoked with X0=0 and
X1=main\_thread\_handle. The crt0 of retail apps determines whether to
boot normally or handle an exception if X0 is set to 0 or not)

The application is supposed to promptly update the contents of elr\_el1
to a user handler (and any other regs it sees fit) and call
svcReturnFromException (error code) to call that handler. The latter is
then expected to promptly abort the program.

svcReturnFromException updates the contents of the kernel stack frame
with what the user provided in the TLS structure, sets TPIDR\_EL0 to 1,
then:

  - if the provided error code is 0, gracefully pivots and returns from
    exception
  - if it is not, replays the exception and pass it to the KDebug (see
    above). One can pass 0x10001 to prevent process termination. If the
    process is attached, this also prevents crash-collection/termination
    (different from the exception handler behavior)

If an exception occurs from the above user handler, the entire exception
handling process will repeat with the new exception.

Note that if a thread that wasn't faulting calls svcReturnFromException,
it signals an "invalid syscall" exception

Note that [IsDebugMode](SMC.md "wikilink") is not used during
exception-handling, except for enabling printing a message to UART-A.
This UART code causes a system-hang on retail (likely due to a loop that
doesn't exit). This printing doesn't seem to run when the process is
attached for debugging?
