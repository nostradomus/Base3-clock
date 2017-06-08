### BOM - bill of materials

#### µ-controller board

Part     | Value                                             | Package      | Description  
-------- | ------------------------------------------------- | ------------ | ------------------------------------------------------------
R1       | 2.2kΩ                                             | 0207/7       | resistor                                            
R2,3,4,5 | 10kΩ                                              | 0207/7       | resistor                                            
LDR1     | [PGM5537](/pdf-files/datasheet-LDR-pgm5537.pdf)   | 0604/4       | light dependent resistor                                           
C1,2,3   | 100nF                                             | C050-025X075 | capacitor                                           
C4,5     | 22pF                                              | C2.5-2       | capacitor                                 
L1       | 10µH                                              | 0207/7       | inductor                                            
D1       | 1N5819                                            | DO41-7.6     | resistor                                            
LED1     | 3mm green                                         | 3mm          | LED                        
X1       | 32.768kHz                                         | TC38H        | RTC clock crystal                                            
X2       | 16MHz                                             | QS           | CPU clock crystal                                            
IC1      | [DS1307+](/pdf-files/datasheet-DS1307.pdf)        | DIL08        | I2C-Bus CLOCK/CALENDAR                                                            
IC2      | [ATmega328p](/pdf-files/datasheet-ATmega328P.pdf) | DIL28        | ATmega328p µ-controller             
IC1b     | 8-pin                                             | DIL08        | IC socket                                                            
IC2b     | 28-pin                                            | DIL28        | IC socket                                                                     
BAT1     | CR1220                                            | CR1220       | through-hole battery holder (CR1220)
BAT1b    | CR1220-3V                                         | CR1220       | 3 volt lithium battery
CON1     | 3-pin                                             | SIL03        | pin header to connect the µ-controller and LED board
CON2     | vertical µUSB                                     | µUSB-V-B     | vertical micro USB connector (type B) with power pins only
CON3     | 2x3 pin-header                                    | 2x3          | ICSP, AVR ISP-6 Serial Programming Header (optional)
CON4     | 5-pin                                             | SIL05        | pin header to connect the analogue slider board (optional)
CON5     | 2-pin                                             | SIL02        | pin header to connect the snooze button
CON6     | 2-pin                                             | SIL02        | pin header to connect RX and TX for the serial communication
CON6b    | 1-pin                                             | SIL01        | pin header to connect the GND for the serial communication
S1       | momentary                                         | 6x6x6mm      | momentary tact push button, button shaft length 6mm                        
S2,3     | momentary                                         | 6x6x16mm     | momentary tact push button, button shaft length 16mm                        
S2b,3b   | cap                                               | 6x6          | tact push button caps (white)                        

#### LED-board-pcb

Part    | Value                                        | Package      | Description  
------- | -------------------------------------------- | ------------ | -----------------------------------------------------
R1      | 4.7kΩ                                        | 0207/7       | resistor                                            
C1-12   | 100nF                                        | C050-025X075 | capacitor                                           
C13     | 10µF/16V                                     | E2-5         | polarized capacitor (radial)                                          
LED1-12 | [WS2812b](/pdf-files/datasheet-WS2812B.pdf)  | 5050         | intelligent RGB LED's
CON1,2  | 3-pin                                        | SIL03        | pin headers to connect the µ-controller and LED board
