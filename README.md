# Data-Driven Traffic Safety Risk Analysis

## Factors Associated with Crash Injury Severity

This project examines roadway, environmental, temporal, vehicle, and collision-related factors associated with injury severity among motor-vehicle occupants involved in fatal crashes.

The analysis uses the 2023 Fatality Analysis Reporting System (FARS) data from the National Highway Traffic Safety Administration (NHTSA) and applies exploratory data analysis and binary logistic regression to identify factors associated with higher or lower odds of severe injury.

### Research Question

**Which roadway, environmental, temporal, speed, and collision-related factors are associated with higher crash injury severity?**

## Data Source

The analysis uses the 2023 Fatality Analysis Reporting System (FARS) National data provided by the National Highway Traffic Safety Administration (NHTSA).

The main data files used in this project are:

- `PERSON.csv` — person-level information, including injury severity
- `ACCIDENT.csv` — crash-level roadway, environmental, lighting, time, and location characteristics
- `VEHICLE.csv` — vehicle-level speed, trafficway, and collision information

## Study Population

The analysis focuses on motor-vehicle occupants involved in fatal crashes.

From the 2023 FARS PERSON data:

- 92,768 person records were available.
- 82,893 motor-vehicle occupants were identified using `PER_TYP`.
- 81,269 occupants had valid injury-severity information and were included in the primary analysis.

### Injury Severity Outcome

Injury severity was converted into a binary outcome:

- **Severe injury:** Suspected Serious Injury or Fatal Injury (`INJ_SEV` = 3 or 4)
- **Non-severe injury:** No Apparent Injury, Possible Injury, or Suspected Minor Injury (`INJ_SEV` = 0, 1, or 2)

Among the 81,269 valid observations:

- Severe injury: **41,361 (50.9%)**
- Non-severe injury: **39,908 (49.1%)**

## Variables Included

The analysis considers variables representing several dimensions of crash and roadway conditions:

### Roadway Characteristics

- Urban/rural setting
- Road functional class
- Intersection involvement
- Trafficway type

### Environmental and Temporal Factors

- Lighting condition
- Weather condition
- Time of day

### Vehicle and Collision Factors

- Speed-related crash involvement
- Travel speed
- Manner of collision

## Methodology

The project follows a data-driven analytical workflow:

1. Data collection from the 2023 NHTSA FARS National dataset
2. Data understanding and variable selection
3. Data cleaning and preprocessing
4. Exploratory data analysis
5. Binary logistic regression
6. Estimation of odds ratios with 95% confidence intervals
7. Interpretation of statistically significant associations
8. Visualization and documentation for reproducibility

Clustered standard errors at the crash (`ST_CASE`) level are used to account for multiple occupants belonging to the same crash.

## Exploratory Findings

Exploratory analysis was conducted to examine how severe injury varied across roadway, environmental, temporal, speed-related, and collision characteristics.

Among the 81,269 occupants included in the primary analysis:

- **50.9%** experienced severe injury.
- **49.1%** experienced non-severe injury.

### Urban and Rural Setting

Among occupants involved in fatal crashes, severe injury was more common in rural than urban settings.

- Rural: **60.0%** severe injury
- Urban: **44.0%** severe injury

### Lighting Condition

The proportion of severe injury was:

- Daylight: **52.79%**
- Dark conditions: **48.79%**

The difference was relatively small at the descriptive level.

### Weather Condition

The proportion of severe injury was:

- Clear weather: **50.23%**
- Adverse or other reported weather: **51.38%**

The descriptive difference was small.

### Intersection Involvement

Severe injury was more common among occupants involved in non-intersection crashes than intersection crashes:

- Non-intersection: **54.07%**
- Intersection: **43.58%**

### Road Functional Class

The proportion of severe injury varied across roadway functional classes:

- Interstate: **47.14%**
- Other Freeways/Expressways: **48.46%**
- Other Principal Arterial: **46.39%**
- Minor Arterial: **49.37%**
- Major Collector: **59.56%**
- Minor Collector: **64.86%**
- Local: **60.07%**

### Time of Day

The proportion of severe injury varied across time periods:

- Night: **56.07%**
- Morning: **52.10%**
- Afternoon: **51.94%**
- Evening: **46.03%**

### Speed-Related Crash Involvement

Speed-related crashes showed the strongest descriptive difference among the main binary variables examined.

- Not speed-related: **44.15%** severe injury
- Speed-related: **73.92%** severe injury

Thus, severe injury was substantially more common among occupants involved in crashes classified as speed-related.

### Travel Speed

Travel-speed information was available for **31,974** observations and missing for **49,295 observations (60.66%)**.

Among observations with available travel-speed information, the proportion of severe injury generally increased across higher speed categories.

This pattern was examined further using a separate logistic regression model with categorized travel speed.

## Regression Results

Two binary logistic regression models were developed to examine factors associated with severe injury among motor-vehicle occupants involved in fatal crashes.

### Model 1: Speed-Related Crash Involvement

Model 1 included speed-related crash involvement as a binary predictor along with roadway, environmental, temporal, trafficway, and collision-related variables.

- Observations: **70,705**
- Pseudo R²: **0.0825**
- Speed-related crash involvement: **OR = 3.737**
- 95% CI: **3.527–3.960**
- p-value: **< 0.001**

Among occupants involved in fatal crashes, those in speed-related crashes had approximately **3.74 times the odds of severe injury** compared with those in crashes not classified as speed-related, after adjustment for the other variables included in the model.

### Model 2: Travel Speed

Model 2 replaced the binary speed-related variable with categorized travel speed to examine whether the association with severe injury varied across different speed ranges.

- Observations: **28,437**
- Pseudo R²: **0.0914**
- Reference category: **0–30 mph**

Adjusted odds ratios for travel speed were:

- **31–45 mph:** OR = **1.171**
- **46–60 mph:** OR = **1.851**
- **61–75 mph:** OR = **2.745**
- **76–90 mph:** OR = **7.496**
- **90+ mph:** OR = **8.485**

The results show a clear increase in the adjusted odds of severe injury across higher travel-speed categories.

The Model 2 sample is substantially smaller because travel-speed information was missing for **49,295 of the 81,269** valid injury-severity observations (**60.66%**).

## Key Findings

Several variables showed meaningful associations with severe injury among occupants involved in fatal crashes.

### Speed

Speed was the strongest predictor examined in the analysis.

- Speed-related crash involvement was associated with approximately **3.74 times higher odds** of severe injury.
- In the travel-speed model, the adjusted odds increased progressively across higher speed categories.
- Occupants in crashes involving **76–90 mph** had approximately **7.50 times the odds** of severe injury compared with the 0–30 mph reference group.
- Occupants in crashes involving **90+ mph** had approximately **8.48 times the odds**.

### Roadway Characteristics

Compared with Interstate roadways in Model 2:

- Other Principal Arterials had OR = **1.239**
- Minor Arterials had OR = **1.350**
- Major Collectors had OR = **1.650**
- Minor Collectors had OR = **1.978**
- Local roads had OR = **1.944**

Entrance/exit ramps also showed elevated odds of severe injury compared with the non-trafficway/driveway reference category (OR = **2.470**).

### Collision Type

Compared with non-motor-vehicle-in-transport collisions:

- Front-to-front collisions had OR = **1.597**
- Angle collisions had OR = **1.355**
- Sideswipe collisions in the same direction had OR = **0.705**
- Sideswipe collisions in the opposite direction had OR = **0.580**

### Urban/Rural Setting

Urban crashes had lower adjusted odds of severe injury than rural crashes in Model 2 (OR = **0.773**).

This corresponds to approximately **1.29 times higher odds in rural settings** relative to urban settings, holding the other variables in the model constant.

### Environmental and Temporal Factors

Dark conditions showed lower adjusted odds than daylight conditions in Model 2 (OR = **0.712**).

Morning, afternoon, and evening periods also showed lower adjusted odds than the night reference period.

Adverse weather was not statistically significant in either model at the 0.05 significance level.

## Limitations

Several limitations should be considered when interpreting the results.

- The analysis uses **fatal-crash data**, so the findings describe associations among occupants involved in fatal crashes rather than risk across all crashes.
- The study is observational; therefore, the estimated associations should **not be interpreted as causal effects**.
- Travel-speed information was missing for **60.66%** of the valid injury-severity observations, resulting in a substantially smaller sample for Model 2.
- The `TRAV_SP` value of `0` represents a stopped motor vehicle in-transport and does not necessarily mean that the vehicle was measured at exactly 0 mph.
- The binary severe-injury outcome combines suspected serious injury and fatal injury, which may represent different injury mechanisms.
- Odds ratios describe associations with the modeled outcome and should not be interpreted as probabilities of injury.
- Pseudo R² values describe model fit and should not be interpreted as prediction accuracy.
- Some variables contain reported unknown or missing values, which were excluded from the complete-case regression models.
- The analysis does not account for every possible factor that may influence injury severity.

## Figures

The project includes visualizations of the main regression findings, including:

- Adjusted odds ratios by travel-speed category
- Adjusted odds ratios by roadway functional class
- Adjusted odds ratios by manner of collision

The regression figures display adjusted odds ratios with **95% confidence intervals** shown where available, and use an odds-ratio reference line at **OR = 1**.

## Reproducibility

The analysis was conducted using Python in Google Colab.

The workflow is designed to be reproducible from the original 2023 NHTSA FARS National dataset. The analysis includes data loading, preprocessing, variable recoding, exploratory analysis, regression modeling, and visualization.

The project files and analysis outputs are organized to allow the workflow to be reviewed and reproduced by other researchers.

## Project Structure

```text
traffic-safety-risk-analysis/
├── data/
├── notebooks/
├── src/
├── outputs/
│   ├── figures/
│   └── tables/
├── README.md
├── requirements.txt
└── LICENSE
```

## Tools and Technologies

- Python
- Google Colab
- Pandas
- NumPy
- Statsmodels
- Matplotlib
- NHTSA FARS 2023 National Dataset
- Binary Logistic Regression
- Exploratory Data Analysis

## Conclusion

This project demonstrates a data-driven approach to examining factors associated with injury severity in fatal crashes.

The analysis identifies **speed-related crash involvement and higher travel-speed categories** as the strongest associations with severe injury in the study population. Roadway functional class, trafficway type, collision manner, urban/rural setting, lighting condition, and time of day also showed meaningful associations in the regression models.

The results provide an analytical framework for understanding patterns in traffic injury severity and demonstrate the use of real-world crash data, statistical modeling, and reproducible data analysis for transportation safety research.





