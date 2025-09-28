<div align="center">
 
# Week 1 : Day 3
# Logic Minimization and State Machine Refinement Techniques

</div>

<div align="center">
 
[![RISC-V](https://img.shields.io/badge/RISC--V-SoC%20Tapeout-blue?style=for-the-badge&logo=riscv)](https://riscv.org/)
[![VSD](https://img.shields.io/badge/VSD-Program-orange?style=for-the-badge)](https://vsdiat.vlsisystemdesign.com/)
![Week](https://img.shields.io/badge/Week-1-green?style=for-the-badge)

</div>

## Table of Content :
1. Foundations of Circuit Optimization Theory
2. Combinational Logic Transformation Strategies
3. State Machine Optimization and Temporal Logic Refinement
4. Dead Code Elimination and Resource Pruning Techniques

### 1. Foundations of Circuit Optimization Theory
Circuit optimization represents a multi-faceted transformation discipline that enhances implementation metrics through algebraic manipulation, structural reorganization, and resource allocation strategies. These methodologies target area reduction, performance enhancement, and energy efficiency through advanced algorithmic approaches including Boolean algebra simplification, redundancy elimination, and register transfer optimization. Post-synthesis verification through Gate-Level Simulation validates functional preservation while ensuring timing closure requirements. Implementation discrepancies between Register Transfer Level abstractions and gate-level netlists typically originate from specification ambiguities, sensitivity list incompleteness, or procedural assignment methodology violations, necessitating rigorous coding standards adherence for implementation reliability.

### 2. Combinational Logic Transformation Strategies
Combinational circuit optimization employs sophisticated algebraic manipulation techniques to achieve structural simplification while preserving functional equivalence through systematic redundancy identification, constant propagation algorithms, and logic path consolidation methodologies. Utilizing primitive Boolean operators including conjunction, disjunction, and complement functions, we executed comprehensive design transformation through meticulous behavioral simulation and synthesis optimization of Register Transfer Level specifications. Through strategic command-line interface utilization, this transformation methodology delivers enhanced circuit density, improved switching characteristics, and superior performance metrics optimized for silicon implementation requirements.

<img width="1857" height="801" alt="Screenshot from 2025-09-28 11-49-37" src="https://github.com/user-attachments/assets/97e93684-fe55-4279-9d07-18743fd922aa" />
<img width="1857" height="801" alt="Screenshot from 2025-09-28 11-45-06" src="https://github.com/user-attachments/assets/130b0c0c-5d77-4ba0-8b29-1c76ba29cc15" />
<img width="1858" height="878" alt="Screenshot from 2025-09-28 12-01-03" src="https://github.com/user-attachments/assets/c1fbbe83-4417-4114-ae82-c940de3696d9" />
<img width="1858" height="878" alt="Screenshot from 2025-09-28 11-55-45" src="https://github.com/user-attachments/assets/f050fa26-510f-4159-9fe4-1c74a0b4337d" />


<img width="1858" height="544" alt="Screenshot from 2025-09-28 12-05-38" src="https://github.com/user-attachments/assets/6ce02082-2c5d-4893-a4ff-f91fd060ef6a" />
<img width="1858" height="573" alt="Screenshot from 2025-09-28 11-54-10" src="https://github.com/user-attachments/assets/dc4ee091-5620-4d00-9f15-e5eaa4987423" />
<img width="1858" height="544" alt="Screenshot from 2025-09-28 11-51-48" src="https://github.com/user-attachments/assets/270869b5-7d42-4957-9564-acf106dd346b" />
<img width="1857" height="544" alt="Screenshot from 2025-09-28 11-40-32" src="https://github.com/user-attachments/assets/0b7159f8-e0bc-4a99-9f75-ece5ece5d207" />



### 3. State Machine Optimization and Temporal Logic Refinement
Sequential circuit optimization encompasses sophisticated transformation algorithms targeting memory-based computational architectures utilizing bistable storage elements and register arrays. This comprehensive methodology integrates state space reduction techniques that minimize finite state machine complexity through equivalent state identification and unreachable state elimination, thereby streamlining control path implementations. Temporal optimization through register relocation algorithms redistributes memory elements across combinational logic boundaries to achieve balanced critical path delays and maximize operational frequency capabilities. Furthermore, state equivalence analysis and merging procedures consolidate functionally identical computational states, yielding substantial resource conservation. These integrated optimization strategies collectively deliver dramatic improvements in silicon utilization efficiency, dynamic power characteristics, and temporal performance boundaries, generating highly optimized, robust sequential hardware architectures engineered for high-performance computational applications.

#### Simulated Outputs:


<img width="1851" height="571" alt="Screenshot from 2025-09-28 12-19-43" src="https://github.com/user-attachments/assets/e777915d-2f98-407a-b40b-980a5f91f5ce" />
<img width="1858" height="567" alt="Screenshot from 2025-09-28 12-17-14" src="https://github.com/user-attachments/assets/31421b53-ad83-4b0f-beb3-f4e50b34769b" />
<img width="1858" height="572" alt="Screenshot from 2025-09-28 12-13-04" src="https://github.com/user-attachments/assets/b9e40d2f-7b18-42fa-b423-ae8799e06c86" />
<img width="1858" height="546" alt="Screenshot from 2025-09-28 12-09-04" src="https://github.com/user-attachments/assets/8a225880-f52d-4e58-8189-178d7596a1c4" />


#### Synthesis on Yosys:
<img width="1851" height="414" alt="Screenshot from 2025-09-28 12-20-40" src="https://github.com/user-attachments/assets/486c8cb5-045c-469f-b1d7-4657b18f4b7c" />
<img width="936" height="1077" alt="Screenshot from 2025-09-28 12-18-32" src="https://github.com/user-attachments/assets/7fb5e2ee-ba5e-4b4b-9cdb-b6dcae8f6b9e" />
<img width="1858" height="428" alt="Screenshot from 2025-09-28 12-14-39" src="https://github.com/user-attachments/assets/4460606d-9fca-4718-a9c0-87afb612ec6c" />
<img width="1858" height="1073" alt="Screenshot from 2025-09-28 12-11-37" src="https://github.com/user-attachments/assets/2d7d6ebb-4abd-47d2-818e-6b743591611b" />


### 4. Dead Code Elimination and Resource Pruning Techniques:
Advanced synthesis frameworks employ sophisticated dataflow analysis algorithms to identify and eliminate computationally orphaned logic structures throughout the design hierarchy! When sequential computational elements generate outputs with zero fanout connectivity, static analysis engines recognize these pathways as unreachable computational branches and systematically eliminate them from the implementation netlist. This automated pruning methodology yields immediate benefits including substantial register count reduction, simplified interconnect topologies with reduced routing congestion, minimized switching activity for enhanced power efficiency, and accelerated synthesis convergence with improved timing closure characteristics!

Our practical investigation demonstrated these principles through counter architecture optimization studies. We analyzed the computational structure through Register Transfer Level specifications, executed comprehensive behavioral verification protocols, and performed synthesis transformation analysis. Through systematic command-line optimization workflows, we observed the automated elimination algorithms effectively streamlining the counter implementation architecture!

<img width="1851" height="374" alt="Screenshot from 2025-09-28 12-33-58" src="https://github.com/user-attachments/assets/1d86cc39-afe2-4a58-9c0c-354d094f5d4a" />


#### Flattening of Multiple_Module_Opt2 

<img width="1850" height="726" alt="Flattening of Module_opt2" src="https://github.com/user-attachments/assets/20675192-b9ec-4b83-8059-10fbb6b45c2b" />


#### Flattening of Multiple_Module_Opt 

<img width="1857" height="800" alt="multiple_module_opt Show" src="https://github.com/user-attachments/assets/3e19bc2f-9947-4562-95f4-657243a6741e" />

