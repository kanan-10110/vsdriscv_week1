<div align="center">
 
# Week 1 : Day 1
# Introduction to Verilog RTL design and Synthesis

</div>

<div align="center">
 
[![RISC-V](https://img.shields.io/badge/RISC--V-SoC%20Tapeout-blue?style=for-the-badge&logo=riscv)](https://riscv.org/)
[![VSD](https://img.shields.io/badge/VSD-Program-orange?style=for-the-badge)](https://vsdiat.vlsisystemdesign.com/)
![Week](https://img.shields.io/badge/Week-1-green?style=for-the-badge)

</div>


## Overview :
Today marked my first deep dive into the fascinating world of hardware description languages! I explored Verilog as the primary vehicle for expressing digital logic concepts. The emphasis was placed entirely on open-source development environments. I discovered the power of circuit simulation through Icarus Verilog (iverilog), an exceptional tool for validating behavioral models. Subsequently, I delved into automated logic transformation using Yosys, another remarkable open-source solution that converts abstract descriptions into implementable hardware. The learning materials were exceptionally clear, and the practical sessions were highly engaging. I concluded the day with strong comprehension of Register Transfer Level (RTL) design methodology.

## Table of content :
1. Introduction to Verilog RTL design and Synthesis
2. Introduction to open-source simulator iverilog
3. Labs using iverilog and gtkwave
4. Introduction to Yosys and Logic synthesis

# The "Circuit Transformation" Methodology 🔄

# 1. Understanding Hardware Description Fundamentals 🏗️

We begin by exploring the underlying principles of digital circuit representation. Establishing this conceptual framework is essential for everything that follows! The most compelling aspect? Digital simulators operate on a sophisticated scheduling algorithm. Rather than continuously monitoring every signal in your design, they maintain an event queue system. When any input transition occurs—whether rising or falling edge—the simulator intelligently schedules only the affected logic blocks for re-evaluation. This selective execution strategy is what enables efficient simulation of complex digital systems!

# 2. Mastering Hardware Languages and Verification Environments (Verilog & Testbenches) 📋

Now we dive into the syntax and semantics of hardware description: Verilog! This specialized language enables engineers to capture their circuit architectures in textual form. Our focus centers on Register Transfer Level (RTL) abstraction, the sweet spot where algorithmic thinking meets hardware reality. For validation purposes, you construct a testbench framework. Consider the Design Under Test (DUT) as your circuit prototype (containing actual signal interfaces), while the testbench serves as the automated test equipment. It orchestrates the stimulus patterns, timing sequences, and verification checks to thoroughly exercise the DUT. Since testbenches represent pure software constructs—not synthesizable hardware—they operate without physical port constraints!

# 3. Hands-on Circuit Validation with Iverilog and GTKWave ⚡

Time for practical implementation! We'll harness the capabilities of the robust open-source simulator Icarus Verilog (iverilog). This environment allows you to execute your hardware descriptions and observe the resulting behavior in detail. The methodology emphasizes iterative refinement—compiling designs, analyzing waveforms through visualization tools like GTKWave, debugging logical inconsistencies, and developing deep intuitive understanding. This experiential approach proves most effective for mastering digital design principles!

```
mkdir VLSI
```
```
cd VLSI
```
```
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
```
<img width="1024" height="418" alt="Gitclone skyrtl" src="https://github.com/user-attachments/assets/0d9a7fb4-8ff7-45db-b167-33b805390e8b" />

```
iverilog good_mux.v tb_good_mux.v
```
Running the a.out file created
```
./a.out
```
<img width="792" height="72" alt="Running the a out file" src="https://github.com/user-attachments/assets/01b01d47-eb00-4d38-9323-d2d318f88f64" />

```
gtkwave tb_good_mux.vcd
```
The test bench instantiates the DUT to connect with it
Got a GTK Wave
<img width="1853" height="573" alt="GTKWave tb_good_mux" src="https://github.com/user-attachments/assets/a74b0422-473b-47ea-944c-fefeaaad1b86" />

# 4. Introduction to Yosys & Logic Synthesis
Here comes the transformative phase: Logic Synthesis using Yosys! We'll witness how behavioral hardware descriptions undergo automatic conversion into optimized gate-level implementations—the fundamental building blocks of integrated circuits. This represents the critical transformation stage that bridges conceptual designs with physical silicon, whether targeting FPGA prototypes or ASIC manufacturing flows. Comprehending this automated translation process forms the bedrock of modern digital engineering, enabling the journey from abstract concepts to fabricated chips.

Open the verilog_files directory in the terminal using below commands:
```
cd VLSI
cd verilog_files
```
For Opening yosys, use the command
```
yosys
```

Now in Yosys, enter the following commands
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog good_mux.v
synth -top good_mux
```
We are reading the liberty file, verilog code of MUX & also synthesizng the RTL Code/Design
<img width="1865" height="1080" alt="Screenshot from 2025-09-27 17-15-04" src="https://github.com/user-attachments/assets/b84ec61d-c3b4-4599-8941-c33f42dea2e0" />
<img width="635" height="406" alt="Screenshot from 2025-09-27 17-17-55" src="https://github.com/user-attachments/assets/02f359e7-7986-4277-b8f4-ca80e98ac4bc" />

Now we will do the technology mapping
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
<img width="845" height="273" alt="Screenshot from 2025-09-27 17-19-51" src="https://github.com/user-attachments/assets/8ba635f0-9c63-4b54-b95f-74872cbad1f8" />

Got a distutils error
<img width="1865" height="449" alt="Distutils Error" src="https://github.com/user-attachments/assets/b91707f2-ba39-49d3-ab4c-2507e1c4247a" />

## To rectify the error
```
sudo apt-get update
sudo apt-get install python3-setuptools
```
To verify if graphiz, xdot and distutils installed or not
```
sudo apt install graphviz xdot
python3 -c "import distutils; print(distutils.__file__)"
```
Now to show the gate level circuit
```
show
```
<img width="1856" height="1007" alt="Screenshot from 2025-09-27 17-20-41" src="https://github.com/user-attachments/assets/348a3cc6-ebd4-456b-90bb-c9192db0be9b" />

Getting the netlist
```
write_verilog -noattr good_mux_netlist.v
!gvim good_mux_netlist.v
```
<img width="1251" height="604" alt="Netlist File" src="https://github.com/user-attachments/assets/199b7e4e-7ffb-4f9f-976c-ed3700c4d662" />
