# Digital Twin for Water Treatment Plant
Data analysis scenario based on a real water treatment plant. The main goal was to estimate the output values of three key sensors (`DBO-S`, `SS-S`, `DQO-S`) during the period in which the electrical panel powering them is scheduled for replacement.

## The problem
A city water treatment plant reached out because three output sensors —`DBO-S`, `SS-S` and `DQO-S`— share an electrical panel that needs to be renewed. Since the plant cannot stop operations during that time, they needed a reliable method to estimate those values from the remaining operational sensors. They provided one year of daily measurements to train and validate the models.

## What the notebook does
The analysis follows a fairly linear logic:

1. Data is loaded and column headers are added according to the dataset documentation
2. Null values (represented as `?`) are cleaned using forward fill and backward fill
3. Individual outliers are detected with the IQR method and global anomalies with Isolation Forest
4. Variable correlation is analysed with Pearson and a one-day time lag hypothesis on water processing is tested
5. A Linear Regression is trained first as a baseline, followed by a Random Forest to estimate the three target sensors
6. Models are evaluated with R², MAE and a precision metric based on relative error (±10%)
7. The final output is a clear recommendation on which model to use for each sensor and which sensors are not reliable enough to predict in production

## Data
The data is publicly available in the UCI repository:  
[Water Treatment Plant Dataset](https://archive.ics.uci.edu/dataset/116/water+treatment+plant)

## Requirements
pandas
numpy
seaborn
matplotlib
scikit-learn

## Results
The analysis found that the `DQO-S` sensor can be reliably estimated using Random Forest, with **76% of predictions falling within a ±10% error margin**. Linear Regression is a viable and lighter alternative (73% within the same margin). The `SS-S` and `DBO-S` sensors showed insufficient predictive performance across both models and are not recommended for production use.

## Project structure
├── README.md
├── ejercicio2.ipynb
└── Datasets/
└── datos/
└── water+treatment+plant/
└── water-treatment.csv
