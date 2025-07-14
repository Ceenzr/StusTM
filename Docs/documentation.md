# Scanning tunneling microscope
## Piezo drivers
Two dual-channel OPA2227 op amps were used to combine signals from DAC in Z+X,Z-X and Z+Y, Z-Y configuration. One decoupling 0.1uF capacitor between each +-15V supply pin and analog ground was added.
## TIA - Transimpedance amplifier
A classic OPA627 TIA configuration with 100M Ohm feedback resistor was used. 5pF capacitor was used to limit osccilations. One decoupling 0.1uF capacitor between each +-15V supply pin and analog ground was added.
## Sample bias driver
At first one OPA2227 was meant to buffer and filter the bias voltage from DAC, however OPA227 was used as one channel would be left redundant, introducing potential unwanted parasitics. OPA227 was design as and inverting unity gain amplifier with a low pass filter.
