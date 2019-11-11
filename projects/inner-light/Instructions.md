Inner Light
===

| | |
|---|---|
| ![action](img/jacket-anim.gif) | ![blurry pic](img/jack-blur.png) |

1. [Intro](#Intro)
2. [Materials](#Materials)
3. [Design Overview](#design-overview)
4. [LED Rope Assembly](#led-rope-assembly)
    1. [Test Rope](#test-rope)
    2. [Cut to Length](#cut-to-length)
    3. [Sew Velcro to LED Rope](#sew-velcro-to-led-rope)
    4. [Sew Velcro to Jacket](#sew-velcro-to-jacket)
    5. [Wire LED Rope](#wire-led-rope)
5. [Electronics](#Electronics)
    1. [Power Cable](#power-cable)
    2. [Power Regulators](#power-regulators)
    3. [Raspberry Pi Soldering](#raspberry-pi-soldering)
6. [Software Installation](#software-installation)
7. [Electronics Housing](#electronics-housing)
8. [Complete Installation](#complete-installation)
9. [Wear It](#wear-it)
10. [Lessons Learned, Failures and Future Improvements](#lessons-learned-failures-and-future-improvements)
11. [References](#References)

Intro
---

The 'Inner Light' project is a light up wearable jacket.
LED 'rope' is strung along the inner lining of a faux leather jacket and provides a diffuse
lighting show that can be controlled by the wearer.

Many years ago, I saw [ch00ftech's](http://ch00ftech.com/2012/01/16/light-up-leather-jacket/) post about a
'light up' leather jacket that had LED lights sewn into the inner lining of a leather jacket.
The effect was very cool and I wanted to see if me and a friend, [star_carcass](https://www.instagram.com/star_carcass/),
could make our own but with a few upgrades, such as beat detection and custom patterns.

The 'Inner Light' project is the result of a collaboration with [star_carcass's](https://www.instagram.com/star_carcass/)
and myself.
I did most of the programming and electronics assembly while [star_carcass](https://www.instagram.com/star_carcass/)
did most of the design, sewing, wiring, final assembly along with the housing assembly for the battery and buck converters.

The jacket has a approximately 3 meters of LED "rope" that is controlled by a Raspberry Pi W Zero.
The Raspberry Pi acts as a WiFi hotspot and serves up a custom web interface for control of the LED strips.
The LED "rope" was chosen because of the diffusion.
The whole jacket runs off of a single 11.1V 5.5Ah LiPo battery.
We've run the jacket over three hours without issue and we expect the charge to last approximately around 5 hours or so
between charges.

Materials
---

| Item | Pic | Approx Cost | Source |
|------|-----|-------------|--------|
| LED RBG Rope (SK6812/SK6218, 5V) | | $20/m x 4m = $80 | [Amazon](https://www.amazon.com/gp/product/B07DN3QP4R) [Ebay](ebay.com/itm/5V-SK6812-LED-Neon-Flex-Tube-Pixel-Strip-Light-3535-RGB-Addressable-360-Round/273955416625) |
| Raspberry Pi W Zero | | $20 | [Amazon](amazon.com/Vilros-Raspberry-Starter-Power-Premium/dp/B0748MBFTS/) [Ebay](ebay.com/itm/Raspberry-Pi-Zero-W-Wireless-Wi-Fi-Version-w-2x40-Gold-Header-Ships-Same-Day/222858178477) |
| Micro SD Card (16Gb) | | $6 | [Amazon](https://www.amazon.com/Sandisk-Ultra-Micro-UHS-I-Adapter/dp/B073K14CVB) [Ebay](ebay.com/itm/SanDisk-16GB-32GB-64GB-128GB-Ultra-Micro-SD-Card-Class-10-98MB-s-Memory-Card-Lot/143318377880) |
| JST-XH Headers (2-pin and 3-pin, right angle) | | $9 | [Amazon](amazon.com/GeeBat-460pcs-Connector-Housing-Adapter/dp/B01MCZE2HM) [Ebay](ebay.com/itm/JST-XH-Connector-Terminal-Header-Assortment-Kit-Male-Female-RIGHT-ANGLE-90-Deg/292219710596) |
| AWG28-18 Crimping Tool | | $23 | [Amazon](amazon.com/IWISS-Professional-Compression-Ratcheting-Wire-electrode/dp/B00OMM4YUY) [Ebay](ebay.com/itm/SN-28B-Pin-Crimp-Plier-Tool-2-54mm-3-96mm-18-28AWG-Crimper-Tool-Dupont-JST-Molex/401949283529) |
| AWG24 Stranded Wire (various colors) | | $15 | [Amazon](amazon.com/StrivedayTMFlexible-Silicone-Electric-electronic-electrics/dp/B01LH1G2IE) [Ebay](ebay.com/itm/24-AWG-Gauge-Stranded-Hook-Up-Wire-Kit-25-ft-Each-0-0201-Dia-UL1007-300-Volts/371133252837) |
| JST SM m/f connectors (2-pin) (5 pair) | | $6 | [Amazon](https://www.amazon.com/gp/product/B07GGNFPQQ) [Ebay](ebay.com/itm/10-Pairs-Jst-Sm-2-Pins-Plug-Male-And-Female-Wire-Connector/323655645814) |
| JST SM m/f connectors (3-pin) (6 pair) | | $7 | [Amazon](amazon.com/ALITOVE-Female-Connector-WS2812B-SK6812-RGBW/dp/B071H5XCN5) [Ebay](ebay.com/itm/2pin-3pin-4pin-5pin-Male-And-Female-22AWG-LED-Strip-Wire-JST-SM-Plug-Connector/401741125239?) |
| Buck Converters (5v, 10A) x3 | | $10 x 3 = $30 | [Amazon](amazon.com/BINZET-Converter-Regulator-Regulated-Transformer/dp/B00J3MHTYG) [Ebay](ebay.com/itm/DC12V-24V-to-5V-10A-50W-Step-Down-Buck-Voltage-Converter-Module-Waterproof-IP68/312733329138) |
| Buck Converter (5v, 3A) (BEC) | | $3 | [Amazon](amazon.com/Ship-Hobbywing-Switch-mode-UBEC-Lowest/dp/B008ZNWOYY) [Ebay](ebay.com/itm/RC-UBEC-5V-6V-3A-Max-5A-Switch-Mode-Lowest-RF-Noise-BEC-Kit-for-RC-Models-Tool/352620354400) |
| Battery (11.1v, 5.5Ah) | | $40 | [Amazon](amazon.com/FLOUREON-5500mAh-Quadcopter-Airplane-Helicopter/dp/B072313FYS) [Ebay](ebay.com/itm/11-1V-5000mAh-3S-55C-Lipo-Battery-Deans-Plug-for-RC-Helicopter-Airplane-Monster/223292866369) |
| Fuse Holder (18Ga) | | $8 | [Amazon](amazon.com/KOLACEN-Automotive-Holder-Regular-Standard/dp/B07C5JGFRH) |
| Fuse (blade, 10A) | |  $20 | [Amazon](amazon.com/EPAuto-AE-009-1-Pieces-Assorted-Standard/dp/B01DYQ5T3O) [Ebay](ebay.com/itm/220-Pcs-Car-Blade-Fuse-Assortment-Assorted-Kit-Blade-Set-Auto-Truck-Automotive/303300580187) |
| SPST Rocker Switch (prewired) | | $10 | [Amazon](amazon.com/COOLOOdirect-Solder-Rocker-Switch-Toggle/dp/B071Y7SMVQ) |
| XT30 Connectors (2 pair) | | $10 | [Amazon](amazon.com/Female-Connector-150mm-Silicone-Battery/dp/B073WWWMQP) [Ebay](ebay.com/itm/4pcs-XT30-Plug-Male-Female-Connector-Silicone-Wire-for-RC-LiPo-Battery-FPV-Drone/383041434902) |
| Jacket | | $50 | [Amazon](https://www.amazon.com/gp/product/B01GKGWBCM) [Ebay](ebay.com/itm/Olivia-Miller-Womens-Faux-Leather-Moto-Biker-Jacket-with-Pockets/283175170552) |
| Velcro (non-sticky backed, 0.25 inch width, black) | | $13 | [Amazon](https://www.amazon.com/dp/B07PZS5D1W) |
| Curved Upholstery Hand Needles | | $5 | [Amazon](amazon.com/Dritz-9020-Curved-Upholstery-Needle/dp/B0009V0V5E) [Ebay](ebay.com/itm/7pcs-Curved-Carpet-Leather-Sewing-Needles-Upholstery-Canvas-Hand-Repair-New-Hot/254354399362) |
| Heavy Thread | | $10 | [Amazon](amazon.com/dp/B07QW8GZF2/ref=twister_B07QX5KR31) [Ebay](ebay.com/itm/69-92-138-Bonded-Nylon-Sewing-Thread-For-Outdoor-Leather-Upholstery-Canvas/254295021529) |
| Heat Shrink Tubing | | $8 | [Amazon](amazon.com/Ginsco-580-pcs-Assorted-Sleeving/dp/B01MFA3OFA) [Ebay](ebay.com/itm/280pcs-Cable-Heat-Shrink-Tubing-Sleeve-Wire-Wrap-Tube-2-1-Assortment-Kit-Box-Set/401747169106?) |
| Solder | | $15 | [Amazon](amazon.com/Rosin-Core-Solder-60-4oz/dp/B0006O933K) [Ebay](ebay.com/itm/60-40-Tin-Lead-Rosin-Core-Solder-Wire-Soldering-Sn60-Pb40-Flux-039-1-0mm-50g/372474772922) |
| Flux | | $15 | [Amazon](amazon.com/MG-Chemicals-Liquid-Leaded-Solder/dp/B005DNR01Q) [Ebay](ebay.com/itm/Delcast-Rosin-Soldering-Flux-Paste-Solder-Welding-Grease-50G/131373589900) |
| Sewing Machine | | $100 | [Amazon](amazon.com/Brother-XM2701-Lightweight-Buttonholer-Instructional/dp/B00JBKVN8S) [Ebay](ebay.com/itm/Brother-XM2701-Lightweight-Full-Featured-Sewing-Machine-with-27-Stitches-NEW/383233984209) |
| Soldering Iron | | $100 | [Amazon](amazon.com/Hakko-FX888D-23BY-Digital-Soldering-Station/dp/B00ANZRT4M/) [Ebay](ebay.com/itm/Hakko-Digital-FX888D-CHP170-bundle-includes-Soldering-Station-CHP170-cutter/183571277471?) |
| Rotary Encoder | | $5 | [Amazon](amazon.com/Cylewet-Encoder-Digital-Potentiometer-Arduino/dp/B07DM2YMT4) [Ebay](ebay.com/itm/US-Stock-3x-Rotary-Encoder-Switch-EC11-Audio-Digital-Potentiometer-Handle-20mm/382748544423) |
| Tap and Die Set | |  $35 | [Amazon](amazon.com/TEKTON-7559-Tap-Metric-39-Piece/dp/B00AHV3DWY/) |
| Bolts, Nuts (2M to 5M) | | $25 | [Amazon](amazon.com/DYWISHKEY-Stainless-Washers-Assortment-Wrenches/dp/B07QLRKYR7) |

### Optional

| Item | Pic | Approx Cost | Source |
|------|-----|-------------|--------|
| Laser Cutter (40W, CO2) | | $500 | [Ebay](ebay.com/itm/40W-CO2-Laser-Engraving-Machine-12-x-8-Engraver-Cutter-w-USB-Port/191857677830) |
| Plywood Stock (1/8") | | $20 | [Amazon](amazon.com/3MM-Baltic-Birch-Plywood-Engraving/dp/B07CHX1GTD) |
| Plywood Stock (1/4") | | $20 | [Amazon](amazon.com/6MM-Baltic-Birch-Plywood-Engraving/dp/B07HBC8NQ9) |
| Spray Paint (black) | | $5 | [Amazon](amazon.com/Krylon-K02754007-Fusion-Spray-Paint/dp/B07LFWTQJX) |

Design Overview
---

The Raspberry Pi Zero W controls all of the LED strips.
All the LED strips (or "neon rope") are wired in series to create a long single strand.
There are approximately 3M of LED strip or about 180 LEDs in total.

The LED "ropes" have velcro sewed onto their silicone housing and the complementary velcro
strip is sewn into the jacket.
Where the LED "ropes" join from the lapel to the collar, they are sewn together to create a
better aesthetic for when the "ropes" transition into each other.

There are six contiguous strips in all, two for the cuff, two for the lapel, one for the back lower
waist and one for the collar.
The mapping for how the LEDs show up is done in software on the Raspberry Pi.

There are three 5V 10A buck converters to power all of the LED strips.
The LED "rope" lights are 60 LEDs per meter.
The LED "rope" lights operate at 5V and each LED in the strip can potentially pull 60mA of current.
In theory this means that each strip only consumes about 3.6A in total, or about 18W, but in practice
the voltage drop across a meter of LED strip is so significant that multiple power sources need
to be deployed to make sure there is no color degradation from power loss.

To overcome the power losses, the three 5V 10A buck converters are used, with a single buck converter
power anywhere from one to three contiguous strips in the jacket.

The Raspberry Pi is put into a housing and connected to it's encoders for direct user input.
Software is installed on the Raspberry Pi to make it into a WiFi access point that a cell phone
can connect to.
The Raspberry Pi, in addition, runs a web service that can be connected to that sends signals
to the software controlling the LED strips.

There is a microphone attached to the Raspberry Pi that can be used in the 'sound reactive' mode.

The battery powers the three buck converts in addition to the smaller buck converter, or BEC, that
powers the Raspberry Pi.
The battery is itself put in a housing along with the buck converters and protected with a blade
fuse to provide short protection.
A toggle switch is also installed to allow for easy power on and off.

Note that while the fuse is technically not required, it is highly recommended as the battery
can push upwards of 100A that can cause fire, explosions, harm and death.
Please understand that the amount of power that is being pushed through is large and that
caution should be used when creating and using this jacket.
Before installing the fuse as an over current protection fault, one of the authors would periodically
explode wires due to stray shorts when assembling similar projects.

The software that runs on the Raspberry Pi consists of a few different components that can be briefly
summarized as follows:

* A web server to listen to web requests and update a config file depending on user options
* A beat server to listen to the microphone and generate 'beat' events
* An encoder server to monitor the encoder states
* An LED driver that loads a memory mapped file and pushes updates to the LED strip
* A manager program that loads the config file on updates, takes input from the encoder monitor and beat
  server and updates the memory mapped file of LED state

In addition there are other various monitoring scripts to restart processes that have failed.
The motivation for the profusion of programs is that each program should do one thing in isolation
without the strict dependency on any other programs.
This made development and testing easier as well as making sure each process is relatively isolated
from each other, providing better protection from one stray process affecting other parts of the
functionality.

All code is free/libre source and can be downloaded from [Github](https://github.com/abetusk/dev/tree/release/projects/inner-light).

LED Rope Assembly
---

References
---

* [ch00ftech: light up leather jacket](http://ch00ftech.com/2012/01/16/light-up-leather-jacket/)
* [GitHub: Inner Light](https://github.com/abetusk/dev/tree/release/projects/inner-light)


