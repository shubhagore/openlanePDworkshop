# **CONTENTS**

## **Day 1 - Inception of open-source EDA, openLane and Sky130 PDK**

* How to talk to computers
* SoC design and OpenLANE
* Get familiar to open-source EDA tools

## **Day 2 - Good floorplan vs bad floorplan and introduction to library cells**

* Chip Floor planning and considerations
* Library Binding and Placement
* Cell design and characterization flows
* General timing characterization parameters

## **Day 3 - Design of a library cell using Magic Layout and ngspice characterization**

* Labs for CMOS inverter ngspice simulations
* Inception of Layout and CMOS fabrication process
* Sky130 Tech File Labs

## Day 4 - Pre-layout timing analysis and importance of good clock tree

* Timing modelling using delay tables
* Timing analysis with ideal clocks using openSTA
* Clock tree synthesis TritonCTS and signal integrity
* Timing analysis with real clocks using openSTA

## Day 5 - Final steps for RTL2GDS
* Routing and design rule check (DRC)
* Power distribution network and routing
* TritonRoute features


# **Sky130 Day1 - Inception of open-source EDA, openLane and Sky130 PDK:**

## **SKY130_D1_SK2 - SoC design and OpenLANE:**

### **SKY_L1 - Introduction to all components of open-source digital asic design:**

#### **Digital ASIC Design:**

Designing the digital application in an automated way requires several elemnets. The elements include hardware descriptive language, EDA tools and Process design kit (PDK) data
![digital_ASIC_design](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/2cd65f27-8f31-4cd3-bfc1-ce8ca5f1d35d)

**Open source digital ASIC design:**

![open_source_digital_asic_design](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/dbeedaef-770a-4510-93cc-6a56616fe18e)

**PDK:** PDK is the collection of files used to model a fabrication process for the EDA tools. It is the interface between designers and fabrication team. PDK includes 
* Design rules such as DRC, LVS, PEX
* Device models,
* Digital Standard cell Libraries,
* I/O libraries, etc.
       
### **SKY_L2 - Simplified RTL to GDSII flow:**

![simplified_RTLto_GDSII_flow](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/2d52f407-778f-428f-a059-f61746930e06)

The flow includes the following steps,
* Synthesis
* Floorplan/Power planning
* Placement
* Clock Tree Synthesis
* Routing
* Signoff

**Synthesis:** This stage converts RTL to the circuit out of components from the standard cell library (SCL). This is usually referred to as Gate level netlist. 

![synthesis](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/3a69b3c9-b655-4609-bfcc-d5b8066d9db2)

Each standard cell has regular layout.

Dimensions of the cell differ from eah other.

Each cell has different views or models,
* Electrical (delay), HDL, spice
* Layout (Abstract and detailed).

**Floorplan:** Size and shape of the die, Macro placement, I/O pins placement, rows definition and power planning are done in Floorplan.

![floorplan](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/daaedeb0-7da9-4741-8531-ac05d8d6a74d)

In power planning, power is circulated using power grid which has alternate horizontal and vertical pattern of metal layers. Power grid is built using rings, stripes, and power is evenly distriuted. Higher metals layers are used for the routing of power as they are thicker (wider), thus reduces the resistivity. This helps for less IR drop and electromigration.

![power_planning](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/d24da1df-57d1-4b68-b3b4-6ba059beb12b)

**Placement:**

According to the netlist, cells are placed in their resepctive locations and cells might overlap, so we do detailed placement to avoid the overlapping and flipped to save site row area (cells are legalized).

![placement](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/cb5c4de7-6a2f-44eb-a4c5-4f3d2bc4624f)

![placement1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/f51d9dd9-8bf3-462b-a5b0-46da882e4008)

**Clock tree synthesis:**

Building a clock tree such that clock reached every clock pin of a sequential block with min skew and insertion delay.

![cts](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/f4946890-8efe-49d6-9845-80b53aa6664d)

**Routing:**

After clock, Signal routing takes place. For each metal layer PDK defines thickness, pitch,width, tracks etc.

![routing](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/57db0967-9581-45f9-935f-dbce47ae764b)

SKY130 has 6 layers. The lowest layer is used for interconnects and is made of titanium nitride and all 5 layers are aluminium. Most routers are grid routers and metal tracks form a routing grid. since the grid is huge, we use divide and conquer approach. Global Routing is performed using coarse grained grids generating routing guides. Fine grained grids uses these routing gudies and impplement the actual routing between wires.

![routing2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/6b8a6df1-fb7f-469c-99b6-319f1ad932b3)

**Signoff:**

Once Routing is done, we do verifictaion during signoff
* Physical verification :
  * Design rule checks (DRC) : verifies whether our design meets design rules. (performed by MAGIC) 
  * Layout vs schematic (LVS) : verifies whether our layout matches with the netlist schematic.(MAGIC AND NETGEN).
* Timing Verification : Static Timing Analysis : Checks whether our design meets all teh timing constraints and is running with the designated frequency.

![signoff](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/2859e628-91c4-4cd3-aeec-a58c451c5af1)

### **SKY_L3 - Introduction to OpenLANE and strive chipsets:**

**OpenLANE ASIC flow:**

![openlane1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/921304b8-c487-41e8-b2e5-e7cbf960a627)

![strive](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/a05b76f6-0713-4fdc-a09c-56d037c5c208)

Main goal is to produce clean GDSII without human help.

Clean GDSII means, having no
* LVS violations
* DRC violations
* timing violations

### **SKY_L4 - Introduction to OpenLANE detailed ASIC flow design:**

**OpenLANE ASIC flow:**

Two modes of operation of openLANE is:
* Autonomus - its like a push button flow, does everything automatically
* Interactive - runs through commands

![openlane2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/851e2411-a8f4-4f2b-8bea-3387a2b6a963)

The flow starts with RTL synthesis. RTL is fed to YOSYS with the design constraints and translates into netlist then optimised and mapped into the synthesizable cells from Standard cell library (SCL) using ABC. ABC is used during optimization. When it comes to OpenLANE we have stratagies where some tragets least area and the other on best timing, this is called **Synthesis exploration**.

![synthesis_exploration](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/f14d30f6-e906-4d2c-95ae-82ca6dfb12cd)

**Design exploration:** When you have more no of configurations in our design, the Design exploration does sweeping job and gives an design matrix which has report on violations, cell count, runtime, utilization etc and from that we can get the best set of configurations and clean layout.

![design_exploration](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/fc1100f3-5581-486d-b672-db3e341a598a)

**OpenLANE Regression Testing:** The design exploration utility is used for regression testing. OpenLANE already does this so that we can run the experssion

![openlane_regression_testing](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/88bb2eb5-8ba0-405d-865f-c4be47016551)

**DFT (DESIGN FOR TEST):** Its an additional testing that is done for correctness of the design by generating test vectors or stimulus.`

![dft](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/36974b27-3f05-4531-8bdf-82aefa9167fa)

**LEC:** Since, we do optomization in Physical Implementation, the output netlist from this might be different from the synthesis netlist. Inorder to avoid any further violations functionally, we need to logically check the design before and after PnR. This is known as Logic Equivalence check

![lec](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/7bd192ac-2c61-40cf-8d8f-86faf91ce83b)

**Antenna:** When a metal wire segment is fabricated and its long enought, it act as antenna and collect charges which can damage the transistor gate that is connected to that wire. so length of the wire must be limited. Usually this job is done by router, if he fails, there are 2 solutions.
* **Bridging:** In this we bridge using top layer so we go upto the top layer and drop back to to the metal layer that has long wire segment.
* **Antenna diode:** Insert the diode next to the transistor that is getting effected by this long wire.

Using OpenLANE we took a preventive approach. we created a fake antenna diode and placed next to every cell during placement. When Magic runs for antenna checkers on the routed layout and reports a violation on a cell input pin, then replace the fake with the real one.

![dealing_with_antenna](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/335c5d56-5158-4af1-b22e-42b83d49b9eb)`

![dealing_with_antenna_violations2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/ec1cc368-d883-4f52-a8e3-4666178524fb)


## **SKY130_D1_SK3 - Get familiar to open-source EDA tools:**

### **SKY_L1 - OpenLANE directory structure in detail:**

* OpenLANE is a flow which consists of many opensource tools.
* The main aim is to have a complete RTL to GDSII flow.
* The working directory is **/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/**

![ubuntu_commands0](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/72b62af4-2aad-4579-b3b2-cd7f85030d1e)

* Few of the linux commands useful are,
  * cd -------------> change diectory - This is to change the path
  * ls -------------> list - This is to list the files and directories present in the path in which we are there
  * ls -lrt --------> This will list all the files and directories in the path in the chronological order 
  * ls --help ------> This can be used to get more details on ls command

![ubuntu_commands1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/c7155d53-07e1-4c31-94b2-48229dacbf7a)

* PDK folder in the path **Desktop/work/tools/openlane_work_dir/** contains all the info related to PDK.

* The PDK which we are using for this workshop is **skywater_130nm PDK**.

* Inside sky130A we can see 2 sub directories namely **libs.ref** and **libs.tech** as shown in the below figure.

![ubuntu_commands2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/2b6cad42-549c-4d9c-9fb0-dba9466ccae3)

  * libs.ref contains all the technology specific information like timing, cell, lef

![ubuntu_commands3](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/9c3c12ae-3755-4606-863e-0db56d616ae1)

  * libs.tech contain all the information related to tool. 

![ubuntu_commands4](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/246abd8e-9334-4eee-a18b-a12ae91ebd0a)

* We will be working on **sky130_fd_sc_hd**. 
  * **fd** - foundary
  * **sc** - standard cell
  * **hd** - high density

* In the below figure, there is a folder by name **techlef** which contains the layer information.

![ubuntu_commands5](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/f7f6df35-af60-47cd-9423-3587efc401d6)

### **SKY_L2 - Design preparation step:**

![ubuntu_commands7](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/073ac8f7-1013-437a-a011-21b7809ae76c)

*docker*

*./flow.tcl -interactive*

* The docker command is executed first and then the tcl script.
* The script here will run in interactive mode (step by step execution).
* It is the script which will invoke the Openlane.
* If we use the lab session from https://www.vlsisystemdesign.com/ then it is not required to configure Docker but if we use our PC we need to configure docker. I have used my PC for this practical session.

*The design for our work is picorv32a, which will be choosen from the following direectory **/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs**

![ubuntu_commands8](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/87b2d7fa-5b7b-48b6-95e7-e7f638d0c0c3)

* The picorv32a will have 3 files,
  * **src file:** RTL will be present and sdc file
  * **config.tcl:** bypasses any configs already done into openLANE., i.e, many of the switches already have a default value. **config.tcl** will have the highest **priority**. The below image shows the config.tcl deatils

![ubuntu_commands9](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/e734775f-a978-470d-a7c4-9939ef47e8da)

  * **sky130A_sky130_fd_sc_hd_config.tcl**

* After this we need to input all the packages that are required to run his flow by using below command

**_package require openlane 0.9_**

![ubuntu_commands7](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/073ac8f7-1013-437a-a011-21b7809ae76c)

* Before running synthesis, we need to prepare the data structure and the design setup stage which will be setting up the data for the file system and data structure. We need to prepare the file system specific to the flow, so that the exact data will be picked up by the correct location by the tool. So we need to create that location by running the command,

_**prep -design picorv32a**_

This stage is known as **design preparation stage.**

![ubuntu_commands10](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/885043ae-ee6f-4d30-bf27-5c8141e81433)

* In the above figure **merging lefs** indicates that it **merges two lef files** namely **cell specific lef file** and **technology related lef file**.

* Before preparing the file system the picorv32a folder contains 3 main files as shown below.

![ubuntu_commands11](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/03e61dba-3824-41c7-a499-4b4809ba9d87)

### **SKY_L3 - Review files after design prep and run synthesis:**

* After preparing the file system the picorv32a folder contains one extra folder by the name run and this will include all the necessary files as shown below.

![ubuntu_commands12](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/0b72749a-6338-4ef5-b830-269e35572199)

  * Here inside tmp folder we can see the **merged lef** file created during the file system preparation.
  * the results folder will have seperate folders for each step 
  * The config.tcl present in the newly created runs folder will basically shows all the default parameters being taken by the run.
  * cmds.log file will have all the commands being used.

![ubuntu_commands13](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/759e027d-911a-4dc1-b877-343966da4171)

* The next step is to run synthesis using the below command,

_**run_synthesis**_

![synthesis_run2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/b3761962-0178-426f-b604-16a687e4e311)

### **SKY_L4 - OpenLANE project git link decription:**

* Should refer to github efabless site and fossi dial up

### **SKY_L5 - Steps to characterize synthesis results:**

* **Flop ratio = No. of D flip flop / Total number of cells**

In my sythesis run the counts are as shown in the figure below,

![synthesis_output1 png](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/91de61b9-4b1d-420c-96fa-6248a55222f1)

![synthesis_output2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/d4dbae2b-4564-485c-993e-827ce0d5816a)

* Flop ratio = 1613/14876 = 0.108429
* Flop percentage = 10.8429

* The reports and results after synthesis can be found in the respective folders.

![synthesis_output3](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/bf8a3d31-9c17-4135-8d43-8d1fdc2af70c)

![synthesis_output4](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/bfe441ef-ae01-4c5f-9578-69363f2208b2)

* The synthesis statistical report will be as shown below,

![synthesis_output5](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/13a43fb4-46d2-4dbe-ac45-4f30c9682b6a)

![synthesis_output6](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/0d6db82e-aaeb-45b6-b79b-4b6612ea58df)


# **Sky130 Day1 - Good floorplan vs bad floorplan and introduction to library cells:**

## **SKY_130_D2_SK1 - Chip floor planning considerations:**

### **SK_L1 - Utilization factor and aspect ratio:**

* In the physical design flow, the first step is to **define the height and width of the core and the die**.

![define_width_height_core_die](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/e7328a58-31e4-4ac6-817f-4f651670ad42)

  * We start with the basic netlist, say 2 flip-flops (one launch and other capture) and a combinational logic in between.
  * * A **netlist** basically describes all the connectivity between an electric design

![netlist_eg](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/eb6eafb5-5714-4dce-a2b9-b4867dce79a8) 

  * Need to convert the symbols into the physical dimensions.
  * Total length and width would be 2 x 2 = 4 sq units(area), this is the minimum area that would be occupied.

![dimension1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/76418f90-4919-4433-a462-8d1abc850702)

  * On the silicon wafer, we have one section referred to as the **die** and inside the die, there is the **core**.
  * The **die encapsulates the core**, a **die** is a small semiconductor material specimen on which the fundamental circuit is fabricated.

### **SK_L2 - Concept of pre-placed cells:**

* In the physical design flow, the second step is to **define the locations of the pre-placed cells**.

![define_location_preplaced_cells](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/ea4b26e5-13d0-43f3-9b03-f3576cd375de)

* Take a combinational logic, we needn't implement the logic everytime completely, the circuit can be divided into smaller bits
* The individual blocks are later connected via wires.
* The IO pins are extended and the blocks are detached, this creates 2 different modules or IP's.

![division_of_ckt](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/0ce30f43-53fc-4eab-ac47-3054459b7384)

* The **advantage** of doing this is that if a particular block is being replicated multiple times, this black-boxed blocks can be implemented and then connected. Need not be implemented evey time.
* There are IPs available in the market such as, Memory, clock-gating cell, comparators, etc. The arrangement of these IPs in a chip is called **Floorplanning**.
* These IP's or blocks have user defined locations and hence are to be placed before the automated placement and routing. Thus these are known as **pre-placed cells**.

### **SK_L3 - De-coupling capacitors:**

* Consider we have the pre placed cells: block a,b and c which are memories
  * These are only implemented once and used multiple times.
  * The locations of these pre placed cells cannot be changed once placed. 
  * Pre-placed cells should be surrounded by the decoupling capacitors.
* When a particular circuit switches, it requires some current, basically at the time of switching, we can say that there is an amount of capacitance there , and when closed, it needs an amount of charge, which it requires from the supply voltage. The supply logic should be capable enough to supply required amount of current to all the gates. Similarly, it is the responsibilty of the Vss to take the charge when the gates switch from logic 1 to 0.
* Actually there would be a drop in the wire due to resistances, inductances, capacitances, etc.
* If the voltage drop is too huge, proper logic 1 and logic 0 cannot be defined and will lead to errors. This is the problem of having a large physical distance between the voltage source and the circuit component.
* The voltage drop should be within the **noise margin**. It shouldn't be in the undefined state.
* This problem can be solved by using **decoupling capacitos** which are large capacitors, completely filled with charge.
* The capacitor essentially de couples the circuit from the power supply
* Whenever there is switching activity, the capacitor slowly depletes its charge and when no switching takes place, then the capacitor replenishes itself.
* The preplaced cells are placed with Decaps to ensure no problems occur
* Local communication(inside the preplaced cells) is taken care of but global planning is to be taken care of next.

### **SK_L4 - Power planning:**

* All the capacitors which were charged to logic to 1 has to discharge to logic 0  through a single **ground tap point**. This will create the **bump** in ground tap point.
* **Ground bounce** is a phenomenon when all the capacitances discharge at the same time, if this bump exceeds the noise margin level, it can lead to an undefined logic value.

![ground_bounce](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/d5b6a8b3-8f4d-41df-9117-fc64e210663b)

* When all the capacitances want to charge, they demand current at the same time and therefore there is a **voltage droop**, it should also not exceed the Noise margin level.

![voltage_droop](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/37df99a2-28b6-4e1c-8457-55ab9acffa0e)

* The above problem can be solved by having **multiple power supplies** instead of a single power supply. The components can withdraw the power from the nearest power source with the help of having multiple power supplies.

![multiple_source](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/5076ee48-5ec1-49cd-bf9e-b5524e896ea5)

### **SK_L5 - Pin placement and logical cell placement blockage:**

* The connectivity information between the gates is coded using the **verilog/VHDL** language and is called the **netlist**. Below figure shows the example of the netlist.

![eg1_pin_placement2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/a3ecbe23-ab29-41a2-9689-efc7f0cee952)

* General convention is to place all the **input ports** on the **left hand side** and **output ports** on the **right hand side**. It also depends on the designer.
* Ordering of **input and output ports are random** because it depends on the placement of the cells.
* The **clock ports are bigger** in size than the data ports as the clock ports keeps driving the complete chip continuosly. Thus resistance should be lower in the clock signal path. Hence lower the resistance bigger is the size of the clock port.
* None of the automated placement and roting tool places the cell in the IO area. Th IO area should be blocked for the cell placement and routing. Thus we perform logical cell placement blockage. Thus no cells are pleced in the IO area as this location is reserved for pin placement.

![pin_placement](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/f9569626-1459-498e-bf48-faeac759937c)

### **SK_L6 - Steps to run floorplan using OpenLANE:**

* Following synthesis the next stage is floorplan. 
* In floorplan die area, core area, aspect ratio, utilization factor are set, place macros and pins, power distribution (pg creation) is done.
* We can view the deafult configuration file (README.md) in the path **~/Desktop/work/tools/openlane_working_dir/openlane/configuration**.

![readme_file1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/7e6a49fe-cc69-4b84-afcd-5568efcb8a11)

![readme_file2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/eea1a618-446d-488d-a4cc-07f4239dbf74)

* For floorplan we have switches. Few of them are floorplan core utilization, floorplan aspect ratio, floorplan sizing, die area, etc.
* The above mentioned parameters are set in the .tcl file of respective stage in the path **~/Desktop/work/tools/openlane_working_dir/openlane/configuration**.

![fp_tcl1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/6dd41dd4-7b7c-444e-95d9-ce52ea6fd94e)

![fp_tcl2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/c09f40ca-6237-4f3b-8ed8-dcc5f4d9834f)

* FP_IO_MODE indicates how we need the pin configuration should be around the core 
  * If pin mode 1: random poition, but equidistant
  * If pin mode 0: not equidistant
* The highest priority for these defaults will be **sky130A_sky130_fd_sc_hd_config.tcl**, and then **config.tcl**, and then the **tcl file** inside the folder as shown above.
* In openlane flow, verical metal and horizontal metal values (mentioned in the config.tcl file in the path openlane_working_dir/design/picorv32a/config.tcl) are 1 more than the normal ones (mentioned in floorplan.tcl file).

### **SK_L7 - Review floorplan files and steps to view floorplan:**




