# RVEMU
This is a software emulator for RV32I user-level ISA.

## Usage:
1. Compile exectuable that runs on bare metal, using custom linker script and startup code.  
   ` riscv32-unknown-elf-gcc -s -ffreestanding -nostartfiles -Tlink.ld startup.s example.c -o rvelf `  
   You'll need a RV32I cross compiler. [Here](https://github.com/stnolting/riscv-gcc-prebuilt) provides one for x64 Linux.

3. Convert the elf file to a C header file.  
   ` xxd -i rvelf > rvelf.h `

5. Compile the main program and run.  
   ` gcc main.c io.c -o main && ./main `

The example program prints first 10 terms of the Fibonacci sequence.

Refer to the example program for input and output with ` ecall `.  
Here's a table of available ` ecall `s. Some of them need a real DE1-SoC Nios II environment or the [CPUlator](https://cpulator.01xz.net/?sys=nios-de1soc) simulator since they use DE1-SoC I/O devices.
| a0 (Decimal) | Description | a1 |
|--------------|-------------|----|
| 0 | exit with status code | int: status code |
| 100 | print an integer to terminal | int: number |
| 101 | print a null-terminated string to terminal | char*: string address |
| 103 | print all registers to terminal | N/A |
| 200 | read DE1-SoC switches | returned switches value |
