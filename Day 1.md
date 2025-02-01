# Inception of open-source EDA, OpenLANE and Sky130 pdk
## How to talk to computers
This is a typical electronic board (Arduino). The design generation is about the chip which is present within the circled part of the image. 

![Image](https://github.com/user-attachments/assets/a4297e83-89d9-4d3d-bcfe-eabccffc8f44)
 
This board can be described in the form of a block diagram. This is a typical board diagram of an Arduino board.
 
![Image](https://github.com/user-attachments/assets/4e056905-70f6-4e71-ac5a-b2d1deea8101)
If we open up the chip, it will look something like the below. 
![Image](https://github.com/user-attachments/assets/87ec91f5-8d7e-4f75-84e9-5446903e074e)

When we talk about a system, we call this as a package. QFN 48 Quad Flat No-leads
The inner connections of the chip looks like the below  
![Image](https://github.com/user-attachments/assets/ff76b118-e3dc-48b9-a93b-83c501d94950)

Chip is at the center of the package. The way that the chip is connected to the package are through the wire bombs. This helps to transfer the input coming from the outside world to the chip.
When we open the chip, it will have various components. There will be PADS which help signal transfer to the chip and vise versa. 
CORE is where all the digital logics are placed. Like AND gate NOR gate
DIE is the size of the entire chip.
 
![Image](https://github.com/user-attachments/assets/ff51efde-3493-4e18-aab5-6f5abe90e662)
A typical chip or the core consists of a SOC, SRAM, DSC, ADC0, ADC1, PLL and SPI. And couple of components. 
![Image](https://github.com/user-attachments/assets/9bd9eb24-ecf1-42e7-a969-fa6f1b92bdf6)

Foundry is an important term in chip design. All your devices are dependent of the Foundry. It is a big factory where chips are made. IP – Intellectual property. Foundry Ips are some intelligent techniques to build the building blocks.
![Image](https://github.com/user-attachments/assets/f04a3640-4799-4f2e-b4cb-610eddee28ea)

Macros: There is a clear distinction between Macros and Foundry IP. Macros are pure digital logic. 
If we need to manufacture the entire chip, Foundry is the one where we need to continuously communicate. There are some interface files, which the Foundry give and with the help of that we communicate with the Foundry. 

RISC-V Instruction Set Architecture (ISA).
This is the language of the computer. 
![Image](https://github.com/user-attachments/assets/6e8381a1-e290-46ff-a001-cfd99659dd2d)
 
If C program needs to be run on a hardware, or a layout. We have to pass the information to the particular hardware in certain terms. This C program is compiles in the assembly language program and is then converted to machine language program which is binary language program - Which is logic 1 and logic 0 which is understood by the hardware of the computer. The bits get executed in the layout. 
Risc-V 
![Image](https://github.com/user-attachments/assets/c95c759b-0a13-4e81-b759-07eb9a473567)

RISC-V architecture  Implementation program  Layout


### Application:
Application softwares runs on the hardwares. ISA is the answer. 
Application softwares enters into the system software. And system softwarevthen converts the application program into the binary language. 
#### Application software
Layers of system software
-	Operating system
  -   Handle IO operation
  -   Allocate memory
  -   Low level system function


-	Compiler
  -   C, C++, VB, Java is taken in
  -   Outout is the instruction
  -   The instruction is dependent on the hardware. Instruction that is implemented by the hardware	

- Assembler 
  -   Converts the instruction into binary language

Then it is understood by the hardware

 ![Image](https://github.com/user-attachments/assets/4141d6d4-e29c-462e-bf8f-2218b51c4c84)


#### Example of a stopwatch:
Input is in C language.
↓
Which enters in the compiler. (the hardware is a RISC-V)
↓
Output is RISC-V instruction
↓
Output of the compiler will go as the input of the assembler
↓
The Assembler will convert the binary numbers which will enter into the hardware.
 
![Image](https://github.com/user-attachments/assets/cc9914e8-c920-49e5-869e-37e1c32e06e8)
 
![Image](https://github.com/user-attachments/assets/b4d5fa53-0b00-46b4-9e40-c4b6009e8720)

The instruction from the Compiler is the Abstract Interface (instruction Set Architecture) or Architecture of the computer.
The instruction is add x6, x10, x6 (add registers, add content inside the registers)
Output of the compiler is a binary output.
RTL is needed to understand the specific instruction. This is the RTL implementation of the instruction set. 
RTL is synthesized into netlist (in the form of gates)
From netlist to the hardware is a physical design implementation of the netlist.

![Image](https://github.com/user-attachments/assets/3976efc8-bb14-4b10-a7f3-524b29877a7b)

 

## SoC Design using OpenLANE

#### Digital ASIC design
![Image](https://github.com/user-attachments/assets/1f0e39e6-d2b9-4072-ad34-f03e5a6297bd)
 
Designing 100% open source digital ASIC has been a dream. 
![Image](https://github.com/user-attachments/assets/3fc6734f-2074-45e2-bbf8-09f8a6d81348)

#### PDK: Process design kit
Collection of files used to model fabrication process of the EDA tools used to design an IC. 
- Process design rules: DRC, LVS, PEX
- Device models
- Digital Standard Cell libraries
- I/O Libraries

![Image](https://github.com/user-attachments/assets/d26289be-65c3-433d-a4b5-b657ae1b9a32)

ASIC flow objective: RTL to GDSII
Also called automated PnR and/or Physical implementation
![Image](https://github.com/user-attachments/assets/ffe79d68-1fa5-4f85-91ca-70c9e29a6165)
![Image](https://github.com/user-attachments/assets/2713d715-da82-43e2-b6e0-ae7742c27d1f)
 
 
SCL: Standard Cell Layout 
Standard cells have regular layout
Each has different views/models 
- Electrical, HDL, SPICE 
- Layout (Abstract and Detailed)
![Image](https://github.com/user-attachments/assets/0d8f2380-1e3f-43d0-b0e6-f9e403af13a7)

### Floor plan and Power Plan (FP+PP):
IT is based on whether you are implementing a single component (Macro) or the whole chip
The objective is to plan the silicon area and create robust power distribution to power the circuit
![Image](https://github.com/user-attachments/assets/f5fcc4f0-2245-4cda-8290-d38400beb745)
![Image](https://github.com/user-attachments/assets/8ab1f2ff-e9ba-47ed-a75a-bacdb49cee0f)

Micro dimensions and pin location, rows and routing tracts are defined.
![Image](https://github.com/user-attachments/assets/910abaf4-6cb8-4f95-bf4d-3ee785143d34)

The power planning is constructed typically a chip is powered by multiple VDD and ground pins. Power pins are connected through rings, horizontal and vertical metal straps. Such parallel structure are meant to reduce resistance and to reduce the electro magnetation problems. The power distribution network uses upper metal layers as they are thicker than lower metal layers hence have lesser resistance. 

### Placement: 
For the Macros Place the Gate-level Netlist on the rows. Connected cells should be placed closed to each other to reduce the interconnect delay. Also to enable successful routing. 
![Image](https://github.com/user-attachments/assets/85d28387-8d66-4eae-91af-e49d6e8124f0)
Placement is done in 2 steps
Global: Tries to find the optimal position for all the cells. Such positions are not necessarily legal. So cells may overlap or may go off rows. 
Detailed: The positions obtained from global position are minimally altered to be legal. 
![Image](https://github.com/user-attachments/assets/d8c10b0d-6970-4cb5-af32-bb1b15a20b25)

### Clock Tree Synthesis:
After placement, it is Routing. Before routing the signals, we need to route the clock. Need to create a clock distribution network. To deliver the clock to all cells. (eg. FF)
The clock distribution looks like a tree. The clock source is the roots, where the elements are the end leaves. The Clock tree is sysnthesized to deliver the clock to all things in good shape with minimum skew and minimum latency.
Clock skew means arrive of the clock to different components at different parts. 
Usually the tree is in H tree, X tree, Fishbone and hybrid of these. 
![Image](https://github.com/user-attachments/assets/1460e8ab-7149-49ab-88fb-c3ee2423e00a)

### Routing
 Signal Routing after placement. Given the placement and routing of clock, fixed number of metal layers is required to find a valid pattern of vertical and horizontal wires to implement the nets to connect the cells together. Router uses the available metal layer as defined by the PDK. Each metal layer PDK defines the thickness , the pitch, the tracks and minimum width. Also defines the VS that can be used to connect wire segments of different metal layers together. 
The Sky_ 130_pdk defines 6 routing layers. 
Lowest layer – Local interconnect layer – Titanium Nitrate layer
 The following 5 layers are all aluminium layers. 
Most routers are grid routers. They construct routing grids out of the metal layer tracks. As the routing grid is huge. Divide and conquer approach is usually used to generate routing guides. 
First global routing is performed using coarse grain grids to generate the routing guides. 
Detailed routing uses the fine grain grids and routing guides to implement the actual wiring. 

### Sign Off:
We can construct the final layout. Which undergoes verification.    Which includes Design Rule Checking (DRC) where we make sure that the final layout works or does not work.
Layout vs schematic (LVS): Make sure that the final layout matches the Gate-level netlist that we started with. 
Timing verification is done through Static Timing Analysis (STA) to make sure that all the timing constraints are met and the circuit will run at the designated clock frequency.

## Open Source EDA tools:
Problems with open source EDA tools
- Tools Qualification
- Tools Calibration
- Missing Tools

Open LANE is opensource and Free. Have to keep the credits and copyrights notice. 
OpenLane started as an open source flow for true Open Source Tape-out experiment.
striVE is a family of open everything SoCs, open PDK, Open EDA, Open RTL,
![Image](https://github.com/user-attachments/assets/7515f245-7d15-45e7-84a7-287b80a54b2a)

Main Goal of OpenLANE is to produce clean GSDII with no human intervention (No human in the loop). 
Clean means 
- No LVS violation
- No DRC violations
- Timing violations (WIP) – We are not there yet.

Open lane is tuned for SkyWater 130nm Open PDK; Also supports XFAB180 and GF130G 
Functional out of the box. 

Openlane can be used to harden Macro and Chips. It has 2 modes of operation.
- Autonomous: Push button flow – we configure the flow and based on the time we get the final GDS flow
- Interractive- We can run commands and step one by one. We can do experimentation and look at the results. 

#### Design Space Exploration:  
Can be used to find the best set of flow configurations and find the best values for them. 
Open Lanes comes with large number of design examples. (43 best design configurations) 

 ![Image](https://github.com/user-attachments/assets/54b491ba-4ab4-4dca-98f5-e1c6ddf01375)
 
Flow starts from Design RTL and ends with the GDSII format. TO function it needs the PDK.
RTL Synthesis: RTL is fed to the YOSYS with design constraints
YOSYS translates the RTL into a logic circuit using generic components.
This can be optimized and mapped into cells from the central cell library using abc. (ABC has to be guided during the optimization. This guidance comes in the form of abc script)  
Open lanes comes with several ABC scripts. We refer to them as synthesis strategies. We have strategies that basically target the least area. And also strategies that target the best timing. Different designs can use different strategies to achieve the objectives. For that we have the systhesis exploration utilility. This can be used to generate reports how the design delay and area is affected by the systhesis strategy. Based on this we can pick the best strategy to continue with. 

 ![Image](https://github.com/user-attachments/assets/98682f66-87d1-40eb-bc03-210d36602d42)
Design Exploration: used to sweep the design configuration and we have more than 16 of them and generate reports. It shows different design metrics and eventually we have more than 35 of them. Choose the number of violations generated after generating the final layout. This is very useful to find the best configurations for open lane in any given design. Also a clean layout. 

 ![Image](https://github.com/user-attachments/assets/502c65dc-7a17-46ee-9268-6ed04ed6f83a)
 
 The exploration utility is also used for regression testing (CI). We run open lane on 70 design and compare the results to the best known ones. 
 ![Image](https://github.com/user-attachments/assets/82abaede-0792-4364-8e5c-1341cc6efa3b)

#### Design for Test: 
After synthesis comes the testing structure insertion. If you want the design to be ready for testing after fabrication. This is an optional step.  
This step uses open source “Fault” 
 ![Image](https://github.com/user-attachments/assets/d8032f25-9bfc-427e-bc57-a1f0806d700d)

#### Physical Implementation:
Use Open ROAD App Automate PnR (Place and Route)
Floor/Power planning 
End decoupling capacitors and tap cells
Placement: Global and detailed
Post placement optimization 
Clock Tree Synthesis (CTS) 
Routing: Global and Detailed. (Use triton route)

We perform optimizations which involves some transformation of the Gate-level Netlist, that was generated by the synthesis step. We need to perform logic equivalence checking using YOSYS. We compare netlist resulted from optimization  done during physical implementation to the gate level netlist generated from the synthesis to make sure that they are functionally equivalent. 
- Everytime the netlist is modified, verification must be performed
- CTS modifies the netlist
- Post placement optimizations modify the netlist
•	LEC is used to formally confirm that the function did not change after modifying the netlist

#### Dealing with Antenna rules violation: 
- When a metal wire segment is fabricated, it can act as an antenna 
- Reactive ion etching causes charge to accumulate on the wire.

- Transistor gates can be damaged during fabrication. 
 ![Image](https://github.com/user-attachments/assets/f9754dbc-a3b4-4032-ac15-5f06818d5901)
Antenna collects changes and damages transistor wires connected to the gates. So length of wires must be limited to address such an issues. Usually is the work of the router. 

If router fails, two solutions
- Bridging: attaches a higher layer intermediary. Requires router awareness (not there yet).
- Add antenna diode cell to leak away charges. Antenna diodes are provided by the SCL. 
![Image](https://github.com/user-attachments/assets/4cf4bf0d-b99b-42c6-a038-b454c9d4a4d2)
 
Antenna diodes are inserted next to the place affected by the long wire segment.
With open lane a preventive approach created a fake antenna diode cell and added to the central cell library. We can add this to every cell input after placement. This is not a real diode but matches the footprint antenna diode. 
After routing we run antenna checker (magic) on the routed layout. 
If the checker report violations on the cell input pin, we replace the fake diode cell with the real one.
The Open Road – recent updates, antenna diodes are automatically inserted  when needed. Also includes the introduction of new tool ARC rules to check antenna rules violation during global routing. 
Have choose any of they methods to handle antenna violations. Either the open LANE approach or Open ROAD approach. 
The sign off in open lane involves a Static Timing Analysis, Design Rule Checking and layout vs schematic. 

#### Timing signoff involves 
- Interconnect RC extraction from the routed Layout followed by the 
- Open STA by Open ROAD
The result of this step is a set of timing report highlighting any timing violation.
 ![Image](https://github.com/user-attachments/assets/f894742e-b75e-4b87-aeaa-445ffdc1adb3)

### Physical verification DRC & LVS:
MAGIC is used for design rules checking SPICE extraction from Layout. 
MAGIC and Netgen are used for LVS 
- Extracted SPICE by Magic Vs. Verilog netlist 

### Open Lane: 
Open Lane is a flow which comprises of many open-source EDA tools. Like YOSYS which used for synthesis. Open SDA,  for SDA analysis. To completely automate the RTS to GDA flow and completely cutoff the human intervention. 

### Terminal on Linux Command
##### Change directory: cd
To go level up or down
##### Listing command: ls -ltr
Listing files in chronological order. 
 ![Image](https://github.com/user-attachments/assets/ff352ce1-e63c-423a-b7f6-a289d465911f)

##### Help: (command name)ls –help
Lists all the switches what do they mean.
##### Command: clear
Clears everything

We will be using PDKS file. OpenLane uses SkyWater 130nm which was recently made opensource. (sky130A)
Opening openlane: Using terminal
##### Open: 
/Desktop/work/tools/openlane_working_dir/openlane
Enter “docker”
Enter: ./flow.tcl -interactive
Enter: package require openlane 0.9

The entry point for OpenLane is the **./flow.tcl** script.
In order to run the flow, you need to execute the following command:
**./flow.tcl -design <design_name>**
For a design named picorv32a, the invocation would look something like this:
**Command:** ./flow.tcl -design picorv32a

 ![Image](https://github.com/user-attachments/assets/119d7f6b-0a37-49ee-b717-d611602893fc)
 ![Image](https://github.com/user-attachments/assets/8b7e7d86-ffeb-4fc7-8637-3fdc58cc1e98)

Command: prep -design picorv32a
 ![Image](https://github.com/user-attachments/assets/7484ee12-0968-45bd-ac7b-be8e7718a588)
 
Files updated in picorv32a
Runs folder created
 ![Image](https://github.com/user-attachments/assets/e079577f-d2da-43dc-a421-0a46736f50c2)
 
Run_synthesis successful
 ![Image](https://github.com/user-attachments/assets/ed04d020-78ce-455e-b7e2-552846eea487)

Find flip flop ratio:
FLIP FLOP RATIO = NO OF DFFs / NO OF CELLS * 100
Sky130_fd_sc_hd__dfxtp_2 / number of cells
1613 / 14876 *100 = 0.108429685 *100
**= 10.8429685%**

 ![Image](https://github.com/user-attachments/assets/ed9bbd37-a8d9-4b8a-8d07-54c1b1812aa3)

File created in Synthesis folder
 ![Image](https://github.com/user-attachments/assets/ed12e998-8ea7-4d65-9777-1db6ae6c2d2a)

