<div align="center">

  # Week 1 : Day 2
# Advanced Library Characterization, Multi-Level Synthesis, and Sequential Element Design

</div>

<div align="center">
 
[![RISC-V](https://img.shields.io/badge/RISC--V-SoC%20Tapeout-blue?style=for-the-badge&logo=riscv)](https://riscv.org/)
[![VSD](https://img.shields.io/badge/VSD-Program-orange?style=for-the-badge)](https://vsdiat.vlsisystemdesign.com/)
![Week](https://img.shields.io/badge/Week-1-green?style=for-the-badge)

</div>

## Table of Content :
1. Advanced Library Characterization Frameworks
2. Multi-Level vs Flattened Synthesis Methodologies  
3. Sequential Element Architectures and Performance Optimization

# 1. Advanced Library Characterization Frameworks
Digital synthesis engines operate through intricate partnerships with characterization databases (standard .lib formats). These repositories encapsulate the electrical behavior and performance metrics of fundamental circuit primitives available for implementation.
The sophisticated aspect lies in the multi-dimensional characterization approach where each primitive exists across multiple operational envelopes—typically spanning weak, nominal, and strong drive strength categories. This creates strategic implementation opportunities:
Aggressive Drive Cells: These leverage enhanced channel width scaling to amplify transconductance characteristics, delivering superior slew rates and reduced transition times. Optimal for performance-critical signal paths, yet demand premium area real estate and contribute to elevated dynamic power profiles.
Conservative Drive Cells: These prioritize geometric compactness and quiescent power efficiency through minimal device sizing. While exhibiting extended propagation characteristics, they provide tactical advantages in timing budget management, specifically addressing hold margin requirements through deliberate delay insertion strategies.
The essence of physical design synthesis centers on multi-objective optimization across the fundamental trinity of metrics: silicon footprint efficiency, energy consumption profiles, and temporal performance characteristics. Advanced synthesis algorithms deploy heuristic optimization engines to traverse this complex solution space while maintaining design rule compliance and operational robustness across environmental variations.

# 2. Multi-Level vs Flattened Synthesis Methodologies
Our investigation centered on architectural decomposition strategies through structured synthesis methodologies. This design philosophy promotes maintainable system complexity by partitioning large-scale integrated circuits into coherent functional units, avoiding monolithic design approaches that become unmanageable.

The comprehensive evaluation of our hierarchical design structure (multiple_modules.v) unfolded through methodical examination stages:

1. Primary validation through behavioral simulation frameworks, coupled with extensive signal integrity analysis via GTKWave visualization platforms to confirm functional specifications.

2. Transformation pipeline execution utilizing Yosys synthesis infrastructure, facilitating the conversion from behavioral abstractions to physical gate-level representations.

3. Exhaustive netlist documentation generation, implementing automated visualization workflows to capture detailed circuit topologies for every constituent module within the design hierarchy!

#### Sub module :
<img width="1856" height="542" alt="Show Sub_module1" src="https://github.com/user-attachments/assets/726dbbee-5051-4793-8d56-c3bb79d228ad" />

#### Multiple Modules:
<img width="1854" height="785" alt="Multiple Modules" src="https://github.com/user-attachments/assets/7da1f63c-53b6-49dc-b42b-d77b9fb4ae58" />

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
```
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
Flattening the output so basically removing the unused files from the main file.
```
flatten
write_verilog multiple_modules_flat.v
```
```
show
```
<img width="1853" height="452" alt="Flattten Show Output" src="https://github.com/user-attachments/assets/9fb2be9b-9ae7-45c5-b0d3-6b3c5b30dcef" />


### 3. Sequential Element Architectures and Performance Optimization
Sequential memory elements constitute the architectural backbone of clocked digital systems! These circuit primitives are absolutely indispensable because they establish state persistence mechanisms and provide temporal decoupling, operating as computational firewalls to prevent metastability phenomena and combinational logic racing conditions arising from unbalanced signal path propagation. The complete system framework operates within synchronized temporal domains, where these storage components exclusively latch data during precisely defined clock transition events, creating deterministic computational sequences and guaranteeing reproducible information transfer protocols.

We analyzed initialization control schemes employing both edge-triggered synchronous protocols and level-sensitive asynchronous override mechanisms for preset/clear operations. Crucially, electrical characteristics demonstrate significant sensitivity to manufacturing Process deviations, supply Voltage variations, and ambient Temperature shifts (comprehensive PVT corner analysis). This multifaceted behavioral dependency is comprehensively modeled within .lib characterization databases, underscoring the absolute necessity of timing-closure-aware synthesis methodologies and extensive post-synthesis verification to ensure dependable silicon behavior across all specified environmental and operational boundaries.
- We simulated the syncres.v , async_set and asyncres.v
- then genrated the Gtkwave
- Synthesised it using Yosys
- We generated individual netlist graphical representation for each design

#### Simulation & GTK Wave Generation:
```
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
```
Now open the dumped/created vcd file in gtkwave
```
gtkwave tb_dff_asyncres.vcd
```
<img width="1856" height="562" alt="GTKWave for Asyncres" src="https://github.com/user-attachments/assets/6e03d09a-c365-406e-b59f-3b6f64a7f815" />
```
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
```
Now open the dumped/created vcd file in gtkwave
```
gtkwave tb_dff_syncres.vcd
```
<img width="1856" height="606" alt="GTK Wave dff_syncres" src="https://github.com/user-attachments/assets/6de35c04-b5fe-447c-835b-0ecf9c9dfe42" />

```
iverilog dff_asyncres_set.v tb_dff_asyncres_set.v
./a.out
```
Now open the dumped/created vcd file in gtkwave
```
gtkwave tb_dff_asyncres_set.vcd
```
<img width="1859" height="575" alt="asyncres_set GTKWave" src="https://github.com/user-attachments/assets/7d2c7714-fe46-4375-8207-53f1649aa495" />


#### Synthesizing asyncres file in Yosys
Open yosys
```
yosys
```
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_asyncres.v
synth -top dff_asyncres
```
<img width="641" height="422" alt="Statistics dffasyncres" src="https://github.com/user-attachments/assets/797b0e2d-ed8c-4407-b312-3564af9ae601" />

```
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
```
show
```
<img width="1856" height="425" alt="Show asyncres" src="https://github.com/user-attachments/assets/fa6bce6b-10d0-4eba-b33c-3d7949a37b14" />

#### Synthesizing syncres file in Yosys
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_syncres.v
synth -top dff_syncres
```

<img width="683" height="425" alt="dff syncres statistics" src="https://github.com/user-attachments/assets/42e85249-3d68-4ac2-a5a9-97cf75134915" />

```
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```

```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

```
show
```
<img width="1859" height="468" alt="Show Syncres" src="https://github.com/user-attachments/assets/166f40fe-08d8-47e5-bb8a-ec30889ab2b8" />

#### Synthesizing async_set file

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_async_set.v
synth -top dff_async_set
```
<img width="648" height="380" alt="Statistics async_Set" src="https://github.com/user-attachments/assets/556b922a-e77d-4fd8-9e34-5b4990461bc6" />

```
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
```
show
```
<img width="1851" height="611" alt="Show asyncres_set" src="https://github.com/user-attachments/assets/e01a164e-458a-4d37-a205-cb433e830f41" />

### Optimizations.
```
gvim mult_*.v -o
```
Launch yosys
```
yosys
```
##### 1.
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mult_2.v
synth -top mul2
```
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
Not needed as there is nothing to map

```
show
```
<img width="525" height="261" alt="Show mul2" src="https://github.com/user-attachments/assets/26e8452c-c66a-48dc-83bf-8510508bf116" />

Writng the netlist
```
write_verilog -noattr mul2_net.v
```
```
!gvim mul2_net.v
```
<img width="1236" height="301" alt="Netlist mul2" src="https://github.com/user-attachments/assets/6bd9e644-f412-4958-8bac-96b759325640" />


##### 2. 
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mult_8.v
synth -top mult8
```
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
Not needed as there is nothing to map

```
show
```
<img width="548" height="258" alt="show mult8" src="https://github.com/user-attachments/assets/6ca85373-8eb9-4adb-a2e4-a7a6ef8c8472" />

Writng the netlist
```
write_verilog -noattr mult8_net.v
```
```
!gvim mult8_net.v
```
<img width="1250" height="322" alt="gvim mult8" src="https://github.com/user-attachments/assets/76034497-a39b-4d4e-bf4c-d9e77d6a76f1" />
