# Overview

Like most D3D11-era GPUs the Tegra X1 has 5 pipeline shader stages:
Vertex, tessellation control, tessellation evaluation, geometry and
fragment. Maxwell GPUs have two vertex shader stages: A and B, using
both is not mandatory or common. There are also compute shaders or
kernels which run on a separate channel.

## Header

Pipeline stage shaders unlike compute kernels have a header documented
by
Nvidia[1](https://download.nvidia.com/open-gpu-doc/Shader-Program-Header/1/Shader-Program-Header.html).
It is a 0x50 byte structure that describes shader's behavior and enabled
features that don't belong to the code itself (e.g. local memory size,
whether it writes global memory). Some of these entries are not
mandatory and are not emitted by Nvidia's compiler.

It is located at the beginning of the program address. Program code
starts right after it (at address 0x50, address 0 on compute kernels).

## Text

Every 4 instructions starting from the first one there's a scheduler
instruction. All instructions are 64 bits long, including scheduler
instructions.

Shaders emitted by Nvidia's compiler include a branching instruction
pointing to itself after the final unconditional exit. The intention of
this "sign" is unknown.

## Registers

Maxwell GPUs have 255 type-less general purpose registers and one
special register with id 255, *nvdisasm* shows it as RZ and *envydis* as
0x0. Writing here is a no-op unless there are side effects. Reading from
RZ returns zero. The fewer registers a shader uses, the more it can be
parallelized.

General purpose registers or GPRs are 32 bits long and are the same for
all operations, these are given meaning on the instructions. Half float
instructions are SIMD and operate on 16 bit pairs, meanwhile double
instructions take two registers to operate. uint64 values are emulated
using uint32 instructions extending their domain through condition
codes; when an instruction has to read an uint64 value it reads two
subsequent registers.

It is a common technique to read or write subsequent registers with a
single instruction. For example TEXS (used to sample a texture) reads
the texture coordinates from Ra and Ra+1, although it gets more complex
with other layouts like 3D textures (it's not Ra+2). The result of the
sample is given in an Rd and their subsequent registers.

TODO Add nvdisasm example

## Predicates

There are 6 general purpose "1-bit" predicates. These can be used to
conditionally execute a given instructions. There is an extra predicate
that always evaluates as true (and false when negated), writing here is
a no-op unless there are side-effects. It is shown as "PT" in
*nvdisasm*.

Most of the time predicates can be negated.

TODO Add nvdisasm example

## Condition codes

These mostly match x86 condition codes. They are explicitly set by
instructions with a ".CC" flag or by special instructions like R2P.

These can be analyzed with the P2R instruction (which moves predicates
or condition codes to a register).

# Analysis Tools

## Disassembling

To disassemble a Maxwell shader or compute kernel there are two
applications:

  - nvdisasm[2](https://developer.nvidia.com/cuda-toolkit)
  - envydis[3](https://github.com/envytools/envytools/tree/master/envydis)

### nvdisasm

Nvidia's disassembler. Since it's made by Nvidia it usually knows more
instruction variants. It tends to print the intention of the
instructions rather than their internal encoding, helping visual
inspection. It can show the binary representation with an option.

One of its major problems is that the input file has to be perfectly
aligned with a stride of 0x20 bytes or it will otherwise fail. Appending
zeroes to the file will make it happy since those are NOP instructions.
Invalid instructions will also abort the disassemble.

To disassemble a Maxwell shader or kernel in a file this command can be
used:

$ nvdisasm -b SM53 <file>

For more information about this program it's recommended to read its
help entry and CUDA Toolkit
Documentation[4](https://docs.nvidia.com/cuda/cuda-binary-utilities/).

### envydis

*envydis* is nouveau's assembler and disassembler. Unlike Nvidia's
disassembler this one doesn't care about alignment or invalid
instructions, so it is useful to analyze a raw memory dump while
searching for a shader or kernel. Its declarative-style C
file[5](https://github.com/envytools/envytools/blob/master/envydis/gm107.c)
describes instructions internal encoding.

To disassemble with it:

$ envydis -m gm107 -i <file>

*envydis* also has an assembler variant: *envyas*. To edit existing
shaders or write shaders from scratch this is easier than assembling the
bits manually.

Since it's the product of reverse engineering the GPU and *nvdisasm*
itself, it might contain errors.

## Dumping existing shaders

One method to dump shaders from commercial games and homebrew
applications is running it on an emulator.

Ryujinx[6](https://ryujinx.org/#/) offers in its configuration file an
entry to dump the encountered shaders in two directories. *Code*
contains shader dumps that are compatible with 'nvdisasm' and 'envydis'
as they are. *Full* is the same as *Code* but it includes the header,
it's intended to be decompiled with *Ryujinx.ShaderTools*.

yuzu[7](https://yuzu-emu.org/) can dump shaders using its disk-based
shader cache with an external tool.
*maxwell-dump*[8](https://gist.github.com/ReinUsesLisp/7ba72d3162e60cab283194fcca3474b2)
is a small C application for this, it follows the same convention as
Ryujinx for *Code* and *Full*. To find the shader file dumped by the
emulator, right click the game from the Qt front-end and select the
option to view the transferable cache file. It's important to highlight
that the file format might change in the future leaving this tool unable
to extract the binaries until it's updated.

# Maxwell Instruction Set Architecture

TODO Define instructions
