# Occupancy and IAQ prediction of a commercial building
This repository aims to construct a model based on building automation system data for occupancy pattern estimation.

The estimated occupancy pattern will validate with the data from the entrance gate.

The results of this repository imply that CO2 sensors are good occupancy detectors rather than only tools for monitoring IAQ.

Moreover, this model can advance the predictive IAQ control in buildings with such IoT networks in building automation system.

# Occupancy history

The hourly occupancy schedule is the vital variable to conduct the predictive IAQ control in buildings.

However, in this case, we have no head counting hardware in the field.

The only support from local staff is providing the daily records of entrance and security gate.

So, we tried to utilize the BA data with [Carbon Dioxide Predictor-Corrector](https://bigladdersoftware.com/epx/docs/9-5/engineering-reference/carbon-dioxide-predictor-corrector.html#carbon-dioxide-predictor-corrector) originated from EnergyPlus simulator to reproduce the occupancy trend in the studying building.

## Carbon Dioxide Predictor-Corrector (Ref: EnergyPlus)
The air mass balance equation for the change in zone air CO<sub>2</sub> concentration may be expressed as follows:
![air mass balance equation](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/air_mass_balance_eq.PNG)


## Input data

![AHU_data](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/AHU_data.PNG)

![CO2_data](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/CO2_data.PNG)

## 
