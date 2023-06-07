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


# **Sky130 Day2 - Good floorplan vs bad floorplan and introduction to library cells:**

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

* The config.tcl file will have all the default settings. Highest priority is for the sky130A_sky130_fd_sc_hd_config.tcl.
* The results/floorplan contains a def file (**Design exchange format**).
* The def file contains a parameter as DIEAREA (lower x axis, lower y axis) (upper x axix, upper y axis)
* 1 micron = 1000 database units.

![fp_def](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/5e14a922-e730-450f-842a-d998c8b6f761)

* To see the actual layout after floorplan, we use magic and the command is as below,

**magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &**

### **SK_L8 - Review of floorplan using magic:**

* To select the entire layout **press s** and then **press v** this will fit the layout to the center.
* To **zoom the specific part of the layout first** **click on left of mouse and then right side of the mouse to form a box and then press z on the keyboard**.
* To select a particular object bring the cursor on the object and then press s n the keyboard. And to know what layer the object is present in type what on tkcon terminal.

![fp_layout1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/3cdde638-4474-4e48-8408-7ab92d2da68a)

![fp_layout2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/63285457-2b40-4899-b832-f23cf140bf32)

![fp_layout3](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/ff35f3a5-0795-4fdc-9246-fe157036cf3b)

* **Tap cells** are meant to **avoid the latch up** issue which occur in CMOS devices, which connect the **nwell to Vdd and substrate to ground**.  
* Tapcells are placed diagonally equidistant.
* Standard cells are present here in the lower left side.

![fp_layout4](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/aec4fbf5-5c64-4d33-9424-ece0d0b6141b)

![fp_layout5](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/834625f5-0d85-45a4-b7fa-4e7c8778f49c)

## **SKY_130_D2_SK2 - Library binding and placement:**

### **SK_L1 - Netlist binding and initial place design:**

* We have a particular netlist with some gates, the shape of these gates will represent the functionality of these gates.
* In reality, we dont have shapes, we have boxes, it has physical dimensions.
* A library is the place where we can find all the informations of each cell. Information includes timing information, size of the cell, width, height, delay, required condition of the cell, shapes of the cell, etc.
* A **library** has various flavors of same cells in the library.
* Till now we have 
  * proper floorplan with input and output ports defined and placed
  * Netlist
  * Physical view of the logic gates. 
* Physical view of the netlist and then place them.
* The cells are placed near to its IO pins so that **delays are avoided**.

### **SK_L2 - Optimize placement using estimated wire length and capacitance:**

* The problems such as only some blocks being closer to their ports, can be solved, using a technique called **optimizing placement**.
* For the last flip-flop, it becomes difficult due to restrictions.

![pnr1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/ac89b230-78b6-47cd-b70a-50ca56ed0b86)

* We will do some estimations, say flip-flop1 to din2, we try to estimate the capacitances in the wires that would be connected before routing.
* Basically in optimize placement step the wire length, and capacitances are estimated, and based on that **repeaters** are inserted. This is done mainly to maintain **signal integrity**. 
* **Repeaters** are **buffers that will recondition the original signal**. Repeaters will reproduce the original signal and send the new signal to the next stage.
* Adding repeaters will create **loss of area**.
* **Slew** is based on the value of the capacitor, the higher the capacitance, the higher is the amount of charge required to charge the capacitor,and slew will be bad.

### **SK_L3 - Final placement optimization:**

* The buffers are placed accordingly wherever required to maintain signal integrity.
* Based on the setup timing analysis, the placement done is verified and checked.

### **SK_L4 - Need for libraries and characterization:**

* Logical synthesis output is an arrangement of gates that describe the original functionality.
* Floorplan: Here we import the netlist from the output of synthesis and decide the shape and size of core and die. This depends on the number of gates and shape and sizes of the gate present in the logical synthesis.
* Placement: The logic cells are placed on the chip such that the initial timing is met.
* Clock tree synthesis: Spreads clock evenly among all the logic cells.
* Routing:
* Static timing analysis (STA): To see the setup time, hold time , maximum available frequency. This is the signoff step
* The one thing common across all these steps are the logic gates. This collection of gates is referred to as the library, these should be represented in a manner such that the EDA tool understands what the gates are.

### **SK_L5 - Congestion aware placement using RePLAce:**

* Placement occurs in 2 stages: 
  * Global: is basically **coarse placement** and there is no legalization (std cell are placed in the std cell rows, they should be abutted to each other, there shouldn't be any overlap) happening here. 
  * Detailed: Legalization happens.
* Objective of global placement is to **reduce wire length**, in openLANE, there is a concept of **HPWL** (half parameter wire length).
* The command used to run placement is
**_run_placement_**

![placement_log](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/a2f77149-45dd-4786-a9c0-cb15b01748bf)

* Placement is where the **standard cell positions are fixed**, to visualize these changes, we go into

Directory: results/placement/
**magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &**

![placement_magic_command](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/a841d54e-2863-43af-9ea3-829f8cc34476)

![placement_layout](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/a13d4be2-e87b-4346-ac80-da83cc79ae6d)

![placement_layout1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/0468c16b-22ff-45bf-93e0-03b8f4b489e5)

* The power-ground network creates the power distribution network
* But in OpenLANE, this does not happen during placement
* A post floorplan and post placement CTS, we do power ground generation just before the routing.

## **SKY_130_D2_SK3 - Cell design and characterizaion flow:**

### **SK_L1 - Inputs for cell design flow:**

* In a typical IC design flow, the buffers, logic gates, etc. are called standard cells.
* Standard cells are placed in a place known as **library**.
* Library has got different gates with different functionalities.
* It also has cells with different sizes, i.e different sized logic gates for example.
* It also has cells with different threshold voltage. Variation in the threshold voltage decides the speed of the cell operation.

![library_details](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/e131d0b2-64ab-46c0-9635-cdf9f81bd120)

* Cell design flow is divided into following parts,
  * **Inputs**:
    * Process design kits (PDKs) given by the foundary, they include DRC & LVS rules, SPICE models, library and user-defined specs.
    * basically a tech file with some rules
    * say rules for poly width, minimum extension rules, etc.
    * There are thousands of rules that are present and need to be followed.
    * For the SPICE models, the threshold voltage equations are seen, they have some parameters called foundry parameters, also called SPICE model parameters 
  * **Design steps**:
  * **Outputs**: These are actual used by EDA tool

### **SK_L2 - Circuit design step:**

* The separation between the power rail and the ground rail will decide the cell height. It is the responsibility of the library developer to maintain this cell height.
* **Drive strength decides the cell width**.
* The top level designer deicdes on the supply voltage.
* The **design steps are three**:
  * **Circuit design:** 
    * Implement the function
    * Model the pmos and nmos to meet the library specifications( for example, w/l ratios) 
    * Typical output is **CDL (circuit description language)**.
  * **Layout design:**
    * Implement the function using MOS transistors
    * to get the PMOS and NMOS network graphs from the implemented design 
  * **Characterization**

### **SK_L3 - Layout design step:**

* The first step is to implement the function
* Next step is to get the PMOS and NMOS network graphs from the implemented design 
* To obtain the path of layout is Euler's path and stick diagram.
* **Euler's path**: Path that is being traced only once. Based on the Euler's path, a stick diagram is drawn
* The next step is to convert this stick diagram into a proper layout, by also following the DRC rules and the top level user specifications.
* The layout can be drawn using an open source tool called **MAGIC**.
* The out of layout is GDSll
* With the layout in hand the final step is to extract the parasitics from the layout and characterize it interms of timing.
* GDSII, LEF , extracted spice netlist(.cir) are the outputs.
* **cir file**: parasitics of each and every element
* The next step is characterization to obtain the timing, noise and power information: output is .libs file

### **SK_L4 - Typical characterizaion flow:**

* From the input stage, the output is a layout, description of the entire circuit, SPICE extracted netlist, subcircuit(has nmos and pmos models)

* Read in the model: This comes out of the foundry
* Read the extradcted SPICE netlist
* To recognise the behaviour of the circuit
* To read the subcircuit of the inverter
* Attach the necessary power sources
* Apply the stimulus (known as characterization setup)
* Provide the necessary output capacitances
* Provide the necessary simulation commands (trans simulation, DC simulation..etc)
* Next step is to feed in all these inputs from the above steps in the form of a characterization software called as **GUNA**. The software will generate Timing, noise, power.libs files 

## **SKY_130_D2_SK4 - General timing characterization parameters:**

### **SK_L1 - Timing threshold definitions:**

* The syntax is understood before, this is important to understand the GUNA software
* Timing threshold definitions:
  * Slew_low_rise_thr (threshold) : low means near the 0 level, defines the point towards the lower side of the power side, typically 20%
  * slew_high_rise_thr
  * slew_low_fall_thr
  * slew_highfall_thr
  * in_rise_thr: related to input waveforms. 50%
  * in_fall_thr: 50%
  * out_rise_thr: related to output : point at which delay can be calculated on the output waveform 50%
  * out_fall_thr: 50%

### **SK_L2 - Propagation delay and transition time:**

* For delay, **out - in** needs to be calculated,
**_time(out_*_thr) - time(in_*_thr)_**
* If there is a movement of the threshold, then this creates problems, we see the output coming before the input, creating a negative delay, which is not possible. This is due to choosing the wrong threshold points.
* If the waveform has high wire delays, then we can have timing problems even after choosing the correct threshold positions.
* **Transition time For a rise wavform**

**_time(slew_high_rise_thr) - timme(slew_low_rise_thr)_**

* For a falling waveform,

**_time(slew_high_fall_thr) - time(slew_low_fall_thr)_**

# **Sky130 Day3 - Design library cell using Magic layout and ngspice characterization:**

## **SKY_130_D2_SK1 - Labs for CMOS inverter ngspice simulations:**

### **SK_L1 - IO Placer revision:**

* From a github link, we will be downloading a **.magic file**, from it, we will be doing **post-layout simulation in ngpsice** and post-characterizing by plugging it into the openLANE flow.
* There is an option to make changes on the fly in the openLANE flow = after running synthesis and floorplan, say we want to change the config of how the IO pins are placed = IO placer allows 4 strategies

**_set ::env(FP_IO_MODE) 2
run_floorplan_**

![pin_loc_change](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/da9c4376-0d30-4f92-948c-47dcb1d6d73f)

### **SK_L2 - SPCIE deck creation for CMOS Inverter:**

* **SPICE deck** is a connectivity information about the netlist, it has inputs, connectivity information, tap points at which output is taken.
* The connectivity of the substrate pin should also be defined.
* Next, we have to define the component values, in the example taken, thw (W/L) ratios are:
  * PMOS: 0.375 u/0.25 u
  * NMOS: 0/375 u/0.25 u 
* The PMOS Should be generally wider than the NMOS, ideally twice or thrice larger than the NMOS.
* The output load calculated here is 10fF
* Input gate voltage: 2.5 V and drain voltage: 2.5 V
* The next step would be to identify the nodes (point which connects the components), to say a component lies betweeen 2 places, we define nodes, the schematic of the inverter being considered is shown below:

![spice_deck](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/67ff0857-7f5a-4ada-8069-e58926552e9e)

### **SK_L3 - SPICE Simulation lab for CMOS Inverter:** 

* The SPICE netlist can be written as,
  * **M1 out in vdd vdd pmos W=0.375u L=0.25u** (<MOSFET name> <drain> <gate> <source> <substrate> <type of MOSFET> <width> <length>) 
  * **M2 out in 0 0 nmos W=0.375u L=0.25u**
  * **cload out 0 10f** (capacitance is in between out and 0)
  * **Vdd vdd 0 2.5**
  * **Vin in 0 2.5**
  * ***** Simulation commands *****
  * **.op**
  * **.dc Vin 0 2.5 0.05**

  * ***** include tsmc_025um_model.mod *****
  * **.LIB "tsmc_025um_model.mod" CMOS_MODELS**
  * **.end**
 
* All the tech parameters are located in the MODEL file
* The model file contains all the information of NMOS and PMOS are stored
* Here, W/L of both NMOS and PMOS = 1.5
       
### **SK_L4 - Switching Threshold Vm:**

* The **Switching Threshold** of a CMOS inverter is the point where the Vin = Vout on the DC Transfer characreristics.     

![spice_threshold](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/5794991d-f68a-42d5-87e4-e6644e8e2072)

### **SK_L5 - Static and dynamic simulations of CMOS inverter:**
       
### **SK_L6 - Lab steps to git clone vsdstdcelldesign:**

* We need to clone the git repo at first
  * **git clone https://github.com/nickson-jose/vsdstdcelldesign.git**

![git_clone](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/b83f7fc6-08c5-4ac3-a42e-6fe51ba4aa5f)
       
* We copy the tech file (/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech) into the folder here (/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/)

![tech_file_copy](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/e5654370-0a41-4eb2-a837-2410e8e84b88)

* For layout we run magic command

_**magic -T sky130A.tech sky130_inv.mag &**_
       
![inverter_layout](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/32e508d6-381d-442b-bd46-9b6c692a84ec)

## **SKY_130_D2_SK2 - Inception of layout and CMOS fabrication process:**

### **SK_L1 - Create active regions:** 
### **SK_L1 - Formation of n-well and p-well:**
### **SK_L1 - Formation of gate terminal:**
### **SK_L1 - Lightly doped drain (LDD) formation:**
### **SK_L1 - Source and drain formation:**
### **SK_L1 - Local interconnect formation:**
### **SK_L1 - High level metal formation:**
       
* The steps are:
  * Selecting a substrate: generally, P-type substrate
  * Creating active region for transistors: Mask1
    *  Isolation between active region pockets by depositing the oxide layer SiO2, silicon nitride Si3N4,then photoresist and masking the layers followed by photolithography and etch of the silicon nitride and remove photoresist. 
    * Then this is placed in oxidation furnace, helps in growing oxide layer in other regions. This process is called **LOCOS "Local oxidation of silicon"** and lastly we strip out Si3N4 using hot phosphoric acid.
  * The field oxide is grown, this process is called LOCOS ( Local Oxidation of silicon): Bird's beak
  * N-well and P-well formation which will be used for PMOS and NMOS fabrication respectively
  * Formation of gate
  * Lightly doped drain (LDD) formation
  * Source and drain formation
  * Formation of contacts and interconnects
  * Higher metal level formation       
       
### **SK_L8 - Lab instructions to sky130 basic layers layout and LEF using inverters:**      

* The right side has all the layer information.       
* Move the cursor across the poly-ndiff intersection so that will select only to that area  and press s, and type what on the tkcon window, this will tell the information
* When the polysilicon crosses the n diffusion it is an nmos.
       
![nmos](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/f2736a07-8547-4a9b-9a5d-8f49179f07b0)
       
![pmos](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/3a77ad56-ed0a-4d20-83be-256d05ff3fa6)
       
* When s is pressed twice, the connected is also selected (in total thrice).

![inverter_layout1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/ae0d85f5-f2c2-4d57-a4cf-a4fe1ab2c395)

* **Library exchange format (.lef)**: The layout of a design is defined in a specific file called LEF.
  * It includes design rules (tech LEF) and abstract information about the cells.
    * Tech LEF - Technology LEF file contains information about the Metal layer, Via Definition and DRCs.
    * Macro LEF - Contains physical information of the cell such as its Size, Pin, their direction.      
       
### **SK_L9 - Lab steps to createstd cell layout and extract spice netlist:**  
       
![file_extraction](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/71ce59aa-98f9-4184-a88c-31e35f136ede)

![file_extraction1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/8cae5bf4-7cec-41d5-a3d0-7bf9fb176961)

![file_extraction2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/add34b6c-06d1-461f-bb1d-3edc63d31054)
  
![file_extraction3](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/c57546fb-e043-4d08-a6b2-78438363c0cb)
 
![file_extraction4](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/2b0f3518-d8be-48a1-a048-576331c85423)
    
 ## **SKY_130_D2_SK3 - Sky130 Tech file Labs:**

### **SK_L1 - Lab steps to create final SPICE deck using Sky130 tech:**
       
* The spice file looks as below before making changes,

![spice_file](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/8e40a8ca-31c1-4a48-a78c-ad71a09cabc0)
   
* The spice file looks as below after making changes,
       
![spice_file1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/c2516121-395a-4868-99e5-b4568b0c88e4)

* To run spice we have to use the command 
  * **_ngspice <spice file name>_**
       
![spice_file2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/d15a387d-8a02-439f-9caa-79e8fc9ff0a4)
     
### **SK_L2 - Lab steps to characterize inverter using sky130 model file:**
       
![spice_command](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/986235f5-41ad-4fa0-89d7-c67fd8399f00)

![inv_plot](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/24a5e7d1-c9f4-4317-9269-7d33a45eae5b)
    
* Characterizing a cell is done by obtaining 4 parameters:
  * Rise tranisition: Time taken for output waveform to transit from a value of 20 percent of max value to 80 percent of max value (VDD)
  * Fall transition: Time taken for output to fall from 80 percent to 20 percent
  * Fall cell delay: time diff between the 50 of the output (difference in time(50% output fall) to time(50% input rise))
  * Rise cell delay:  difference in time(50% output rise) to time(50% input fall)
       
* **Rise transition:**
    * Max value: 3.3V, 20 percent is 0.66
       
      at 0.6 : x0 = 2.16162e-09, y0 = 0.5625

      at 2.66: x0 = 2.2524e-09, y0 = 2.60008

      Rise transition = x0 diff = 0.0908ns
       
* **Fall transition:**

* For fall tranistion, 80 percent to 20 percent
       
at 2.66: x0 = 4.05475e-09, y0 = 2.63981
       
at 0.6 : x0 = 4.09713e-09, y0 = 0.600042
       
Fall tranisition: 0.0424ns       
      
* **Cell rise delay:**

at 1.65:

x0 = 2.21687e-09, y0 = 1.65007

x0 = 2.14985e-09, y0 = 1.65007
       
cell rise delay(propagation delay): 0.067ns
       
* **Cell fall delay:**       
       
x0 = 4.07826e-09, y0 = 1.65017
       
x0 = 4.05e-09, y0 = 1.65017
       
Cell fall delay: 0.0282ns  
       
![delay_coordinates](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/ef1bd817-aeaa-4806-a4ac-95c0ca6ab414)
       
* Next objective is to use the layout and create a lef file, this will be used in openLANE and it is plugged into the picorv32 core.      
       
### **SK_L3 - Lab introduction to magic tool options and DRC rules:**       
       
* The website used id **www.opencircuitdesign.com/magic/**      
       
### **SK_L4 - Lab introduction to Sky130 pdk's and steps to download labs:**       
       
![drc1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/6acbed6d-a1fe-484e-8464-11270400c78a)

![drc2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/589edb87-939d-4f8d-94da-5e49b402cd42)
  
![drc3](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/aa34e99d-63ec-4120-aef6-5f6b8809ace5)
       
![drc4](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/a75e1070-b92f-4880-bd38-e70bc160bbb5)
       
### **SK_L5 - Lab introduction to magic and steps to load Sky130 tech-rules:**  
       
* For better graphics use command **magic -d XR**.
* Consider the example of simple failing set of rules of metal 3 layer. Either run this by magic command line **magic -d XR metal3.mag** or from the magic console window, **menu - file - open -load - metal3.mag**
       
![metal3_magic](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/595661b4-e79a-435f-ab52-9e0079613e02)
           
### **SK_L6 - Lab excercise to fix poly.9 error in Sky130 tech-file:**       
       
### **SK_L7 - Lab excercise to implement poly resistor spacing to diff and tap:**   
       
We have few drc errors and calls out a rule number. You can see these rules on google skywater pdk read the doc page.

From metal 3.4 drc rules, Via2 must be enclosed by metal3 by atleast 0.065u. Magic tablet is of using many derived layers and in which via is one. Via represents the area filled with contact cuts. Draw a large area of M3 contatc using mouse pointer hovering over the m3contact icon on the side toolbar. Now with cursor box around the m3 area, type command cif see VIA2. This create contatc cuts which are bloack sqaure shaped. These dont exist on the drawn layout, but they represent as mask layer VIA2, that will end up in the GDS Futher details about these are metioned in cif output section in tech file. The view we see is feedback entry and can dismiss it with feed clear We use snap internal command snap int for the cursor to move along the edge of the grid. There are few spacing rukes metioned like spacing between Via2 and metal 3 is 0.065u. If we put the curosor between the contact cut and drawn via edge and click box in tkcon command, we will get the distance. The tool automatically places and do spacing of the contact, there wont be any DRC errors and the distance will not be smaller than the specified one.

![image](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/87bb3d8a-debd-40cf-b2a0-cc3bd2e7e62c)
       
### **SK_L8 - Lab challenge excercise to describe DRC error as geometrical construct:**       
       
First load the poly file by load poly.mag on tkcon window. Finding the error by mouse cursor and find the box area, Poly.9 is violated due to spacing between polyres and poly.
       
### **SK_L9 - Lab challenge to find missing or incorrect rules and fix them:**       
       
       
       
       
       
       
       
       
       
       
