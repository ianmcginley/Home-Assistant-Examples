# These are my automations that I have for my aquatemp controlled pool heat pump (Astral Viron iHP195).

These are the full automation yamls that are loadable. My Device has an entity name of climate.aquatemp - yours might be different. This may or may not work with TUYA devices. Also depends on my Fronius Integration with consumption monitoring in place for the Solar entity use. Yours may vary in name and capability.


### Turn On Pool heater (this is the first automation that will run at start of day)
When feed into the grid is greater than 2.6kW (eg solar production - power consumption of the house results in a 2.6kW feed-in value for 10 minutes)
- turn on the heat pump
- set hvac_mode to auto
- set target temp to 35

### Turn Down Consumption of Pool (stage 1 of dropping power)
This sets the fan speed to low, to drop from auto status. The result in this is that the power draw of the Heat Pump could go from ~3kW-4kW down to ~2kW-2.5kW
This retains the target temperature however.

### Turn Down Temperature base on Inlet Temp (stage 2 of dropping power)
This sets the target temperature to 2.0 degrees LESS than the heat pump recorded inlet_temperature entity attribute. Also sets hvac_mode/fan to auto.
This has the result that the heat pump will go into an idle state as it as 'reached' the target temperature, but not turn the heat pump off.
Over about 10 minutes the heat pump will drop to about 900w and then eventually stop consuming energy.

### Turn Up Consumption of Pool (restore power levels)
When solar returns and my feed in starts to boost again, this automation returns back to auto and target temperature of 35. Back to initial conditions. 
Note, i don't both with stepping back up the chain, i go back to full power. In my experience I don't see the need.

### Turn Off Pool Heater at Sunset (end of day)
The heat pump is usually idling by now due to stage 2 of setting target temp to below inlet_temp, but I want to ensure it's properly off overnight.

### Creating a Calculation of effective heatpump output ###
This is a template sensor with some calculations in in that need to be explained.

        {% set flow_rate_lps = 2 %} 
        
Change the value to a best prediction of flow of water by your pump in litres per second

        {% set water_heat_capacity = 4.186 %}
        
This is an accepted value for the specific heat capacity of PURE water, however due to salt, chlorine, calcium, magnesium etc in the pool water it might be different - and research suggests lower, but probably is not affecting the calculation at all. If you want to simplify, set to 4.0. Units are Joules per Kilogram of water per degree Celsius - J/kg·°C.

        {% set hp_state = state_attr('climate.aquatemp', 'power') %}

This Gets the current state of the power system for the Climate Integration which is AquaTemp, the HACS plugin for my pool. If the HP is off, then it stands to reason any effective power out is 0.
