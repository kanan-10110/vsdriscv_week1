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
<img width="1857" height="799" alt="Sub module" src="https://github.com/user-attachments/assets/29332c4a-da72-4217-85a9-78ee3942ff79" />


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
<img width="1857" height="730" alt="multiple modules" src="https://github.com/user-attachments/assets/1d476989-60d2-47ec-b880-ebad29e4c587" />


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
<img width="1857" height="568" alt="1" src="https://github.com/user-attachments/assets/e9d099f3-b9d3-441d-bb5f-2ba74e286832" />


```
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
```
Now open the dumped/created vcd file in gtkwave
```
gtkwave tb_dff_syncres.vcd
```

<img width="1857" height="594" alt="2" src="https://github.com/user-attachments/assets/544e499e-5813-4d78-858b-2e89a38e117d" />

```
iverilog dff_asyncres_set.v tb_dff_asyncres_set.v
./a.out
```
Now open the dumped/created vcd file in gtkwave
```
gtkwave tb_dff_asyncres_set.vcd
```
<img width="1857" height="567" alt="3" src="https://github.com/user-attachments/assets/1cc17729-69f0-4b8c-9e2d-a4f442ee07de" />


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


<img width="1857" height="430" alt="Screenshot from 2025-09-28 11-26-33" src="https://github.com/user-attachments/assets/6b7f9343-6b0b-4403-8992-2a5712018414" />


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

<img width="1857" height="430" alt="Screenshot from 2025-09-28 11-26-33" src="https://github.com/user-attachments/assets/cfb03984-a748-4094-9197-47a47ccc3546" />


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

<img width="1857" height="412" alt="Screenshot from 2025-09-28 11-28-17" src="https://github.com/user-attachments/assets/cb326ed4-6e93-4d9b-a012-97e3e90d4980" />


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

<img width="1857" height="821" alt="Screenshot from 2025-09-28 11-30-02" src="https://github.com/user-attachments/assets/e283fedb-6a91-4617-b55d-ab5fc0d78f10" />

Writng the netlist
```
write_verilog -noattr mul2_net.v
```
```
!gvim mul2_net.v
```

<img width="1236" height="301" alt="mul2 netlist" src="https://github.com/user-attachments/assets/a55952a5-48bc-4760-a548-18333555e342" />


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

<img width="1857" height="821" alt="Screenshot from 2025-09-28 11-33-13" src="https://github.com/user-attachments/assets/d8aa2a50-5400-41f9-9339-fe7a5781e34b" />


Writng the netlist
```
write_verilog -noattr mult8_net.v
```
```
!gvim mult8_net.v
```
<img width="1250" height="322" alt="mult8 gvim netlist" src="https://github.com/user-attachments/assets/32d2ec04-d95f-4731-b113-9c2c9465a5d2" />
