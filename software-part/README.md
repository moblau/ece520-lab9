# Lab 9 - HW and SW debugging, Part 2

## Introduction
The purpose of Lab 9, Part 2 is to introduce the use of the TCF profile and G Profile. The TCF profile can simply be added to the running program in the debug section of Vitis. For the G Profile, there are several steps required to prepare the processor to be interrupted by the G Profiler. The lab shows that the FIR filter impleneted in the FPGA fabric is much faster than the FIR filter implemented on the processor. 

## Procedure
The first step in the lab is to create the block design in Vivado with the two FIR filter IPs that were imported from github. 

![block design](/img/bd.png)
**Figure 9.1:** Block design created in Vivado for Lab 9, part 2 Profiling

The .xsa file is opened in Vitis and the source code from github was imported to the application. The TCF Profiler was enabled in the debug window and then monitored in the TCF Profiler window. Next, the settings were configured to enable software and hardware profiling. The hardware profile showed that the FPGA filter worked much faster than the software filter. The hardware filter was monitored with different sampling frequencies in the profiling. This can be seen in a table in the Questions section.

## Results

Results for TCF Profile, SW G Profile and HW G Profile can be seen [here](https://youtu.be/nSV6Qppw2dU)

## Questions
2. What change do you see in lab7.c source file as a result of this step?
   1. The change is happens from the preprocessor. When the SW_Profile flag is set, the fir_software() function gets exectuted. When it is not set, the filter_hw_accel_input() function gets exectued.
3. Present a table/graph and compare your results. Write your conclusion from applying different sampling frequency to the profiling process. Is there any relationship between the number of samples taken and number of function calls? How about other factors? Explain exactlyhow profiling is affected by sampling frequency? What is more accurate; lower sampling rate or higher sampling rate? What happens if sampling rate is decreases to its minimum possible? What happens if sampling rate is decreases to its maximum possible

| Sample Frequency | Name | Samples | Calls | Time/Call | % Time |
| ---------------- | ---- | ------- | ----- | --------- | ------ |
| 10000  | filter_hw_accel_input | 2 | 60 | 3.333us | 0.11% |
| 100000 | filter_hw_accel_input | 8 | 60 | 1.333us | 0.04% |
| 500000 | filter_hw_accel_input | 69 | 60 | 2.299us | 0.29% |

4. What change do you see in lab7.c source file as a result of this step?
   1. See answer to question 2.
5. Write your conclusion from applying different sampling frequency to the profiling process. Is there any relationship between the number of samples taken and number of function calls? How about other factors? Explain exactly how profiling is affected by sampling frequency? What is more accurate; lower sampling rate or higher sampling rate? What happens if sampling rate is  decreases to its minimum possible? What happens if sampling rate is decreases to its maximum possible?
   1. THe number of samples increases as the sample frequency increases.The time/call is fastest at 100KHz sample frequency. The % Time is largest for the largest sample frequency, 500KHz.
6. How does software profiling compare to hardware profiling? Elaborate your answer. Has the number of calls changed? Why or why not? Has the time changed? Why or why not?
   1. In the software profiling, the filter works much slower. The processor has to step through each line of code and run its algorithm. In the hardware profiling, the processor simply hands the data over to the PL and the PL returns it really quickly. 
7. What is the most noticeable change in the hardware profile compared to software profile?
   1. The most noticeably change is how much faster the hardware profile is compared to the software profile.
8. What is the reason for this significant reduction in average time spent per call as well as time spent for filtering function? Explain your answer. Find the ratio of the speed up for each sampling frequency while profiling the application. Explain your result using a table or graph.
   1. The programmable logic can work much faster in this case than the processor.
9.  Explain how FIR filter is integrated to the SDK project as a hardware accelerated HLS core? How does software communicate with the FIR core on FPGA fabric? What is being sent to the FIR core as input data and what do you expect to see as output?
    1.  The input data to the FPGA fabric is the input samples from the processor code. The FIR filter IP in the PL has the same filter coefficients than in the coefficients file in Vitis. 


## Conclusions
Part 2 of lab 9 taught me how I can use tools in Vitis to perform debugging on a system on chip application. The TCF Profile did not require much set up, and the G Profile was required a flag to be set in the compiler . Both of these types of debugging can be very useful in larger applications where you are trying to improve timing and efficieny of your application. 