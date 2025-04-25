# ElectionPredictor

## Can we predict the U.S. presidential vote at the county level using only demographic and socioeconomic data?


## Overview

This project explores the intersection of machine learning and political science by analyzing whether demographic and economic factors alone are enough to predict election outcomes in the United States. Specifically, we built and trained four different classification models to predict whether a U.S. county would vote Democratic or Republican during presidential elections from 2008 to 2020.

Our goal wasn’t just to create an accurate predictor, but to possibly find some common patterns in America’s voting behavior, understand model performance across different architectures, and visualize what these models can tell us about the electorate.


## Purpose

In many political forecasting tools, polling and sentiment analysis dominate the landscape. But what if those tools weren’t available? Could we use static features like education, income, and age distribution to predict how a region would vote?

This project is our attempt to answer that question, using machine learning that include these features.


## Models Used

We trained and compared the following four models in our project:

1. **Three-Layer Neural Network**
   - A fully connected multilayer perceptron (MLP) built using PyTorch.
   - Consists of three layers: input to 128 neurons, then to 64 neurons, and finally to a single output neuron.
   - Uses ReLU activations between layers and applies dropout regularization of 30% to help prevent overfitting.
   - Outputs a single probability score after applying a sigmoid activation at the final layer.

2. **Two-Layer Neural Network**
   - A simpler fully connected neural network, also built using PyTorch.
   - Consists of two layers: input to 64 neurons and then directly to the output neuron.
   - Includes a ReLU activation and dropout of 30% after the first layer before producing a final sigmoid output.
   - Provides a lightweight alternative to the 3-layer network for faster training and fewer parameters.

3. **Logistic Regression (PyTorch Implementation)**
   - A basic logistic regression model implemented using a single fully connected layer followed by a sigmoid activation.
   - Serves as a fundamental linear classifier for binary classification tasks.
   - Offers interpretable weights but is limited to modeling linear decision boundaries.

4. **Linear Regression Model (PyTorch Implementation)**
   - A simple linear model that maps the input features directly to a single output without a final sigmoid activation initially.
   - Trained using binary cross-entropy loss, treating the output as probabilities.

**Note:**  
- All models were trained using a common PyTorch NeuralNetworkTrainer class that included early stopping, batch processing, and validation monitoring.  
- Training histories (loss curves) and confusion matrices were plotted for all models for side-by-side comparison.

Each of these models followed a train, validation, and test set. To ensure balanced training and reduce partisan bias, we chose to train our models using data from the 2008 and 2016 presidential elections, years in which each major political party won once. We beleived this allowed the model to learn from a more diverse set of electoral outcomes and avoid overfitting to a single party's victory pattern.

Originally, the training set included 2008 and 2012, both of which were Democratic victories. We recognized that this introduced a potential bias, encouraging the model to favor Democratic outcomes by default. By incorporating 2016, a Republican win, we introduced necessary variation to help the model generalize more effectively to future elections.

We then decided to use the year 2012 as our validation set to evaluate the models performance, as well as any fine-tuning to the model and its hyperparameters. 

This then led us to use the 2020 election year data on our test, which we seem to get very good results.

## Best Performing Model

The Three Layer Neural Network was the best performing model across all evaluation metrics.

Its deeper architecture, with two hidden layers (128 and 64 neurons), allowed it to better capture the complex, nonlinear relationships in the county level election data compared to simpler models like logistic regression or a basic two layer network. The inclusion of dropout regularization helped it generalize well without overfitting.

The 3 Layer MLP consistently achieved:
- Validation accuracies exceeding 80%.
- Balanced F1-scores for both Democratic and Republican classes.
- Strong predictive performance even for closely contested swing counties.

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
