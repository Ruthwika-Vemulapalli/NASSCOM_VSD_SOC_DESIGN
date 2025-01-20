# NASSCOM_VSD_SOC_DESIGN
DIGITAL VLSI SOC DESIGN AND PLANNING
SECTION-1: INCEPTION OF OPEN-SOURCE EDA,OpenLANE and Sky130PDK
In an embedded board, the part of the board that is considered as chip is only the PACKAGE of the chip which is a protective layer or packet bound over the actual chip and the actual manufatured chip is usually present at the center of a package wherein, the connections from package is fed to the chip by WIRE BOUND method which represents basic wired connection.

Inside the chip, all the signals from the external world to the chip and vice versa is passed through PADS. The area bound by the pads is CORE where all the digital logic of the chip is placed. Both the core and pads make up the DIE which is the basic manufacturing unit in regards to semiconductor chips

FOUNDRY is the place where the semiconductor chips are manufactured and FOUNDRY IP's are Intellectual Properties based on a specific foundry and these IP's require a specific level of intelligence to be produced whereas, repeatable digital logic blocks are called MACROS.

ISA (Intruction Set Architecture)
A C program which has to be run on a specific hardware layout which is the interior of a chip in your laptop, there is certain flow to be followed.
Initially, this particular C program is compiled in it's assembly language program which is nothing but RISC-V ISA (Reduced Instruction Set Compting - V Intruction Set Architecture).
Following this, the assembly language program is then converted to machine language program which is the binary language logic 0 and 1 which is understood by the hardware of the computer.
Directly after this, we've to implement this RISC-V specification using some RTL (a Hardware Description Language). Finally, from the RTL to Layout it is a standard PnR or RTL to GDSII flow.


There are mainly 3 different parts in this course. They are:
RISC-V ISA
RTL and synthesis of RISC-V based CPU core - picorv32
Physical design implementation of picorv32


Open-source Implementation
For open-source ASIC design implemantation, we require the following enablers to be readily available as open-source versions. They are:-
RTL Designs
EDA Tools
PDK Data
Initially in the early ages, the design and fabrication of IC's were tightly coupled and were only practiced by very few companies like TI, Intel, etc.
In 1979, Lynn Conway and Carver Mead came up with an idea to saperate the design from the fabrication and to do this they inroduced structured design methodologies based on the λ-based design rules and published the first VLSI book "Introduction to VLSI System" which started the VLSI education.
This methodology resulted in the emergence of the design only companies or "Fabless Companies" and fabrication only companies that we usually refer to as "Pure Play Fabs".
The inteface between the designers and the fab by now became a set of data files and documents, that are reffered to as the "Process Design Kits (PDKs)".
The PDK include but not limited to Device Models, Technology Information, Design Rules, Digital Standard Cell Libraries, I/O Libraries and many more.
Since, the PDK contained variety of informations, and so they were distributed only under NDAs (Non-Disclosure Agreements) which made it in-accessible to the public.
Recently, Google worked out an agreement with skywater to open-source the PDK for the 130nm process by skywater Technology, as a result on 30 June 2020 Google released the first ever open-source PDK.

ASIC design is a complex step that involves tons of steps, various methodologies and respective EDA tools which are all required for successful ASIC implementation which is achieved though an ASIC flow which is nothing but a piece of software that pulls different tools togather to carry out the design process.

OpenLANE Open-source ASIC Design Implementation Flow
The main objective of the ASIC Design Flow is to take the design from the RTL (Register Transfer Level) all the way to the GDSII, which is the format used for the final fabrication layout.

Synthesis is the process of convertion or translation of design RTL into circuits made out of Standard Cell Libraries (SCL) the resultant circuit is described in HDL and is usually reffered to as the Gate-Level Netlist.
Gate-Level Netlist is functionally equivalent to the RTL.
The fundemental building blocks which are the standard cells have regular layouts.
Each cell has different views/models which are utilised by different EDA tools like liberty view with electrical models of the cells, HDL behavioral models, SPICE or CDL views of the cells, Layout view which include GDSII view which is the detailed view and LEF view which is the abstract view

IMPLEMENTATION:
1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
2. Calculate the flop ratio.
   Flop Ratio = (No of D Flip Flops)/(Total number of cells)
   Percentage of DFF's= Flop Ratio*100

Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
Commands to invoke the OpenLANE flow and perform synthesis:

# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit












Calculation of Flop Ratio and DFF % from synthesis statistics report file
Flop Ratio = 1613/14876 = 0.1084296
Percentage of DFF's = 0.108429685*100 = 10.84296%

Section 2 - Floorplan and Introduction to library cells

Implementation
Section 2 tasks:-

Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
Calculate the die area in microns from the values in floorplan def.
Load generated floorplan def in magic tool and explore the floorplan.
Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
Load generated placement def in magic tool and explore the placement.
 Area of die in microns = (Die width in microns)*(Die height in microns)

 1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
Commands to invoke the OpenLANE flow and perform floorplan
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Now we can run floorplan
run_floorplan

According to floorplan def

1000 Unit Distance = 1 Micron

Die width in unit distance = 660685-0 = 660685

Die height in unit distance = 671405-0671405

Distance in microns = Die width in microns = Value in Unit Distance 1000 A 660.685 Місrons 660685 1000

Die height in microns 671405 1000 = 671.405 Microns

Area of die in microns = 660.685*671.405 = 443587.212425 Square Microns

3. Load generated floorplan def in magic tool and explore the floorplan.
Commands to load floorplan def in magic in another terminal
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &














4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
Command to run placement
# Congestion aware placement by default
run_placement



















Section 3 - Design library cell using Magic Layout and ngspice characterization
Implementation
Section 3 tasks:-
Clone custom inverter standard cell design from github repository Standard cell design and characterization using OpenLANE flow.
Load the custom inverter layout in magic and explore.
Spice extraction of inverter in magic.
Editing the spice model file for analysis through simulation.
Post-layout ngspice simulations.
Find problem in the DRC section of the old magic tech file for the skywater process and fix them.
1. Clone custom inverter standard cell design from github repository

# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

# Change into repository directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

# Check contents whether everything is present
ls

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &

2. Load the custom inverter layout in magic and explore.










3. Spice extraction of inverter in magic.
Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic


# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice



4. Editing the spice model file for analysis through simulation.
Measuring unit distance in layout grid









5. Post-layout ngspice simulations.
Commands for ngspice simulation

# Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice

# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a

Rise transition time calculation
Rise transition time = Time taken for output to rise to 80% - Time taken for output to rise to 20%

20% of output = 660 mV
80% of output = 2.64 V



Fall transition time = 4.0955 - 4.0536 = 0.0419 ns = 41.9 ps
Rise Cell Delay Calculation
Rise Cell Delay: Time taken for output to rise to 50% - Time taken for input to fall to 50%
 50% of 3.3V = 1.65V

 Fall Cell Delay: Time taken for output to fall to 50% - Time taken for input to rise to 50%
 50% of 3.3V = 1.65V
 Fall Cell Delay =4.07 - 4.05 =0.02 ns =20ps

 Commands to download and view the corrupted skywater process magic tech file and associated files to perform drc corrections

 # Change to home directory
cd

# Command to download the lab files
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

# Since lab file is compressed command to extract it
tar xfz drc_tests.tgz

# Change directory into the lab folder
cd drc_tests

# List all files and directories present in the current directory
ls -al

# Command to view .magicrc file
gvim .magicrc

# Command to open magic tool in better graphics
magic -d XR &


 


 Section 4 - Pre-layout timing analysis and importance of good clock tree
 Fix up small DRC errors and verify the design is ready to be inserted into our flow.
Save the finalized layout with custom name and open it.
Generate lef from the layout.
Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
Run openlane flow synthesis with newly inserted custom inverter cell.
Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
Do Post-Synthesis timing analysis with OpenSTA tool.
Make timing ECO fixes to remove all violations.
Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
Post-CTS OpenROAD timing analysis.
Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.


1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
Conditions to be verified before moving forward with custom designed cell layout:

Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.


Commands to open the custom inverter layout
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &

Commands for tkcon window to set grid as tracks of locali layer
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um


2. Save the finalized layout with custom name and open it.
Command for tkcon window to save the layout with custom name
# Command to save as
save sky130_vsdinv.mag

Command to open the newly saved layout
# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_vsdinv.mag &


3. Generate lef from the layout.
Command for tkcon window to write lef

# lef command
lef write

4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
Commands to copy necessary files to 'picorv32a' design 'src' directory


# Copy lef file
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy lib files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/


5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
Commands to be added to config.tcl to include our custom cell in the openlane flow


set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]


6. Run openlane flow synthesis with newly inserted custom inverter cell.
Commands to invoke the OpenLANE flow include new lef and perform synthesis

# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.

Commands to view and change parameters to improve timing and run synthesis
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
Since we are facing unexpected un-explainable error while using run_floorplan command, we can instead use the following set of commands available based on information from Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl and also based on Floorplan Commands section in Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md
# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or
Now that floorplan is done we can do placement using following command
# Now we are ready to run placement
run_placement

Commands to load placement def in magic in another terminal
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/24-03_10-03/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

Command for tkcon window to view internal layers of cells

# Command to view internal connectivity layers
expand


9. Do Post-Synthesis timing analysis with OpenSTA tool.
Since we are having 0 wns after improved timing run we are going to do timing analysis on initial run of synthesis which has lots of violations and no parameters were added to improve timing

Commands to invoke the OpenLANE flow include new lef and perform synthesis

# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis







   












