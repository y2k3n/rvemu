# RVEMU
This is a software emulator for RV32I user-level ISA.

## Usage:
1. Compile exectuable that runs on bare metal, using custom linker script and startup code.  
   ``` riscv32-unknown-elf-gcc -s -ffreestanding -nostartfiles -Tlink.ld startup.s example.c -o rvelf ```  
   You'll need a RV32I cross compiler. https://github.com/stnolting/riscv-gcc-prebuilt provides one for x64 Linux.

3. Convert the elf file to a C header file.  
   ``` xxd -i rvelf > rvelf.h ```

5. Compile the main program and run.  
   ``` gcc main.c io.c -o main && ./main ```

The example program prints first 10 terms of the Fibonacci sequence.
