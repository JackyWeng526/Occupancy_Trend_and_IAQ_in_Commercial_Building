# Occupancy and IAQ prediction of a commercial building
This repository aims to construct a model based on building automation system data for occupancy pattern estimation.

The estimated occupancy pattern will validate with the data from the entrance gate.

The results of this repository imply that CO<sub>2</sub> sensors are good occupancy detectors rather than only tools for monitoring IAQ.

Moreover, this model can advance the predictive IAQ control in buildings with such IoT networks in building automation system (BAS).

# Occupancy history

The hourly occupancy schedule is the vital variable to conduct the predictive IAQ control in buildings.

However, in this case, we have no head counting hardware in the field.

The only support from local staff is providing BAS data and the daily records of building operations.

So, we try to utilize the BA data with [Carbon Dioxide Predictor-Corrector](https://bigladdersoftware.com/epx/docs/9-5/engineering-reference/carbon-dioxide-predictor-corrector.html#carbon-dioxide-predictor-corrector) originated from EnergyPlus simulator to reproduce the occupancy trend in the studying building.

## Simplfied Occupancy Corrector (Ref: [EnergyPlus](https://bigladdersoftware.com/epx/docs/9-5/engineering-reference/index.html))
The air mass balance equation for the change in zone air CO<sub>2</sub> concentration can be expressed as follows:
![air mass balance equation](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/air_mass_balance_eq.PNG)

We ignore some terms and import some default values to simplify the equation because of the following reasons:
1. There is only two ventilation devices (AHU) handling IAQ of northen and sourthern zones in each floor, thus we assume there is no zone exchange effect and ignore the second term in the right-hand side.
2. The variables of CO<sub>2</sub> concentration are collected by BAS for differences calculation.
3. The default coefficients is provided by EnergyPlus and ASHRAE 62.1. They will then be optimized by data-driven analysis and linear regression.

Therefore, the equation of the Simplfied Occupancy Corrector is demonstrated below:
![occ balance equation](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/Occ_balance_eq.PNG)

With this equation and the following input data, we are able to reproduce the detailed occupancy history in the building.

## Input data
The revelant dataset is originated from the existing BAS.

We collect the data of AHUs and CO<sub>2</sub> sensors shown below.

![AHU_data](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/AHU_data.PNG)

![CO2_data](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/CO2_data.PNG)

Also, we are fortunate to have the daily records of entrance gate released by local staff for data validation.
![Gate Records](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/Gate_Record.PNG)

## Results of Occupancy History Reproduction
Through the Simplfied Occupancy Corrector (SOC), the hourly occupancy history of each floor in the building can be calculated.

The integrated daily occupancy of the whole building is validated by the entrance gate records to optimize the SOC coefficients.

The preliminary outcome, with r<sup>2</sup> = 0.92 and MAE = 53.33 people, are plotted below.
![PP_estimation_0]()
