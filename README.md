# Data and ML models for predicting the thermal conductivity of nanofluids with spherical particles
## Files included:           
### Experimental data
experimental_data_list.xlsx - list of experimental papers from which data was collected.\
experimental_data.xlsx - data in excel form with name of papers next to it.\
exp_data_csv.csv - data in csv form for use in ML models

### Correlation data
HC_model_data.csv - Hamilton-Crosser model data.\
KK_model_data_new.csv - Koo and Kleinstreuer model data.\
JC_model_data_new.csv - Jang and Choi model data.\
Xie_model_data.csv - Xie et al model data.

### Baseline ML models
BM1.h5, BM2.h5, BM3.h5, BM4.h5, BM5.h5 - Models in the order listd in table 3 in the paper.

### Transfer learning based ML models
TLM1.h5, TLM2.h5, TLM3.h5, TLM4.h5 TLM5.h5 - Models in the order listd in table 4 in the paper.

## Intructions for using the ML models
The following one-hot vector encoding has been used to encode the particle material and fluids:

### Particle Materials:
Al2O3 - 10000000\
CuO - 01000000\
Fe - 00100000\
MgO - 00010000\
SiC - 00001000\
SiO2 - 00000100\
TiO2 - 00000010\
ZnO - 00000001

### Fluids
40:60 EG/W - 1000\
60:40 EG/W - 0100\
EG - 0010\
W - 0001

The volume concentration of particles (phi) is expressed as a fraction (e.g. 5% concentration corresponds to phi = 0.05). The phi value in the training data varies from 0.005-0.06. The the following formula is used to normalize phi before using in the ML model.\
phi' = (phi - 0.005)/(0.06 - 0.005)

The temperature is expressed in deg Celcius, and then normalized using the following formula (range is 20-60):\
T' = (T - 20)/(60 - 20)\
The data in the experimental list does have a few datapoints that lie a bit beyond this range, but the values remain in the same order of magnitude, so I dont hink it should cause any problems.

Particle diameter is expressed in meters, and normalized using the following formula (range 10nm - 150nm):\
s' = (s - 1e-8)/(1.5e-7 - 1e-8)

Therefore, the input to the ML models is finally a 15 dimensional vector composed of:\
input = '8 dimensional vector for material','4 dimensional vector for fluid', phi', T', s';

The output value is half the thermal conductivity enhancement (due to the way the data was normalized to get the thermal conductivity enhancement values were normalized). Thus, the actual thermal conductivity enhancement (keff/kf) = (ML Model output) x 2


