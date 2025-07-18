# Scanning tunneling microscope

## Piezo drivers
Two dual-channel OPA2227 op amps were used to combine signals from DAC in Z+X,Z-X and Z+Y, Z-Y configuration. One decoupling 0.1uF capacitor between each +-15V supply pin and analog ground was added.

## TIA - Transimpedance amplifier
A classic OPA627 TIA configuration with 100M Ohm feedback resistor was used. 5pF capacitor was used to limit osccilations. One decoupling 0.1uF capacitor between each +-15V supply pin and analog ground was added.

## Sample bias driver
At first one OPA2227 was meant to buffer and filter the bias voltage from DAC, however OPA227 was used as one channel would be left redundant, introducing potential unwanted parasitics. OPA227 was design as and inverting unity gain amplifier with a low pass filter.

## ADC - Analog to digital converter
Initially ADS1256 was selected to convert the signal from TIA to a digital signal for the microcontroller. Though, it was left as it could not accept bipolar input voltages. 

ADS8681 was used with pseudo-differential input and SPI communication protocol.

A unipolar ADC could be used if the input signal is shifted accordingly, using this configuration higher resolution might be possible at the cost of potentialy introducing some imperfections as a voltage reference and an additional op amp are required.

Buffering/filtering the output from OPA627 was considered but omitted at first, as OPA627 has high slew rate (55V/µs) and is fine to use with an ADC right away. TIA already has a small second order low pass filter + ADS8681's pseudo-differential configuration should clean up the signal - TIA AGND signal is subtracted from TIA Tip signal (both of them should pick up kind of the same noise)

However, one dual channel OPA1612 second order active low pass filter was added using 330R and 4.7nF resulting in a cutoff frequency of about 102.6 KHz. OPA1612 features insanely low noise (1.1 nV/√Hz at 1 kHz) and ultralow distortion (0.000015% at 1 kHz) mandatory for clean readings of the ADC. Even though it has around half the slew rate of OPA627, it should not slow down the process too much as measurements are not taken at a high pace.

For better accuracy REF5040 external reference was selected, as it provides the high accuracy reference voltage of 4.096V necessary for delicate apparatus.

## DACs - Digital to analog converters
DAC8554 was scrapped due to its inability to output bipolar voltages. *edit: might be usable with A/B configuration*
Solutions:

A) merge two DAC channels with a differential OPAMP: + potentially higher resolution; - possible unwanted phase shift, signal may be delayed esspecially when using 8 channels is required

B) use one unipolar DAC with level shifting: + cheaper, resolution could be higher as with bipolar; - 4 level shifting op amps required (1 per channel), potentially inaccurate level shift ( voltage may be offserrt inaccurately, though this could be limited by using the dac within proper precise range and subtracting half of desired range with either reference voltage (may not be accurate) or using second chanel running at desired voltages as conditions should be more or less the same for the two channels of the DAC.

C) use a bipolar DAC: + ready out of the box solution, no shifting, no other components needed; - quite expensive, low availability here

After careful consideration configuration C was used, mainly due to its simplicity and no centering or shifting problems. However, I will definitely still look into the other solutions in the future, as if properly calibrated, they might excel in terms of resolution (esspecially conf. A).

DAC7734 was selected based on its higher availibility and surprisingly lower price, although it is kind of old.
