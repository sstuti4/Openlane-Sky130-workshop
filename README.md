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
  
   **1. Synthesis** : Synthesis is process of converting RTL (Synthesizable Verilog code) to technology specific gate level netlist. Standard cell library and technology related information acts as input for it.
   
   **2. Floorplan & Power Planning** : The floorplan is the process of determining the dimensions, macro placement, power grid generation and pin placement. Power is provided to components with the help of power straps, power rings and power pads. Power planning helps tp reduce resistance and in addressing problems like electromigration.
   
   **3. Placement** : Placement steps helps reduce interconnect delays and enable successful route. Firstly ***global placement*** is performed which finds optimum positions for cells. Then with the help of the global placement results detailed placement takes place. ***Detailed placement*** ensures minimally altered and close to required placement.
   
   **4. Clock Tree Synthesis** : This step is used to route clock signal. It is important that clock signal routing takes place before signal routing, as clock signal help ensure valid data signal transmission.
   
   **5. Signal Routing** : In routing, valid horizontal and vertical pattern of wires found to implement nets connecting cells together. *Global route* generates route guides on the basis of which *detailed route* is performed.  
   
   **6. Sign-off** : In sign-off stage *Physical verification* done with the help of DRC & LVS and *Timing verification* carried out with static timing analysis. 
   
   
   Concepts like design exploration and Antenna diode were discussed. For adding new design or update in flow tools, reconfiguration for design is needed. **Design exploration** helps in finding best configuration for design. Command to run it. **Antenna Diode** problem arises for long nets which is avoided by using fake antenna diodes next to every cell after placement. Later Antenna Checker (Magic) is run. If it reports antenna violations then fake diode replaced by actual one. 
   
   # LAB
   
   ** To run OpenLANE**
   
![Openlane_run](https://user-images.githubusercontent.com/73339656/97084069-07cd4100-1632-11eb-88ed-2b30db19f669.jpg)
   

# 3. Day 2: Chip floorplan and Introduction to Library Cells

On Day 2, definition of width and height of core and die. Factors like *Utilization factor* and *Aspect ratio* important to understand a design were introduced and their effects were discussed. Steps involved to define location of *pre-placed cell*  & it's advantage of enhacing reusability and *de-coupling capacitors*  and how they help during switching to avoid failure explained. A fully charged De-coupling cap placed paralllel to circuits to ensure proper supply of peak current *Ipeak* by decoupling them from main supply voltage. Hence de-coupling cap ensures *proper local communication* while multiple Vdd & Vss lines lead to *proper global communication* avoiding voltage droop and ground bounce conditions. Step of placing *logical cell placement blockage* to avoid PnR tool to place anything.   

**Characterization**

Input information required by Characterization softwares are PDKs, DRC & LVS rules and spice models. The design steps of it involve *Circuit Design* and *Layout design* characterization. The software GUNA used for characterization. The characterization can be classified as Timing characterization, Power characterization and Noise characterization.

**Steps involved in Characterization**

* Model file of CMOS containing basic property defitions.
* Read extracted Spice Netlist
* Recognize the behavior of cell
* Read the subcircuits
* Attact the power sources
* Apply input or stimulus
* Provide necessary output capacitance
* Provide necessary simulation commands


# 4. Day 3: Design and Characterization of cells using Magic Layout tool and ngspice

# 5. Day 4: Timing Analysis using OpenSTA, Clock Tree Synthesis & Signal Integrity

# 6. Day 5: Routing and SPEF Extraction

# 7. Acknowledgements
  * Kunal Ghosh, Co-founder (VSD Corp. Pvt. Ltd)

  
