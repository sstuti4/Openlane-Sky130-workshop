# Openlane-Sky130-workshop
An informative workshop on advanced Physical Design using OpenLANE/Sky130 organized by VSD Corp. It helped me gain hands-on experience of full ASIC implementation steps from RTL to GDSII using Google-Skywater's first manufacturable open source 130nm process design kit. The workshop focused on building basics by imparting exposure to conceptual as well as practical approach.Learnings: Design Exploration, Logic Equivalence Check (LEC), Antenna Diode Concept, Decoupling Cap, Pin Placement, Timing Characterization and familiarity with files like libs/db, LEF, DEF, SDC and SPEF. Tools used: Magic, ngspice, OpenSTA, TritonRoute, yosys and OpenROAD.   

# Contents
1. Introduction to Openlane
2. Day 1: SoC Design and familiarity to open source eda tools
3. Day 2: Chip floorplan and Introduction to Library Cells
4. Day 3: Design and Characterization of cells using Magic Layout tool and ngspice
5. Day 4: Timing Analysis using OpenSTA, Clock Tree Synthesis & Signal Integrity
6. Day 5: Routing and SPEF Extraction

# 1. Introduction to OpenLANE
OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault, OpenPhySyn, SPEF-Extractor and custom methodology scripts for design exploration and optimization. It is a tool started for true open source tape-out experience and comes with APACHE version 2.0 . The goal of OpenLANE is to produce clean GDSII without any human intervention. OpenLANE is tuned for Skywater 130nm open PDK and can be used to produce hard macros and chips.

* **Modes of Operation of OpenLANE**

     **1.  Autonomous Mode:**    Push buttons triggered flow.
     
     **2.  Interactive Mode:**    Run commands and steps one by one.
 

# 2. Day 1: SoC Design and familiarity to open source eda tools

Day 1 started with basic introduction to *System On Chip* and *RISC-V Instruction Set Architecture(ISA)*. How RISC-V flow helps in communicating to computers was expalined. In RISC-V flow, our code is converted to RISC-V ISA using compiler then implementation of  RTL takes place in Hardware Description Language (HDL) and from it to Layout form.

**Components reqired for open-source implementation of Digital ASIC Design**

* **RTL IP** : Easily available on open source platforms 

* **EDA Tools** : QFlow, OpenROAD and OpenLANE

* **PDK Data** : Open source PDK released by Google & Skywater

**Simplified RTL to GDS Flow**
  
   **1. Synthesis** :
   
   **2. Floorplan & Power Planning**
   
   **3. Placement** :
   
   **4. Clock Tree Synthesis** :
   
   **5. Signal Routing** :
   
   **6. Sign-off** :

# 3. Day 2: Chip floorplan and Introduction to Library Cells

# 4. Day 3: Design and Characterization of cells using Magic Layout tool and ngspice

# 5. Day 4: Timing Analysis using OpenSTA, Clock Tree Synthesis & Signal Integrity

# 6. Day 5: Routing and SPEF Extraction

# 7. Acknowledgements
  * Kunal Ghosh, Co-founder (VSD Corp. Pvt. Ltd)

  
