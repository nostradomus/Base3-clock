# :clock10: µ-controller based Ternary clock with colorful read-out

## What

At school, kids learn to count from 1 to 10 (probably because of the number of fingers on your hands ;-). As such, in daily life, the decimal system is by far the most popular, and most intuitive to use. Computer scientists tend to prefer [binary](https://en.wikipedia.org/wiki/Binary_number) (0-1) or [hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal) (x0-xF) systems. All of them are just a way of representing quantity (or whatever info you want) in a non-ambiguous way.

In a [ternary or base-3 systems](https://en.wikipedia.org/wiki/Ternary_numeral_system), only 0,1 and 2 are used. Being way less common, reading figures like 12201211 might make your brain-processor to get hot. The µ-controller driven clock in this repository is based on the ternary numeral system.

A web-version is already available in a [related repository](https://github.com/nostradomus/Base3-clock-webversion). In order to see a fully functional demo, click on [this link to our server](http://nostradomus.ddns.net/clock.html).

## Why

Some might find the idea a little crazy, others will say its fun. I think it is an excellent tool to train the brain... and I am probably having a twisted mind :laughing:

Anyhow, after having played around with javascript and css for the [web-version](https://github.com/nostradomus/Base3-clock-webversion), a new challenge popped up. I felt the need for a massive stand-alone living-room version.

## How

A first brainstorm storming session has resulted in a pretty complete [mindmap](docs/project-mindmap.mm) in the [docs folder](docs/).

![Project mindmap](images/project-mindmap.png)

`...more on the way, be patient...`

## Progress status

 - [x] have a [crazy idea](#why)
 - [x] write the [functional specifications](#how)
 - [x] build a proof-of-concept prototype
 - [ ] design and build the final [electronics](#electronics)
 - [x] write [code for the µ-controller](#µ-controller-code) respecting best-practices
 - [ ] design and build a [state-of-the-art housing](#mechanical-construction)
 - [ ] write an end-user manual

## Technical details

### How to read this clock

Each line or column (depending on how you mount the clock) represents a part of the time :

line | description | values
-----|-------------|-------
1 | hours | 00-23
2 | minutes | 00-59
3 | seconds | 00-59

Each element of the line represents one base-3 digit, with a different color for each possible value :
 - 0 : `light off`
 - 1 : `green`
 - 2 : `red`

In a horizontal configuration, the numbers should be read from right to left.

The rightmost element is the least significant trit (yes trit, not bit).

The leftmost element is the most significant trit.

### The Maths, a bit of theory...

The same way binary or decimal numeral systems are based on powers of their respective radices 2 and 10, the **ternary** system is based on powers of `3`.

trit    | least significant |       |        |         |          | ... | most significant
--------|-------------------|-------|--------|---------|----------|-----|-----------------
power   | 0                 | 1     | 2      | 3       | 4        | ... |
decimal | 1                 | 3     | 9      | 27      | 81       | ... |
range   | 0/1/2             | 0/3/6 | 0/9/18 | 0/27/54 | 0/81/162 | ... |

So to convert a ternary number to the decimal system, you have to start with the rightmost digit, multiply it with 3^0, multiply the next digit with 3^1, 3^2, and so on...

So for example (11021)ter = 1x3^0 + 2x3^1 + 0x3^2 + 1x3^3 + 1x3^4 =  (111)dec

The ternary numbers for the clock will have maximum 4 digits (max 3 for the hours).
 - `hours` : (000)ter - (222)ter => (0)dec - (26)dec
 - `mins/secs` : (0000)ter - (2222)ter => (0)dec - (80)dec

### Electronics

#### RTC module

One of the key components to build a clock is a basic RTC circuit. This piece of hardware will give you the correct time, and continue counting every second. A crystal driven oscillator will do this with minimum drift. Next, as you don't want to set the clock after every power cut (or after having it switched off for a while), we'll connect a small battery to the chip, to remember our settings, and to continue counting. For this clock I have chosen the [DS1307](pdf-files/datasheet-DS1307.pdf) from Maxim Integrated. The circuit is based on the specifications in the [manufacturer's datasheet](pdf-files/datasheet-DS1307.pdf). All communications with the chip will be over I2C. The only tricky part with this hardware is the [PCB layout](images/RTC-board-pcb.png) around the crystal and chip's oscillator section. No signal lines should cross these zones, unless protected by a ground plane in between.

[![RTC circuit](images/RTC-board-schematic-s.png)](images/RTC-board-schematic.png)      [![RTC pcb](images/RTC-board-pcb-m.png)](images/RTC-board-pcb.png)

#### RGB LED interface board

For the first version of this clock, I have opted for intelligent RGB-LED's as interface. It concerns [WS2812b](pdf-files/datasheet-WS2812B.pdf) LED's which need power and serial data. Each LED is having four connections (+5V, GND, data in, and data out). The µ-controller has to send all data as a long train of bits over only one datapin. Each LED, with its small built-in chip, will strip-off the first frame from data train on its data "in" pin, and transparently push forward all other frames on its data "out" pin. The µ-controller will, as such, produce twelve dataframes for each interface refresh. The twelve LED's, installed in three rows of four, are each having a specific function. The [LED pcb board](images/LED-board-pcb.png) has been designed as single layer. However the [WS2812b](pdf-files/datasheet-WS2812B.pdf) LED's being SMD components, the copper layer has been designed on the component side of the pcb. Depending on the mechanical requirements of your housing, the through-hole components can be mounted on either side of this pcb. It might however be a good idea to bend the capacitors lead 90° in case of mounting on the component side, to limit the overall height.

LED | c1         | c2       | c3       | c4
----|------------|----------|----------|-----------
r1  | mode       | hour mst | <......> | hour lst
r2  | minute mst | <....... | .......> | minute lst
r3  | second mst | <....... | .......> | second lst

[![LED interface schematic](images/LED-board-schematic-s.png)](images/LED-board-schematic.png)   [![LED interface PCB](images/LED-board-pcb-s.png)](images/LED-board-pcb.png)

#### µ-Controller board

The brain of the system is based on an [ATmega328p](pdf-files/datasheet-ATmega328P.pdf) µ-controller (yes, like the [Arduino UNO](https://www.arduino.cc/)). The choice was pretty obvious for multiple reasons. The design is easy, the IDE is well-known, specific libraries exist for the RTC and RGB LED's, and a hardware interface is available for the I2C protocol. The designed configuration is rather straightforward as well. Around IC2, some standard circuitry can be found. X2, C4 and C5 provide a stable clock for the controller. Reseting the running application can be done by button S1 (and R1). This will however not affect the clock time (stored in the RTC chip), or the alarm settings (stored in the ATmega's EEPROM). L1 and C2 provide smooth powering for the ADC inputs, which we will use for the dusk detection, and the optional color calibration module. CON3 is a so called in-system-programming connector update the application without having to extract the [ATmega328p](pdf-files/datasheet-ATmega328P.pdf) µ-controller. The whole system is powered by a standard USB power supply, to be connected to the micro-USB connector CON2. Optionaly, R1 and LED1 can be fit on the pcb as a power-ON indicator. As a simplified keyboard, S2 and S3 will get 'mode' and 'set' functionality. The required pull-up resistors are integrated in the controller, and set by software. IC1, X1, C1 and BAT1 represent the RTC part of the clock as described [above](#rtc-module).

`...more on the way, be patient...`

### µ-Controller code

`...on the way, be patient...`

### Mechanical construction

`...on the way, be patient...`

## Contributors

If you are having any good suggestions, just drop me a line [:email:](http://nostradomus.ddns.net/contactform.html).
If feasible, I'll be happy to implement proposed improvements.
And if you are having lots of time, I'll be happy to share the work with you ;-).

When you create your own version, don't forget to send us some nice pictures of your construction. We'll be happy to publish them in the :confetti_ball:Hall of Fame:confetti_ball:.

## :globe_with_meridians: License

There is no specific license attached to this project.

If you like it, have fun with it (at your own risk of course :-D), and especially, be creative.

Oh, and when using anything from this repository, it is highly appreciated if you mention its origin.
