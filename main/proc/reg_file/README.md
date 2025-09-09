# Register File
## Shelby Hartman

## Description of Design

The register file module is composed of 32 registers, each of which stores 32-bits using a D-flip flop. Each D-flip flop writes on the positive clock edge and can be reset to 0 using an asynchronous clear, called ctrl_reset in the main register file, which resets all registers at once. readRegA, readRegB, and writeReg addresses are all input into the register file, specifying which registers to read data from and write data to. 

Decoders take these 5-bit addresses and translate them into a 32-bit bus. For the decoder using the writeReg address, each wire in the bus goes to one of the registers and turns on its input enable. This then turns on the enable signal on each D-flip flop inside the register and writes in the input data signal, data_writeReg. A write enable control signal turns the decoder on and off, determining whether any data can be written to a register on a particular clock cycle. 

The decoders taking in readRegA and readRegB addresses also output to 32-bit buses where only one of the wires can be on at once. Each wire in the bus feeds into the enable of a tristate-buffer with its input connected to the output of one of the registers. This effectively acts as an output enable, selecting which register's outputs get read by the register file while restricting all the others. 

Every register except register 0 can be written to. Register 0 ignores any attempts to write data into it and always outputs 32'b0 when read. 

## Bugs
