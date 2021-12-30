# Overview Kernel System Call ABIs

*Brief overview over the syscall ABIs of different kernels.*

System calls, or somtimes called Hypercalls, have different 
ABIs on different platforms and kernels. This is a brief 
overview over the most important systems. It shows what 
registers are used for parameter passing, when a syscall happens.

# x86_64 (with `sysenter` instruction)

|             | Syscall Number | Arg 0 | Arg 1 | Arg 2 | Arg 3 | Arg 4 | Arg 5 | Comment                                                                                                                                                                                             |
|-------------|----------------|-------|-------|-------|-------|-------|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Linux       | `rax`          | `rdi` | `rsi` | `rdx` | `r10` | `r8`  | `r9`  | Source: <https://github.com/torvalds/linux/blob/35776f10513c0d523c5dd2f1b415f642497779e2/arch/x86/entry/entry_64.S> System V x86_64 Calling Convention except for Arg 3                             |
| XNU (MacOS) | `rax`          | `rdi` | `rsi` | `rdx` | `rcx` | `r8 ` | `r9`  | Source: <https://github.com/apple/darwin-xnu/blob/a1babec6b135d1f35b2590a1990af3c5c5393479/osfmk/i386/x86_hypercall.h#L38> System V x86_64 Calling Convention                                       |
| Windows NT  | ?              | ?     | ?     | ?     | ?     | ?     | ?     | Can't find good resource. Perhaps Microsoft likes to changes system call parameters (and the ABI?) often. That's the reason why all applications are programmed against NTDLL.                      |
| NOVA/Hedron | `rdi`          | `rdi` | `rsi` | `rdx` | `rax` | `r8`  | `rcx` | Source: <https://github.com/udosteinberg/NOVA/blob/arm/inc/x86_64/regs.hpp#L51> rdi holds the sys call number in the 4 first bits. Bits 4-63 have a different meaning depending on the system call. |
| Xen         | `rax`          | `rdi` | `rsi` | `rdx` | `r10` | `r8`  | `r9`  | Source: <https://github.com/xen-project/xen/blob/master/xen/arch/x86/x86_64/entry.S#L235> System V x86_64 Calling Convention except for Arg 3                                         |

