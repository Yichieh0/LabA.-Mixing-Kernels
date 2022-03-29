# Mixing-Kernels
# Mixing-Kernels
‧Tools
Version : Vitis 2021.2 with xilinx_u50_gen3x16_xdma_201920_3
Version : Vivado 2021.2 with xilinx_u200

This Lab is about mixing RTL kernels, it follows the Xilinx Vitis tutorials :
https://github.com/Xilinx/Vitis-Tutorials/tree/2021.2/Hardware_Acceleration/Feature_Tutorials/01-rtl_kernel_workflow
https://github.com/Xilinx/Vitis-Tutorials/tree/2021.2/Hardware_Acceleration/Feature_Tutorials/02-mixing-c-rtl-kernels

	In the previous lab, we practiced how to do emulation using C++ kernels. Actually, we also can build kernels in C, OpenCL or RTL code. All types of Kernels will be packaged into object file (.xo). This is a brief introduction to how to put RTL kernels into your design.
	There are two main aspects to this topic :
‧Mixing C++ and RTL Kernels
This part will be divided into two steps : 
1. C++ Kernel only
	In this step, we’ll need the followings source code:
-> C++ Kernel : krnl_vadd.cpp
-> Host : host_step1.cpp
	Follows the vitis flow in Lab3, we can easily done the software and hardware emulation.

2. Mixing Kernel
	In this step, we’ll need the followings source code:
-> C++ Kernel : krnl_vadd.cpp, rtl_kernel_wizard_0.cpp
	  -> RTL Kernel : rtl_kernel_wizard_0.xo
	  -> Host : host_step2.cpp
Before we begin step 2, we have to generate a default RTL kernel for host code :
a. Build an empty Vitis application projec
b. Xilinx >> Launch RTL Kernel Wizard 
c. General Settings – keep all the options default
d. Scalars – set the scalar argument into 0
e. Global Memory – keep all the options default
f. Streaming Interface – keep all the options default
g. Summary – check the design fit the requirement
h. Packing – generate the object file
After follows all the steps above, we can finally get our default object file. It will be automatically added into the vitis project.

-Report
Remind that RTL kernel can only tested by doing hardware emulation. You should have an equivalent C++ kernel for software emulation.

. software emulation

- C++ kernel software emulation timeline trace

![image](https://raw.githubusercontent.com/Yichieh0/LabA.-Mixing-Kernels/main/report/C%20kernel%20software%20emulation%20timeline%20trace.jpg?token=GHSAT0AAAAAABS6VEEEPPNZW2QA7HRNNSAIYSCNBWQ)

- Mixing kernels software emulation timeline trace

![image](https://raw.githubusercontent.com/Yichieh0/LabA.-Mixing-Kernels/main/report/Mixing%20kernels%20software%20emulation%20timeline%20trace.png?token=GHSAT0AAAAAABS6VEEFVY25ZYTOWYKRRH2EYSCM3NQ)

. hardware emulation

- C++ kernel hardware emulation timeline trace

![image](https://raw.githubusercontent.com/Yichieh0/LabA.-Mixing-Kernels/main/report/C%2B%2B%20kernel%20hardware%20emulation%20timeline%20trace.png?token=GHSAT0AAAAAABS6VEEE5KVYOHK4YRYNJOICYSCNCPQ)

- Mixing kernels hardware emulation timeline trace

![image](https://raw.githubusercontent.com/Yichieh0/LabA.-Mixing-Kernels/main/report/Mixing%20kernels%20hardware%20emulation%20timeline%20trace.png?token=GHSAT0AAAAAABS6VEEFQQHWMDE67N3DGQEEYSCM3EQ)

‧(.xo) packaging
In the lab we mentioned above, we added the default RTL kernel generated by vitis RTL Kernel Wizard. In this chapter, two ways to package RTL design to Xilinx object file (.xo) will be introduced. For an easy B=A+B kernel, we can build it by the following steps :
-Package IP/Package XO flow

a. Build an empty vivado RTL project

b. Add kernel source into project

c. Tools >> Create and Package New IP

d. Select Package your own current project

e. Browse the IP address

f. Click the Finish button

g. Open the IP Packager

h. Specify the Control Protocol

i. Edit Ports and Interfaces

j. Repeat the process to associate ap_clk with the m01_axi interface, and the s_axi_control interface.

k. Add Control Registers and Address Offsets

l. Check Integrity, Assign Properties, and Package IP

- RTL Kernel Wizard flow

a. Build an empty Vitis application project

b. Xilinx >> Launch RTL Kernel Wizard 

c. General Settings – named the kernel and set the interface to ap_ctrl_chain

d. Scalars – keep all the options default

e. Global Memory – set the interface number to 2, and named the Argument

f. Streaming Interface – keep all the options default

g. Summary – check the design fit the requirement

h. Packing – generate the object file

