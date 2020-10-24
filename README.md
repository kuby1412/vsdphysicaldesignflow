# vsdphysicaldesignflow
This repository contains all the information needed to run RTL2GDSII flow using open source EDA tools. OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault and custom methodology scripts for design exploration and optimization.


# Overview of Physical Design flow
Place and Route (PnR) is the core of any ASIC implementation and Openlane flow integrates into it several key open source tools which perform each of the respective stages of PnR.
Below are the stages and the respective tools (in ( )) that are called by openlane for the functionalities as described:
- Synthesis
  - Generating gate-level netlist ([yosys](https://github.com/YosysHQ/yosys)).
  - Performing cell mapping ([abc](https://github.com/YosysHQ/yosys)).
  - Performing pre-layout STA ([OpenSTA](https://github.com/The-OpenROAD-Project/OpenSTA)).
- Floorplanning
  - Defining the core area for the macro as well as the cell sites and the tracks ([init_fp](https://github.com/The-OpenROAD-Project/OpenROAD/tree/master/src/init_fp)).
  - Placing the macro input and output ports ([ioplacer](https://github.com/The-OpenROAD-Project/ioPlacer/)).
  - Generating the power distribution network ([pdn](https://github.com/The-OpenROAD-Project/pdn/)).
- Placement
  - Performing global placement ([RePLace](https://github.com/The-OpenROAD-Project/RePlAce)).
  - Perfroming detailed placement to legalize the globally placed components ([OpenDP](https://github.com/The-OpenROAD-Project/OpenDP)).
- Clock Tree Synthesis (CTS)
  - Synthesizing the clock tree ([TritonCTS](https://github.com/The-OpenROAD-Project/OpenROAD/tree/master/src/TritonCTS)).
- Routing
  - Performing global routing to generate a guide file for the detailed router ([FastRoute](https://github.com/The-OpenROAD-Project/FastRoute/tree/openroad)).
  - Performing detailed routing ([TritonRoute](https://github.com/The-OpenROAD-Project/TritonRoute)).
  - Performing SPEF extraction ([SPEF_EXTRACTOR](https://github.com/HanyMoussa/SPEF_EXTRACTOR)).
- GDSII Generation
  - Streaming out the final GDSII layout file from the routed def([Magic](https://github.com/RTimothyEdwards/magic)).
- DRC & LVS
  - Performing DRC Checks & Antenna Checks ([Magic](https://github.com/RTimothyEdwards/magic)).
  - Performing LVS Checks ([Netgen](https://github.com/RTimothyEdwards/netgen)).
  
 # Setting up OpenLANE
 
 Detailed description on how to build and invoke openlane is given in this [link](https://github.com/njose939/openlane_build_script).
 
 Use the following example to check the overall setup:

```bash
./flow.tcl -design spm
```
The above flow.tcl command will run RTL2GDS flow for design named "spm" (non-interactive mode). Same can be done for other designs which are located ~/work/tools/openlane_working_dir/openlane/designs)

OpenLANE can also be run interactively as shown ([here](https://github.com/efabless/openlane/blob/master/doc/advanced_readme.md)).

