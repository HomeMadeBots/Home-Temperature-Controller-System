# Home-Temperature-Controller-System
Describes a system allowing to control the temperature of your home.

## System overview

![system overview](http://www.plantuml.com/plantuml/proxy?src=https://raw.github.com/HomeMadeBots/Home-Temperature-Controller-System/master/uml/system_overview.puml)

### Boiler
The system "Boiler" is a home boiler that can be activated or deactivated by
respectively closing or opening an electrical circuit.

### Home temperature controller

The system "Home temperature controller" (HTC) shall pilot a boiler in order to
regulate the ambient air temperature of the home depending on settings from the
occupier.  
According to different operating modes, the system shall be able to regulate the
ambient air temperature of the home to configurable targeted temperatures
depending on the clock and the week day.
The system shall display the different settings, the current clock and the
measured ambient air temperature.

## System requirements

### Clock

* The HTC shall display the current clock i.e. the day, the hour and the minute.
* The HTC shall allow the occupier to set each parameter (day, hour, minute) of
the current clock.

### Home temperature
* The HTC shall display the current air temperature (in °C) of the home.

### Targeted temperatures setting

* The HTC shall allow the occupier to set two targeted temperature ("Low" and
"High").
* The HTC shall display the targeted temperatures ("Low" and "High") set by the
occupier.
* The "High" targeted temperature cannot be lower than the "Low" targeted
temperature.
* The "Low" targeted temperature cannot be greater than the "High" targeted
temperature.
* The targeted temperatures ("Low" and "High") shall be set between 15°C and 25°C.

### Modes setting

* The HTC shall allow the occupier to choose among 4 different operating modes
(Low, High, Normal, Homeday).
* The HTC shall display the mode choosen by the occupier.
* In "High" mode, the HTC shall regulate the home temperature to the configured
targeted "High" temperature.
* In "Low" mode, the HTC shall regulate the home temperature to the configured
targeted "Low" temperature.
* In "Homeday" mode, the HTC shall regulate the home temperature to the
targeted temperature (Low or High) depending on the clock as specified on the
following timing diagram.  
![homeday timing diagram](http://www.plantuml.com/plantuml/proxy?src=https://raw.github.com/HomeMadeBots/Home-Temperature-Controller-System/master/uml/homeday_timing_diagram.puml)
* In "Normal" mode, the HTC shall regulate the home temperature depending on the
week day.  
On Monday, Tuesday and Friday, the system shall regulate the home temperature to
the targeted temperature ("Low" or "High") depending on the clock as specified
on the following timing diagram :  
![workday timing diagram](http://www.plantuml.com/plantuml/proxy?src=https://raw.github.com/HomeMadeBots/Home-Temperature-Controller-System/master/uml/workday_timing_diagram.puml)  
On Wednesday and Thursday (home office) and on Saturday and Sunday (weekend),
the HTC shall regualte the home temperature to the targeted temperature ("Low"
or "High") depending on the clock as specified on the timing diagram for the
"Homeday" mode.

### Boiler management

* The boiler shall be activated or desactivated according to the following
statemachine (to avoid bounces) :  
![boiler management state machine](http://www.plantuml.com/plantuml/proxy?src=https://raw.github.com/HomeMadeBots/Home-Temperature-Controller-System/master/uml/boiler_management_state_machine.puml)

## Physical architecture

![HTC physical architecture](http://www.plantuml.com/plantuml/proxy?src=https://raw.github.com/HomeMadeBots/Home-Temperature-Controller-System/master/uml/system_physical_arch.puml)

Note that the battery actually provides power to the Arduino board, the LCD and
the relay.

### DS18B20

It is a digital air temperature sensor. Information is sent to/from the DS18B20
over a 1-Wire interface.

### LCD

It is a liquid cristal display drived using a HD44780 device. Seven digital pins
are needed.

### Keypad

It is a five buttons keypad connected to only one analog pin. The key value is
read through a five stages voltage divider.

### Relay

It is a normally open power relay drived through a digital pin.

### Arduino

It is an Arduino board (i.e. Leonardo).

## Electrical diagram

## Embedded software

The software loaded on the Arduino board of the HTC is described in 
[this repository](https://github.com/HomeMadeBots/Home_Temperature_Controller).