# Calculation for different components of PCB

General specs.
Battery powering the system is a 6v Lead Acid, voltage from 4-6 volt can be expected.
Blinkers are expected to use somewhere between 15-25W @ 6V, meaning min 2.5 A, max 4.1 A

## Relay, Optoisolator and relevant BJT.

The relay chosen to blink the blinkers is [J1021CS53VDC.45](https://www.digikey.no/en/products/detail/cit-relay-and-switch/J1021CS53VDC-45/14002015) 
Important specs are:
- SPDP contact form
- Contact current Rating, 5 A
- 150 mA coil current @ 3 V
- Non latching coil

While the relay itself should provide galvanic isolation for the system, an additional layer of safety for the microcontroller is added in the form of Optoisolator.

The Optoisolator used is [FODM8801A]([https://www.digikey.no/no/products/detail/sharp-socle-technology/PC81710NIP1B/7798258](https://www.digikey.no/no/products/detail/onsemi/FODM8801A/3133896))

This optocoupler should be driven by the STM32F4, this MCU's IO pins are driven at 3.3V, and has a maximum sink/source current per pin of 25 mA.
The optoisolator should be driven with a forward current of 20 mA, this can be handled safely by the mcu. A current limiting resistor is used to set this current. this is calculated by:

$$ R = {(Vdd-Vf) \over If}$$

Then using Vdd = 3.3 V, If = 20 mA, and Vf = 1.35V, the resustoir value is set to:

$$ R = {(3.3 V - 1.35 V)\over 10 mA} = 97.5 \ohm \approx 100 \ohm $$


Output of the optoisloator is rated for maxmimum 75 V, and 30 mA. Therefore this cannot directly drive the relay which requires 150 mA coil current. '
To solve this an NPN BJT is used, [PDTD113ZT,215](https://www.digikey.no/en/products/detail/nexperia-usa-inc/PDTD113ZT-215/1163780). This BJT has a maximum collector current of 500 mA which is enough.

The BJT has built in Bias for the pins.  $1 k\ohm$ Base resistor, and $10 k\ohm$ at the emitter. This means the BJT should at most draw:

$$I = V/R = 3.3 V / 1k\ohm = 3.3 mA$$
