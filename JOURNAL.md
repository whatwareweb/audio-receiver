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

I learned a lot about class AB amplifier design and feedback circuitry, mostly the ESP's tutorial on how to design an amplifier. From this page, I learned how to modify this schematic to increase performance.

time spent:5 hours
