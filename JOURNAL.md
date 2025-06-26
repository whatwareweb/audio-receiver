---
title: "Audio Reciever"
author: "whatware"
description: "OSHW DIY audio reciever"
created_at: "2025-06-18"
---

total time spent: 35-40hr

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


# June 22 - basically just a ton of data entry 😭
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

# June 23  - Footprints, PCB layout and routing
First I continued on assigning footprints, it was basically just resistors left. One of the annoying things with resistors and capacitors is that some of the model names are super long and just a huge pain to decode to figure out what the right footprint is. I would go off of the Mouser description, but I found several examples of that being incorrect.
Another thing I found while assigning these footprints are that the component numbers of the resistors was somehow messed up when I copied over the hierarchical schematic, so I had to go in and fix that as well. I finally checked to make sure all the parts were in stock, and then it was time for pcb layout!

![image](https://github.com/user-attachments/assets/7541d769-4069-49cd-9c0c-911a2dc8cfe1)

When starting on the PCB layout, the very first thing I did was separate out the 2 channels and the screw terminals. This is so I could focus on layout of one audio channel, and then simply replicate that layout on the other channel. 
![image](https://github.com/user-attachments/assets/f229d68f-9b7a-4ff6-ad0a-53d8e11e6b97)

I started by laying out the large output to-220 transistors near where the edge of the PCB would be. This is because they will need a heatsink, which needs to be off the edge of the board. I also needed to space them a good bit apart as the 5w power resistors are extremely large. I then looked for the transistor heatsink I was going to use. A transistor heatsink is necessary in this case because the transistors can dissipate 6-8w depending on the load, which is a lot of heat. Due to this, I decided to go with the HSE-B381-04H heatsink, which dissipates a lot of heat for its small footprint, and it will do even better with a fan.

Otherwise, I just laid out the components similar to how they are on the schematic. Since this is a low-frequency analog circuit, it is not super critical about stray inductances and capacitances (except for the input, but more on that later), so it's fine to lay out components wherever generally (within reason).

![image](https://github.com/user-attachments/assets/a0ff537a-d2d7-4341-9d08-01a5e32a153b)


One thing that I had to learn to do was how to duplicate the layout. Because I used hierarchical schematics to replicate the component layout, it is possible to just duplocate the layout as well, chich i learned how to do from this youtube tutorial. https://www.youtube.com/watch?v=qqdjBNkwqCc

It was at this point that I realized that the layout i had made was terrible, because it was basically impossible to wire it up so that the input was not capacitively to the ouput. I tried to fix it, but i realized eventually that a new layout would be better, so I started over on the layout.

While routing, there were several traces that needed significant current flow, so for these I had to make extra-large traces.
![image](https://github.com/user-attachments/assets/d1eff19d-cd88-402d-800f-57c921cafc7c)

Here is the schematic mostly finished with the replicated layout for the second channel:
![image](https://github.com/user-attachments/assets/086fbeb4-0310-4c97-9f9d-aab5338b569a)

After completing the layout, here is what the board looks like;
![image](https://github.com/user-attachments/assets/43806eee-389f-4220-822c-315b5a223971)
and here's the 3d view:
![image](https://github.com/user-attachments/assets/6e937910-74af-4b4d-ae34-9aefaef173de)

OK awesome, the amplifier PCB is finished. Now, I need to get started on the input board pcb. This board is going to be based around the CD4052B, with some supporting components and 4 RCA jack inputs. It will also have a jack for the microcontroller to connect to to switch the input.

First thing is as always to get started on the schematic, so I added in the main IC. However, at this point I realized that it would be annoying to use this IC because it cannot output above and below the supply rails, so it would be better to use a different IC. Also, it has a pretty high resistance. However that's gonna have to wait for tomorrow because i'm out of time.

Time spent: 7h

# June 24 - lots of research on switching ICs
First thing I did today was look for an alternative for that IC. After like an hour and a half of searching, one thing that made it significantly easier was that I found an IC with a much much lower on resistance, the MAX4618, which is pin-compatible with the standard 4052. I also found this random Stackexchange post that showed how to DC-bias the analog voltage, which solved one of the problems I was having with biasing: https://electronics.stackexchange.com/questions/14404/dc-biasing-audio-signal . This method of biasing will reduce the amount of noise coming from the power supply via the capacitor on the resistor voltage divider. This will avoid switching noise from appearing on the input of the amplifier. I also found this great video explaining how to reduce the ESR of capacitors to be able to reduce switching noise as much as possible: https://www.youtube.com/watch?v=Bt1hi9C1Upk . Ant it somehow was my lucky day, because in the Youtube recommended page of that video, there was this video, which provided a ton more info on just what I was trying to do! https://www.youtube.com/watch?v=93teJFpJiZU
Sadly I had to go to bed after watching all these, but this is so much helpful information that i'll hopefully be able to finish this tomorrow!

time spent: 3h

# June 25 - 
Time to put everything I learned yesterday into practice! After watching the video, I decided to switch back to the cd4052b again 😭 However, this time I found a power supply on Mouser that can supply 5VDC and -5VDC, so that should work great for this application. I also realized, since the impedance of the main audio amplifier is so low, the ON-resistance shouldn't matter too much. However, I still do have to worry about decoupling capacitors especially for the IC, because any noise or ripple in the power supply will be audible in the audio signal. 

After drawing up the schematic for this input board, it looks like this: 
![image](https://github.com/user-attachments/assets/ec82f2b7-5af9-4a04-b554-5e3668945afd)

so now I need to assign footprints and find parts. During this process, I found a great part for the RCA connectors that had all 4 audio input jacks in one part. However, this was not compatible with my schematic, because it had all the jacks in one part. Luckily, Mouser had symbols available for this part, so I was able to download them off of their site. The symbol was pretty ugly though, so I just edited it to make it more similar to the existing coaxial connector symbol. This was my first time creating multi-unit symbols, so I had to learn how to do this, I found a great tutorial on the Kicad forums: https://forum.kicad.info/t/kicad-7-8-creating-schematic-symbols-with-multiple-units/47166

After drawing up the schematic, I double checked the circuit again just to be 100% sure. I did not find any mistakes, so I went aheead to designing the PCB. When I converted the scheamtic to PCB though, I found that one of the footprints was wrong, so I went ahead and changed that. Then I went ahead and routed the rest of the PCB. Here it is: 
![image](https://github.com/user-attachments/assets/9cda270e-6506-476b-891a-af5f7b31aa2c)
This routing was pretty self-explanatory and nothing really special about it. Here's the 3d view:
![image](https://github.com/user-attachments/assets/2814fda5-36de-4b92-93de-6dc28ed3c73f)

Magically, the 3d model for the RCA jacks seems to have been imported automatically when I downloaded the footprint and symbol from Mouser.

Next, with the input board finished, I needed to make the control board. I plan to build this control board around the Attiny84 IC, which is a very simple, cheap, and well-documented microcontroller which can work with the Arduino IDE. I also plan to have one of those really cheap OLED screens, and 4 or so buttons. For the OLED screen, I found great documentation on how to add this from the #hackpad channel in the slack.

Getting started on the schematic, luckily the Attiny chip was available in the default Kicad symbols, so that made that easy. Next, I followed this guide on Instructables to figure out how to hook everything up. https://www.instructables.com/Mini-Game-Console-With-ATTINY84-and-OLED-Display/ This guide is for a game console, but it has most of the same concepts as I'm using here in this control board. 

Here's the control board scheamtic:

![image](https://github.com/user-attachments/assets/f6a135c5-029f-4814-8b48-9b036173b7d1)
It includes the header pins for programming the Attiny, which will be necessary when uploading the software.

When I got to laying out the components, I decided to lay out the OLED screen horizontally on top of the 4 buttons, which were arranged into a D-pad and one button.

![image](https://github.com/user-attachments/assets/5e2987ac-e055-4635-bba7-5a611fe18a37)

Here is the 3d view of the finished board:

![image](https://github.com/user-attachments/assets/1b52a9d0-2237-4e90-a391-be2315fcfb8d)

and here's the layout:

![image](https://github.com/user-attachments/assets/d6cb069c-7942-4607-93c4-076550d106be)

OK, now with all 3 boards out of the way, it's time to start CAD. This is the part I think I will struggle with the most, because I've not had much experience. I've heard good things about Onshape before, so I'll make an account there and see if it lives up to the hype. I began by importing the 3D model of the amplifier PCB. I used this tutorial to be able to do so: https://deadbadger.cz/blog/importing-kicad-board-to-onshape . However, I then realized I had absolutely zero idea what I was doing, so I went and watched a Youtube tutorial on Onshape: https://www.youtube.com/watch?v=2utLjjkXpIg

I quickly made this box to hold the components:
![image](https://github.com/user-attachments/assets/eb28ab5a-5aa4-4fe1-87ab-d2225bacce1c)
and that is the main amplifier PCB model in there. 

ANd here is the cad finished! It's not the best, but since I am brand new to Onshape I think it'll do!
![image](https://github.com/user-attachments/assets/256e7402-3646-4cb0-b103-d9a268aeace9)

Time spent: 7h
