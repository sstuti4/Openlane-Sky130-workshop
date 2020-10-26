# Openlane-Sky130-workshop
An informative workshop on advanced Physical Design using OpenLANE/Sky130 organized by VSD Corp. It helped me gain hands-on experience of full ASIC implementation steps from RTL to GDSII using Google-Skywater's first manufacturable open source 130nm process design kit. The workshop focused on building basics by imparting exposure to conceptual as well as practical approach.Learnings: Open source tools, Characterization of Cell, SPICE simulations, Static timing Anlaysis concepts, Commands of various OpenLANE tools, 16-mask CMOS Fabrication, Antenna Diode Concept, Decoupling Cap, Routing algorithm & Steps, Timing Characterization and familiarity with files like libs/db, LEF, DEF, SDC and SPEF. Tools used: Magic, ngspice, OpenSTA, TritonRoute, yosys, SPEF extractor and OpenROAD.   

# Contents
<a href="#1-Introduction-to-Openlane">1. Introduction to Openlane</a>

<a href="#2-Day-1-SoC-Design-and-familiarity-to-open-source-eda-tools">2. Day 1: SoC Design and familiarity to open source eda tools</a>

<a href="#3-Day-2-Chip-floorplan-and-Introduction-to-Library-Cells">3. Day 2: Chip floorplan and Introduction to Library Cells</a>

<a href="#4-Day-3-Design-and-Characterization-of-cells-using-Magic-Layout-tool-and-ngspice">4. Day 3: Design and Characterization of cells using Magic Layout tool and ngspice</a>

<a href="#5-Day-4-Timing-Analysis-using-OpenSTA-Clock-Tree-Synthesis-and-Signal-Integrity">5. Day 4: Timing Analysis using OpenSTA, Clock Tree Synthesis and Signal Integrity</a>

<a href="#6-Day-5-Routing-and-SPEF-Extraction">6. Day 5: Routing and SPEF Extraction</a>

# 1. Introduction to OpenLANE
OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault, OpenPhySyn, SPEF-Extractor and custom methodology scripts for design exploration and optimization. It is a tool started for true open source tape-out experience and comes with APACHE version 2.0 . The goal of OpenLANE is to produce clean GDSII without any human intervention. OpenLANE is tuned for Skywater 130nm open PDK and can be used to produce hard macros and chips.

**Modes of Operation of OpenLANE**

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
   
   **To run OpenLANE**
   
   
![openlane_run](https://user-images.githubusercontent.com/73339656/97091831-5e4f7500-165c-11eb-9f42-7883403cfcf4.png)

 
 
 **Result of synthesis showing design components**
 
![synthesis_result](https://user-images.githubusercontent.com/73339656/97091954-55ab6e80-165d-11eb-86bd-ba674f8e6b72.png)
 


**Slack Calculation of design**
 
 ![slack_calc](https://user-images.githubusercontent.com/73339656/97088964-0a3f9300-1652-11eb-8ca9-6bb3c6348e0f.png)
   

# 3. Day 2: Chip floorplan and Introduction to Library Cells

On Day 2, definition of width and height of core and die. Factors like *Utilization factor* and *Aspect ratio* important to understand a design were introduced and their effects were discussed. Steps involved to define location of **pre-placed cell**  & it's advantage of enhacing reusability and **de-coupling capacitor**  and how they help during switching to avoid failure explained. A fully charged De-coupling cap placed paralllel to circuits to ensure proper supply of peak current *Ipeak* by decoupling them from main supply voltage. Hence de-coupling cap ensures proper *local communication* while multiple Vdd & Vss lines lead to proper *global communication* avoiding voltage droop and ground bounce conditions. Step of placing **logical cell placement blockage** to avoid PnR tool to place anything.   

**Characterization**

Input information required by Characterization softwares are PDKs, DRC & LVS rules and spice models. The design steps of it involve *Circuit Design* and *Layout design* characterization. The software GUNA used for characterization. The characterization can be classified as Timing characterization, Power characterization and Noise characterization.

**Characterization flow steps**

* Model file of CMOS containing basic property definitions
* Read extracted Spice Netlist
* Recognize the behavior of cell
* Read the subcircuits
* Attact the power sources
* Apply input or stimulus
* Provide necessary output capacitance
* Provide necessary simulation commands


# LAB

**Floorplan Result**

![floorplan_result](https://user-images.githubusercontent.com/73339656/97092549-75916100-1662-11eb-984d-7ab7e8908010.png)

**Layout of Design using Magic tool**

![magic_layout](https://user-images.githubusercontent.com/73339656/97092597-d1f48080-1662-11eb-9504-711b6cd864ef.png) 


# 4. Day 3: Design and Characterization of cells using Magic Layout tool and ngspice

OpenLANE offers an interesting feature of making changes into parameters on the go. This helps to deal with issues like congestion. SPICE deck formation contains informations like components connectivity and values and information about nodes. It was showed how W/L ratio of MOS impacts its conductivity and hence reason of carefully defining W/L ratio of MOS to ensure same *rise* and *fall* delay for clock signals. CMOS robustness defined with the help of parameter that is **Switching Threshold (Vm)**. Switching threshold defined by conditions  **Vgs=Vds** and **Idsp=-Idsn**. 

**SPICE Commands
 **To include MOS**
           
    .include ./libs/pshort.lib
    .include ./libs/nshort.lib

**Netlist Description of MOS**

    M1 out in  VPWR VPWR pshort w=37 l=23
    M2 out in  VGND VGND nshort w=35 l=23
    
**Command for Transient Analysis**

    .tran 1n 20n
            
**Important parameters of Timing Characterization**
* **Rise Delay** : Time taken for waveform to rise from 20% to 80% of VDD.
* **Fall Delay** : Time taken for waveform to fall from 80% to 20% of VDD.
* **Propagation Delay** : Measured between 50% of Input transition to 50% of Output transition.

**16-Mask CMOS Process Steps**
* **Substrate Selection** : Selection of base layer on which other regions will be formed.
* **Create active region for transistors** : SiO2 and si3N2 deposited. Pockets created using photoresist and lithography. 
* **Nwell & Pwell formation** : Pwell uses boron and nwell uses phosphorous. Drive in diffusion by placing in high temp furnace.
* **Creating Gate terminal** : For desired *threshold value* NA (doping Concentration) and Cox to be set.
* **Lightly Doped Drain (LDD) formation** : LDD done to avoid *hot electron effect* and *short channel effect*.
* **Source and Drain formation** : Forming the the source and drain.
* **Contacts & local interconnect Creation** : SiO2 removed using HF etch. *Titanium* deposited using sputtering.
* **Higher Level metal layer formation** : Upper layers of metals deposited.


**NOTE** : The values shown are standard value and might change according to requirements. 

# LAB

**Layout of Inv using Magic**

![inv_layout](https://user-images.githubusercontent.com/73339656/97113874-1b9ca400-1713-11eb-90b8-dd0bf88f7c4a.png)

**Transient Analysis Plot using ngspice**

![transient_analysis](https://user-images.githubusercontent.com/73339656/97114751-60770980-1718-11eb-877b-0396e38f764b.png)


# 5. Day 4: Timing Analysis using OpenSTA, Clock Tree Synthesis and Signal Integrity

Topic of Delay tables explored on Day 5. I learned that delay and output transition values of any particular cell are calculated with the help of values of *input transition* and *output load* values. Delay table and output transition table of a cell contain different value for each combination of input trans and output load, represented in form of lookup tables in liberty file. With the help of interpolation and extrapolation the values of point in range can also be calculated for precise result.  

**Setup & Hold  Slack Analysis**
* Setup and hold time define a window of time in which our data should remain unchanged for desired data transfer to take place. Factors like uncertainty and skew also play an important role in this. **Clock skew is the difference between Source Clock path and Destination Clock path**. Slack defined as difference between actual time and required time is monitored. Positive or zero Slack indicates no violation whereas negative slack value indicates violation of timing. 

**Commands to change configuration variables settings**
   
    set ::env(SYNTH_STRATEGY) 1
    set ::env(SYNTH_SIZING) 1
 
 **OpenROAD Commands**
 
    read_lef /openLANE_flow/designs/picorv32a/runs/trial/tmp/merged.lef
    read_def /openLANE_flow/designs/picorv32a/runs/trial/results/cts/picorv32a.cts.def
    write_db pico1.db
    read_verilog /openLANE_flow/designs/picorv32a/runs/trial/results/synthesis/picorv32a.synthesis_cts.v
    read_liberty $::env(LIB_SYNTH_COMPLETE)
    lik_design picorv32a
    read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
    set_propagated_clock [all_clocks]
    report_checks -path_delay min_max -digits 4


# LAB

**sky130_fd_sc_hd File containing layer information of Cell**

![layer_info](https://user-images.githubusercontent.com/73339656/97115367-6969da00-171c-11eb-9266-37a83cfb3a83.png)

**Steps to Convert Magic Layout in Standard Cell LEF**

![texthelper](https://user-images.githubusercontent.com/73339656/97116187-9b316f80-1721-11eb-8990-ba28527dad30.png)


![tkcon_1](https://user-images.githubusercontent.com/73339656/97116190-a1bfe700-1721-11eb-8fed-9189a3a5b419.png)


![magic_command](https://user-images.githubusercontent.com/73339656/97116196-a71d3180-1721-11eb-997d-7db9af28c7c4.png)


![tkcon_2](https://user-images.githubusercontent.com/73339656/97116200-abe1e580-1721-11eb-8aaa-a9db94561508.png)


![lef_info](https://user-images.githubusercontent.com/73339656/97116204-b308f380-1721-11eb-926d-f383af26a949.png)

![layout_1](https://user-images.githubusercontent.com/73339656/97117154-e9e20800-1727-11eb-8667-babaa596cc10.png)

![layout_2](https://user-images.githubusercontent.com/73339656/97117167-f6666080-1727-11eb-9fed-aa4d1fa00399.png)

**CTS Step Result**

![cts_result](https://user-images.githubusercontent.com/73339656/97117697-80fc8f00-172b-11eb-8982-bdce6ec6afe2.png)

**Clock Buffer List of design**
![buf_list](https://user-images.githubusercontent.com/73339656/97117700-8659d980-172b-11eb-8aee-4cc578cf0f5e.png)


# 6. Day 5: Routing and SPEF Extraction

Routing method finds out best possible pattern for connection between two end points, of which one point is *target node* while the other is *source node*. **Maze Routing-Lee's Algorithm** was introduced. In this technique firstly routing grids are created and source & target nodes are indentified. Then the blocks adjacent to one under consideration are assigned same numbers and this process is repeated till we reach the target node. Once this done the pattern with minimum number of turns preferably a *l* spaced pattern is finalised for route. 

**Typical DRC rules for pair of wires**
1. Wire width
2. Wire pitch 
3. Wire Spacing

These DRC rules exist because of limitations of the Lithography technique. Deviation takes place in lithography leading to changes which might lead to an unintended open circuit or short circuit and to avoid this the DRC rules are fixed. Another DRC Violation type is Signal short which can be dealt by changing layers. 

**Routing Technique Classified into**
* **Global Route** : Performed using fast route. In this step route guides are formed.
* **Detailed Route** : Performed using *TritonRoute*. 

**Triton Route**
It performs *initial detailed route* and tries to route within the route guide provided by fast route. It works on MILF-based panel routing with intra-layer parellel route and inter-layer sequential route technique. Input files required for triton route are LEF,DEF and preprocessed route guide. Output is in form of detailed routing with optimum wire length and Via count.

**Steps for preprocessed route guides**
* **Initial route guide** : Basic connectiving informatons using route guides.
* **Splitting** : Routes in non-preferred direction are split into unit width.
* **Merging** : Touching guides have edge orthogonal to the preferred route guide direction are merged.
* **Bridging** : Edges parallel to preferred one are bridged using additional layers.
* **Preprocessed Route** : Now all route guides are in preferred direction as required. 

# LAB

**Routing Result of Design**

![routing_result](https://user-images.githubusercontent.com/73339656/97088698-58539700-1650-11eb-9f81-d773c09df730.png)

**SPEF Extraction**

![spef_result](https://user-images.githubusercontent.com/73339656/97091405-5a6e2380-1659-11eb-8df4-bde2e06fb572.png)

# 7. Acknowledgements
  * Kunal Ghosh, Co-founder (VSD Corp. Pvt. Ltd)

  
