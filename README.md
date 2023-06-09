# **CS 21 Project 2: Extending a 32-bit CPU Instruction Set**

## **Description**
For this project, our goal was to extend the MIPS 32-bit Single Cycle Processor (SCP) (Harris & Harris, 2013) instruction set. Main languages used were Verilog and SystemVerilog. Main IDE used was Xilinx Vivado.

A nuanced understanding of **Hardware Definition Language** (HDL) (specifically **SystemVerilog**) and digital circuits (especially the **controller**, **data path** and **arithmetic logic unit** components of a CPU) is key to succeeding on this project. We modified the processor to accomodate 5 new instructions:
1. Shift left logical (sll)
2. Store byte (sb)
3. Branch on less than or equal (ble)
4. Load immediate (li)
5. Zero-from-right (zfr)

Please see my **Documentation** intro (`For Submission\Documentation.pdf`) or the MIPS Green Sheet (`MIPS Green Sheet (Berkeley).pdf`) for the MIPS32 instruction formats. You may also consult Appendix B of Harris & Harris (2013) or the Project 2 Specs (please [email](yshebron@up.edu.ph) me for access) for the complete instruction set and their expected effect.

Our technical documentation skills were also sharpened by this project, one that required *line-by-line* explanation of code. Discussed in the documentation *per added instruction* are:
* HDL edits
* Testbench for simulations. 
* Test code (in assembly and in machine code) for verifying if the extended instruction set is working.
* Demonstration that the processor can now successfully execute the instruction required.

Extreme care was also taken to maintain the baseline integrity of the single cycle MIPS processor. That is, we extended the capability of the CPU *without breaking anything* in the process. The integrity checks are the testbenches `Simulation Sources\testbench.sv` with machine code `Simulation Sources\testbench.txt` and `Simulation Sources\testbench_2.sv` with machine code `Simulation Sources\testbench_2.txt`. The instruction memory component were also tested using the `imem_testbench`.

### **Quick Links**
- See `CS21_Project2_Specs.pdf` for full specifications. Please [email](yshebron@up.edu.ph) me for access. Promising quick response.
- Project Documentation in `For Submission\Documentation.pdf`.
- Link to Video Documentation [here](https://drive.google.com/file/d/1N0l3GV2r9BShghN13NfjL3-9g5s0T68J/view?usp=sharing).

## **Schematics**
Before the modifications, the SCP is only capable of handling R-type, lw, sw, and beq instructions, with the following schematic diagram (Harris & Harris, 2013):
![MIPS32_SCP_orig.png](MIPS32_SCP_orig.png)
After the modifications, the SCP is now also capable of sll, sb, ble, li, and zfr, with the following schematic diagram:
![MIPS32_SCP_final.png](MIPS32_SCP_final.png)
Full schematics can be found in `Circuit Diagrams.drawio` (draw.io needed).

## **Requirements**
It is suggested for you to only watch the video documentation or skim through the written documentation due to the project's tediousness. Design, simulation, and testbench files from the workbench (`CS21_Project2_v2\`) were also fetched for your quick reference. You may browse them in the directories `Design Sources\`, `Instruction Tests\` & `Simulation Sources\`, and `Testbenches\` respectively.

However, if you really wish to verify the results on your end, the following would be needed.
- Windows 10 or higher
- For high-performance systems, one may use Xilinx Vivado 2021.2 Suite: Download through this [link](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vivado-design-tools/2021-2.html) (will require account registration).
- For low-performance systems, one may use EDA Playground. Web app through https://edaplayground.com/ (will require account registration). Please see Project 2 Specs page 25 for full guide. 
- Minimal space and at least 4 GB memory for EDA playground. At least 70 GB of space and 8 GB of memory for Xilinx Vivado.

**Remark:** Please note that this project was accomplished through Vivado.

## **Running Simulations**
This guide will only focus on the Vivado platform. Analogous steps can be expected in EDA Playground.
1. Start Vivado. Complete the set-up and account registration process.
2. Once Vivado is started, open an existing workbench through File. Select the following directory in your clone of this repository: `CS21_Project2_v2\`. This step will load all Design and Simulation sources to your Vivado session.
3. Once the workbench has loaded, you may begin testing the added instructions. Select the appropriate testbench for the desired instruction that you will test in the Sources pane, right click it, and select "Move to top".
4. Reorder the hiearchy of files by refreshing the Sources pane.
5. Open `memfile.mem` in the Vivado Sources pane, and its contents will appear in a tab the Vivado Editor panel.
6. Copy the contents of the desired instruction test from `Instruction Tests\` to `memfile.mem` (overwrite it).
7. Finally, hit Simulate from the Menu Bar. This will produce a waveform diagram that you may examine for any errors (as we did in the documentation). You may also watch the TCL Console panel for any issues (the testbench is very verbose).

## **Sample I/O**
For testing, say, the sll instruction, you will open `Instruction Tests\sll memfile.txt` and copy its machine code contents to your `memfile.mem` (also shown below).
```
2010000c
00108200
00108200
00108200
2210000c
ac100054
```
An assembly translation of that machine code can be found in  `Instruction Tests\sll tester.asm`. Simulating the workbench with the appropriate testbench on top (`sll_testbench.sv`) will then produce the following waveform diagram (truncated to only show the last few cycles):
![sll_waveform.png](sll_waveform.png)

As expected, the diagram is clean and error-free. The TLC Console panel would also accompany this with a "Success" message. Video documentation includes a full discussion of the entire waveforms.

### **Reference**
Harris, D. M., & Harris, S. (2013). *Digital Design and Computer Architecture (2nd ed.).* Elsevier Inc. https://doi.org/10.1016/C2011-0-04377-6

---
Yenzy Urson S. Hebron \<yshebron@up.edu.ph\>

University of the Philippines Diliman

2nd Semester A.Y. 2021-2022

© Course Materials by Sir Wilson Tan and Sir Ivan Carlo Balingit
