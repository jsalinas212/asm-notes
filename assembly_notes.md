## 8086 Registers (16 Bit CPU)

Registers are memory space in CPUs that are 100x faster than RAM and 1000x faster that HDDs.

General Purpose Registers (GPR)

- AX [AH - High Byte, AL - Low Byte] 
- BX [BX, BL]
- CX [CH, CL]
- DX [DH, DL]

AX and DX are used for explicit stuff. BX used by C++ for something specific. You have to PUSH and POP BX to use. CX used as counter and in loops. Any can be used for math and loops, however.

Index Registers

- SI (Source Index)
- DI (Destination Index)
- BP (Base Pointer)
- SP (Stack Pointer)

SI and DI used in string comparisons and searching. No byte version on 8086. BP and SP automatic and used by stack function calls and returns.

Instruction Pointer (Program Counter)

- IP

Point in RAM where instructions are read from for execution. When you call a function, you change value of IP.

Segment Registers

- CS
- DS
- ES
- SS

Used by OS for paging and threading. Segmented memory no longer used in modern computing. Flat memory is used.

Flag Registers

- Flags

Stores the state of comparisons and other instructions to act on that information.

## 80386 Registers (32 bit CPU)

Backward compatible with 8086 16 bit registers, but the registers also have a 32 bit version. 32 bit versions have the same names but with an E in front of them.

- EAX
- EBX
- ECX
- EDX

The initial X is the low 16 bits (CX, for example, same as CL, and CH would be high 16 bits for a total of 32 bits).

- ESI
- EDI
- EBP
- ESP

- EIP

32 bit instruction pointer.

- eFlags

Segment Registers

- CS
- DS
- ES
- SS
- FS
- GS

Still  not used for modern computing.

## 64 Bit Processing

Same names, but with R at the front instead of E.

- RAX (R1)
- RBX (R2, etc...)
- RCX
- RDX
- RSI
- RDI
- RSP
- RBP
- RIP
- R8
- R9
- R10
- R11
- R12
- R13
- R14
- R15
- RFlags

Can now use low bytes with Index Registers. the R# registers can access 32 bit by specifying R#D. D is DWORD (32 bit), but you can specify W (Word/16 bit), or B (Byte/8 Bit). RAX middle alpha is kept for backward compatibility, but is technically R1D. Normal to use 32 bit will zero the top of 64 bit.

## Fundamental Data Types

Most will allow using structs, but CPU itself only knows few int types and few float types.

Ints:

- byte (0 to 255 unsigned)
- word (0 to 65535 unsigned)
- dword (0 to 2^32 unsigned)
- qword (0 to 2^64 unsigned)

Floats: (IEEE754)

- real4
- real8
- real10 (x87 FPU only)

SIMD Pointers: (Packed versions of Ints and Floats.)

- xmmword (128 bits, SSE packed)
- ymmword (256 bits, AVX packed)
- zmmword (512 bits, for AVX512)

Signed vs Unsigned (No type safety, up to programmer.)

DIV and MUL vs iDIV and iMUL. ADD and SUB there is no difference.

Two's Complement: Most significant bit (left-most) is the sign bit. Number is positive if sign bit is 0 and negative if 1. If sign bit is 1, value represented is negative and logical complement of pattern is incremented.

MOV and LEA are used to move data around.

MOV takes two operands of the same size and moves (copies) from source to destination.

MOV dest, src

Does not change Flags.
If both are same reg, acts as NOP

Can't MOV memory to memory.

LEA (Load Effective Address)

Load effective address of variable to create a pointer.

LEA dest, src

## Flags

| 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|  | NT | IOPL | OF | DF | IF | TF | SF | ZF |  | AF |  | PF |  | CF |

Only 0 to 15, the rest are reserved and/or sys flags.

- Carry Flag is an undersigned overflow. 1 means overflow on left-most bit.
- Parity Flag is not very useful. Error checking bit or odd even.
- Auxiliry Flag is not useful. Overflow on lowest nibble.
- Zero Flag is very useful. RTFM. Last result was 0. Useful for comparisons.
- Sign Flag. Tells you if result is either negative or positive.
- Direction Flag. Determines direction of string instructions (Forward or Backwards, stp or cld).
- Overflow Flag. Signed overflow. Overflow on 2nd from left bit.
- Trap Flag.
- Interupt Flag.

Repeatedly used memory addresses are cached in CPU L1 or L2 cache.