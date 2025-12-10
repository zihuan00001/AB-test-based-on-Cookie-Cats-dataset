# Cookie Cats Mobile Game: A/B Testing Analysis  
## Project Background
Cookie Cats is a classic "Match-3" mobile puzzle game. As players progress through the levels, they encounter "Gates" that force them to wait a certain period or make an in-app purchase to continue playing. This mechanism serves not only to drive monetization but also to provide players with a forced break, helping to prevent gameplay burnout (boredom).  
The Core Question of this A/B Test: How does moving the first "Gate" from Level 30 to Level 40 impact player engagement (game time) and retention rates?
This project analyzes the A/B test data using statistical methods to evaluate whether this alteration resulted in a significant improvement in key business metrics
## Experimental Design & Preparation
### 1. Metric Definition
To quantitatively evaluate the business impact of "moving the gate from Gate 30 to Gate 40," we defined the following metric framework prior to launching the experiment:
Overall Evaluation Criteria (OEC):  
* 1-Day Retention (Retention_1)  
* 7-Day Retention (Retention_7)  
* Total Game Rounds (Sum_GameRounds)


### 2. Sample Size Estimation (Power Analysis)
Goal: To prevent the inability to detect real differences due to insufficient sample size (Type II errors).  
* Basic Logic: We back-calculated $N$ based on hypothesis testing parameters:  
  - Significance Level ($\alpha$): 0.05 (Controls the False Positive Rate).
  - Statistical Power ($1-\beta$): 0.80 (Ensures an 80% probability of detecting a difference if one exists).  
  - Minimum Detectable Effect (MDE): Set at a relative lift of 2%~5% (Based on the business ROI threshold)
* Calculation: Using statistical formulas, the required sample size per group was calculated to be approximately 16,000 users.
* Data Status: The actual dataset contains 90,189 users (approx. 45,000 per group), far exceeding the theoretical minimum. This ensures the experiment possesses extremely high statistical power.

### 3.Traffic Splitting & Randomization
Assumption: The data was collected based on the following splitting mechanism:
* Unit of Diversion: User_ID
  - Principle: Ensures the same user sees the same gate version throughout the entire experiment lifecycle (avoiding a fragmented experience where a user sees Gate 30 one day and Gate 40 the next).
* Splitting Algorithm: Hash(User_ID + Salt) % 100
  - Principle: Compared to a simple Random(), hashing provides Determinism and Orthogonality. It effectively distributes user characteristics (e.g., device type, region, registration time) to eliminate Selection Bias.
 
### 4.Experiment Duration
* Principle: The experiment must cover a full Weekly Cycle.
* Reasoning: Casual mobile game users exhibit a distinct "Weekend Effect" (activity is significantly higher on weekends compared to weekdays). To smooth out temporal volatility, data collection must persist for at least 7 days (or multiples thereof, like 14 days).
* Assumption: We assume this dataset covers integer week windows, effectively avoiding time-based bias.

## Dataset

      Columns           |                                              Description
      userid            |                                 The unique identifier of the player
      version           |             Experimental grouping: gate_30 (Control group) or gate_40 (experimental group)
      sum_gamerounds    |      The total number of game rounds played by the player within the first 14 days after installation
      retention_1       |     Next-day retention: Whether the player logs in again on the first day after installation (True/False)
      retention_7       |     7-day retention: Whether the player logs in again on the 7th day after installation (True/False)

## Methodology  
The analysis utilizes Python for comprehensive data cleaning and statistical inference. The key steps are outlined below:  
### 1. Data Preprocessing  
* Integrity Check: Verified that there were no missing values or duplicate User IDs in the dataset.  
* Outlier Handling: Identified and removed a single extreme outlier with a sum_gamerounds count of 49,854. This was done to prevent this specific data point from skewing the mean calculations.
### # Cookie Cats Mobile Game: A/B Testing Analysis  
## Project Background
Cookie Cats is a classic "Match-3" mobile puzzle game. As players progress through the levels, they encounter "Gates" that force them to wait a certain period or make an in-app purchase to continue playing. This mechanism serves not only to drive monetization but also to provide players with a forced break, helping to prevent gameplay burnout (boredom).  
The Core Question of this A/B Test: How does moving the first "Gate" from Level 30 to Level 40 impact player engagement (game time) and retention rates?
This project analyzes the A/B test data using statistical methods to evaluate whether this alteration resulted in a significant improvement in key business metrics
## Experimental Design & Preparation
### 1. Metric Definition
To quantitatively evaluate the business impact of "moving the gate from Gate 30 to Gate 40," we defined the following metric framework prior to launching the experiment:
Overall Evaluation Criteria (OEC):  
* 1-Day Retention (Retention_1)  
* 7-Day Retention (Retention_7)  
* Total Game Rounds (Sum_GameRounds)




### 2. Sample Size Estimation (Power Analysis)
Goal: To prevent the inability to detect real differences due to insufficient sample size (Type II errors).  
* Basic Logic: We back-calculated $N$ based on hypothesis testing parameters:  
  - Significance Level ($\alpha$): 0.05 (Controls the False Positive Rate).
- Statistical Power ($1-\beta$): 0.80 (Ensures an 80% probability of detecting a difference if one exists).  
  - Minimum Detectable Effect (MDE): Set at a relative lift of 2%~5% (Based on the business ROI threshold)
* Calculation: Using statistical formulas, the required sample size per group was calculated to be approximately 16,000 users.
* Data Status: The actual dataset contains 90,189 users (approx. 45,000 per group), far exceeding the theoretical minimum. This ensures the experiment possesses extremely high statistical power.


### 3.Traffic Splitting & Randomization
Assumption: The data was collected based on the following splitting mechanism:
* Unit of Diversion: User_ID
  - Principle: Ensures the same user sees the same gate version throughout the entire experiment lifecycle (avoiding a fragmented experience where a user sees Gate 30 one day and Gate 40 the next).
* Splitting Algorithm: Hash(User_ID + Salt) % 100
  - Principle: Compared to a simple Random(), hashing provides Determinism and Orthogonality. It effectively distributes user characteristics (e.g., device type, region, registration time) to eliminate Selection Bias.

### 4.Experiment Duration
* Principle: The experiment must cover a full Weekly Cycle.
* Reasoning: Casual mobile game users exhibit a distinct "Weekend Effect" (activity is significantly higher on weekends compared to weekdays). To smooth out temporal volatility, data collection must persist for at least 7 days (or multiples thereof, like 14 days).
* Assumption: We assume this dataset covers integer week windows, effectively avoiding time-based bias.


## Dataset


      Columns           |                                              Description
userid            |                                 The unique identifier of the player
      version           |             Experimental grouping: gate_30 (Control group) or gate_40 (experimental group)
      sum_gamerounds    |      The total number of game rounds played by the player within the first 14 days after installation
      retention_1       |     Next-day retention: Whether the player logs in again on the first day after installation (True/False)
retention_7       |     7-day retention: Whether the player logs in again on the 7th day after installation (True/False)


## Methodology  
The analysis utilizes Python for comprehensive data cleaning and statistical inference. The key steps are outlined below:  
### 1. Data Preprocessing
* Integrity Check: Verified that there were no missing values or duplicate User IDs in the dataset.  
* Outlier Handling: Identified and removed a single extreme outlier with a sum_gamerounds count of 49,854. This was done to prevent this specific data point from skewing the mean calculations

### 2. Experimental Design & Sample Size Calculation  
Prior to testing, the theoretical required sample size was calculated based on Statistical Power ($1-\beta = 0.8$) and Significance Level ($\alpha = 0.05$) to ensure the reliability of the results.  
* Mean Metrics: Minimum Detectable Effect (MDE) set at 5 game rounds.  
* Proportion Metrics: MDE set at a relative lift of 2% (for 1-Day Retention) and 5% (for 7-Day Retention).
* Conclusion: The actual sample size (approx. 45,000 users per group) is sufficient to detect these effects.

### 3. Hypothesis Testing
One-tailed tests were conducted for the three core metrics ($H_1$: Treatment Group Metric > Control Group Metric):1)   
* Game Rounds (Mean Metric)  
  - Test Method: Levene's Test (for homogeneity of variance) + T-test / Z-test.  
  - Result: P-value ≈ 1.0. Failed to reject the null hypothesis.  
* 1-Day & 7-Day Retention (Proportion Metric)  
    - Test Method: Proportions Z-test.  
    - Result: Failed to reject the null hypothesis. Furthermore, the retention rates for the treatment group were numerically slightly lower than those of the control group
 
# Cookie Cats Mobile Game: A/B Testing Analysis  
## Project Background
Cookie Cats is a classic "Match-3" mobile puzzle game. As players progress through the levels, they encounter "Gates" that force them to wait a certain period or make an in-app purchase to continue playing. This mechanism serves not only to drive monetization but also to provide players with a forced break, helping to prevent gameplay burnout (boredom).  
The Core Question of this A/B Test: How does moving the first "Gate" from Level 30 to Level 40 impact player engagement (game time) and retention rates?
This project analyzes the A/B test data using statistical methods to evaluate whether this alteration resulted in a significant improvement in key business metrics
## Experimental Design & Preparation
### 1. Metric Definition
To quantitatively evaluate the business impact of "moving the gate from Gate 30 to Gate 40," we defined the following metric framework prior to launching the experiment:
Overall Evaluation Criteria (OEC):  
* 1-Day Retention (Retention_1)  
* 7-Day Retention (Retention_7)  
* Total Game Rounds (Sum_GameRounds)




### 2. Sample Size Estimation (Power Analysis)
Goal: To prevent the inability to detect real differences due to insufficient sample size (Type II errors).  
* Basic Logic: We back-calculated $N$ based on hypothesis testing parameters:  
  - Significance Level ($\alpha$): 0.05 (Controls the False Positive Rate).
- Statistical Power ($1-\beta$): 0.80 (Ensures an 80% probability of detecting a difference if one exists).  
  - Minimum Detectable Effect (MDE): Set at a relative lift of 2%~5% (Based on the business ROI threshold)
* Calculation: Using statistical formulas, the required sample size per group was calculated to be approximately 16,000 users.
* Data Status: The actual dataset contains 90,189 users (approx. 45,000 per group), far exceeding the theoretical minimum. This ensures the experiment possesses extremely high statistical power.


### 3.Traffic Splitting & Randomization
Assumption: The data was collected based on the following splitting mechanism:
* Unit of Diversion: User_ID
  - Principle: Ensures the same user sees the same gate version throughout the entire experiment lifecycle (avoiding a fragmented experience where a user sees Gate 30 one day and Gate 40 the next).
* Splitting Algorithm: Hash(User_ID + Salt) % 100
  - Principle: Compared to a simple Random(), hashing provides Determinism and Orthogonality. It effectively distributes user characteristics (e.g., device type, region, registration time) to eliminate Selection Bias.

### 4.Experiment Duration
* Principle: The experiment must cover a full Weekly Cycle.
* Reasoning: Casual mobile game users exhibit a distinct "Weekend Effect" (activity is significantly higher on weekends compared to weekdays). To smooth out temporal volatility, data collection must persist for at least 7 days (or multiples thereof, like 14 days).
* Assumption: We assume this dataset covers integer week windows, effectively avoiding time-based bias.


## Dataset


      Columns           |                                              Description
userid            |                                 The unique identifier of the player
      version           |             Experimental grouping: gate_30 (Control group) or gate_40 (experimental group)
      sum_gamerounds    |      The total number of game rounds played by the player within the first 14 days after installation
      retention_1       |     Next-day retention: Whether the player logs in again on the first day after installation (True/False)
retention_7       |     7-day retention: Whether the player logs in again on the 7th day after installation (True/False)


## Methodology  
The analysis utilizes Python for comprehensive data cleaning and statistical inference. The key steps are outlined below:  
### 1. Data Preprocessing
* Integrity Check: Verified that there were no missing values or duplicate User IDs in the dataset.  
* Outlier Handling: Identified and removed a single extreme outlier with a sum_gamerounds count of 49,854. This was done to prevent this specific data point from skewing the mean calculations.
### # Cookie Cats Mobile Game: A/B Testing Analysis  
## Project Background
Cookie Cats is a classic "Match-3" mobile puzzle game. As players progress through the levels, they encounter "Gates" that force them to wait a certain period or make an in-app purchase to continue playing. This mechanism serves not only to drive monetization but also to provide players with a forced break, helping to prevent gameplay burnout (boredom).  
The Core Question of this A/B Test: How does moving the first "Gate" from Level 30 to Level 40 impact player engagement (game time) and retention rates?
This project analyzes the A/B test data using statistical methods to evaluate whether this alteration resulted in a significant improvement in key business metrics
## Experimental Design & Preparation
### 1. Metric Definition
To quantitatively evaluate the business impact of "moving the gate from Gate 30 to Gate 40," we defined the following metric framework prior to launching the experiment:
Overall Evaluation Criteria (OEC):  
* 1-Day Retention (Retention_1)
* 7-Day Retention (Retention_7)  
* Total Game Rounds (Sum_GameRounds)








### 2. Sample Size Estimation (Power Analysis)
Goal: To prevent the inability to detect real differences due to insufficient sample size (Type II errors).
* Basic Logic: We back-calculated $N$ based on hypothesis testing parameters:  
  - Significance Level ($\alpha$): 0.05 (Controls the False Positive Rate).
- Statistical Power ($1-\beta$): 0.80 (Ensures an 80% probability of detecting a difference if one exists).  
  - Minimum Detectable Effect (MDE): Set at a relative lift of 2%~5% (Based on the business ROI threshold)
* Calculation: Using statistical formulas, the required sample size per group was calculated to be approximately 16,000 users.
* Data Status: The actual dataset contains 90,189 users (approx. 45,000 per group), far exceeding the theoretical minimum. This ensures the experiment possesses extremely high statistical power.




### 3.Traffic Splitting & Randomization
Assumption: The data was collected based on the following splitting mechanism:
* Unit of Diversion: User_ID
  - Principle: Ensures the same user sees the same gate version throughout the entire experiment lifecycle (avoiding a fragmented experience where a user sees Gate 30 one day and Gate 40 the next).
* Splitting Algorithm: Hash(User_ID + Salt) % 100
  - Principle: Compared to a simple Random(), hashing provides Determinism and Orthogonality. It effectively distributes user characteristics (e.g., device type, region, registration time) to eliminate Selection Bias.


### 4.Experiment Duration
* Principle: The experiment must cover a full Weekly Cycle.
* Reasoning: Casual mobile game users exhibit a distinct "Weekend Effect" (activity is significantly higher on weekends compared to weekdays). To smooth out temporal volatility, data collection must persist for at least 7 days (or multiples thereof, like 14 days).
* Assumption: We assume this dataset covers integer week windows, effectively avoiding time-based bias.




## Dataset




      Columns           |                                              Description
userid            |                                 The unique identifier of the player
      version           |             Experimental grouping: gate_30 (Control group) or gate_40 (experimental group)
sum_gamerounds    |      The total number of game rounds played by the player within the first 14 days after installation
      retention_1       |     Next-day retention: Whether the player logs in again on the first day after installation (True/False)
retention_7       |     7-day retention: Whether the player logs in again on the 7th day after installation (True/False)




## Methodology
The analysis utilizes Python for comprehensive data cleaning and statistical inference. The key steps are outlined below:  
### 1. Data Preprocessing
* Integrity Check: Verified that there were no missing values or duplicate User IDs in the dataset.  
* Outlier Handling: Identified and removed a single extreme outlier with a sum_gamerounds count of 49,854. This was done to prevent this specific data point from skewing the mean calculations


### 2. Experimental Design & Sample Size Calculation  
Prior to testing, the theoretical required sample size was calculated based on Statistical Power ($1-\beta = 0.8$) and Significance Level ($\alpha = 0.05$) to ensure the reliability of the results.  
* Mean Metrics: Minimum Detectable Effect (MDE) set at 5 game rounds.  
* Proportion Metrics: MDE set at a relative lift of 2% (for 1-Day Retention) and 5% (for 7-Day Retention).
* Conclusion: The actual sample size (approx. 45,000 users per group) is sufficient to detect these effects.


### 3. Hypothesis Testing
One-tailed tests were conducted for the three core metrics ($H_1$: Treatment Group Metric > Control Group Metric):1)   
* Game Rounds (Mean Metric)
- Test Method: Levene's Test (for homogeneity of variance) + T-test / Z-test.  
  - Result: P-value ≈ 1.0. Failed to reject the null hypothesis.  
* 1-Day & 7-Day Retention (Proportion Metric)  
    - Test Method: Proportions Z-test.
- Result: Failed to reject the null hypothesis. Furthermore, the retention rates for the treatment group were numerically slightly lower than those of the control group# Cookie Cats Mobile Game: A/B Testing Analysis  
## Project Background
Cookie Cats is a classic "Match-3" mobile puzzle game. As players progress through the levels, they encounter "Gates" that force them to wait a certain period or make an in-app purchase to continue playing. This mechanism serves not only to drive monetization but also to provide players with a forced break, helping to prevent gameplay burnout (boredom).  
The Core Question of this A/B Test: How does moving the first "Gate" from Level 30 to Level 40 impact player engagement (game time) and retention rates?
This project analyzes the A/B test data using statistical methods to evaluate whether this alteration resulted in a significant improvement in key business metrics
## Experimental Design & Preparation
### 1. Metric Definition
To quantitatively evaluate the business impact of "moving the gate from Gate 30 to Gate 40," we defined the following metric framework prior to launching the experiment:
Overall Evaluation Criteria (OEC):  
* 1-Day Retention (Retention_1)  
* 7-Day Retention (Retention_7)  
* Total Game Rounds (Sum_GameRounds)




### 2. Sample Size Estimation (Power Analysis)
Goal: To prevent the inability to detect real differences due to insufficient sample size (Type II errors).  
* Basic Logic: We back-calculated $N$ based on hypothesis testing parameters:  
  - Significance Level ($\alpha$): 0.05 (Controls the False Positive Rate).
- Statistical Power ($1-\beta$): 0.80 (Ensures an 80% probability of detecting a difference if one exists).  
  - Minimum Detectable Effect (MDE): Set at a relative lift of 2%~5% (Based on the business ROI threshold)
* Calculation: Using statistical formulas, the required sample size per group was calculated to be approximately 16,000 users.
* Data Status: The actual dataset contains 90,189 users (approx. 45,000 per group), far exceeding the theoretical minimum. This ensures the experiment possesses extremely high statistical power.


### 3.Traffic Splitting & Randomization
Assumption: The data was collected based on the following splitting mechanism:
* Unit of Diversion: User_ID
  - Principle: Ensures the same user sees the same gate version throughout the entire experiment lifecycle (avoiding a fragmented experience where a user sees Gate 30 one day and Gate 40 the next).
* Splitting Algorithm: Hash(User_ID + Salt) % 100
  - Principle: Compared to a simple Random(), hashing provides Determinism and Orthogonality. It effectively distributes user characteristics (e.g., device type, region, registration time) to eliminate Selection Bias.

### 4.Experiment Duration
* Principle: The experiment must cover a full Weekly Cycle.
* Reasoning: Casual mobile game users exhibit a distinct "Weekend Effect" (activity is significantly higher on weekends compared to weekdays). To smooth out temporal volatility, data collection must persist for at least 7 days (or multiples thereof, like 14 days).
* Assumption: We assume this dataset covers integer week windows, effectively avoiding time-based bias.


## Dataset


      Columns           |                                              Description
userid            |                                 The unique identifier of the player
      version           |             Experimental grouping: gate_30 (Control group) or gate_40 (experimental group)
      sum_gamerounds    |      The total number of game rounds played by the player within the first 14 days after installation
      retention_1       |     Next-day retention: Whether the player logs in again on the first day after installation (True/False)
retention_7       |     7-day retention: Whether the player logs in again on the 7th day after installation (True/False)


## Methodology  
The analysis utilizes Python for comprehensive data cleaning and statistical inference. The key steps are outlined below:  
### 1. Data Preprocessing
* Integrity Check: Verified that there were no missing values or duplicate User IDs in the dataset.  
* Outlier Handling: Identified and removed a single extreme outlier with a sum_gamerounds count of 49,854. This was done to prevent this specific data point from skewing the mean calculations.
### # Cookie Cats Mobile Game: A/B Testing Analysis  
## Project Background
Cookie Cats is a classic "Match-3" mobile puzzle game. As players progress through the levels, they encounter "Gates" that force them to wait a certain period or make an in-app purchase to continue playing. This mechanism serves not only to drive monetization but also to provide players with a forced break, helping to prevent gameplay burnout (boredom).  
The Core Question of this A/B Test: How does moving the first "Gate" from Level 30 to Level 40 impact player engagement (game time) and retention rates?
This project analyzes the A/B test data using statistical methods to evaluate whether this alteration resulted in a significant improvement in key business metrics
## Experimental Design & Preparation
### 1. Metric Definition
To quantitatively evaluate the business impact of "moving the gate from Gate 30 to Gate 40," we defined the following metric framework prior to launching the experiment:
Overall Evaluation Criteria (OEC):  
* 1-Day Retention (Retention_1)
* 7-Day Retention (Retention_7)  
* Total Game Rounds (Sum_GameRounds)








### 2. Sample Size Estimation (Power Analysis)
Goal: To prevent the inability to detect real differences due to insufficient sample size (Type II errors).
* Basic Logic: We back-calculated $N$ based on hypothesis testing parameters:  
  - Significance Level ($\alpha$): 0.05 (Controls the False Positive Rate).
- Statistical Power ($1-\beta$): 0.80 (Ensures an 80% probability of detecting a difference if one exists).  
  - Minimum Detectable Effect (MDE): Set at a relative lift of 2%~5% (Based on the business ROI threshold)
* Calculation: Using statistical formulas, the required sample size per group was calculated to be approximately 16,000 users.
* Data Status: The actual dataset contains 90,189 users (approx. 45,000 per group), far exceeding the theoretical minimum. This ensures the experiment possesses extremely high statistical power.




### 3.Traffic Splitting & Randomization
Assumption: The data was collected based on the following splitting mechanism:
* Unit of Diversion: User_ID
  - Principle: Ensures the same user sees the same gate version throughout the entire experiment lifecycle (avoiding a fragmented experience where a user sees Gate 30 one day and Gate 40 the next).
* Splitting Algorithm: Hash(User_ID + Salt) % 100
  - Principle: Compared to a simple Random(), hashing provides Determinism and Orthogonality. It effectively distributes user characteristics (e.g., device type, region, registration time) to eliminate Selection Bias.


### 4.Experiment Duration
* Principle: The experiment must cover a full Weekly Cycle.
* Reasoning: Casual mobile game users exhibit a distinct "Weekend Effect" (activity is significantly higher on weekends compared to weekdays). To smooth out temporal volatility, data collection must persist for at least 7 days (or multiples thereof, like 14 days).
* Assumption: We assume this dataset covers integer week windows, effectively avoiding time-based bias.




## Dataset




      Columns           |                                              Description
userid            |                                 The unique identifier of the player
      version           |             Experimental grouping: gate_30 (Control group) or gate_40 (experimental group)
sum_gamerounds    |      The total number of game rounds played by the player within the first 14 days after installation
      retention_1       |     Next-day retention: Whether the player logs in again on the first day after installation (True/False)
retention_7       |     7-day retention: Whether the player logs in again on the 7th day after installation (True/False)




## Methodology
The analysis utilizes Python for comprehensive data cleaning and statistical inference. The key steps are outlined below:  
### 1. Data Preprocessing
* Integrity Check: Verified that there were no missing values or duplicate User IDs in the dataset.  
* Outlier Handling: Identified and removed a single extreme outlier with a sum_gamerounds count of 49,854. This was done to prevent this specific data point from skewing the mean calculations


### 2. Experimental Design & Sample Size Calculation  
Prior to testing, the theoretical required sample size was calculated based on Statistical Power ($1-\beta = 0.8$) and Significance Level ($\alpha = 0.05$) to ensure the reliability of the results.  
* Mean Metrics: Minimum Detectable Effect (MDE) set at 5 game rounds.  
* Proportion Metrics: MDE set at a relative lift of 2% (for 1-Day Retention) and 5% (for 7-Day Retention).
* Conclusion: The actual sample size (approx. 45,000 users per group) is sufficient to detect these effects.


### 3. Hypothesis Testing
One-tailed tests were conducted for the three core metrics ($H_1$: Treatment Group Metric > Control Group Metric):1)   
* Game Rounds (Mean Metric)
- Test Method: Levene's Test (for homogeneity of variance) + T-test / Z-test.  
  - Result: P-value ≈ 1.0. Failed to reject the null hypothesis.  
* 1-Day & 7-Day Retention (Proportion Metric)  
    - Test Method: Proportions Z-test.
    - Result: Failed to reject the null hypothesis. Furthermore, the retention rates for the treatment group were numerically slightly lower than those of the control group

## Results & Conclusion  
Based on rigorous statistical testing, the following conclusions were drawn:  
* Game Duration: Moving the gate to Level 40 did not significantly increase the average number of game rounds played.  
* Player Retention: Neither 1-Day nor 7-Day retention rates showed any significant improvement in the gate_40 version compared to the gate_30 baseline.  
* Insight: The data suggests that delaying the placement of the gate (allowing users to play longer before encountering a forced break/stoppage) did not enhance player stickiness or engagement.

## Business Recommendations  
Based on the current data, it is not recommended to move the gate from Level 30 to Level 40.  
We suggest maintaining the current configuration (gate_30). Future A/B tests could explore alternative gate placements, such as introducing the gate at an earlier level, to see if that impacts retention positively.

## Tech Stack
* Python
  - Pandas & Numpy: Data Manipulation & Cleaning
  - Statsmodels & Scipy: Power Analysis (Sample Size Calculation), Normal Distribution Simulation, Z-test, T-test, etc.
