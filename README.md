Sky130 Day1 - Inception of open-source EDA, openLane and Sky130 PDK:

SKY130_D1_SK2 - SoC design and OpenLANE:

SKY_L1 - Introduction to all components of open-source digital asic design:

Digital ASIC Design:

Designing the digital application in an automated way requires several elemnets. The elements include hardware descriptive language, EDA tools and Process design kit (PDK) data
![digital_ASIC_design](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/2cd65f27-8f31-4cd3-bfc1-ce8ca5f1d35d)


Open source digital ASIC design:

![open_source_digital_asic_design](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/dbeedaef-770a-4510-93cc-6a56616fe18e)

PDK: PDK is the collection of files used to model a fabrication process for the EDA tools. It is the interface between designers and fabrication team. PDK includes 
       
Design rules such as DRC, LVS, PEX,

Device models,

Digital Standard cell Libraries,

I/O libraries, etc.
       

SKY_L2 - Simplified RTL to GDSII flow:

![simplified_RTLto_GDSII_flow](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/2d52f407-778f-428f-a059-f61746930e06)

The flow includes the following steps,

Synthesis

Floorplan/Power planning

Placement

Clock Tree Synthesis

Routing

Signoff

Synthesis: This stage converts RTL to the circuit out of components from the standard cell library (SCL). This is usually referred to as Gate level netlist. 

![synthesis](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/3a69b3c9-b655-4609-bfcc-d5b8066d9db2)

Each standard cell has regular layout.

Dimensions of the cell differ from eah other.

Each cell has different views or models,

i. Electrical (delay), HDL, spice

ii. Layout (Abstract and detailed).

Floorplan: Size and shape of the die, Macro placement, I/O pins placement, rows definition and power planning are done in Floorplan.

![floorplan](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/daaedeb0-7da9-4741-8531-ac05d8d6a74d)

In power planning, power is circulated using power grid which has alternate horizontal and vertical pattern of metal layers. Power grid is built using rings, stripes, and power is evenly distriuted. Higher metals layers are used for the routing of power as they are thicker (wider), thus reduces the resistivity. This helps for less IR drop and electromigration.

![power_planning](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/d24da1df-57d1-4b68-b3b4-6ba059beb12b)

Placement: 

According to the netlist, cells are placed in their resepctive locations and cells might overlap, so we do detailed placement to avoid the overlapping and flipped to save site row area (cells are legalized).

![placement](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/cb5c4de7-6a2f-44eb-a4c5-4f3d2bc4624f)

![placement1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/f51d9dd9-8bf3-462b-a5b0-46da882e4008)

Clock tree synthesis:

Building a clock tree such that clock reached every clock pin of a sequential block with min skew and insertion delay.

![cts](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/f4946890-8efe-49d6-9845-80b53aa6664d)

Routing:

After clock, Signal routing takes place. For each metal layer PDK defines thickness, pitch,width, tracks etc.

![routing](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/57db0967-9581-45f9-935f-dbce47ae764b)

SKY130 has 6 layers. The lowest layer is used for interconnects and is made of titanium nitride and all 5 layers are aluminium. Most routers are grid routers and metal tracks form a routing grid. since the grid is huge, we use divide and conquer approach. Global Routing is performed using coarse grained grids generating routing guides. Fine grained grids uses these routing gudies and impplement the actual routing between wires.

![routing2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/6b8a6df1-fb7f-469c-99b6-319f1ad932b3)

Signoff:

Once Routing is done, we do verifictaion during signoff

1. Physical verification :
Design rule checks (DRC) : verifies whether our design meets design rules. (performed by MAGIC) Layout vs schematic (LVS) : verifies whether our layout matches with the netlist schematic.(MAGIC AND NETGEN).

2. Timing Verification : Static Timing Analysis : Checks whether our design meets all teh timing constraints and is running with the designated frequency.

![signoff](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/2859e628-91c4-4cd3-aeec-a58c451c5af1)


SKY_L3 - Introduction to OpenLANE and strive chipsets:

OpenLANE ASIC flow:

![openlane1](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/921304b8-c487-41e8-b2e5-e7cbf960a627)

![strive](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/a05b76f6-0713-4fdc-a09c-56d037c5c208)

Main goal is to produce clean GDSII without human help.

Clean GDSII means, having no

1. LVS violations

2. DRC violations

3. timing violations


SKY_L4 - Introduction to OpenLANE detailed ASIC flow design:

OpenLANE ASIC flow:

Two modes of operation of openLANE is:

autonomus - its like a push button flow, does everything automatically
Interactive - runs through commands

![openlane2](https://github.com/shubhagore/openlanePDworkshop/assets/135098553/851e2411-a8f4-4f2b-8bea-3387a2b6a963)

The flow starts with RTL synthesis. RTL is fed to YOSYS with the design constraints and translates into netlist then optimised and mapped into the synthesizable cells from Standard cell library (SCL) using ABC. ABC is used during optimization. When it comes to OpenLANE we have stratagies where some tragets least area and the other on best timing, this is called SYNTHESIS EXPLORATION.
