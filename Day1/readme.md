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
<img width="1859" height="296" alt="Git Clone" src="https://github.com/user-attachments/assets/757dd339-50d2-4a55-b09a-5ab9af333140" />

```
iverilog good_mux.v tb_good_mux.v
```
Running the a.out file created
```
./a.out
```

```
gtkwave tb_good_mux.vcd
```
The test bench instantiates the DUT to connect with it
Got a GTK Wave

<img width="1852" height="572" alt="gtkwave good_mux" src="https://github.com/user-attachments/assets/4d3dfcd2-36cb-431c-b675-88d0f4c2c6d8" />


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
<img width="1857" height="1040" alt="Screenshot from 2025-09-28 11-02-05" src="https://github.com/user-attachments/assets/30dd5ba2-8d9d-4d20-85f9-4270d328bc1a" />



Now we will do the technology mapping
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```


Got a distutils error



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
<img width="1857" height="858" alt="Screenshot from 2025-09-28 11-02-51" src="https://github.com/user-attachments/assets/38621c54-67dc-4825-8c03-4c519dd44b9d" />



Getting the netlist
```
write_verilog -noattr good_mux_netlist.v
!gvim good_mux_netlist.v
```
