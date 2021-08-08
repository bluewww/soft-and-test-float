# Soft and Test Float

Berkley [SoftFloat](http://www.jhauser.us/arithmetic/SoftFloat.html) and
[TestFloat](http://www.jhauser.us/arithmetic/TestFloat.html) for emulating and
testing floating point routines.

This repository combines both and adds explicit support for RISC-V.

For SoftFloat this mean the specialization of the software floating routines to
match RISC-V specified behavior.

For TestFloat this means adding a generic `RISCV` build target and a more
customised target named `RISCV-PULP`. The `RISCV` target tests the `f` and `d`
extensions, while the `RISCV-PULP` target additionaly tests `xfhalf` (half float
extension). This means the latter requires PULP GCC. Both targets currently
assume `rv32` and link against `newlib`.

`RISCV-PULP` is mainly used to test the softfloat routines in the gdb simulator
of PULP GCC. To do that make sure you have the PULP GCC Toolchain's binaries in
your `PATH` and then run:

```bash
cd SoftFloat-3e/build/Linux-RISCV-GCC
make all
cd ../../../TestFloat-3e/build/Embedded-PULP-GCC/
make all
riscv32-unknown-elf-run testfloat -rnear_even -all1
riscv32-unknown-elf-run testfloat -rnear_even -all2
```
