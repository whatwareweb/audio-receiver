# audio-receiver
OSHW audio reciever and amplifier
![image](https://github.com/user-attachments/assets/4f015e63-ae5e-4899-b7e0-d035019090e2)

![0001-0060](https://github.com/user-attachments/assets/e6bd2177-1706-44fa-a885-5fde33961854)




### What is it
This is an audio receiver and amplifier with a classic design. I built it because I wanted to learn more about Class AB amplifier design and analog circuitry in general.

### Why use it
Class-D amplifiers, as used in receivers these days, offer lots of power, but the sound quality can be lacking.

Class-AB amplifiers, while less efficient and therefore harder to get high power output, have overall less distortion and can offer a better signal-to-noise ratio if designed properly.

The design of the amplifier portion is similar to amplifiers built in the so-called "Golden age" of Hi-fi audio, in the 70s and 80s. I wanted a Class-AB amplifier that had the great sound quality of products from times gone by, but with modern features such as digital screens, and without the clunky mechanical interfaces of older receivers.

### Goals
My goals for this project were to have good sound quality with modern features, and also to use industry standard practices for receiver assembly to make it easy to assemble.

### Features
 - Stereo audio amplifier
 - 4 input channels
 - Volume control
 - Digitally selectable inputs
 - OLED display with renamable inputs
 - 15w per channel output
 - All-analog signal path
 - 3 separate PCBs for low noise

### Usage
It is super simple, just hook up a line level signal to the RCA jacks on the back, and select your input and you're good to go!

### Wiring
To wire up the internal parts, simply connect the +/-5v line from the first power supply to the input board, the +5v line to the control board, and the +36v line from the 2nd power supply to the amplifier board, as shown in the PCB silkscreen. Then, using the Phoenix cables in the BOM, connect the Phoenix connectors together. 
![image](https://github.com/user-attachments/assets/c0c744b8-105f-4ebf-ae21-315923edc48e)


### PCB screenshots
![image](https://github.com/user-attachments/assets/5a289160-5d17-4d67-b57a-a452f3fbccd6)
![image](https://github.com/user-attachments/assets/708e6c93-590d-4da3-956e-3690656630c5)
![image](https://github.com/user-attachments/assets/b07cf53d-5b73-4520-8fc8-490e1c298acb)


## BOM
|Qty|Value                          |Mouser URL                                                                                                                             |Mouser PN            |price|lumped price|
|---|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|---------------------|-----|------------|
|2  |10uF                           |https://www.mouser.com/ProductDetail/Wurth-Elektronik/860020672010?qs=sGAEpiMZZMsh%252B1woXyUXj4jKQI6sNRw6%252B%2FnWw7D23Ww%3D         |710-860020672010     |0.11 |0.22        |
|6  |100uF                          |https://www.mouser.com/ProductDetail/Nichicon/UVR1H101MPD1TD?qs=sGAEpiMZZMsh%252B1woXyUXj9Qfu%2FLgQWnHf9Zyy1TLY94%3D                   |647-UVR1H101MPD1TD   |0.25 |1.5         |
|2  |100pF                          |https://www.mouser.com/ProductDetail/Walsin/YP501101K040BAND5P?qs=sGAEpiMZZMsh%252B1woXyUXj9Vc%2FsqQGnyVc97Ek7nEcX0%3D                 |791-YP501101K40AND5  |0.11 |0.22        |
|2  |2200uF                         |https://www.mouser.com/ProductDetail/Rubycon/35YXJ2200M16X25?qs=sGAEpiMZZMsh%252B1woXyUXj57M5zdvZVAFuY6LrCottNI%3D                     |232-35YXJ2200M16X25  |1.15 |2.3         |
|2  |33uF                           |https://www.mouser.com/ProductDetail/Wurth-Elektronik/860010672011?qs=sGAEpiMZZMsh%252B1woXyUXj4jKQI6sNRw6%2FzsPRxKesag%3D             |710-860010672011     |0.12 |0.24        |
|2  |100nF                          |https://www.mouser.com/ProductDetail/Walsin/YV101103Z060HAND5P?qs=sGAEpiMZZMsh%252B1woXyUXj9Vc%2FsqQGnyVkbUw7FMjgKQ%3D                 |791-YV101103Z60HAND5 |0.1  |0.2         |
|8  |1N4148                         |https://www.mouser.com/ProductDetail/onsemi-Fairchild/1N4148-T50R?qs=sGAEpiMZZMtbRapU8LlZD%252B6h%2FWulpAkrNJDKqwRgmZcB5SlWjKcc2w%3D%3D|512-1N4148T50R       |0.1  |0.8         |
|8  |UF4004                         |https://www.mouser.com/ProductDetail/Diotec-Semiconductor/UF4004?qs=OlC7AqGiEDlRgKmeDlLF1Q%3D%3D                                       |637-UF4004           |0.12 |0.96        |
|1  |Fuse Holder                    |https://www.mouser.com/ProductDetail/Eaton-Electronics/BK-1A5601?qs=sfCJykTDjbAGESUvg%2FlMZw%3D%3D                                     |504-1A5601           |0.5  |0.5         |
|1  |Screw_Terminal_01x03           |https://www.mouser.com/ProductDetail/Phoenix-Contact/1757255?qs=uD%2FdkN7XIa0ez8xszzicKg%3D%3D                                         |651-1757255          |0.93 |0.93        |
|1  |Screw_Terminal_01x04           |https://www.mouser.com/ProductDetail/Same-Sky/TB007-508-04BE?qs=vLWxofP3U2wnrmN2C1kFLw%3D%3D                                           |490-TB007-508-04BE   |0.94 |0.94        |
|1  |Screw_Terminal_01x02           |https://www.mouser.com/ProductDetail/Same-Sky/TB007-508-02BE?qs=vLWxofP3U2y6PFKAfCqKUQ%3D%3D                                           |490-TB007-508-02BE   |0.49 |0.49        |
|2  |BC559                          |https://www.mouser.com/ProductDetail/Diotec-Semiconductor/BC559A?qs=OlC7AqGiEDlWVUSYP2ErFQ%3D%3D                                       |637-BC559A           |0.1  |0.2         |
|4  |BD139                          |https://www.mouser.com/ProductDetail/STMicroelectronics/BD139-16?qs=RfHREzyZwW%252BVwEMhVd3zpQ%3D%3D                                   |511-BD139-16         |0.62 |2.48        |
|2  |BD140                          |https://www.mouser.com/ProductDetail/STMicroelectronics/BD140-16?qs=RfHREzyZwW%252BkgnSLCtGbjg%3D%3D                                   |511-BD140-16         |0.45 |0.9         |
|2  |MJE3055                        |https://www.mouser.com/ProductDetail/onsemi/MJE3055TG?qs=HVbQlW5zcXUpZ6jjVRRo8A%3D%3D                                                  |863-MJE3055TG        |0.85 |1.7         |
|2  |MJE2955                        |https://www.mouser.com/ProductDetail/onsemi/MJE2955TG?qs=HVbQlW5zcXV0Q1cBURTsUg%3D%3D                                                  |863-MJE2955TG        |1.23 |2.46        |
|4  |33k                            |https://www.mouser.com/ProductDetail/YAGEO/MFR-25FTF52-33K?qs=gt1LBUVyoHmEHRwLqpWLLA%3D%3D                                             |603-MFR-25FTF52-33K  |0.1  |0.4         |
|8  |2k2                            |https://www.mouser.com/ProductDetail/YAGEO/MF0207FTE52-2K2?qs=KUIzHt%2Fe91lZCf2OHy2lbw%3D%3D                                           |603-MF0207FTE52-2K2  |0.1  |0.8         |
|2  |100R                           |https://www.mouser.com/ProductDetail/YAGEO/MFR-12FTF52-100R?qs=oAGoVhmvjhzHogggiomzAA%3D%3D                                            |603-MFR-12FTF52-100R |0.1  |0.2         |
|2  |1k                             |https://www.mouser.com/ProductDetail/YAGEO/MFR-25FTF52-1K?qs=Uzd%2Fwh%252BZzhBCS7HxlKfPkQ%3D%3D                                        |603-MFR-25FTF52-1K   |0.1  |0.2         |
|2  |560                            |https://www.mouser.com/ProductDetail/YAGEO/FMP200JR-52-560R?qs=wcZjbqjoJehIyDJh2zs3Bw%3D%3D                                            |603-FMP200JR-52-560R |0.15 |0.3         |
|4  |2R7                            |https://www.mouser.com/ProductDetail/YAGEO/SQP500JB-2R7?qs=sGAEpiMZZMsPqMdJzcrNwl88Wd0KdECunjP3GAgCqls%3D                              |603-SQP500JB-2R7     |0.54 |2.16        |
|2  |12k                            |https://www.mouser.com/ProductDetail/YAGEO/MFR25SFTF26-12K?qs=sGAEpiMZZMsPqMdJzcrNwqpmsrDQJrmxnqH2%2F1fJqXZRHayDc4k%252B4A%3D%3D       |603-MFR25SFTF26-12K  |0.1  |0.2         |
|2  |2R7                            |https://www.mouser.com/ProductDetail/YAGEO/CFR-25JR-52-2R7?qs=sGAEpiMZZMsPqMdJzcrNwiPCnpFTGbbhiVnCR3xqnQk%3D                           |603-CFR-25JR-52-2R7  |0.1  |0.2         |
|2  |100nF                          |https://www.mouser.com/ProductDetail/Walsin/RD21B104K500A5HAND?qs=ZrPdAQfJ6DNDZtFW9mG29g%3D%3D                                         |791-RD21B104K500A5HA |0.19 |0.38        |
|2  |10uF                           |https://www.mouser.com/ProductDetail/TDK/FG28X5R1E106MRT06?qs=LtAzLad%252BoeUoMYHhhxs3zA%3D%3D                                         |810-FG28X5R1E106MR06 |0.45 |0.9         |
|1  |PJRAS4X2U01AUX                 |https://www.mouser.com/ProductDetail/Switchcraft/PJRAS4X2U01X?qs=mcPJWgAPNreWN%252BuSt4UsAA%3D%3D                                      |502-PJRAS4X2U01X     |5.22 |5.22        |
|1  |Screw_Terminal_01x04           |https://www.mouser.com/ProductDetail/Phoenix-Contact/1757268?qs=uD%2FdkN7XIa2BicmSj3mD7g%3D%3D                                         |651-1757268          |1.26 |1.26        |
|1  |Screw_Terminal_01x03           |https://www.mouser.com/ProductDetail/Phoenix-Contact/1757255?qs=uD%2FdkN7XIa0ez8xszzicKg%3D%3D                                         |651-1757255          |0.93 |0.93        |
|1  |Screw_Terminal_01x03           |https://www.mouser.com/ProductDetail/Same-Sky/TB007-508-03BE?qs=vLWxofP3U2zHYiGqNs1vAA%3D%3D                                           |490-TB007-508-03BE   |0.72 |0.72        |
|1  |CD4052B                        |https://www.mouser.com/c/?q=595-CD4052BE                                                                                               |595-CD4052BE         |0.6  |0.6         |
|1  |100nF                          |https://www.mouser.com/ProductDetail/Walsin/RD21B104K500A5HAND?qs=ZrPdAQfJ6DNDZtFW9mG29g%3D%3D                                         |791-RD21B104K500A5HA |0.19 |0.19        |
|1  |Screw_Terminal_01x04           |https://www.mouser.com/ProductDetail/Phoenix-Contact/1757268?qs=uD%2FdkN7XIa2BicmSj3mD7g%3D%3D                                         |651-1757268          |1.26 |1.26        |
|1  |Screw_Terminal_01x02           |https://www.mouser.com/ProductDetail/Same-Sky/TB007-508-02BE?qs=vLWxofP3U2y6PFKAfCqKUQ%3D%3D                                           |490-TB007-508-02BE   |0.49 |0.49        |
|5  |SW_Push                        |https://www.mouser.com/ProductDetail/Same-Sky/TS02-66-55-BK-260-LCR-D?qs=A6eO%252BMLsxmT6x4NEvNu8bQ%3D%3D                              |179-TS026655BK260LCR |0.1  |0.5         |
|1  |ATtiny84A-SS                   |https://www.mouser.com/ProductDetail/Microchip-Technology/ATTINY84A-SSFR?qs=TI%2F9gtmDCEEVjKMalwq6aQ%3D%3D                             |556-ATTINY84A-SSFR   |1.08 |1.08        |
|4  |heatsinks                      |https://www.mouser.com/ProductDetail/Same-Sky/HSS-B20-NP-12?qs=u4fy%2FsgLU9Mva%2Fp9%252ByZBdw%3D%3D                                    |n/a                  |0.59 |2.36        |
|1  |m3 bolts                       |https://www.homedepot.com/p/Hillman-M3-0-5-x-10-mm-Internal-Hex-Button-Head-Cap-Screws-20-Pack-44456/204801187                         |n/a                  |5.74 |5.74        |
|1  |m3 nuts                        |https://www.homedepot.com/p/Hillman-Metric-Hex-Nuts-M3-x-0-50-Coarse-Thread-4053/204801247                                             |n/a                  |6.62 |6.62        |
|1  |fuse holder                    |https://www.mouser.com/ProductDetail/Eaton-Electronics/BK-1A5601?qs=sfCJykTDjbAGESUvg%2FlMZw%3D%3D                                     |n/a                  |0.5  |0.5         |
|2  |fuses                          |https://www.mouser.com/ProductDetail/Schurter/0034.1519?qs=ar9f0rk5DXBZIZv2oGoEHA%3D%3D                                                |n/a                  |0.47 |0.94        |
|2  |red terminal post              |https://www.mouser.com/ProductDetail/SparkFun/PRT-09739?qs=WyAARYrbSnb2d3ZiFmZgWQ%3D%3D                                                |n/a                  |0.75 |1.5         |
|2  |black terminal post            |https://www.mouser.com/ProductDetail/SparkFun/PRT-09740?qs=WyAARYrbSnbVb9GdE8xnVA%3D%3D                                                |n/a                  |0.75 |1.5         |
|2  |internal phoenix connector 3pin|https://www.mouser.com/ProductDetail/Phoenix-Contact/1757022?qs=sGAEpiMZZMvlX3nhDDO4ANTLkcKs1Zj3jcphtS8o9Tk%3D                         |n/a                  |2.89 |5.78        |
|2  |internal phoenix connector 4pin|https://www.mouser.com/ProductDetail/Phoenix-Contact/1757035?qs=sGAEpiMZZMvlX3nhDDO4AH7PhxHWF%252BlKb5jy%252B%2F%252BeCXE%3D           |n/a                  |3.85 |7.7         |
|1  |fan                            |https://a.co/d/h5aS2CF                                                                                                                 |n/a                  |15.95|15.95       |
|1  |dip16 socket                   |https://www.mouser.com/ProductDetail/TE-Connectivity/1-2199298-4?qs=fK8dlpkaUMvpL10rY9Abiw%3D%3D                                       |n/a                  |0.25 |0.25        |
|1  |36v psu                        |https://www.mouser.com/ProductDetail/MEAN-WELL/LRS-150-36?qs=vDxCgdWo2h82V5jS5IXvUQ%3D%3D                                              |n/a                  |19.8 |19.8        |
|1  |+ / - 5v psu                   |https://www.mouser.com/ProductDetail/MEAN-WELL/PD-2505?qs=V9a8iPeg90ze2O5SXmOiQQ%3D%3D                                                 |n/a                  |16   |16          |
|1  |oled display                   |https://a.co/d/fhCKttE                                                                                                                 |n/a                  |6.29 |6.29        |
|1  |Input switcher PCB             |n/a – pcbway                                                                                                                           |n/a                  |5    |5           |
|1  |control board pcb              |n/a – pcbway                                                                                                                           |n/a                  |5    |5           |
|1  |amp board pcb                  |n/a – pcbway                                                                                                                           |n/a                  |27.78|27.78       |
|   |                               |                                                                                                                                       |                     |     |            |
|   |                               |                                                                                                                                       |                     |     |            |
|   |                               |                                                                                                                                       |                     |     |            |
|   |                               |                                                                                                                                       |                     |     |            |
|   |                               |                                                                                                                                       |                     |     |            |
|   |                               |                                                                                                                                       |                     |     |            |
|   |                               |                                                                                                                                       |                     |     |            |
|   |Total                          |                                                                                                                                       |                     |     |            |
|   |163.74                         |                                                                                                                                       |                     |     |            |
