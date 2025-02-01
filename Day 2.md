# Sky130 Day 2 - Good floorplan vs bad floorplan and introduction to library cells
## Chip Floor planning considerations
### Utilization factor and aspect ratio
How do we come up with the height (H) and width (W) of the Core and Die 
 ![Image](https://github.com/user-attachments/assets/c3fb1cb5-5ef7-4000-bcc0-2d91b8595687)
Example: Basic netlist that has launch flop and capture flop
 ![Image](https://github.com/user-attachments/assets/96a1eebc-99be-4171-bf3a-7eddd13843f8)
 
Netlist defines the connection between all the components.
While defining the dimensions of the chip, we are mostly dependent on the dimension of the logic gates and Flip flops. 
 ![Image](https://github.com/user-attachments/assets/cbb6792b-310c-4845-b7fa-c1d2af0107c5)
 ![Image](https://github.com/user-attachments/assets/363c54d5-38e7-4f87-9a0b-2672dc152a56)
We are mostly interested in the dimensions of the standard cells and not the wires at the moment. We need to calculate the area occupied in the silicon wafer. 
Assume that the are occupied by one standard cell is 1 unit, the minimum space needed will be 2 x 2 = 4 square units.
 ![Image](https://github.com/user-attachments/assets/e14cdb68-0215-4ba7-be48-b90f11873537)
- Core is where we actually place the logic.
- Die encapsules the core. This is the area in which the core is built. And circuit will not exceed this area.
- This die is imprinted multiple times on the silicon wafer to increase its throughput.
![Image](https://github.com/user-attachments/assets/a3b47345-f3b9-4d92-89b5-bf81de3c4f78)
When we place the core within the die, it occupies 100% of the area. Which means 100% utilization. 
**Utilization factor = (Area occupied by the netlist) / (Area of the core)**
Utilization factor = 4 x 1 units / 2 x 2 units
Utilization factor = 1 
When utilization factor is 1 for example in the given picture. Your core is completely occupied and extra cells cannot be added. There is no space left.
In practical scenario we go for 50% to 60% utilization. Utilization factor is 0.5 or 0.6.
 ![Image](https://github.com/user-attachments/assets/d146e935-ac1e-4fee-8910-57a866e1d940)

**Aspect ratio:** 
Aspect ratio = Height / Width
= 2 units / 2 units = 1
When the Aspect ratio is 1, it signifies that the chip is a square shaped.
When aspect ratio is 0.5 or 0.6 it signifies that the chip is a rectangle shape.
![Image](https://github.com/user-attachments/assets/13597f9e-b7ff-4ae7-b7aa-7c0ed861dce8)
 
In the above picture, Utilization is 0.5 where we have more space to place more cells. 
Aspect ratio is 0.5 signifying that the chip is rectangle.
![Image](https://github.com/user-attachments/assets/36a9eac4-621d-4795-a62e-93be1acf4217)
 
The same 2 x2 cells are placed in a core of 4 x 4.
Here the utilization factor is 0.25, which means that 75% of the core is available for more placement of cells only.
Aspect ratio is 1 and hence the chip is a square.

### Preplaced cells:  
The are macros or Ips which are pieces of complex logics 
A combinational logic is taken and cut into 2 parts. The cut logics are placed in block 1 and 2. New connections are given ensure that the same function is retained.
 ![Image](https://github.com/user-attachments/assets/72b235ee-be94-4876-bc14-3d55c2dc6386)
 
The separate black boxes are implemented separately. Block 1 will have separate inout and output.  Block 2 will have input from block 1.
The advantage of separating the black boxes is that it can be implemented one time and it can be reused multiple times in the circuit.
 ![Image](https://github.com/user-attachments/assets/c5b01502-76c5-4fd9-878d-207c415d0186)
 
This is concept of reused models. Where we have small modules that can be reused on the top level. There are many other IPs readily available in the market. 
All of these can be implemented once and used multiple times. This has to be done before routing. Since they are done before automated placement and routing, they are called preplaced cells. 
 ![Image](https://github.com/user-attachments/assets/0fa8c1fa-d986-41e6-9e56-0736d7849d37)
 
Preplaced cells are placed depending on the design background. Arrangements of the IP’s in a chip is called floor planning. 
Once they are placed, the locations can’t be moved. 
We have the surround the preplaced cells with decoupling capacitors. 
In a circuit if the output switches from logic 0 to logic 1, there is a amount current demand that it needs. The charge will be sent form the supply voltage. It is the responsibility of the supply voltage to supply the necessary current to all the logic. Same way it is the responsibility of VSS to take the charge. When current flows through a physical wire to the circuit, there is a drop in voltage. Any physical dimension will have some resistance,. Resistance and inductance are repeated multiple times. The power supply might be 1 volt but when it reaches the circuit, it might not be 1 volt. It may be 0.8 or 0.7 volts. This output should be within the noise margin range. 
 ![Image](https://github.com/user-attachments/assets/2e91c0a2-5dc8-49b5-888d-4859e002c6d2)
If the voltage is not within the noise margin range, we might not get logic 1 as output. 
We solve this problems using decoupling capacitors. The amount of supply needed by the circuit is supplied by the decoupling capacitor. Since they are placed close to the circuit, there wont be any drop in voltage. Whenever there is a switching activity, the decoupling capacitor loses some charge to the circuit. When there is no switches happening, the decoupling capacitor replenishes its charge. 
 
![Image](https://github.com/user-attachments/assets/21a41d25-e046-43a1-8962-4202802e0794)
  ![Image](https://github.com/user-attachments/assets/2cc991bc-a9de-4c41-a4fc-cf013e125f4b)
  
Placement of decoupling capacitor close to the blocks.

### Power planning:
For a single macro the power problem was solved using a decoupling capacitor. But if we multiply the macro multiple times, power needs to be supplied to all the macros. 
 ![Image](https://github.com/user-attachments/assets/3c062d51-201d-4667-a64b-7d37567418d9)

When all the logic 1s are discharged from 1 to 0. The single ground which was supposed to be 0 there is a ground bump. If the bump exceeds the 0 threshold and reaches the undefined level, and can become unpredictable. 
 ![Image](https://github.com/user-attachments/assets/a99fc29c-586f-495e-8c02-fcf3e2c970dc)
If a single power source has to charge all the ones, there will be phenomenon called voltage droop. This lowering of the supply voltage. If it goes less than VDD. 
At the same time, VSS which was supposed to be at 0, it becomes higher. 
 ![Image](https://github.com/user-attachments/assets/74105c36-293e-4b70-b236-36ea2799a4f1)
Single source power supply.
**Solution:** If there are power supplies in multiple regions, this will not occur. 
 ![Image](https://github.com/user-attachments/assets/7b356b6d-d274-4adc-9453-63849fa177ec)
Multiple source power supply. Power can be taken from the nearest power supply. Or drop the power to the nearest ground. 
 
Before power planning 
![Image](https://github.com/user-attachments/assets/d434d319-ace7-47f8-b967-82f9ed38654a)
 
After power planning
![Image](https://github.com/user-attachments/assets/b88fdcee-84aa-4abd-8d73-fbd901c94ba2)

This is the reason why there are power meshes.

#### Pin Placement:
  ![Image](https://github.com/user-attachments/assets/f09e41b6-5904-4320-ae60-510fc71506bf)
  ![Image](https://github.com/user-attachments/assets/667d7fb1-e93e-4fce-b2d4-fd9d95531263)
  
Input side and output side depends on the designer and it varies.
Complete knowledge of the design is needed for pin placement. Front end team defines the netlist connectivity and backend team decides the pin placement
Clock pins are bigger than data ports. Clocks continuously drive the flipflop all the time. The least resistance path is needed.
 ![Image](https://github.com/user-attachments/assets/a8b8da16-0de6-4be3-b72a-5b06437e1307)
The area around the core is blocked for pin placement and no cells are placed in this area.
![Image](https://github.com/user-attachments/assets/3db2e265-d79e-4dc7-84ce-9a7555284c4d) 

Labs:
 ![Image](https://github.com/user-attachments/assets/8bca8806-b66c-4b49-b473-5c008b39d4e0)
![Image](https://github.com/user-attachments/assets/f943f48d-a57a-4e6f-94d7-4cd3222f8ac1)
 ![Image](https://github.com/user-attachments/assets/0776dfc0-6019-4a59-8086-a310d4573efc)
![Image](https://github.com/user-attachments/assets/10fad0c2-e688-4c4b-a166-7fabae13b55e)
![Image](https://github.com/user-attachments/assets/18753a52-632a-4058-8ba9-19e73d624521)
  ![Image](https://github.com/user-attachments/assets/7bd7979e-4739-429a-aeab-dd28eac1a54f)
![Image](https://github.com/user-attachments/assets/da282353-bcf7-418f-907c-9a23065b8ad5)
![Image](https://github.com/user-attachments/assets/e72de968-b683-4d36-b86f-2edc52578dca)
![Image](https://github.com/user-attachments/assets/950da8af-b643-49d2-861f-44e2ae9fafe5)
![Image](https://github.com/user-attachments/assets/7da015ae-9992-421f-b7e9-f9fd61af4366)
 ![Image](https://github.com/user-attachments/assets/b33e39c2-adbb-4db5-889b-17430424519a)
![Image](https://github.com/user-attachments/assets/63d94687-fc35-4fef-b6e7-03177a338995)
 ![Image](https://github.com/user-attachments/assets/d260c3cf-8e50-4583-b900-14eadcffd02e)
![image](https://github.com/user-attachments/assets/da63529d-453a-449f-aa3d-4d58820362c7)
![image](https://github.com/user-attachments/assets/2b756bc5-1445-465a-b2c2-6ba0e43dc010)
![image](https://github.com/user-attachments/assets/f4791eee-0696-4942-bc50-84d094005e4c)
![image](https://github.com/user-attachments/assets/b52e8d0b-f8d6-4a36-a10d-8176c7d41380)
![image](https://github.com/user-attachments/assets/e4d6521c-2518-4285-b5c5-9f9dba6270e5)
 

**Binding netlist with physical cells:**

The first step is to bind the netlist with physical cells 

 ![image](https://github.com/user-attachments/assets/52193f59-2df2-4bed-bdb2-5992886710da)

Give shapes and size to each of the gates
The blocks for each gate are available in the library. In different size as shown in picture.

**Placement:**  
![image](https://github.com/user-attachments/assets/d4c2f3fb-5c84-4750-a126-fa0c15af7fe2)

Place the netlist and place in the floor plan. 

**Optimize floor plan:**
![image](https://github.com/user-attachments/assets/f135f94e-c940-4693-88e1-0b7bfd5dcf54)

No big distance between the input, and output. 
 ![image](https://github.com/user-attachments/assets/07d72415-a381-4122-8c5e-76c967f17f5b)

Buffers are placed to bridge the distance between the flipflop and input. Repeaters will take the signal repeat or recondition, or reproduce and send it again.
No delay and this is a high frequency circuit. No delay. 
 ![image](https://github.com/user-attachments/assets/5965236e-238e-4c79-a7b7-7dd269cf528a)

If the distance is sufficient, no buffer is needed. Once the threshold limit is crossed, buffer is added.
![image](https://github.com/user-attachments/assets/5856e562-94f6-43b2-a5e4-8bd4bbe60b34)

 
After the placement, timing analysis is done to ensure that the placement is ideal.

##### Library Characterization and modelling:
The gates are modelling in such a way that it is understood by the tool. 
Steps: Logic synthesis   Floor planning  Placement  CTS routing

### Cell Design Flow 
Any of the cells placed are called Standard cells. In IC design flow, library keeps the standard cells.
Placement and routed version.
 ![image](https://github.com/user-attachments/assets/0feb8b3b-f1ff-4705-833f-deff90cde922)

Library has cells with different functionality, size, it has got cells with different voltage threshold. 
Cell design has 3 components  
![image](https://github.com/user-attachments/assets/90b65615-0b2e-4d21-adc6-c5002278135e)

Looking at an inverter:
Input from foundry
 ![image](https://github.com/user-attachments/assets/33c432bf-211c-43a7-a816-223a475c271a)
![image](https://github.com/user-attachments/assets/84d2d09a-2617-4bf3-a009-3745e39666e5)

 
**User defined specification:**
Cell height is defined by the library developer. 
Supply voltage – library owner designs the library cell based on the noise margin
Metal layer: certain libraries has to be built on certain metal layers
Pin location where the input and output
Drawn gate length

#### Design steps:
Implement the function
Model the transistor inorder to meet the library requirements
**Circuit design:**
 ![image](https://github.com/user-attachments/assets/549a000e-960c-43a8-bebd-cd1d41b0d17a)

**Layout design:**
Art of layout – Euler’s path and stick diagram
 ![image](https://github.com/user-attachments/assets/0a242aa6-38ac-4fd0-a429-1f9c4c28586c)

Layout part
 ![image](https://github.com/user-attachments/assets/83c7f928-d0ee-4102-a23f-3e255a981ef3)


#### Characterization flow:
1.	Reading the models
2.	Read the extracted spice netlist
3.	Define the behaviour of the buffer
4.	Read the subcircuits of the inverter
5.	Attach the necessary power sources
6.	Apply the stimulus
7.	Provide the necessary output capacitance
8.	Necessary command stimulation
Next to feed in all these inputs in 1 to 8 configuration file to the characterization software GUNA. This will generate timing, noise and power models. 

#### Timing characterization:
 ![image](https://github.com/user-attachments/assets/d3a79d8e-961d-4dfc-91c0-83c5eb13cf6e)

Based on these 8 values we will calculate others values.
Propagation delay:
Delay = Time(out_*_thr) – time (in_*_thr) 
 ![image](https://github.com/user-attachments/assets/05dac900-5202-495c-ba1b-d3ce35c82b08)

Negative delay is because of poor choice of threshold points
 ![image](https://github.com/user-attachments/assets/f8d1dcb8-8c0a-4514-be50-205206583eed)

Circuit is not designed properly and huge wire delays

Transition delay:
Slew rise = time (slew_high_rise_thr) - time (slew_low_rise_thr)
Slew fall = time (slew_high_fall_thr) - time (slew_low_fall_thr)
 ![image](https://github.com/user-attachments/assets/39fcab57-bb13-47d4-b72d-93731fcb8235)


