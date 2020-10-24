## Prediction of illness for hospitalized people (Final grade: 6/6)

In this task, relevant quantities (represented by both real numbers and booleans) such as: body temperature(real), insuline levels(real), has had a sepsis(boolean) etc. are given for a wide set of patients (17000). This values are recorded for 12h + 12h (one day in total). We trained ElasticNet and MLPRegressor to forcast the vital parameters of people in the second 12h given the values of the same vital parameters in the first 12h. 
