# COIN
A minimal instruction set computer (MISC) design. Implemented in [CALM](https://github.com/las-r/calm).

## Specifications
**RAM:** 64 KiB\
**Reg. File:** 16 registers (each register is `u8`, r0 tied to 0)\
**Call Stk.:** 8 addresses (16 B)\
**Data Pntr.:** `u16`\
**Inst. Pntr.:** `u16`

## Instructions
### Format
`[opc 4] [x 4] [y 4] [z 4]`

### Opcodes
| Opcode | Mnemonic | Description |
| --- | --- | --- |
| `0x0` | `LDI` | Rx = yz |
| `0x1` | `SHR` | Rx = (Ry >> Rz) |
| `0x2` | `CLL` | push IP; IP = data + Rx |
| `0x3` | `RET` | pop IP |
| `0x4` | `AND` | Rx = Ry & Rz |
| `0x5` | `NOR` | Rx = ~(Ry | Rz) |
| `0x6` | `ADD` | Rx = Ry + Rz |
| `0x7` | `SUB` | Rx = Ry - Rz |
| `0x8` | `JMP` | IP = yz + Rx |
| `0x9` | `OUT` | print ascii of RAM[DP] |
| `0xa` | `SKZ` | skip if Rx == 0 |
| `0xb` | `SKC` | skip if CARRY |
| `0xc` | `MVI` | DP = RyRz + Rx |
| `0xd` | `STO` | RAM[DP + Rx] = RyRz |
| `0xe` | `LOD` | Rx = RAM[DP + Ry] |
| `0xf` | `HLT` | halt clock |

## Other Notes
- Program is stored starting at 0x0, which is also where IP starts.
- DP starts at 0x400.
- Only arithmetic operations (`ADD`, `SUB`) update CARRY, `AND` and `NOR` do not.