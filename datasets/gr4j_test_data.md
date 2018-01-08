## Original GR4J test dataset

This test dataset was extracted from the GR4J_en.xlsx spreadsheet, available from https://webgr.irstea.fr/en/modeles/journalier-gr4j-2/fonctionnement_gr4j/  

The dataset (gr4j_test_data.csv) contains two years of data (1991-01-01 to 1992-12-31) for the _Le Léguer à Belle-Isle-en-Terre_ watershed, with an area of 260 km<sup>2</sup>.

It has 6 columns:
1. Date
2. Precip (mm)
3. ETP (mm)
4. Qobs (m3/s)
5. Qobs (mm/day)
6. Qsim (mm/day)


Observed discharge (Qobs) in mm/day is calculated using the formula:

    Qobs * 86.4 / basin_area

Simulated discharge is calculated using the GR4J model with parameters:

|Parameter | Transf. value | Real value | Trasf function |
|----------|---------------|-----------|---|
| X1: production store max. capacity (mm)             | 5.77  | 320.107| exp()     |
| X2: catchment water exchange coefficient (mm)       | 1.62  | 2.421  | sinh()    |
| X3: one-day max. capacity of routing reservoir (mm) | 4.24  | 69.628 | exp()     |
| X4: HU1 unit hydrograph time base (days)            | -0.12 | 1.389  | exp()+0.5 |

The model readme mentions that the model uses the real values. The transformed values eases the optimization steps. This is something to be evaluated when using the python optimization routines.

Tranf. function is how the transformed value is converted into the real value:  
real = func(trasf)  
Transformed values are rounded to two decimal places. Thou some differences in the results could occur.

Model parameters were adjusted for the first year of data and compared to the seccond year. Adjustment coefficients obtained for the parameters above are:

| Coef.       | value (%) |
| ------------| ----------|
| Nash(Q)     | 91.9      |
| Nash(VQ)    | 86.5      |
| Nash(ln(Q)) | 77.5      |
| Balance     | 100.8     |

VQ is the square root of the discharge.
