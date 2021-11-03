# RejsaCAN

RejsaCAN is a 3x5 centimeter small ESP32 based board aimed at car use that I put together for my own use in my assorted crazy car projects. The board has an on board CAN interface and can be powered directly from the car (5-24V). It also includes the option to auto shutdown so not to drain the car battery.

There is no bespoke code for the board apart from pin definitions, it's just a piece of universal hardware, but by using easy to use open source Arduino libraries it can be made to interface not only to various CAN buses, Network/Wifi and Bluetooth but to numerous sensors and other peripherals using the ESP32's built in interfaces.

If you think the board really would fit your project you can give me a holler at magnust@gmail.com. I had JLCPCB make and assemble my own small batch of boards.
  
You find 3D printable housings here:
-  <a href=3dprints>3D printable housings</a>  

and you find example code here:
- <a href=examples>Code examples</a>
  
Check out ideas and what I'm using the board for here: 
- <a href=-%20PROJECTS%20->projects directory</a>   
 
  
![blink](https://user-images.githubusercontent.com/32169384/139061702-0c1ab4f7-c37c-45c9-a2f5-edc9db0142e6.gif)

![3D-bottom](https://user-images.githubusercontent.com/32169384/138956826-b0159cc9-2b37-40f7-a675-4153993f79ef.png)


## ESP32 interfaces

- SPI bus
- I2C bus
- BLE (Bluetooth 4.2)
- Wifi (both as AP or client)
- Numerous TCP/IP standards (everything from simple http, mqtt, ajax, ntp to running a full webserver on it with a user interface)
- USB port (serial in/out)
- Analog input, PWM or analog output

## Examples

- Read CAN data and send back CAN packets to control the car (set to sport mode as default, lock doors when driving away, this is one of my current projects)
- CAN to BLE or network/Wifi bridge
- CAN interface for sniffing CAN bus with for example SavvyCAN
- Read I2C/SPI/analog sensor data and write to CAN bus for CAN bus based data loggers
- Publish live telemetric data on internet from Racechrono (I'm starting this project now) 
- Drive alarm beeper or LED to show status of CAN data (like my small project Money Shift Saver and also low oil pressure warning)
- Drive high power peripherals using a driver board
- Translate CAN data between two CAN buses (like my small project Current Gear HUD here on github)

- I have already made a connector board to attach the RejsaCAN on the back of the commonly available small ILI9341 touch screen.

## Ideas for peripherals

- A second CAN port (MCP2515 board)
- IR camera sensor arrays (MLX90xxx or AMG8833) to log tire, brake, drivetrain temperatures over BLE to Racechrono or CAN based loggers (like my project RejsaRubberTrac)
- Laser based TOF distance sensor to log suspension travel (I did this too with RejsaRubberTrac) 
- SPI or I2C based color displays to show CAN bus data like IC intake or oil temps or alarms
- SPI or I2C based color displays to show live telemetric data fetched over BLE from Racechrono
- Driver board to drive high power items
- Step motor drivers
- Multiple input analog or digital boards

# Functionality

## Auto shutdown

When the engine is running and charging the car battery the incoming voltage used to power the board is a little bit higher than when the engine is stopped. This can be used to automate board shutdown so not to drain the car battery.

As default the on board DC-DC power circuit will shutdown the whole board when the power voltage is below the "engine is running" threshold and boot up the board when it is above. This can be disabled by a small modification (a trace cut) on the board so it always runs regardless of voltage between 5V and 24V.

In addition to the above, once the board is up and running you can programmatically force it to keep running even if the voltage from the car drops below the threshold voltage if the engine is stopped. Keeping the board running regardless of the threshold is done by pulling a pin high forcing the DC DC converter to stay running. You can also monitor one input pin that will go low when the power voltage drops below the set threshold, to for example starting a timer to keep the board running during a pit stop or a red light, even if the car engine temporarily shuts down. 

Powering the whole board with 5V via the USB type C connector will also disable the on board DC-DC circuit's auto shutdown.
   
   
<img src=pics/matrix%20power%20scenarios.gif>
   
   
## CAN interface

You can hook the board up straight to the car's OBD2 port or attach it directly to any CAN bus. You just need to connect the four wires. 12V power, ground, CAN high and low. There is of course a bus termination resitor on the board, it can be disabled if not needed. More CAN ports can be added using cheap MCP2515 boards.

## Three on board LEDs  

The board has two LEDs that are controlled by pins on the ESP32. These can be used for anything, like indicating Wifi/BLE being connected, errors or whatnot. 

There is also a third LED that indicates that the board is powered on.

![2 0-photo](https://user-images.githubusercontent.com/32169384/138956858-b6349ac5-0dbd-4614-9e06-7fb566154747.jpg)

## Housing

Check out 3D printable housings in the <a href=3dprint>the 3D-print directory</a>

![small-housing(0)](https://user-images.githubusercontent.com/32169384/138956886-f83ddebf-1960-4e5f-990a-a6d5ac4cba14.jpg)

![obd2-housing](https://user-images.githubusercontent.com/32169384/140200102-75e56449-3a75-4f79-912c-df56c4e33605.png)

## Schematics

<img src=pics/Schematic_RejsaCAN%20v2.1.png>

## Connecting the board

I've used a widely available OBD2 splitter cable (flat cable) that has one male and two female connectors. I hook up the male connector to the car, cut off one female connector and wire the remaining pig tail cable into the RejsaCAN board and one female connector is then free for other equipment to hook up to the car.

Picture showing what wires to use but please measure your cable and don't trust all these splitter cables to be 100% identical. (the second female splitter connector is not visible in pic)

<img src=pics/OBD2%20splitter%20pinout.jpg>




