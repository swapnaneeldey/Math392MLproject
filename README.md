# ElectionPredictor

## Can we predict the U.S. presidential vote at the county level using only demographic and socioeconomic data?


## Overview

This project explores the intersection of machine learning and political science by analyzing whether demographic and economic factors alone are enough to predict election outcomes in the United States. Specifically, we built and trained four different classification models to predict whether a U.S. county would vote Democratic or Republican during presidential elections from 2008 to 2020.

Our goal wasn’t just to create an accurate predictor, but to possibly find some common patterns in America’s voting behavior, understand model performance across different architectures, and visualize what these models can tell us about the electorate.


## Purpose

In many political forecasting tools, polling and sentiment analysis dominate the landscape. But what if those tools weren’t available? Could we use static features like education, income, and age distribution to predict how a region would vote?

This project is our attempt to answer that question, using machine learning that include these features.


## Models Trained

We trained and compared the following four models:

1. **Logistic Regression**
   - A straightforward baseline model used for binary classification.
   - Provided interpretable coefficients but limited in handling complex, nonlinear patterns.

2. **Multilayer Perceptron (MLP)**
   - A classic fully connected neural network built using PyTorch.
   - Included multiple hidden layers with ReLU activation and dropout regularization.

3. **PyTorch Neural Network (Custom MLP)**
   - Custom designed with flexibility in architecture and training control.
   - Enabled precise tuning and checkpoint saving for best model performance.

4. **TensorFlow Dense Neural Network**
   - Implemented with Keras for accessibility and comparison.
   - Similar architecture to the PyTorch model, used to validate consistency across frameworks.

Each of these models followed a train, validation, and test set. To ensure balanced training and reduce partisan bias, we chose to train our models using data from the 2008 and 2016 presidential elections, years in which each major political party won once. We beleived this allowed the model to learn from a more diverse set of electoral outcomes and avoid overfitting to a single party's victory pattern.

Originally, the training set included 2008 and 2012, both of which were Democratic victories. We recognized that this introduced a potential bias, encouraging the model to favor Democratic outcomes by default. By incorporating 2016, a Republican win, we introduced necessary variation to help the model generalize more effectively to future elections.

We then decided to use the year 2012 as our validation set to evaluate the models performance, as well as any fine-tuning to the model and its hyperparameters. 

This then led us to use the 2020 election year data on our test, which we seem to get very good results.

## Best Performing Model

The PyTorch MLP model emerged as the most effective, demonstrating the best generalization performance. Its architecture allowed it to model non linear relationships in the data more effectively than logistic regression, and it offered more control and flexibility than the TensorFlow implementation.

It consistently achieved:
- Over 80% accuracy
- Balanced precision and recall across both classes (Democratic and Republican)
- Strong performance even in closely contested counties


## Visualizations and Interpretation

Several plots were generated during training and evaluation like the ones listed below:

- **Confusion Matrix**: Illustrated how well each model performed across true/false positives and negatives. The PyTorch model had the most balanced performance.
- **Training & Validation Curves**: Showed stable learning without signs of overfitting, validating our use of dropout layers and batch normalization.
- **Feature Influence**: This is something that is not explicitly visualized but could see strong correlations between some features:
  - Higher education & urbanization == Democrat
  - Older, rural, less-educated populations == Republican


## Dataset

We worked with a dataset containing conditional probabilities (`P(democrat|C)`, `P(republican|C)`, `P(other|C)`) for each U.S. county, alongside over 100 features including:
- Age and Gender Distribution
- Racial Demographics
- Income Brackets
- Educational Attainment
- Urban vs. Rural Classifications

Each entry corresponded to one county in one of the election years: 2008, 2012, 2016, or 2020.


## How to Run

1. Open the notebook:

```bash
cd Notebooks
jupyter notebook Election_script.ipynb
```

2. Ensure the required data files are available:

- `dataset.csv` and `probabilities.csv` should be located in the `data/` directory.

3. The notebook will walk you through:

- Data preprocessing  
- Training and evaluating four different models  
- Generating performance visualizations  
- Drawing final conclusions based on model results

All code resides in the `Notebooks/` folder, and data inputs are organized in the `data/` directory.

## Conclusion

This project confirmed that a county's demographics tell a surprisingly accurate story about its voting behavior. We found that machine learning, without polling or public opinion, can identify repeatable patterns that reflect real political divides.

The neural network's performance proves that when trained well, static features can yield powerful insights into societal behavior.
