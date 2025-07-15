# Scanning tunneling microscope
## Piezo drivers
Two dual-channel OPA2227 op amps were used to combine signals from DAC in Z+X,Z-X and Z+Y, Z-Y configuration. One decoupling 0.1uF capacitor between each +-15V supply pin and analog ground was added.
## TIA - Transimpedance amplifier
A classic OPA627 TIA configuration with 100M Ohm feedback resistor was used. 5pF capacitor was used to limit osccilations. One decoupling 0.1uF capacitor between each +-15V supply pin and analog ground was added.
## Sample bias driver
At first one OPA2227 was meant to buffer and filter the bias voltage from DAC, however OPA227 was used as one channel would be left redundant, introducing potential unwanted parasitics. OPA227 was design as and inverting unity gain amplifier with a low pass filter.
##DACs
DAC8554 was scrapped due to its inability to output bipolar voltages. //edit: might be usable with A/B configuration
Solutions: 
A) merge two DAC channels with a differential OPAMP: + potentially higher resolution; - possible unwanted phase shift, signal may be delayed esspecially when using 8 channels is required
B) use one unipolar DAC with level shifting: + cheaper, resolution could be higher as with bipolar; - 4 level shifting op amps required (1 per channel), potentially inaccurate level shift ( voltage may be offserrt inaccurately, though this could be limited by using the dac within proper precise range and subtracting half of desired range with either reference voltage (may not be accurate) or using second chanel running at desired voltages as conditions should be more or less the same for the two channels of the DAC.
C) use a bipolar DAC: + ready out of the box solution, no shifting, no other components needed; - quite expensive, low availability here
