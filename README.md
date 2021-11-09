# Dimmable LEDs
Low voltage led lights designed to be strung in parallel. The brightness is controlled by amplitude modulation of a 500 Hz signal placed on top of the DC supply rail. 

## Features
* Output power adjustable from 100mW to 3-5 Watts (depending on how hot you want the junctions)
* Protection against reverse polarity connection
* Protection against supply under voltage
* With proper implementation, resistance of cable has negligable effect on brightness
* Fast rising startup edges and brief voltage spikes have no major effect

## Theory of Opperation
These lights take advantage of the fact that the ac imput impedance of each light is essentially infinite. The wires by comparason have very little impedance so there is negligiable voltage division even with impactical wire lengths.

### Signal Path
The rectified and then low pass filtered ac signal is used as the "voltage reference" for a constant current driver for the LEDs. The signal goes throught the following path.
1. ac coupling capacitor is used to remove the dc supply voltage
2. decoupled signal is amplified by a non-inverting amplifier with a gain of about 10
  * because the signal oscillates around ground and no negative supply rail is provided to the opamp this has the effect of rectifying the signal, but with gain and no diode drop.
3. The rectified signal is low pass filtered with an RC of ~ 80ms
4. This filtered signal used as the reference voltage in the opamp transistor current source with an emitter resistor of 3.3 ohms

### Under Voltage Protection
If there is insuffiecient voltage to turn on the LED's, but the ac signal is provided the opamp will drive as much current into the base of the npn as it can. If the opamp was simply connected to the supply rail, 30mA * 30V is about a watt and that would likely be unacceptable for a soic 8 opamp. Instead the positive supply pin is conneceted to a 5k resistor which goes to Vcc with a 10k resistor from the supply pin to ground. This limits to max possible current throught the opamp to just 6 mA and max power for the opamp happens around 3mA giving 50mW a very safe figure. The resistor could dissipate 200 mW worst case which is below rating. This has the additional benifit of allowing the use of lower voltage opamps, or add additional safety margin to rated maximum supply voltage.

### Start Up
 Due to the low pass filter the startup is quite gentle even if the supply rail has a fast edge.
