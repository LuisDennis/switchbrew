# Userspace

The userspace virtual address space can be either 32 or 36 bits.
\[2.0.0+\] introduced support for 38 bit address spaces.

There are two regions randomized and enforced by the kernel, each one
with upper bits random and 2MB-aligned:

  - ReservedHeapRegion, available from
    [SVC\#svcGetInfo](SVC#svcGetInfo.md##svcGetInfo "wikilink").
  - ReservedMapRegion, available from
    [SVC\#svcGetInfo](SVC#svcGetInfo.md##svcGetInfo "wikilink").
  - \[2.0.0+\] NewReservedMapRegion, available from
    [SVC\#svcGetInfo](SVC#svcGetInfo.md##svcGetInfo "wikilink").
  - \[2.0.0+\] TlsIoRegion, not available to userspace.

The main binary is placed at an address that is provided to the kernel
by Loader via
[SVC\#svcCreateProcess](SVC#svcCreateProcess.md##svcCreateProcess "wikilink").

Typically on 2.0.0+ systems, the main binary region has randomness in
bits 37-21.

For the stack mapping region, the userland randomizes a page-offset
where to start inside the region. This adds some additional entropy.

Binaries mapped by RO are mapped randomly everywhere in the entire
address space. The base address for each NRO has all bits randomized and
are 4K-aligned. This means that typically, on 2.0.0+ systems, bits 37-12
of the NRO base address are random.

For all binaries(main area / NROs), the R-- section is always located
immediately after R-X. The RW- section is always located immediately
after the R-- section. Hence, there's no extra randomization /
guard-pages for these sections.

On version [1.0.0](1.0.0.md "wikilink"), the initial binaries loaded
into memory by the kernel always have the upper 32-bits as all-zero, so
there are 6 fewer bits of layout randomization.

Binaries loaded within the main-binary-region are loaded into memory in
the following order, immediately after each other, for the binaries
which exist in [ExeFS](ExeFS.md "wikilink"):

  - rtld
  - main
  - subsdk\*
  - sdk

## ASLR Implementation

The kernel uses a MT19937 random number generator, seeded by
[smcGetRandomBytes](SMC#GetRandomBytes.md##GetRandomBytes "wikilink").

### 1.0.0

`if (AddressSpaceType == 2) {`  
`  BaseAddr = 0x80000000; // 64-bit`  
`  RandomMax = 0x6400;`  
`}`  
`else {`  
`  BaseAddr = 0x40000000; // 32-bit`  
`  RandomMax = 0x200;`  
`}`  
  
`if (AddressSpaceType == 4) {`  
`  MapRegionSize = 0;`  
`  HeapRegionSize = 0x80000000;`  
`}`  
`else {`  
`  MapRegionSize = 0x40000000;`  
`  HeapRegionSize = 0x40000000;`  
`}`  
  
`if (EnableAslr) {`  
`  rnd0 = GetRandomRange(0, RandomMax) << 21;`  
`  rnd1 = GetRandomRange(0, RandomMax) << 21;`  
`}`  
`else {`  
`  rnd0 = rnd1 = 0;`  
`}`  
  
`this->MapBaseAddr = BaseAddr + min(rnd0, rnd1)`  
`this->HeapRegionBaseAddr = this->MapBaseAddr + MapRegionSize + max(rnd0, rnd1) - min(rnd0, rnd1)`

# Kernel

For more details, see [\#Notes](#Notes "wikilink"). Here comes a
summary.

PXN bit is set in the MMU descriptor for userland code pages. This means
that userland code pages are not executable in kernel mode (this is
equivalent to SMEP on x86).

For userland pages, the kernel has same access as userland (either both
are read-only or both are read-write). It does not have SMAP. The
previous rule has one exception: pages that are mapped unreadable in
usermode are still forced readable from kernelmode.

KASLR is being used since [5.0.0](5.0.0.md "wikilink"), but not before,
with the following pseudocode (might contains some errors):

    DRAM crt0 mapping (ttbr1): offsets DRAM with (rand64ViaSmc() % 0x3FFF0 << 21), allocates exactly (end - _start) + 1GB.
    This is a "linear" mapping. Permissions are set properly.
    
    KERN_ADDRSPACE       := [VA(_start) : min(0xFFFFFFFFFFE00000 - VA(_start), 0x40000000)]
    DRAM_FROM_SECTION1   := DRAM[0x808cd000:] // 0x808cd000 corresponds to start of section1 (loaded INI1) data, reused later
    
    /* Global Randomize range: 0xFFFFFF8000000000 to 0xFFFFFFFFFFE00000. */
    /*
        Randomize picks a random integer in ranges, clears as many low bits required,
        then checks if the address is acceptable, if not it attempts to iterate through page table entries.
        
        If it doesn't find anything, it picks another integer. In case of general failure, the whole operation
        may be done from the start again (maybe ?).
    */
    
    /* Core0 executes this big KASLR function, then powers on the other CPUs (?). */
    MapPartially(RandomizeL1Boundary(DRAM, sizeof(DRAM)) -> DRAM_FROM_SECTION1: offsetof DRAM_FROM_SECTION1,
    
    /* Randomize */
    KERN_ADDRSPACE {
        Randomize(IOAndInitialStacks, 0x2000000) {
            Map(Randomize(UartA, 0x1000)) -> UartA,
            GuardPage,
            Map(Randomize(Gicd, 0x1000)) -> Gicd,
            GuardPage,
            Map(Randomize(Gicc, 0x1000)) -> Gicc,
            ForEachCore {
                GuardPage,
                Map(Randomize(EntryThreadStack, 0x1000)) -> NextFreePage(),
                GuardPage,
                Map(Randomize(IdleSchedulerThreadStack, 0x1000)) -> NextFreePage(),
                GuardPage,
                Map(Randomize(EL1AbortStack, 0x1000)) -> NextFreePage(),
            }
        },
        
        Randomize(KernelStacks, 0xE00000),
        Map(Randomize(SlabHeaps, 0x7E9000, AFTER(VA(_end)) -> PA(_end)),
        Randomize(Kip1DecompressionBuffer, 0x8000000), /* 128 MB VA range */
    },
    
    Map(RandomizePageBoundary(GuardPage + KCoreContext * 4)) -> NextFreePages(4)

## 1.0.0

| Virtual                               | Physical                   | Size    | Attributes       | Permissions | Description                                 |
| ------------------------------------- | -------------------------- | ------- | ---------------- | ----------- | ------------------------------------------- |
| 0xFFFFFFFFBFC00000-0xFFFFFFFFBFC45FFF | 0x800A0000                 | 0x46000 | 0x78B            | R-X         | Kernel .text                                |
| 0xFFFFFFFFBFC46000-0xFFFFFFFFBFC48FFF | 0x800E6000                 | 0x3000  | 0x6000000000078B | R--         | Kernel .rodata                              |
| 0xFFFFFFFFBFC49000-0xFFFFFFFFBFC4FFFF | 0x800E9000                 | 0x7000  | 0x6000000000070B | RW-         | Kernel .data+.bss                           |
| 0xFFFFFFFFBFD72000-0xFFFFFFFFBFD72FFF | 0x6000F000                 | 0x1000  | 0x60000000000607 | RW-         | Exception vectors                           |
| 0xFFFFFFFFBFDB5000-0xFFFFFFFFBFDB5FFF | 0x60007000                 | 0x1000  | 0x60000000000607 | RW-         | Flow controller                             |
| 0xFFFFFFFFBFDB7000-0xFFFFFFFFBFDB7FFF | 0x60004000                 | 0x1000  | 0x60000000000607 | RW-         | Primary ICTLR                               |
| 0xFFFFFFFFBFDB9000-0xFFFFFFFFBFDB9FFF | 0x60001000                 | 0x1000  | 0x60000000000607 | RW-         | Resource Semaphore                          |
| 0xFFFFFFFFBFDBB000-0xFFFFFFFFBFDBBFFF | 0x70016000                 | 0x2000  | 0x60000000000607 | RW-         | ATOMICS                                     |
| 0xFFFFFFFFBFDBE000-0xFFFFFFFFBFDBEFFF | 0x7000E000                 | 0x1000  | 0x60000000000607 | RW-         | PMC                                         |
| 0xFFFFFFFFBFDC0000-0xFFFFFFFFBFDC0FFF | 0x60006000                 | 0x1000  | 0x60000000000607 | RW-         | Clock and reset                             |
| 0xFFFFFFFFBFDC2000-0xFFFFFFFFBFDC2FFF | 0x7001D000                 | 0x1000  | 0x60000000000607 | RW-         | MC1                                         |
| 0xFFFFFFFFBFDC4000-0xFFFFFFFFBFDC4FFF | 0x7001C000                 | 0x1000  | 0x60000000000607 | RW-         | MC0                                         |
| 0xFFFFFFFFBFDC6000-0xFFFFFFFFBFDC6FFF | 0x70019000                 | 0x1000  | 0x60000000000607 | RW-         | MC                                          |
| 0xFFFFFFFFBFDC8000-0xFFFFFFFFBFDC8FFF | 0x70006000                 | 0x1000  | 0x60000000000607 | RW-         | UART-A                                      |
| 0xFFFFFFFFBFDCA000-0xFFFFFFFFBFDCBFFF | 0x80060000                 | 0x2000  | 0x6000000000070B | RW-         |                                             |
| 0xFFFFFFFFBFDCE000-0xFFFFFFFFBFDCFFFF | 0x80068000                 | 0x2000  | 0x6000000000070B | RW-         | Kernel main stack (cpu0)                    |
| 0xFFFFFFFFBFDD2000-0xFFFFFFFFBFDD2FFF | 0x80070000                 | 0x1000  | 0x6000000000070B | RW-         | Kernel runner stack (cpu0)                  |
| 0xFFFFFFFFBFDD4000-0xFFFFFFFFBFDD5FFF | 0x80062000                 | 0x2000  | 0x6000000000070B | RW-         |                                             |
| 0xFFFFFFFFBFDD8000-0xFFFFFFFFBFDD9FFF | 0x8006A000                 | 0x2000  | 0x6000000000070B | RW-         | Kernel main stack (cpu1)                    |
| 0xFFFFFFFFBFDDC000-0xFFFFFFFFBFDDCFFF | 0x80071000                 | 0x1000  | 0x6000000000070B | RW-         | Kernel runner stack (cpu1)                  |
| 0xFFFFFFFFBFDDE000-0xFFFFFFFFBFDDFFFF | 0x80064000                 | 0x2000  | 0x6000000000070B | RW-         |                                             |
| 0xFFFFFFFFBFDE2000-0xFFFFFFFFBFDE3FFF | 0x8006C000                 | 0x2000  | 0x6000000000070B | RW-         | Kernel main stack (cpu2)                    |
| 0xFFFFFFFFBFDE6000-0xFFFFFFFFBFDE6FFF | 0x80072000                 | 0x1000  | 0x6000000000070B | RW-         | Kernel runner stack (cpu2)                  |
| 0xFFFFFFFFBFDE8000-0xFFFFFFFFBFDE9FFF | 0x80066000                 | 0x2000  | 0x6000000000070B | RW-         |                                             |
| 0xFFFFFFFFBFDEC000-0xFFFFFFFFBFDEDFFF | 0x8006E000                 | 0x2000  | 0x6000000000070B | RW-         | Kernel main stack (cpu3)                    |
| 0xFFFFFFFFBFDF0000-0xFFFFFFFFBFDF0FFF | 0x80073000                 | 0x1000  | 0x6000000000070B | RW-         | Kernel runner stack (cpu3)                  |
| 0xFFFFFFFFBFDFB000-0xFFFFFFFFBFDFBFFF | 0x50041000                 | 0x1000  | 0x60000000000607 | RW-         | ARM Interrupt Distributor                   |
| 0xFFFFFFFFBFDFD000-0xFFFFFFFFBFDFDFFF | 0x50042000                 | 0x1000  | 0x60000000000607 | RW-         | Interrupt Controller Physical CPU interface |
| 0xFFFFFFFFBFDF2000-0xFFFFFFFFBFDF3FFF | 0x80060000+(cpuid\*0x2000) | 0x2000  | 0x6000000000070B | RW-         |                                             |
| 0xFFFFFFFFBFDF6000-0xFFFFFFFFBFDF7FFF | 0x80068000+(cpuid\*0x2000) | 0x2000  | 0x6000000000070B | RW-         | Kernel main stack (per-core self-mirror)    |
| 0xFFFFFFFFBFDFF000-0xFFFFFFFFBFDFFFFF | 0x80084000+(cpuid\*0x1000) | 0x1000  | 0x6000000000070B | RW-         | Kernel runner stack (per-core self-mirror)  |
| 0xFFFFFFFE00000000-...                | 0x80000000                 | ...     | 0x60000000000709 | RW-         | Raw DRAM access                             |

## 2.0.0

| Cores | Virtual                               | Physical   | Size    | Attributes       | Permissions | Description                                 |
| ----- | ------------------------------------- | ---------- | ------- | ---------------- | ----------- | ------------------------------------------- |
| All   | 0xFFFFFFF7FFC00000-0xFFFFFFF7FFC62FFF | 0x800A0000 | 0x63000 | 0x78B            | R-X         | Kernel .text                                |
| All   | 0xFFFFFFF7FFC63000-0xFFFFFFF7FFC65FFF | 0x80103000 | 0x3000  | 0x6000000000078B | R--         | Kernel .rodata                              |
| All   | 0xFFFFFFF7FFC66000-0xFFFFFFF7FFC6EFFF | 0x80106000 | 0x9000  | 0x6000000000070B | RW-         | Kernel .data+.bss                           |
| All   | 0xFFFFFFF7FFDC0000-0xFFFFFFF7FFDC0FFF | 0x60006000 | 0x1000  | 0x60000000000607 | RW-         | Clock and Reset                             |
| All   | 0xFFFFFFF7FFDC2000-0xFFFFFFF7FFDC2FFF | 0x7001D000 | 0x1000  | 0x60000000000607 | RW-         | MC1                                         |
| All   | 0xFFFFFFF7FFDC4000-0xFFFFFFF7FFDC4FFF | 0x7001C000 | 0x1000  | 0x60000000000607 | RW-         | MC0                                         |
| All   | 0xFFFFFFF7FFDC6000-0xFFFFFFF7FFDC6FFF | 0x70019000 | 0x1000  | 0x60000000000607 | RW-         | MC                                          |
| All   | 0xFFFFFFF7FFDC8000-0xFFFFFFF7FFDC8FFF | 0x70006000 | 0x1000  | 0x60000000000607 | RW-         | UART-A                                      |
| All   | 0xFFFFFFF7FFDCA000-0xFFFFFFF7FFDCAFFF | 0x80060000 | 0x2000  | 0x6000000000070B | RW-         |                                             |
| All   | 0xFFFFFFF7FFDCE000-0xFFFFFFF7FFDCEFFF | 0x80068000 | 0x2000  | 0x6000000000070B | RW-         |                                             |
| All   | 0xFFFFFFF7FFDD2000-0xFFFFFFF7FFDD2FFF | 0x80070000 | 0x1000  | 0x6000000000070B | RW-         |                                             |
| All   | 0xFFFFFFF7FFDD4000-0xFFFFFFF7FFDD4FFF | 0x80062000 | 0x2000  | 0x6000000000070B | RW-         |                                             |
| All   | 0xFFFFFFF7FFDD8000-0xFFFFFFF7FFDD8FFF | 0x8006A000 | 0x2000  | 0x6000000000070B | RW-         |                                             |
| All   | 0xFFFFFFF7FFDDC000-0xFFFFFFF7FFDDCFFF | 0x80071000 | 0x1000  | 0x6000000000070B | RW-         |                                             |
| All   | 0xFFFFFFF7FFDDE000-0xFFFFFFF7FFDDEFFF | 0x80064000 | 0x2000  | 0x6000000000070B | RW-         |                                             |
| All   | 0xFFFFFFF7FFDE2000-0xFFFFFFF7FFDE2FFF | 0x8006C000 | 0x2000  | 0x6000000000070B | RW-         |                                             |
| All   | 0xFFFFFFF7FFDE6000-0xFFFFFFF7FFDE6FFF | 0x80072000 | 0x1000  | 0x6000000000070B | RW-         |                                             |
| All   | 0xFFFFFFF7FFDE8000-0xFFFFFFF7FFDE8FFF | 0x80066000 | 0x2000  | 0x6000000000070B | RW-         |                                             |
| All   | 0xFFFFFFF7FFDEC000-0xFFFFFFF7FFDECFFF | 0x8006E000 | 0x2000  | 0x6000000000070B | RW-         |                                             |
| All   | 0xFFFFFFF7FFDF0000-0xFFFFFFF7FFDF0FFF | 0x80073000 | 0x1000  | 0x6000000000070B | RW-         |                                             |
| All   | 0xFFFFFFF7FFDFB000-0xFFFFFFF7FFDFBFFF | 0x50041000 | 0x1000  | 0x60000000000607 | RW-         | ARM Interrupt Distributor                   |
| All   | 0xFFFFFFF7FFDFD000-0xFFFFFFF7FFDFDFFF | 0x50042000 | 0x1000  | 0x60000000000607 | RW-         | Interrupt Controller Physical CPU interface |
| All   | 0xFFFFFFF800000000-...                | 0x80000000 | ...     | 0x60000000000709 | RW-         | Raw DRAM access                             |

## 3.0.0

| Cores | Virtual                               | Physical   | Size    | Attributes       | Permissions | Description                                 |
| ----- | ------------------------------------- | ---------- | ------- | ---------------- | ----------- | ------------------------------------------- |
| All   | 0xFFFFFFF7FFC00000-0xFFFFFFF7FFC4AFFF | 0x800A0000 | 0x4B000 | 0x78B            | R-X         | Kernel .text                                |
| All   | 0xFFFFFFF7FFC4B000-0xFFFFFFF7FFC4DFFF | 0x800EB000 | 0x3000  | 0x6000000000078B | R--         | Kernel .rodata                              |
| All   | 0xFFFFFFF7FFC4E000-0xFFFFFFF7FFC5AFFF | 0x800EE000 | 0xD000  | 0x6000000000070B | RW-         | Kernel .data+.bss                           |
| All   | 0xFFFFFFF7FFDAC000-0xFFFFFFF7FFDACFFF | 0x60006000 | 0x1000  | 0x60000000000607 | RW-         | Clock and Reset                             |
| All   | 0xFFFFFFF7FFDAE000-0xFFFFFFF7FFDAEFFF | 0x7001D000 | 0x1000  | 0x60000000000607 | RW-         | MC1                                         |
| All   | 0xFFFFFFF7FFDB0000-0xFFFFFFF7FFDB0FFF | 0x7001C000 | 0x1000  | 0x60000000000607 | RW-         | MC0                                         |
| All   | 0xFFFFFFF7FFDB2000-0xFFFFFFF7FFDB2FFF | 0x70019000 | 0x1000  | 0x60000000000607 | RW-         | MC                                          |
| All   | 0xFFFFFFF7FFDB4000-0xFFFFFFF7FFDB4FFF | 0x70006000 | 0x1000  | 0x60000000000607 | RW-         | UART-A                                      |
| All   | 0xFFFFFFF7FFDFB000-0xFFFFFFF7FFDFBFFF | 0x50041000 | 0x1000  | 0x60000000000607 | RW-         | ARM Interrupt Distributor                   |
| All   | 0xFFFFFFF7FFDFD000-0xFFFFFFF7FFDFDFFF | 0x50042000 | 0x1000  | 0x60000000000607 | RW-         | Interrupt Controller Physical CPU interface |

## 4.0.0

| Cores | Virtual                               | Physical   | Size    | Attributes       | Permissions | Description                                 |
| ----- | ------------------------------------- | ---------- | ------- | ---------------- | ----------- | ------------------------------------------- |
| All   | 0xFFFFFFF7FFC00000-0xFFFFFFF7FFC50FFF | 0x800A0000 | 0x51000 | 0x4000000000078B | R-X         | Kernel .text                                |
| All   | 0xFFFFFFF7FFC51000-0xFFFFFFF7FFC53FFF | 0x800F1000 | 0x3000  | 0x6000000000078B | R--         | Kernel .rodata                              |
| All   | 0xFFFFFFF7FFC54000-0xFFFFFFF7FFC61FFF | 0x800F4000 | 0xE000  | 0x6000000000070B | RW-         | Kernel .data+.bss                           |
| All   | 0xFFFFFFF7FFDAC000-0xFFFFFFF7FFDACFFF | 0x60006000 | 0x1000  | 0x60000000000607 | RW-         | Clock and Reset                             |
| All   | 0xFFFFFFF7FFDAE000-0xFFFFFFF7FFDAEFFF | 0x7001D000 | 0x1000  | 0x60000000000607 | RW-         | MC1                                         |
| All   | 0xFFFFFFF7FFDB0000-0xFFFFFFF7FFDB0FFF | 0x7001C000 | 0x1000  | 0x60000000000607 | RW-         | MC0                                         |
| All   | 0xFFFFFFF7FFDB2000-0xFFFFFFF7FFDB2FFF | 0x70019000 | 0x1000  | 0x60000000000607 | RW-         | MC                                          |
| All   | 0xFFFFFFF7FFDB4000-0xFFFFFFF7FFDB4FFF | 0x70006000 | 0x1000  | 0x60000000000607 | RW-         | UART-A                                      |
| All   | 0xFFFFFFF7FFDFB000-0xFFFFFFF7FFDFBFFF | 0x50041000 | 0x1000  | 0x60000000000607 | RW-         | ARM Interrupt Distributor                   |
| All   | 0xFFFFFFF7FFDFD000-0xFFFFFFF7FFDFDFFF | 0x50042000 | 0x1000  | 0x60000000000607 | RW-         | Interrupt Controller Physical CPU interface |

The rest are are mapped to core-specific physaddrs, each one is
0x1000-bytes. Descriptor ORR-value = 0x6000000000070B.

| Vmem               | Physmem                                            |
| ------------------ | -------------------------------------------------- |
| 0xFFFFFFF7FFDF7000 | \<physaddr from vmem 0xFFFFFFF7FFDF6000\> + 0x1000 |
| 0xFFFFFFF7FFDF3000 | \<physaddr from vmem 0xFFFFFFF7FFDF2000\> + 0x1000 |
| 0xFFFFFFF7FFDF6000 | 0x800XX000                                         |
| 0xFFFFFFF7FFDF2000 | 0x800XX000                                         |
| 0xFFFFFFF7FFDFF000 | 0x800XX000                                         |
| 0xFFFFFFF7FFDF9000 | 0x800XX000                                         |

## Notes

### 2.0.0

` Granule size for TTBR0*_EL1 is 4KB.`  
` TTBR0_EL1 vmem starts at vaddr 0x0.`  
` vmem end-addr for TTBR1_EL1 is 0xffffffffffffffff. vmem start-addr for TTBR1_EL1 is 0xFFFFFFF000000000.`  
` T0SZ = 31. Hence, bit-size of the TTBR0*_EL1 vmem region is 33. (0x0000000200000000)`  
` T1SZ = 28. Hence, bit-size of the TTBR1*_EL1 vmem region is 36. (0x0000001000000000)`  
` `  
` Note: ARM config for TTBR0 is presumably configured for userland later.`  
` `  
` See arm-doc for "Table D4-25 Translation table entry addresses when using the 4KB translation granule".`  
` `  
` See arm-doc for "Overview of VMSAv8-64 address translation using the 4KB translation granule".`  
` `  
` See arm-doc for "Table D4-11 TCR.TnSZ values and IA ranges, 4K granule with no concatenation of tables".`  
` Both TTBR*_EL1 use "Initial lookup level" 1. Therefore, the TTBR*_EL1 tables are level1.`  
` `  
` Due to T*SZ, Stage1/Stage2 translation for the initial table(level1) are the same, except Stage2 uses hard-coded T0SZ.`  
` Basically, the table is accessed as: ((u64*)tablebase)[<IA[y:30]>], where y = (37-T*SZ)+26. That is, starting at bit "y" ending(inclusive) at bit30. For TTBR0*_EL1, y = 32, while for TTBR1_EL1 y = 35.`  
` Hence, for TTBR0, index=((vaddr>>30) & 0x7), and for TTBR1, index=((vaddr>>30) & 0x3f).`

"Vector Base Address Register (EL1)" = 0xfffffff7ffc50800.

The table for TTBR0 only contains the following:

  - Vmem 0x80000000 is mapped to physmem 0x80000000, using a size loaded
    from a register. This is only done when: "endaddr = 0x7fffffff +
    size; if(endaddr \>= 0x80000001){...}"
      - The size is loaded from: "(u32 \*0x70019050 & 0x3fff) \<\< 20;"
      - The value written to the MMU-table descriptor is: "physaddr |
        val | 0x709;". val is 1\<\<52 when "tmp\>\>34" is non-zero and
        when "if((physaddr & 0x3c0000000) == 0)", otherwise val=0.
        tmp=size at the start and increased by 0xffffffffc0000000 each
        loop iteration. physaddr is increased by 0x40000000 each loop
        iteration.

TTBR1:

  - vmem 0xFFFFFFF800000000 is mapped to physmem 0x80000000. Similar to
    above, except tmp=0 due to wrap-around, etc. This also has
    usermode/kernel XN enabled in the descriptor ORR-value. The
    chunksize used when increasing addr is 0xfffffff840000000, with
    another +=0x40000000 separate from the addr cmp for the loop.
      - "endaddr = 0x3fffffff + (<size from above> |
        0xfffffff800000000); enaddr = (endaddr & 0xffffffffc0000000)-1;
        if(endaddr \>= 0xfffffff800000001){<map mem>}"

<!-- end list -->

  - Initializes level2 pagetable descriptor for vmem 0xFFFFFFF7C0000000.
    descriptor = 0x3 | physaddr. physaddr is core-specific.
  - Initializes level3 pagetable descriptor for vmem 0xFFFFFFF7FFC00000.
    descriptor = 0x3 | physaddr. physaddr is core-specific.
  - The content of the pagetable for the following level3 mmutables are
    not initialized in the main mmutable-init func. descriptor =
    0x8007c003(0x3 | <physaddr tablebase>). tablebase=0x8007c000.
      - Initializes level3 pagetable descriptor for vmem
        0xFFFFFFF7FEE00000. physaddr = tablebase + (0x1\<\<12).
      - Initializes level3 pagetable descriptor for vmem
        0xFFFFFFF7FF000000. physaddr = tablebase + (0x2\<\<12).
      - Initializes level3 pagetable descriptor for vmem
        0xFFFFFFF7FF200000. physaddr = tablebase + (0x3\<\<12).
      - Initializes level3 pagetable descriptor for vmem
        0xFFFFFFF7FFA00000. physaddr = tablebase + (0x7\<\<12).
      - Initializes level3 pagetable descriptor for vmem
        0xFFFFFFF7FEC00000. physaddr = tablebase.
      - Initializes level3 pagetable descriptor for vmem
        0xFFFFFFF7FF400000. physaddr = tablebase + (0x4\<\<12).
      - Initializes level3 pagetable descriptor for vmem
        0xFFFFFFF7FF600000. physaddr = tablebase + (0x5\<\<12).
      - Initializes level3 pagetable descriptor for vmem
        0xFFFFFFF7FF800000. physaddr = tablebase + (0x6\<\<12).

# Secure Monitor

Unless otherwise mentionned, block descriptors (in our case, the one
uses for the DRAM identity mapping) are all ORRed by 0x401 and page
descriptors by 0x403.

## [1.0.0](1.0.0.md "wikilink")

| Vmem        | Physmem    | Size    | Descriptor ORR-value | Permissions | Description                                 |
| ----------- | ---------- | ------- | -------------------- | ----------- | ------------------------------------------- |
| 0x1F0000000 | 0x50041000 | 0x1000  | 0x40000000000324     |             | ARM Interrupt Distributor                   |
| 0x1F0002000 | 0x50042000 | 0x1000  | 0x40000000000324     |             | Interrupt Controller Physical CPU Interface |
| 0x1F0005000 | 0x70006000 | 0x1000  | 0x40000000000324     |             | UART-A                                      |
| 0x1F0007000 | 0x60006000 | 0x1000  | 0x40000000000324     |             | Clock and Reset                             |
| 0x1F0009000 | 0x7000E000 | 0x1000  | 0x40000000000304     |             | PMC                                         |
| 0x1F000B000 | 0x60005000 | 0x1000  | 0x40000000000304     |             | TMR                                         |
| 0x1F000D000 | 0x6000C000 | 0x1000  | 0x40000000000304     |             | System Registers                            |
| 0x1F000F000 | 0x70012000 | 0x2000  | 0x40000000000304     |             | SE                                          |
| 0x1F0012000 | 0x700F0000 | 0x1000  | 0x40000000000304     |             | SYSCTR0                                     |
| 0x1F0014000 | 0x70019000 | 0x1000  | 0x40000000000304     |             | MC                                          |
| 0x1F0016000 | 0x7000F000 | 0x1000  | 0x40000000000304     |             | FUSE                                        |
| 0x1F0018000 | 0x70000000 | 0x4000  | 0x40000000000304     |             | MISC                                        |
| 0x1F001D000 | 0x60007000 | 0x1000  | 0x40000000000304     |             | Flow controller                             |
| 0x1F001F000 | 0x40002000 | 0x1000  | 0x40000000000304     |             | IRAM                                        |
| 0x1F0021000 | 0x7000D000 | 0x1000  | 0x40000000000304     |             | I2C-5                                       |
| 0x1F0023000 | 0x6000D000 | 0x1000  | 0x40000000000304     |             | GPIO-1                                      |
| 0x1F0025000 | 0x7000C000 | 0x1000  | 0x40000000000304     |             | I2C                                         |
| 0x1F0180000 | 0x40020000 | 0x10000 | 0x40000000000324     |             | IRAM                                        |
| 0x1F01A0000 | 0x7C010000 | 0x10000 | 0x40000000000384     |             | TZRAM                                       |
| 0x1F01C3000 | 0x80010000 | 0x10000 | 0x40000000000324     |             | EMEM                                        |
| 0x1F01C2000 | 0x8000F000 | 0x1000  | 0x40000000000324     |             | EMEM                                        |
| 0x1F01E0000 | 0x7C013000 | 0xB000  | 0x304                |             | TZRAM (Secure Monitor)                      |
| 0x1F01F0000 | 0x7C01E000 | 0x2000  | 0x304                |             | TZRAM (Secure Monitor and ARMv8 init)       |
| 0x1F01F6000 | 0x7C01E000 | 0x1000  | 0x40000000000304     |             | TZRAM                                       |
| 0x1F01F8000 | 0x7C01F000 | 0x1000  | 0x40000000000304     |             | TZRAM                                       |
| 0x1F01FA000 | 0x7C010000 | 0x1000  | 0x304                |             | TZRAM (Secure Monitor exception vectors)    |
| 0x1F01FC000 | 0x7C011000 | 0x1000  | 0x40000000000304     |             | TZRAM                                       |
| 0x1F01FE000 | 0x7C012000 | 0x1000  | 0x40000000000304     |             | TZRAM                                       |

## [2.0.0](2.0.0.md "wikilink")

| Vmem        | Physmem    | Size    | Descriptor ORR-value | Permissions | Description                                           |
| ----------- | ---------- | ------- | -------------------- | ----------- | ----------------------------------------------------- |
| 0x7C010000  | 0x7C010000 | 0x10000 | 0x300                |             | TZRAM                                                 |
| 0x40020000  | 0x40020000 | 0x20000 | 0x300                |             | iRAM-C                                                |
| 0x1F0080000 | 0x50041000 | 0x1000  | 0x40000000000304     |             | ARM Interrupt Distributor                             |
| 0x1F0082000 | 0x50042000 | 0x2000  | 0x40000000000304     |             | Interrupt Controller Physical CPU interface           |
| 0x1F0085000 | 0x70006000 | 0x1000  | 0x40000000000324     |             | UART-A                                                |
| 0x1F0087000 | 0x60006000 | 0x1000  | 0x40000000000324     |             | Clock and Reset                                       |
| 0x1F0089000 | 0x7000E000 | 0x1000  | 0x40000000000304     |             | PMC                                                   |
| 0x1F008B000 | 0x60005000 | 0x1000  | 0x40000000000304     |             | TMR                                                   |
| 0x1F008D000 | 0x6000C000 | 0x1000  | 0x40000000000304     |             | System Registers                                      |
| 0x1F008F000 | 0x70012000 | 0x2000  | 0x40000000000304     |             | SE                                                    |
| 0x1F0092000 | 0x700F0000 | 0x1000  | 0x40000000000304     |             | SYSCTR0                                               |
| 0x1F0094000 | 0x70019000 | 0x1000  | 0x40000000000304     |             | MC                                                    |
| 0x1F0096000 | 0x7000F000 | 0x1000  | 0x40000000000304     |             | FUSE (0x7000F800)                                     |
| 0x1F0098000 | 0x70000000 | 0x4000  | 0x40000000000304     |             | MISC                                                  |
| 0x1F009D000 | 0x60007000 | 0x1000  | 0x40000000000304     |             | Flow Controller                                       |
| 0x1F009F000 | 0x40002000 | 0x1000  | 0x40000000000304     |             | iRAM-A                                                |
| 0x1F00A1000 | 0x7000D000 | 0x1000  | 0x40000000000304     |             | I2C5 - SPI 2B-6                                       |
| 0x1F00A3000 | 0x6000D000 | 0x1000  | 0x40000000000304     |             | GPIO-1 - GPIO-8                                       |
| 0x1F00A5000 | 0x7000C000 | 0x1000  | 0x40000000000304     |             | I2C-I2C4                                              |
| 0x1F00A7000 | 0x6000F000 | 0x1000  | 0x40000000000304     |             | Exception vectors                                     |
| 0x1F0180000 | 0x40020000 | 0x10000 | 0x40000000000324     |             | iRAM-C                                                |
| 0x1F0190000 | 0x40003000 | 0x1000  | 0x40000000000324     |             | iRAM-A                                                |
| 0x1F01A0000 | 0x7C010000 | 0x10000 | 0x40000000000380     |             | TZRAM                                                 |
| 0x1F01C3000 | 0x80010000 | 0x10000 | 0x40000000000324     |             | EMEM                                                  |
| 0x1F01C2000 | 0x8000F000 | 0x1000  | 0x40000000000324     |             | EMEM                                                  |
| 0x1F01E0000 | 0x7C013000 | 0xB000  | 0x300                |             | TZRAM (Secure Monitor)                                |
| 0x1F01F0000 | 0x7C01E000 | 0x2000  | 0x300                |             | TZRAM (Secure Monitor and ARMv8 init)                 |
| 0x1F01F4000 | <varies>   | 0x1000  | 0x40000000000320     |             | DRAM (SPL .bss buffer visible to the Security Engine) |
| 0x1F01F6000 | 0x7C01E000 | 0x1000  | 0x40000000000300     |             | TZRAM                                                 |
| 0x1F01F8000 | 0x7C01F000 | 0x1000  | 0x40000000000300     |             | TZRAM                                                 |
| 0x1F01FA000 | 0x7C010000 | 0x1000  | 0x300                |             | TZRAM (Secure Monitor exception vectors)              |
| 0x1F01FC000 | 0x7C011000 | 0x1000  | 0x40000000000300     |             | TZRAM                                                 |
| 0x1F01FE000 | 0x7C012000 | 0x1000  | 0x40000000000300     |             | TZRAM                                                 |

## [5.0.0](5.0.0.md "wikilink")

5.0.0 modified the address map to have separate .text, .rodata, and
.rwdata segments, instead of a single RWX segment.

However, the .rodata and .rwdata segments are both (mistakenly?) mapped
R-W.

Because the same L3 page is shared for all mappings, this required
modifying segment layout significantly to prevent clashes.

| Vmem        | Physmem    | Size    | Descriptor ORR-value | Description                                           |
| ----------- | ---------- | ------- | -------------------- | ----------------------------------------------------- |
| 0x7C010000  | 0x7C010000 | 0x10000 | 0x300                | TZRAM Identity RWX (for init)                         |
| 0x40020000  | 0x40020000 | 0x20000 | 0x300                | IRAM Identity RWX (for init)                          |
| 0x1F0080000 | 0x50041000 | 0x1000  | 0x40000000000304     | ARM Interrupt Distributor                             |
| 0x1F0082000 | 0x50042000 | 0x2000  | 0x40000000000304     | Interrupt Controller Physical CPU                     |
| 0x1F0085000 | 0x70006000 | 0x1000  | 0x40000000000324     | UART-A                                                |
| 0x1F0087000 | 0x60006000 | 0x1000  | 0x40000000000324     | Clock and Reset                                       |
| 0x1F0089000 | 0x7000E000 | 0x1000  | 0x40000000000304     | PMC                                                   |
| 0x1F008B000 | 0x60005000 | 0x1000  | 0x40000000000304     | Timers                                                |
| 0x1F008D000 | 0x6000C000 | 0x1000  | 0x40000000000304     | System Registers                                      |
| 0x1F008F000 | 0x70012000 | 0x2000  | 0x40000000000304     | Security Engine                                       |
| 0x1F00AD000 | 0x70412000 | 0x2000  | 0x40000000000304     | Erista: Nothing Present, Mariko: Security Engine 2    |
| 0x1F0092000 | 0x700F0000 | 0x1000  | 0x40000000000304     | SYSCTR0                                               |
| 0x1F0094000 | 0x70019000 | 0x1000  | 0x40000000000304     | Memory Controller                                     |
| 0x1F0096000 | 0x7000F000 | 0x1000  | 0x40000000000304     | Fuse Registers                                        |
| 0x1F0098000 | 0x70000000 | 0x4000  | 0x40000000000304     | MISC Registers                                        |
| 0x1F009D000 | 0x60007000 | 0x1000  | 0x40000000000304     | Flow Controller                                       |
| 0x1F009F000 | 0x40002000 | 0x1000  | 0x40000000000304     | IRAM                                                  |
| 0x1F00A1000 | 0x7000D000 | 0x1000  | 0x40000000000304     | I2C-5                                                 |
| 0x1F00A3000 | 0x6000D000 | 0x1000  | 0x40000000000304     | GPIO-1                                                |
| 0x1F00A5000 | 0x7000C000 | 0x1000  | 0x40000000000304     | I2C                                                   |
| 0x1F00A7000 | 0x6000F000 | 0x1000  | 0x40000000000304     | BPMP Exception Vectors                                |
| 0x1F00A9000 | 0x7001C000 | 0x1000  | 0x40000000000304     | MC0                                                   |
| 0x1F00AB000 | 0x7001D000 | 0x1000  | 0x40000000000304     | MC1                                                   |
| 0x1F0100000 | 0x7C010000 | 0x10000 | 0x40000000000380     | TZRAM (R-- for context save)                          |
| 0x1F0140000 | 0x7C012000 | 0x9000  | 0x300                | TZRAM (R-X .text)                                     |
| 0x1F0149000 | 0x7C01B000 | 0x1000  | 0x40000000000300     | TZRAM (RW- .rodata)                                   |
| 0x1F014A000 | 0x7C01C000 | 0x2000  | 0x40000000000300     | TZRAM (RW- .rwdata)                                   |
| 0x1F01A0000 | 0x40020000 | 0x10000 | 0x40000000000324     | IRAM (RW- for context save)                           |
| 0x1F01B0000 | 0x40003000 | 0x1000  | 0x40000000000324     | IRAM (BPMP firmware destination)                      |
| 0x1F01C7000 | 0x8000F000 | 0x1000  | 0x40000000000324     | DRAM (SE Context Save destination)                    |
| 0x1F01E0000 | 0x7C010000 | 0x2000  | 0x300                | TZRAM (RWX pk2ldr for init)                           |
| 0x1F01F4000 | X          | 0x1000  | 0x40000000000723     | DRAM (SPL .bss buffer visible to the Security Engine) |
| 0x1F01F6000 | 0x7C010000 | 0x1000  | 0x40000000000300     | TZRAM (stacks)                                        |
| 0x1F01F8000 | 0x7C011000 | 0x1000  | 0x40000000000300     | TZRAM (stacks)                                        |
| 0x1F01FA000 | 0x7C01D000 | 0x1000  | 0x40000000000300     | TZRAM (stacks, warmboot crt0)                         |
| 0x1F01FC000 | 0x7C01E000 | 0x1000  | 0x40000000000300     | TZRAM (L2 Page Table)                                 |
| 0x1F01FE000 | 0x7C01F000 | 0x1000  | 0x40000000000300     | TZRAM (L3 Page Table)                                 |
|             |            |         |                      |                                                       |

## [6.0.0](6.0.0.md "wikilink")

6.0.0 reduced the .rwdata segment to one page (previously 2).

| Vmem        | Physmem    | Size    | Descriptor ORR-value | Description                                           |
| ----------- | ---------- | ------- | -------------------- | ----------------------------------------------------- |
| 0x7C010000  | 0x7C010000 | 0x10000 | 0x300                | TZRAM Identity RWX (for init)                         |
| 0x40020000  | 0x40020000 | 0x20000 | 0x300                | IRAM Identity RWX (for init)                          |
| 0x1F0080000 | 0x50041000 | 0x1000  | 0x40000000000304     | ARM Interrupt Distributor                             |
| 0x1F0082000 | 0x50042000 | 0x2000  | 0x40000000000304     | Interrupt Controller Physical CPU                     |
| 0x1F0085000 | 0x70006000 | 0x1000  | 0x40000000000324     | UART-A                                                |
| 0x1F0087000 | 0x60006000 | 0x1000  | 0x40000000000324     | Clock and Reset                                       |
| 0x1F0089000 | 0x7000E000 | 0x1000  | 0x40000000000304     | PMC                                                   |
| 0x1F008B000 | 0x60005000 | 0x1000  | 0x40000000000304     | Timers                                                |
| 0x1F008D000 | 0x6000C000 | 0x1000  | 0x40000000000304     | System Registers                                      |
| 0x1F008F000 | 0x70012000 | 0x2000  | 0x40000000000304     | Security Engine                                       |
| 0x1F00AD000 | 0x70412000 | 0x2000  | 0x40000000000304     | Erista: Nothing Present, Mariko: Security Engine 2    |
| 0x1F0092000 | 0x700F0000 | 0x1000  | 0x40000000000304     | SYSCTR0                                               |
| 0x1F0094000 | 0x70019000 | 0x1000  | 0x40000000000304     | Memory Controller                                     |
| 0x1F0096000 | 0x7000F000 | 0x1000  | 0x40000000000304     | Fuse Registers                                        |
| 0x1F0098000 | 0x70000000 | 0x4000  | 0x40000000000304     | MISC Registers                                        |
| 0x1F009D000 | 0x60007000 | 0x1000  | 0x40000000000304     | Flow Controller                                       |
| 0x1F009F000 | 0x40002000 | 0x1000  | 0x40000000000304     | IRAM                                                  |
| 0x1F00A1000 | 0x7000D000 | 0x1000  | 0x40000000000304     | I2C-5                                                 |
| 0x1F00A3000 | 0x6000D000 | 0x1000  | 0x40000000000304     | GPIO-1                                                |
| 0x1F00A5000 | 0x7000C000 | 0x1000  | 0x40000000000304     | I2C                                                   |
| 0x1F00A7000 | 0x6000F000 | 0x1000  | 0x40000000000304     | BPMP Exception Vectors                                |
| 0x1F00A9000 | 0x7001C000 | 0x1000  | 0x40000000000304     | MC0                                                   |
| 0x1F00AB000 | 0x7001D000 | 0x1000  | 0x40000000000304     | MC1                                                   |
| 0x1F0100000 | 0x7C010000 | 0x10000 | 0x40000000000380     | TZRAM (R-- for context save)                          |
| 0x1F0140000 | 0x7C012000 | 0x9000  | 0x300                | TZRAM (R-X .text)                                     |
| 0x1F0149000 | 0x7C01B000 | 0x1000  | 0x40000000000300     | TZRAM (RW- .rodata)                                   |
| 0x1F014A000 | 0x7C01C000 | 0x1000  | 0x40000000000300     | TZRAM (RW- .rwdata)                                   |
| 0x1F01A0000 | 0x40020000 | 0x10000 | 0x40000000000324     | IRAM (RW- for context save)                           |
| 0x1F01B0000 | 0x40003000 | 0x1000  | 0x40000000000324     | IRAM (BPMP firmware destination)                      |
| 0x1F01C7000 | 0x8000F000 | 0x1000  | 0x40000000000324     | DRAM (SE Context Save destination)                    |
| 0x1F01E0000 | 0x7C010000 | 0x2000  | 0x300                | TZRAM (RWX pk2ldr for init)                           |
| 0x1F01F4000 | X          | 0x1000  | 0x40000000000723     | DRAM (SPL .bss buffer visible to the Security Engine) |
| 0x1F01F6000 | 0x7C010000 | 0x1000  | 0x40000000000300     | TZRAM (stacks)                                        |
| 0x1F01F8000 | 0x7C011000 | 0x1000  | 0x40000000000300     | TZRAM (stacks)                                        |
| 0x1F01FA000 | 0x7C01D000 | 0x1000  | 0x40000000000300     | TZRAM (stacks, warmboot crt0)                         |
| 0x1F01FC000 | 0x7C01E000 | 0x1000  | 0x40000000000300     | TZRAM (L2 Page Table)                                 |
| 0x1F01FE000 | 0x7C01F000 | 0x1000  | 0x40000000000300     | TZRAM (L3 Page Table)                                 |
|             |            |         |                      |                                                       |

# IRAM

## BIT

During boot, the BootROM saves the BCT in IRAM at address 0x40000100.
The preceding 0x100 bytes (IRAM memory range from 0x40000000 to
0x40000100) contain a structure called BIT (Boot Info Table) which
encapsulates the BCT in IRAM and is initialized by the BootROM as
follows:

<table>
<thead>
<tr class="header">
<th><p>Offset</p></th>
<th><p>Size</p></th>
<th><p>Field</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x00</p></td>
<td><p>0x04</p></td>
<td><p>BootRomVersion</p></td>
<td><p>Set to 0x00210001 (BOOTDATA_VERSION_T210).</p></td>
</tr>
<tr class="even">
<td><p>0x04</p></td>
<td><p>0x04</p></td>
<td><p>DataVersion</p></td>
<td><p>Set to 0x00210001 (BOOTDATA_VERSION_T210).</p></td>
</tr>
<tr class="odd">
<td><p>0x08</p></td>
<td><p>0x04</p></td>
<td><p>RcmVersion</p></td>
<td><p>Set to 0x00210001 (BOOTDATA_VERSION_T210).</p></td>
</tr>
<tr class="even">
<td><p>0x0C</p></td>
<td><p>0x04</p></td>
<td><p>BootType</p></td>
<td><p><code>None = 0</code><br />
<code>Cold = 1</code><br />
<code>Recovery = 2</code><br />
<code>Uart = 3</code><br />
<code>ExitRcm = 4</code></p></td>
</tr>
<tr class="odd">
<td><p>0x10</p></td>
<td><p>0x04</p></td>
<td><p>PrimaryDevice</p></td>
<td><p>Set to 0x05 (IROM) on coldboot.</p></td>
</tr>
<tr class="even">
<td><p>0x14</p></td>
<td><p>0x04</p></td>
<td><p>SecondaryDevice</p></td>
<td><p>Set to 0x04 (SDMMC) on coldboot.</p></td>
</tr>
<tr class="odd">
<td><p>0x18</p></td>
<td><p>0x04</p></td>
<td><p>BootTimeLogInit</p></td>
<td><p>Value from TIMERUS_CNTR_1US when the BootROM enters its main function.</p></td>
</tr>
<tr class="even">
<td><p>0x1C</p></td>
<td><p>0x04</p></td>
<td><p>BootTimeLogExit</p></td>
<td><p>This is the value that gets written into SB_CSR before nvboot. (0x10)</p></td>
</tr>
<tr class="odd">
<td><p>0x20</p></td>
<td><p>0x04</p></td>
<td><p>BootReadBctTickCnt</p></td>
<td><p>Time spent reading the BCT.</p></td>
</tr>
<tr class="even">
<td><p>0x24</p></td>
<td><p>0x04</p></td>
<td><p>BootReadBLTickCnt</p></td>
<td><p>Time spent parsing the bootloader info from the BCT.</p></td>
</tr>
<tr class="odd">
<td><p>0x28</p></td>
<td><p>0x04</p></td>
<td><p>OscFrequency</p></td>
<td><p>Value from CLK_RST_CONTROLLER_OSC_CTRL.</p></td>
</tr>
<tr class="even">
<td><p>0x2C</p></td>
<td><p>0x01</p></td>
<td><p>DevInitialized</p></td>
<td><p>Set to 1 after the boot device is initialized.</p></td>
</tr>
<tr class="odd">
<td><p>0x2D</p></td>
<td><p>0x01</p></td>
<td><p>SdramInitialized</p></td>
<td><p>Set to 1 after the SDRAM parameters are parsed.</p></td>
</tr>
<tr class="even">
<td><p>0x2E</p></td>
<td><p>0x01</p></td>
<td><p>ClearedForceRecovery</p></td>
<td><p>Set to 1 if bit 2 was set in APBDEV_PMC_SCRATCH0.</p></td>
</tr>
<tr class="odd">
<td><p>0x2F</p></td>
<td><p>0x01</p></td>
<td><p>ClearedFailBack</p></td>
<td><p>Set to 1 if bit 4 was set in APBDEV_PMC_SCRATCH0.</p></td>
</tr>
<tr class="even">
<td><p>0x30</p></td>
<td><p>0x01</p></td>
<td><p>InvokedFailBack</p></td>
<td><p>Set to 1 if the bootloaders have different versions in the BCT.</p></td>
</tr>
<tr class="odd">
<td><p>0x31</p></td>
<td><p>0x01</p></td>
<td><p>IRomPatchStatus</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0x32</p></td>
<td><p>0x01</p></td>
<td><p>BctValid</p></td>
<td><p>Set to 1 if the BCT was parsed successfully.</p></td>
</tr>
<tr class="odd">
<td><p>0x33</p></td>
<td><p>0x09</p></td>
<td><p>BctStatus</p></td>
<td><p>Each bit contains the status for BCT reads in a given block.</p></td>
</tr>
<tr class="even">
<td><p>0x3C</p></td>
<td><p>0x04</p></td>
<td><p>BctLastJournalRead</p></td>
<td><p>Contains the status of the last journal block read.</p>
<p><code>None = 0</code><br />
<code>Success = 1</code><br />
<code>ValidationFailure = 2</code><br />
<code>DeviceReadError = 3</code></p></td>
</tr>
<tr class="odd">
<td><p>0x40</p></td>
<td><p>0x04</p></td>
<td><p>BctBlock</p></td>
<td><p>Block number where the BCT was found.</p></td>
</tr>
<tr class="even">
<td><p>0x44</p></td>
<td><p>0x04</p></td>
<td><p>BctPage</p></td>
<td><p>Page number where the BCT was found.</p></td>
</tr>
<tr class="odd">
<td><p>0x48</p></td>
<td><p>0x04</p></td>
<td><p>BctSize</p></td>
<td><p>Size of the BCT in IRAM (0x2800).</p></td>
</tr>
<tr class="even">
<td><p>0x4C</p></td>
<td><p>0x04</p></td>
<td><p>BctPtr</p></td>
<td><p>Pointer to the BCT in IRAM (0x40000100).</p></td>
</tr>
<tr class="odd">
<td><p>0x50</p></td>
<td><p>0x18*4</p></td>
<td><p>BlState</p></td>
<td><p>Contains the state of attempts to load each bootloader.</p>
<table>
<thead>
<tr class="header">
<th><p>Offset</p></th>
<th><p>Size</p></th>
<th><p>Field</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x00</p></td>
<td><p>0x04</p></td>
<td><p>Status</p></td>
</tr>
<tr class="even">
<td><p>0x04</p></td>
<td><p>0x04</p></td>
<td><p>FirstEccBlock</p></td>
</tr>
<tr class="odd">
<td><p>0x08</p></td>
<td><p>0x04</p></td>
<td><p>FirstEccPage</p></td>
</tr>
<tr class="even">
<td><p>0x0C</p></td>
<td><p>0x04</p></td>
<td><p>FirstCorrectedEccBlock</p></td>
</tr>
<tr class="odd">
<td><p>0x10</p></td>
<td><p>0x04</p></td>
<td><p>FirstCorrectedEccPage</p></td>
</tr>
<tr class="even">
<td><p>0x14</p></td>
<td><p>0x01</p></td>
<td><p>HadEccError</p></td>
</tr>
<tr class="odd">
<td><p>0x15</p></td>
<td><p>0x01</p></td>
<td><p>HadCrcError</p></td>
</tr>
<tr class="even">
<td><p>0x16</p></td>
<td><p>0x01</p></td>
<td><p>HadCorrectedEccError</p></td>
</tr>
<tr class="odd">
<td><p>0x17</p></td>
<td><p>0x01</p></td>
<td><p>UsedForEccRecovery</p></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td><p>0xB0</p></td>
<td><p>0x3C</p></td>
<td><p>SecondaryDevStatus</p></td>
<td><p>Structure to hold secondary boot device status. For SDMMC, the following applies:</p>
<table>
<thead>
<tr class="header">
<th><p>Offset</p></th>
<th><p>Size</p></th>
<th><p>Field</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x00</p></td>
<td><p>0x01</p></td>
<td><p>FuseDataWidth</p></td>
</tr>
<tr class="even">
<td><p>0x01</p></td>
<td><p>0x01</p></td>
<td><p>FuseVoltageRange</p></td>
</tr>
<tr class="odd">
<td><p>0x02</p></td>
<td><p>0x01</p></td>
<td><p>FuseDisableBootMode</p></td>
</tr>
<tr class="even">
<td><p>0x03</p></td>
<td><p>0x01</p></td>
<td><p>FuseDdrMode</p></td>
</tr>
<tr class="odd">
<td><p>0x04</p></td>
<td><p>0x01</p></td>
<td><p>DiscoveredCardType</p></td>
</tr>
<tr class="even">
<td><p>0x05</p></td>
<td><p>0x03</p></td>
<td><p>Reserved</p></td>
</tr>
<tr class="odd">
<td><p>0x08</p></td>
<td><p>0x04</p></td>
<td><p>DiscoveredVoltageRange</p></td>
</tr>
<tr class="even">
<td><p>0x0C</p></td>
<td><p>0x01</p></td>
<td><p>DataWidthUnderUse</p></td>
</tr>
<tr class="odd">
<td><p>0x0D</p></td>
<td><p>0x01</p></td>
<td><p>PowerClassUnderUse</p></td>
</tr>
<tr class="even">
<td><p>0x0E</p></td>
<td><p>0x01</p></td>
<td><p>AutoCalStatus</p></td>
</tr>
<tr class="odd">
<td><p>0x0F</p></td>
<td><p>0x01</p></td>
<td><p>Reserved</p></td>
</tr>
<tr class="even">
<td><p>0x10</p></td>
<td><p>0x10</p></td>
<td><p>Cid</p></td>
</tr>
<tr class="odd">
<td><p>0x20</p></td>
<td><p>0x04</p></td>
<td><p>NumPagesRead</p></td>
</tr>
<tr class="even">
<td><p>0x24</p></td>
<td><p>0x04</p></td>
<td><p>NumCrcErrors</p></td>
</tr>
<tr class="odd">
<td><p>0x25</p></td>
<td><p>0x01</p></td>
<td><p>BootFromBootPartition</p></td>
</tr>
<tr class="even">
<td><p>0x27</p></td>
<td><p>0x15</p></td>
<td><p>Reserved</p></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td><p>0xEC</p></td>
<td><p>0x04</p></td>
<td><p>UsbChargingStatus</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0xF0</p></td>
<td><p>0x04</p></td>
<td><p>SafeStartAddr</p></td>
<td><p>Pointer to the end of the BCT in IRAM (0x40002900).</p></td>
</tr>
<tr class="odd">
<td><p>0xF4</p></td>
<td><p>0x0C</p></td>
<td><p>Padding</p></td>
<td><p>Must be empty.</p></td>
</tr>
</tbody>
</table>

# Carveouts

The MC (Memory Controller) provides multiple configurable memory
carveouts which allow to protect and limit access to sensitive DRAM
regions. Carveouts work on the physical access level, thus acting as the
last protection barrier from unauthorized memory accesses.

A total of 9 programmable carveouts are available from which 4 have a
fixed function (TZDRAM, VPR, SEC and MTS) and 5 are generalized
carevouts (GSCs 1 to 5).

## TZDRAM Carveout

Defines a DRAM region that can only be accessed by TrustZone-secure
clients. Currently unused by the Switch.

This carveout is controlled by the following MC registers:

    MC_SECURITY_CFG0
    MC_SECURITY_CFG1
    MC_SECURITY_CFG3

## VPR Carveout

Defines a DRAM region that can only be accessed by clients that are part
of the video decode and display process (Display, GPU, TSEC, VIC, NVENC,
NVDEC and HDA). Currently unused by the Switch.

This carveout is controlled by the following MC registers:

    MC_VIDEO_PROTECT_GPU_OVERRIDE_0
    MC_VIDEO_PROTECT_GPU_OVERRIDE_1
    MC_VIDEO_PROTECT_BOM
    MC_VIDEO_PROTECT_SIZE_MB
    MC_VIDEO_PROTECT_REG_CTRL

## SEC Carveout

Defines a DRAM region that can only be accessed by the
[TSEC](#TSEC "wikilink"). Deprecated and unused by the Switch.

This carveout is controlled by the following MC registers:

    MC_SEC_CARVEOUT_BOM
    MC_SEC_CARVEOUT_SIZE_MB
    MC_SEC_CARVEOUT_REG_CTRL

## MTS Carveout

Defines a DRAM region for Falcon microcode. Deprecated and unused by the
Switch.

This carveout is controlled by the following MC registers:

    MC_MTS_CARVEOUT_BOM
    MC_MTS_CARVEOUT_SIZE_MB
    MC_MTS_CARVEOUT_ADR_HI
    MC_MTS_CARVEOUT_REG_CTRL

## Generalized Carveouts

These carveouts can be freely configured for any client that supports
them.

These carveouts are controlled by the following MC registers:

    MC_SECURITY_CARVEOUT1/2/3/4/5_BOM
    MC_SECURITY_CARVEOUT1/2/3/4/5_BOM_HI
    MC_SECURITY_CARVEOUT1/2/3/4/5_SIZE_128KB
    MC_SECURITY_CARVEOUT1/2/3/4/5_CLIENT_ACCESS0
    MC_SECURITY_CARVEOUT1/2/3/4/5_CLIENT_ACCESS1
    MC_SECURITY_CARVEOUT1/2/3/4/5_CLIENT_ACCESS2
    MC_SECURITY_CARVEOUT1/2/3/4/5_CLIENT_ACCESS3
    MC_SECURITY_CARVEOUT1/2/3/4/5_CLIENT_ACCESS4
    MC_SECURITY_CARVEOUT1/2/3/4/5_CLIENT_FORCE_INTERNAL_ACCESS0
    MC_SECURITY_CARVEOUT1/2/3/4/5_CLIENT_FORCE_INTERNAL_ACCESS1
    MC_SECURITY_CARVEOUT1/2/3/4/5_CLIENT_FORCE_INTERNAL_ACCESS2
    MC_SECURITY_CARVEOUT1/2/3/4/5_CLIENT_FORCE_INTERNAL_ACCESS3
    MC_SECURITY_CARVEOUT1/2/3/4/5_CLIENT_FORCE_INTERNAL_ACCESS4
    MC_SECURITY_CARVEOUT1/2/3/4/5_CFG0

### GSC1

This carveout is, by default, for NVDEC. In the Switch's case, this
carveout is not used.

It is configured as follows:

    *(u32 *)MC_SECURITY_CARVEOUT1_BOM = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_BOM_HI = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_SIZE_128KB = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_CLIENT_ACCESS0 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_CLIENT_ACCESS1 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_CLIENT_ACCESS2 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_CLIENT_ACCESS3 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_CLIENT_ACCESS4 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_CLIENT_FORCE_INTERNAL_ACCESS0 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_CLIENT_FORCE_INTERNAL_ACCESS1 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_CLIENT_FORCE_INTERNAL_ACCESS2 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_CLIENT_FORCE_INTERNAL_ACCESS3 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_CLIENT_FORCE_INTERNAL_ACCESS4 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT1_CFG0 = 0x4000006;

### GSC2

This carveout is, by default and in the Switch's case, for the GPU
(WPR1).

It is configured as follows:

    *(u32 *)MC_SECURITY_CARVEOUT2_BOM = 0x80020000;
    *(u32 *)MC_SECURITY_CARVEOUT2_BOM_HI = 0;
    *(u32 *)MC_SECURITY_CARVEOUT2_SIZE_128KB = 2;
    *(u32 *)MC_SECURITY_CARVEOUT2_CLIENT_ACCESS0 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT2_CLIENT_ACCESS1 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT2_CLIENT_ACCESS2 = 0x3000000;
    *(u32 *)MC_SECURITY_CARVEOUT2_CLIENT_ACCESS3 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT2_CLIENT_ACCESS4 = 0x300;
    *(u32 *)MC_SECURITY_CARVEOUT2_CLIENT_FORCE_INTERNAL_ACCESS0 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT2_CLIENT_FORCE_INTERNAL_ACCESS1 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT2_CLIENT_FORCE_INTERNAL_ACCESS2 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT2_CLIENT_FORCE_INTERNAL_ACCESS3 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT2_CLIENT_FORCE_INTERNAL_ACCESS4 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT2_CFG0 = 0x440167E;

### GSC3

This carveout is, by default, for the GPU (WPR2). In the Switch's case,
this carveout is not used.

It is configured as follows:

    *(u32 *)MC_SECURITY_CARVEOUT3_BOM = 0;
    *(u32 *)MC_SECURITY_CARVEOUT3_BOM_HI = 0;
    *(u32 *)MC_SECURITY_CARVEOUT3_SIZE_128KB = 0;
    *(u32 *)MC_SECURITY_CARVEOUT3_CLIENT_ACCESS0 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT3_CLIENT_ACCESS1 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT3_CLIENT_ACCESS2 = 0x3000000;
    *(u32 *)MC_SECURITY_CARVEOUT3_CLIENT_ACCESS3 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT3_CLIENT_ACCESS4 = 0x300;
    *(u32 *)MC_SECURITY_CARVEOUT3_CLIENT_FORCE_INTERNAL_ACCESS0 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT3_CLIENT_FORCE_INTERNAL_ACCESS1 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT3_CLIENT_FORCE_INTERNAL_ACCESS2 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT3_CLIENT_FORCE_INTERNAL_ACCESS3 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT3_CLIENT_FORCE_INTERNAL_ACCESS4 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT3_CFG0 = 0x4401E7E;

### GSC4

This carveout is, by default, for TSECA. In the Switch's case, this
carveout is used by the Kernel.

It is initially configured as follows:

    *(u32 *)MC_SECURITY_CARVEOUT4_BOM = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_BOM_HI = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_SIZE_128KB = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_CLIENT_ACCESS0 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_CLIENT_ACCESS1 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_CLIENT_ACCESS2 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_CLIENT_ACCESS3 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_CLIENT_ACCESS4 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_CLIENT_FORCE_INTERNAL_ACCESS0 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_CLIENT_FORCE_INTERNAL_ACCESS1 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_CLIENT_FORCE_INTERNAL_ACCESS2 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_CLIENT_FORCE_INTERNAL_ACCESS3 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_CLIENT_FORCE_INTERNAL_ACCESS4 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT4_CFG0 = 0x8F;

Then further configured using
[smcConfigureCarveout](SMC#ConfigureCarveout.md##ConfigureCarveout "wikilink").

### GSC5

This carveout is, by default, for TSECB. In the Switch's case, this
carveout is reserved for the Kernel.

It is initially configured as follows:

    *(u32 *)MC_SECURITY_CARVEOUT5_BOM = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_BOM_HI = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_SIZE_128KB = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_CLIENT_ACCESS0 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_CLIENT_ACCESS1 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_CLIENT_ACCESS2 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_CLIENT_ACCESS3 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_CLIENT_ACCESS4 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_CLIENT_FORCE_INTERNAL_ACCESS0 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_CLIENT_FORCE_INTERNAL_ACCESS1 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_CLIENT_FORCE_INTERNAL_ACCESS2 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_CLIENT_FORCE_INTERNAL_ACCESS3 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_CLIENT_FORCE_INTERNAL_ACCESS4 = 0;
    *(u32 *)MC_SECURITY_CARVEOUT5_CFG0 = 0x8F;

It can be further configured using
[smcConfigureCarveout](SMC#ConfigureCarveout.md##ConfigureCarveout "wikilink"),
but it's currently unused.
