Sky130 Day1 - Inception of open-source EDA, openLane and Sky130 PDK:

SKY130_D1_SK2 - SoC design and OpenLANE:

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
       

Simplified RTL to GDSII flow:

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




