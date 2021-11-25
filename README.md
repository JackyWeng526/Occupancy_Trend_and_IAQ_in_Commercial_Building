# Occupancy and IAQ prediction of a commercial building
This repository aims to construct a model based on building automation system data for occupancy pattern estimation.

The estimated occupancy pattern will validate with the data from the entrance gate.

The results of this repository imply that CO2 sensors are good occupancy detectors rather than only tools for monitoring IAQ.

Moreover, this model can advance the predictive IAQ control in buildings with such IoT networks in building automation system.

## Occupancy history
In this case, we have no head counting hardware in the field.

The only support from local staff is providing the daily records of entrance and security gate.

So, we tried to utilize the BA data with [Carbon Dioxide Predictor-Corrector](https://bigladdersoftware.com/epx/docs/9-5/engineering-reference/carbon-dioxide-predictor-corrector.html#carbon-dioxide-predictor-corrector) originated from EnergyPlus simulator to reproduce the occupancy trend in the building.
