---
title: "Audio Reciever"
author: "whatware"
description: "OSHW DIY audio reciever"
created_at: "2025-06-18"
---
# June 18 - setup and starting on schematic
Today i got the Git repo set up and started making the project with Kicad. This was my first Highway project so I had to learn how to set up the repo and submission and everything for that.

I got started first on the schematic of the audio amplifier itself, since that is the core part of this whole project. I did some research on various amplifier design philosophies, and decided on Class AB as it offers very high quality sound with decent efficiency. After a little more research, I decided to base my schematic design off of [Elliot Sound project 217](https://www.sound-au.com/project217.htm) because it offers a class AB design, around 62% efficiency (which is pretty good for a class AB design), good sound quality, and most importantly, a low input voltage requirement. Other amplifier designs require either a negative DC voltage or a high input voltage of 70 volts or higher, but this amplifier operates well at 24V and can even run down to 5V while still remaining functional. This decreases overall cost, because negative voltages are typically made using expensive linear power supplies.

I first constructed the basic amplifier design in the simulation software QUCS-S. The amplifier design seems to be performing excellent in simulation. The simulation model file for QUCS-S can be found in the PCB/sim directory of this repo.
![image](https://github.com/user-attachments/assets/250ab517-9d3b-48b7-bdea-d190320ca546)

I next reconstructed the schematic from the simulation into Kicad. I also added in a couple of tweaks to improve performance of the amplifier. First, I increased the value of the output capacitor from 1000 to 2200uF, which should help improve the low frequency (bass) response. Secondly, I changed out the 1N4004 diodes connected to the emitters of the power transistors for some UF4004 diodes, 2 in parallel for each diode there to hopefully reduce heat buildup and improve HF response.

One of the features of Kicad that I learned for this was creating hierarchical sheets. This is useful for this because I only want to have to create the schematic for the amplifier portion once. Then, I can use that hierarchical sheet twice in the parent sheet for both audio channels.
![image](https://github.com/user-attachments/assets/a089c318-e2e3-4696-9778-9ea1591eb5c4)

I learned a lot about class AB amplifier design and feedback circuitry, and LOTS of math that goes into calculating all the component values! The ESP site has another page that has a tutorial on how to design different kinds of amplifiers, so that was really helpful and explained everything super well. From that page, I learned how to modify the original schematic to increase performance.

time spent:5 hours

# June 20 - amp schematic, BOM, start work on input board schematic
The first thing I worked on today was setting up the hierarchical sheets. This is necessary so that I can make a schematic of each of the amplifier channels. I then connected all the pins to some screw terminals so that the multiple PCBs in this project can interconnect. I then double-checked the amplifier schematic again, just to be 100% sure I didn't miss anything.
![Screenshot_20250620_231847](https://github.com/user-attachments/assets/39ec94df-ca37-4ad9-9b21-68f34d0b4508)

Next, I started on the PCB design for the amplifier. I decided to keep the PCBs for the amplifier, the input board, and the digital board separate, because this helps avoid digital noise from the digital board interfering with the analog board. Also, I plan to use SMD components on the digital board, so keeping that separate from the analog and input boards will help make assembly easier.

To start designing the amplifier board PCB, I first needed to assign all the footprints for the devices, which I looked up components for on Mouser Electronics, adding parts to the KiCAD BOM in the meantime. Some things of note here is that I had to choose some high-voltage capacitors and some high-power rated resistors because this amplifier will have voltages in excess of 30 volts which is higher than many capacitors, and over 1W dissipated through the output resistors. I followed the ESP page for guidance on the capacitor voltages, as it has a readout of all the voltages in the amplifier. Also, for the fuse holder, apparently the official way to have a fuse and a fuse holder in Kicad is through a seemingly sketchy workaround where you add an extraneous component in the schematic where it is not present on the PCB.
![Screenshot_20250620_231909](https://github.com/user-attachments/assets/cb48a70b-ac86-498d-aa9e-092dd9fcf713)

I got bored of looking for components, and decided to switch gears to start designing the input board. I needed to research what kind of IC I would need to switch the audio inputs. I knew that I wanted the reciever to have a microcontroller and a display, and since the code would be so simple, I could probably just use a PIC chip or an ATTiny. This gave me several options for the audio input analog switch, including an analog mux IC, an analog switch IC, or keep it simple and use 2 back-to-back MOSFETS. I eventually decided to try the CD4052B, as it effectively offered 4 stereo inputs (technically 8 inputs but they are ganged together, so they're perfect for my use case) and only required 2 GPIO on the microcontroller to switch between the inputs. Another nice perk of this IC is that is included in Kicad by default, which just makes my life easier. However, I ran out of time at this point and had to go to bed.

Time spent: 4.5 hours


# June 22 - basically just data entry 😭
The first thing i did was to finish up on the BOM. Just more looking up products in Mouser, so pretty straightforward. One quirk I had to do was to pub another non-placed fuse holder in the schematic to appear on the BOM. A couple things of note were the resistor power values, I had to calculate those from the given example voltages in the schematic. For some of the higher-power resistors it was a little difficult to find resistors that fit the specs, so I had to learn a lot about Mouser's search features to find the resistors i needed.
![image](https://github.com/user-attachments/assets/eebd2d85-1adb-4742-867c-eaa6a9d3cfe4)

After that was the painful step of double-checking every single component I selected. I am always super paranoid about this because if I copy pasted any of the links in the BOM wrong. It is a good thing I did this, because looking through it, I found that the BC63916 and the BC640TA are are actually not truly complementary, and the BC639TA which would have been the correct replacement part is out of production. Therefore, I had to find substitute parts, and I settled on the BD139 and BD140. These transistors are also specifically designed for audio amplification, and have similar specs including the hFE gain, so they should work great. However, this transistor swap caused some confusion with the pinouts of the different transistors, so I had to double check the symbol and footprint editor to make sure they would end up in the right place. Also, doing this, somehow the numbers of all the transistors got mixed up, so I had to fix that. I eventually decided to just delete the second schematic sheet, and copy it later after I had finished making all the entries in the BOM, because it was causing a lot of hassle with the component ordering.

It was very lucky that I double-checked all the components, because I found an under-specced resistor R8, that was only rated for 600mW when it should have been at least a watt or 2. I also discovered that on R9 and R10 I had copied the wrong link into the BOM.
![image](https://github.com/user-attachments/assets/4f34bcd1-47d7-400f-b4b0-0418e28dd795)



The next thing to do was to decide on a type of connector for the internal wiring between the PCBs. I considered using standard Dupont or IDC style connectors, but those seemed too unprofessional for this application and would require a crimping tool as well. I also considered ribbon cables, but these would require SMD soldering. I eventually found phoenix connectors, as they had screw terminals so that custom cables could be easily made without a crimping tool. For the power, I found that barrier blocks seemed to be the best choice as they could handle more current. For the actual speaker terminals, binding posts are the standard type of connector found on amplifiers in recent years, and I figured that I could just connect screw terminals with wires from the PCB to the binding posts which would be screwed on the back of the cabinet. Since I had parts that would not be laid out on the PCB, I added those to a separate text BOM file.

Next up was to get the footprints assigned for all of the parts, but before I could do that, I had to retrieve the Mouser part number of all the Mouser devices.
![image](https://github.com/user-attachments/assets/a27eb3cd-aafa-4a3a-a9ce-72d30f2452c4)

With that out of the way, I started looking up all the part numbers on Mouser to get the correct footprints for the part. However, while doing this, I found that the transistors did not have the proper pin assignments in the footprint for the 4 power output transistors, so I had to fix that. However, I didn't get to finish all the footprints in time, so I left that for tomorrow.

Time spent: 6 hours
