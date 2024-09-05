# Design
The design of the processor

## Registers

### General Purpose Registers (GPRs)
The main 64-Bit registers are just a 64-Bit unsigned register.

* `Sx0`: A GPR also used for the accumulator register in arithmetic operation
* `Sx1`: A GPR also used for the index register in loops etc.
* `Sx2`: A GPR also used for a jump address register so it jumps to that address.
* `Sx3-SxF` Just GPRs

### System Registers
Some registers will be very important to the system like the stack pointers

* `IP`: The instruction pointer only readable not writeable
* `SP`: The stackpointer that points to the current address of the stack
* `SBP`: Stack Base Pointer points to the base address of the stack
* `SMP`: Stack Max Pointer contains the maximal address of the stack to prevend a bit of stack corruption
* `CR`: Control Register for entering system variables like some flags for the `FLAGS` register
* `FLAGS`: Contains flags of the current processor state

### Structure Registers
There are registers for "structures" like the Memory Segmentation Table

* `MSTP`: The Pointer that points to the start address of the Memory Segmentation Table (MST)

## Memory Management

### Paging
TODO: Paging :skull:

## Opcodes
* `0x00`: `NOP` No Operation
* `0x01`: `MOV` Move a value from one register to another
    * `MOV op1, op2` op1 can be a register or a memory address, op2 can be a register or a value or a memory address 
    * op2 -> op1
* `0x02`: `ADD` Add two values
    * `ADD op1, op2` op1 can be a register or a memory address, op2 can be a register or a value or a memory address and puts the result into `Sx0`
    * `Sx0` = op1 + op2
* `0x03`: `SUB` Subtract two values
    * `SUB op1, op2` op1 can be a register or a memory address, op2 can be a register or a value or a memory address and puts the result into `Sx0`
    * `Sx0` = op1 - op2
* `0x04`: `MUL` Multiply two values
    * `MUL op1, op2` op1 can be a register or a memory address, op2 can be a register or a value or a memory address and puts the result into `Sx0`
    * `Sx0` = op1 * op2
* `0x05`: `DIV` Divide two values
    * `DIV op1, op2` op1 can be a register or a memory address, op2 can be a register or a value or a memory address and puts the result into `Sx0`
    * `Sx0` = op1 / op2
* `0x06`: `JMP` Jump to a specific address
    * It will jump to the address in the `Sx2` register
* `0x07`: `JE` Jump if equal
    * `JE op1, op2` op1 can be a register or a memory address, op2 can be a register or a value or a memory address
    * If op1 == op2 then jump to the address in the `Sx2` register
* `0x08`: `JNE` Jump if not equal
    * `JNE op1, op2` op1 can be a register or a memory address, op2 can be a register or a value or a memory address
    * If op1 != op2 then jump to the address in the `Sx2` register
* `0x09`: `HLT` Halt the processor
    * Stops the processor
* `0x0A`: `PUSH` Push a value to the stack
    * `PUSH op1` op1 can be a register or a memory address
    * Pushes the value of op1 to the stack
* `0x0B`: `POP` Pop a value from the stack
    * `POP op1` op1 can be a register or a memory address
    * Pops the value from the stack to op1
* `0x0C`: `INT`: Interrupt
    * `INT op1` op1 can be a register or a memory address
    * Calls an interrupt with the number of op1
