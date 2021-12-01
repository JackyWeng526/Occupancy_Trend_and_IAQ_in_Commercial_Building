# Occupancy and IAQ Prediction of a Commercial Building
This study aims to construct a model based on building automation system data for future occupancy pattern estimation.

The estimated hourly occupancy pattern can provide a chance of conducting a predictive control strategy for optimal outdoor air ventilation.

This study demonstrates an effective way of conducting predictive ventilation control by a data-driven occupancy trend model.

The results also imply that CO<sub>2</sub> sensors are good occupancy detectors rather than only tools for monitoring IAQ.

Moreover, the proposed model can advance the predictive IAQ control in buildings with such IoT networks in building automation system (BAS).


# Methodology

The hourly occupancy schedule is the vital variable to conduct the predictive IAQ control in buildings.

However, in this case, we have no head counting hardware in the field.

The only support from local staff is providing BAS data and the daily records of building operations.

So, we try to utilize the BA data with [Carbon Dioxide Predictor-Corrector](https://bigladdersoftware.com/epx/docs/9-5/engineering-reference/carbon-dioxide-predictor-corrector.html#carbon-dioxide-predictor-corrector) originated from EnergyPlus simulator to reproduce the occupancy trend in the studying building.

## Simplfied Occupancy Corrector for Occupancy History (Ref: [EnergyPlus](https://bigladdersoftware.com/epx/docs/9-5/engineering-reference/index.html))
The air mass balance equation for the change in zone air CO<sub>2</sub> concentration can be expressed as follows:
![air mass balance equation](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/air_mass_balance_eq.PNG)

We ignore some terms and import some default values to simplify the equation because of the following reasons:
1. There is only two ventilation devices (AHU) handling IAQ of northen and sourthern zones in each office floor, thus we assume there is no zone exchange effect and ignore the second term in the right-hand side.
2. The variables of CO<sub>2</sub> concentration are collected by BAS for differences calculation.
3. The default coefficients is provided by EnergyPlus and ASHRAE 62.1. They will then be optimized by data-driven analysis and linear regression.

Therefore, the equation of the Simplfied Occupancy Corrector is demonstrated below:
![occ balance equation](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/Occ_balance_eq.PNG)

With this equation and the following input data, we are able to reproduce the detailed occupancy history in the building.

## Input Data
The revelant dataset is originated from the existing BAS.

We collect the data of AHUs and CO<sub>2</sub> sensors shown below.

![AHU_data](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/AHU_data.PNG)

![CO2_data](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/CO2_data.PNG)

Also, we are fortunate to have the daily records of entrance gate released by local staff for data validation.
![Gate Records](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/Gate_Record.PNG)

## Validation of Occupancy History Reproduction
Through the Simplfied Occupancy Corrector (SOC), the hourly occupancy history of each floor in the building can be calculated.

The integrated daily occupancy of the whole building is validated by the entrance gate records to optimize the SOC coefficients.

The preliminary outcome, with r<sup>2</sup> = 0.94 and MAE = 35.1 people, are plotted below.

![PP_estimation](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/Population_estimate_1.PNG)

Where the details of each floor can also be revealed from the reliable occupancy history data.

![PP_distribution](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/Population_distribution.PNG)


# Predictve Model for Hourly Occupancy Trend
Once we have the occupancy history with operation data of a building, we obtain the vital variables for the IAQ prediction and outdoor air optimization (OAO) strategy.

We try both ANN method (by tensorflow) and GBDT method (by lightgbm) for predicting the future occupancy trend.

![Occ_pred_model](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/Occ_pred_model.PNG)

The algorithm, data quantity, variable selection, lag features, and future step of the target in this predictive occupancy model are currently optimized.

The optimal model proposed here can predict the hourly occupancy data for the next day based on the last 24-hour historical data. (As shown in the right part of the above figure.)


# IAQ Prediction and Predictive Control Strategy Application
By means of occupancy trend predictions, we can estimate how much outdoor air volume should be supplied to the office floor referring to ASHRAE 62.1. 

Based on the OA estimation, we are able to produce a predictive control strategy of AHU frequency converter derived from occupancy trend predictions.

Correspondingly, the predicted indoor CO<sub>2</sub> can also be calculated by the equations above. 

(NO NEED to build another complicated model for CO<sub>2</sub> predictions!)

The results are all demonstrated in the figure.

![Predictive_Control_Analysis](https://github.com/JackyWeng526/Occupancy_Trend_and_IAQ_in_Commercial_Building/blob/main/docs/Predictive_Control_Analysis.PNG)

As we can see, if we implement the dynamic predictive control strategy which lowers the AHU frequency, we can have energy-saving potentials of AHU operations without compromising  IAQ and occupants' health and productivity. (Thanks to instructions in ASHRAE 62.1.)

Moreover, we regard that this study is innovative and extensible. 

There are still many subjects in this study that can be investigated, discussed, and in-field validated in future work.


# Authors
- [@Jacky Weng](https://github.com/JackyWeng526)


# Acknowledgement
The module and the application here are just one of the sample works, not the real one in the field.
