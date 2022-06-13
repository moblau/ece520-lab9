# Lab 9 - HW and SW Debugging - Part 1

## Introduction
The purpose of Lab 9 is to get practice with using the integrated logic analyzer and virtual input and output in Vivado. Part 1 is done entirely in Vivado and has no software component in Vitis. 

A binary counter is implented with an IP and connected to the 4 LEDs on the Zybo. The VIO output enables and disables the counter. The status of the counter is displayed in the ILA. 

## Procedure
The two steps to completing this lab are building the block design and mapping the pins of the block design to the hardware on the Zybo. A binary counter IP, ILA IP, VIO IP, Clock Wizard IP, and Slice IP were added to the block design. The output of the binary counter was connected to the input of the ILA and VIO. The output of the VIO was connected the clock enable of the binary counter. The block design is shown in Figure 9.1

![block design](/img/bd.png)  
**Figure 9.1:**: Block Design for Lab 9, Binary Counter

## Results
![vio](/img/vio.png)
**Figure 9.2**: Virtual input and output showing the status of the counter and the virtual output enabling the counter

![ila](/img/ila.png)
**Figure 9.3**: Integrated logic analyzer showing the binary counter incrementing

The video demo is [here](https://youtu.be/oSLDtp9R5qk)

## Conclusion
Lab 9 Part 1 helped me practice the workflow of implementing a block desing and mapping pins to the hardware. The ILA and VIO can be helpful in larger, real world applciations of FPGAs.