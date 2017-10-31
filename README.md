# Project description
One of the most used instruments in a microbiology laboratory is the microbiological incubator, it is used for bacteria growth, incubation of cells and tempered storage. This project aims to create a incubator that can be fabricated in a typical makerspace environment at a low cost while achieving the same performance as commercial units. The incubator features a parametric CAD design to allow the users to modify it depending on their volume requirements. Finally, the proposed incubator has two power options: mains-powered mode and battery powered mode for portable instrumentation in remote environments. 

# Hardware
The incubator is designed in Autodesk Fusion 360 which is free to use by hobbyist users, academics and small startups. The user is able to select parameters related to the incubator dimensions. The incubator is designed in such way that it allows fabrication by a laser cutter and easy assembly. Currently, the incubator is tested only using acrylic however significant performance improvement can be achieved if Styrofoam is used instead. The latest version of the design files is available here: http://a360.co/2z1mDeq
![components](https://github.com/Sammy93/incubator/blob/master/components.png)
The figure above shows the main body components of the portable incubator. The first three components on the left have to be lasercut twice, the fan/heater holder and heater guard once, and the rails 6 times (4 times for the inside of the incubator to create glass slide holders and 2 times for the bottom of the incubator to create legs for thermal). 
The prototypes of the incubators were lasercut with 3 mm acrylic, the parameters for the laser cutting depend on the machine you are using but you want to use the lowest power/speed settings to ensure a good fit between the components. Once you have cut the different parts, they can be assembled and glued with superglue. You can buy an off-the-shelf acrylic glue but superglue works just as fine and you can get 8 tubes for £1 from Poundland. 
# Electronics
![electronic_components]( https://github.com/BioMakers/41_Low_cost_laser_cut_incubator_for_microbiology/blob/master/electronics.png)

In order to keep the project accessible to everyone, the electronics were kept to a bare minimum and only a pair of wire strippers and a screwdriver are needed (no soldering required). There are 6 main components which are shown on the figure below. The cheapest place to buy these components is from eBay or Aliexpress and the total cost comes down to approximately £30 including a mains power supply/charger and portable battery pack. 

[3D printer heater element](http://www.ebay.co.uk/itm/UK-3D-Printer-Extruder-Hot-End-12V-40W-Ceramic-Cartridge-Heater-6x20mm-RepRap-/142215386105?hash=item211cb293f9:g:z~wAAOSw2xRYVWfi) - £2.35

[Power bank](http://www.ebay.co.uk/itm/External-10000mAh-Power-Bank-Pack-Portable-USB-Battery-Charger-For-Mobile-Phone-/331757688400?hash=item4d3e4c9650:g:QeoAAOSwXXxZPiuU) - £8.49

[Arduino Nano](http://www.ebay.co.uk/itm/New-Nano-V3-0-For-Arduino-with-CH340G-5V-16M-compatible-ATmega328P-UK-Seller-/151765624720?hash=item2355efa790:g:aSkAAOSw3ydVvbcE) - £3.28

[5V 40 mm computer fan](http://www.ebay.co.uk/itm/5v-40mm-Computer-Cool-Mini-Fan-PC-Black-Cooler-Computer-Peripherals-/192216994492?hash=item2cc10692bc:g:qLgAAOSwvflZQQfQ) - £1.78

[DS18B20 temperature sensor](http://www.ebay.co.uk/itm/DS18B20-Digital-Temperature-Sensor-Chip-Dallas-TO92-Raspberry-Arduino-UK-SELLER-/171715143364?var=&hash=item27fb0526c4:m:myBBZo0GVfLRc0Tsm_0VqEw) - £1.38 

[Mains power supply](http://www.ebay.co.uk/itm/DC5V-2A-UK-3pin-USB-Charger-Wall-Plug-Power-Adapter-for-Tablet-PC-Ebook-Reader-/400643776728?epid=1387527207&hash=item5d483ae0d8:g:dtMAAOSwAodWFFHe) – £3.38

[Mix jumper cables](http://www.ebay.co.uk/itm/40-pcs-Dupont-Cables-M-F-M-M-F-F-Jumper-Breadboard-Wire-GPIO-Ribbon-Pi-Arduino-/131947670558?var=&hash=item1eb8b1ac1e:m:mRpNb6sdi9IYKOJOCgbTGfg) - £4.98

 
![electronic_schematic]( https://github.com/BioMakers/41_Low_cost_laser_cut_incubator_for_microbiology/blob/master/incubator_schematic.png)

The connection between the different components is described in the schematic below, the connection between individual components can be made using jumper cables. For the connection between the power bank/mains charger one requires stripping one end of an USB cable and exposing the power wires (red and black). These can then be twisted together with Male to Female jumper cables and screwed to the Vin/GND ports of the IRF520 (circled in black) and the 5V/GND ports of the Arduino. In addition, the fan should also be connected to the Vin/GND ports of IRF520. 
The wires for the heating element should be shortened, stripped and connected to the V+/V- of the IRF520 board (circled in orange). The SIG pin of the IRF520 (circled in blue) should be connected to the Arduino pin D2 using a Female-to-Female jumper cable, additionally the GND cable adjacent to the SIG/VCC should also be connected to the Arduino. 
![IRF520_connectors]( https://github.com/BioMakers/41_Low_cost_laser_cut_incubator_for_microbiology/blob/master/IRF520_connectors.png)

Finally, the temperature sensor should be connected to the Arduino with Female-to-Female jumper cables. It is important to also connected a resistor (~4.7 kOhms) between the DQ pin of the sensor and the 3.3V power pin (it can be avoided if you follow this guide: https://wp.josh.com/2014/06/23/no-external-pull-up-needed-for-ds18b20-temp-sensor/ but it is not tested). This can be done as shown on the photo below, please ensure that the temperature body itself is covered with insulation tape (this is a temporary solution until a better sensor packaging is developed). The DQ pin should also be connected to D10 of the Arduino. 
  
 
# Performance and software functionality
The performance of the assembled incubator was measured overnight; the temperature was set to 38 degrees setpoint and the resulting temperature fluctuations in the incubator were recorded over 12 hours. The ripple in the temperature is approximately 0.25 degrees which is below the noise limit/accuracy of the temperature sensor. The warm up time of the incubator was approximately 24 minutes which could be significantly improved if the incubator is insulated better. The average power consumption is approximately 0.7 A at 5V (varying between 0.3 A and 1.2 A depending on the ambient temperature) suggesting that the incubator is not insulated efficiently from the surrounding. For a 10,000 mAh power bank one can expect approximately 10 hours of operation but this may vary depending on whether the battery has a true capacity and the ambient temperature. The current version of the incubator relies on thermal insulation provided by the acrylic sheet however future plans including adding a layer of Calcium-Magnesium Silicate Thermal Insulation which should significantly improve the insulation or adding an air gap by using thinner two 2 mm sheets of acrylic instead of a single 3 mm. 
![performance]( https://github.com/BioMakers/41_Low_cost_laser_cut_incubator_for_microbiology/blob/master/performance.png)

 
# Photos of the incubator 
![incubator_side]( https://github.com/BioMakers/41_Low_cost_laser_cut_incubator_for_microbiology/blob/master/incubator_side.jpg)
![incubator_side]( https://github.com/BioMakers/41_Low_cost_laser_cut_incubator_for_microbiology/blob/master/incubator_inner.jpg)


