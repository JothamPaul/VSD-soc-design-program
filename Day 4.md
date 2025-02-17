# Pre-layout timing study and the value of a well-designed clock tree

Utilizing Delay Tables for Timing Modeling and Transforming Grid Data into Track Data 
This section will cover the conversion of grid information to track information and timing modeling with delay tables. Let's dissect it in detail: 

## Timing Modeling with Delay Tables
### Delay Tables:

Information regarding the delay (propagation time) of signals via different components (such gates, wires, and interconnects) is provided via delay tables. 
These tables aid in estimating signal arrival timings and guarantee that the design is timed correctly. 

Delay tables are used to simulate the behavior of standard cells, macros, and other components during the physical design phase. 
They direct the routing and placement tools to maximize timing signal closure.

#### Converting Grid Info to Track Info 
In physical design, we need to translate grid information (such as rows and columns) into track information.
On each metal layer, tracks stand for predetermined vertical and horizontal paths.

When building standard cells, keep the following in mind: Input and output ports should align with the junction of vertical and horizontal tracks.
The width and height of the standard cell should be odd multiples of the track pitch and vertical track pitch, respectively.

### LEF File Extraction:

We need the LEF (Library Exchange Format) file for the inverter cell in order to continue.
Extract it from the current Inverter cell to offer vital information for the place-and-route (PNR) operation.
Open the tracks.info file to learn more about the horizontal and vertical tracks available on each metal layer.
This file specifies pitch, spacing, and other relevant details necessary for efficient routing.

# Day 4 Labs
![WhatsApp Image 2025-02-17 at 00 05 02](https://github.com/user-attachments/assets/7276f6f4-2a9f-4b62-a0f0-22a3ef810e6e)

![WhatsApp Image 2025-02-17 at 00 05 03](https://github.com/user-attachments/assets/18545a54-f8f1-4a3c-91bc-bc7530d74841)

![WhatsApp Image 2025-02-17 at 00 05 03 (1)](https://github.com/user-attachments/assets/2cb9e326-2245-4c0e-a083-7131886c946b)

![WhatsApp Image 2025-02-17 at 00 05 03 (2)](https://github.com/user-attachments/assets/f70c697f-75ad-4b40-9198-58cfcda72fb6)

![WhatsApp Image 2025-02-17 at 00 05 03 (3)](https://github.com/user-attachments/assets/9d7a28bf-730d-4305-9513-b42afc23f11a)

![WhatsApp Image 2025-02-17 at 00 05 04](https://github.com/user-attachments/assets/547200d8-7193-4367-99d2-5e9dce22989b)

![WhatsApp Image 2025-02-17 at 00 05 04 (1)](https://github.com/user-attachments/assets/02286a54-41d3-4e7c-95c7-3cbcdef85fc3)

![WhatsApp Image 2025-02-17 at 00 05 04 (2)](https://github.com/user-attachments/assets/39a4f82e-2df0-4134-9618-bd7dfc989391)

![WhatsApp Image 2025-02-17 at 00 05 05](https://github.com/user-attachments/assets/6c4cd77d-c907-4b77-82b5-7224ae844373)

![WhatsApp Image 2025-02-17 at 00 05 05 (1)](https://github.com/user-attachments/assets/4f383ef5-b236-40b4-895f-2adfbed88629)

![WhatsApp Image 2025-02-17 at 00 05 06](https://github.com/user-attachments/assets/10495af3-5290-417b-b700-3669d2e3d7fb)

![WhatsApp Image 2025-02-17 at 00 05 06 (1)](https://github.com/user-attachments/assets/7bd6c8e2-4709-4351-9239-71fc047370c2)

![WhatsApp Image 2025-02-17 at 00 05 06 (2)](https://github.com/user-attachments/assets/efa6b7f8-3781-433c-8f3f-ed65612b8426)

![WhatsApp Image 2025-02-17 at 00 05 07](https://github.com/user-attachments/assets/23a1e49f-5753-4126-82fa-d5086be968fb)

![WhatsApp Image 2025-02-17 at 00 05 07 (1)](https://github.com/user-attachments/assets/6fd6b5aa-d674-43a5-8352-4af522aaba33)

![WhatsApp Image 2025-02-17 at 00 05 07 (2)](https://github.com/user-attachments/assets/8d8fae83-8d94-409e-87db-4a7c05344d31)

![WhatsApp Image 2025-02-17 at 00 05 08](https://github.com/user-attachments/assets/0a635c7

![WhatsApp Image 2025-02-17 at 00 05 08 (1)](https://github.com/user-attachments/assets/f1e3bcae-47de-41c4-8433-fd53d8371477)

![WhatsApp Image 2025-02-17 at 00 05 09](https://github.com/user-attachments/assets/f116a152-f94f-4fbd-aedb-d558565e6bd5)

![WhatsApp Image 2025-02-17 at 00 05 09 (1)](https://github.com/user-attachments/assets/65a26d75-4c52-4808-9417-9d3076d1bbef)

![WhatsApp Image 2025-02-17 at 00 05 09 (2)](https://github.com/user-attachments/assets/9f66376a-c8a0-407c-904a-595001fab2ec)

![WhatsApp Image 2025-02-17 at 00 05 10](https://github.com/user-attachments/assets/f5ef9be9-c5b2-4b74-afff-84572ebdc174)

![WhatsApp Image 2025-02-17 at 00 05 10 (1)](https://github.com/user-attachments/assets/6a9c8e88-ad57-4527-ac26-2e469284d1a9)

![WhatsApp Image 2025-02-17 at 00 05 10 (2)](https://github.com/user-attachments/assets/5120e1b8-1ae2-44f8-9459-3956a307f0ab)

![WhatsApp Image 2025-02-17 at 00 05 11](https://github.com/user-attachments/assets/5cd58c81-9d15-41a4-995f-c12b75be7745)

![WhatsApp Image 2025-02-17 at 00 05 11 (1)](https://github.com/user-attachments/assets/b09a8267-80cf-482a-be67-86a70640c13c)

![WhatsApp Image 2025-02-17 at 00 05 12 (2)](https://github.com/user-attachments/assets/164c3fd6-331c-4286-92d4-8667f272dfab)

![WhatsApp Image 2025-02-17 at 00 05 13 (1)](https://github.com/user-attachments/assets/5edb4a01-4635-48cd-bc6f-a452887d92af)

![WhatsApp Image 2025-02-17 at 00 05 13 (2)](https://github.com/user-attachments/assets/7a021959-8468-4c21-84a8-16c62fee7630)

![WhatsApp Image 2025-02-17 at 00 05 13](https://github.com/user-attachments/assets/9f62efa3-2647-41d8-b124-a6b4ce224c60)

![WhatsApp Image 2025-02-17 at 00 05 14 (3)](https://github.com/user-attachments/assets/9e76e75d-9a79-4b93-9121-e34ced202d5a)

![WhatsApp Image 2025-02-17 at 00 05 16 (1)](https://github.com/user-attachments/assets/1f65c1fe-a040-4a66-be29-e808a286d98a)

![WhatsApp Image 2025-02-17 at 00 05 16 (2)](https://github.com/user-attachments/assets/2aba2c94-cac4-4e56-bbe4-23b13eb43807)

![WhatsApp Image 2025-02-17 at 00 05 16](https://github.com/user-attachments/assets/c25c8f49-1c0c-42d9-b76f-34a6d0a0f5a4)

![WhatsApp Image 2025-02-17 at 00 05 20 (2)](https://github.com/user-attachments/assets/b0f607f5-6629-4f99-b2e2-bc98af144c3a)

![WhatsApp Image 2025-02-17 at 00 05 23 (3)](https://github.com/user-attachments/assets/dc366e35-f7fa-4da8-b83f-48d59b9a0ff4)

![WhatsApp Image 2025-02-17 at 00 05 25](https://github.com/user-attachments/assets/e11b5d0c-a9ad-44d4-94ba-ea4ba3dadd7e)
