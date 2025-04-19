# Predicting Democratic or Republican Votes Given a Various Demographic of People 
A project that predicts whether a county is likely to vote Democratic or Republican using real voting data across four presidential electiomn years from a variety of factors using a dataset provided from our Professor.

## Stakeholders
**Campaign Strategies**: Detecting counties that would be more likely to lean Democratic based on the demographic factors.
**Political Analyst**: Identifying demographic traits that could link to voting patterns

## Key Performance Indicators (KPI)
**Accuracy** of classification if Democratic win vs not
**Confusion Matrix**
**Model generalizability** across each election year
**Interpretability** of model features and their influence on prediction

## The Dataset
This data is across 4 U.S presidential election dates; the year 2008, 2012, 2016, and finally 2020.
The specific type of dataset we are using to predict Democratic or Republican votes consist of over 100 features expressed as conditional probabilities, meaning each feature is in the form of `P(attribute|C)`:
- **Age and Education**: `P(male_25_34_bachelors|C)` — probability that someone in the county is a 25–34-year-old male with a bachelor's degree
- **Gender breakdown**: `P(persons_male|C)`, `P(persons_female|C)`
- **Marital status**: `P(female_divorced|C)`, `P(male_never_married|C)`
- **Race and ethnicity**: `P(persons_white|C)`, `P(persons_black|C)`, `P(persons_hispanic|C)`
- **Income distribution**: `P(households_income_25k_50k|C)`, `P(households_income_under_10k|C)`
- **Poverty and employment**: `P(persons_below_poverty|C)`, `P(labor_force_employed|C)`
- **Veteran and immigration status**: `P(civilians_veteran|C)`, `P(persons_foreign_born|C)`
And many more conditional demographic features.
In addition, the dataset includes **vote share probabilities** for the three major voting categories:

- `P(democrat|C)` – probability that a county voted Democrat
- `P(republican|C)` – probability that a county voted Republican
- `P(other|C)` – probability that a county voted for other parties

These probabilities are not used as features for model training. Instead, they are used to compute the target variable:

 `target_democrat_win` = 1 if `P(democrat|C)` is the highest among the three parties, else 0

This binary target is what the model is trained to predict using the **demographic features** only.


## Modeling Approach
For our model, we used a Neural Network (NN), which is a popular model that is used for handling datasets with many features like ours.
Here is the breakdown of our Approach to model the data:
### Data Feature Selection

To begin, we needed to prepare the dataset:

- **Removed non-numeric columns** which include identifiers like `county` or `state`, and vote outcome columns like `democrat`, `republican`, and `other`.
- **Removed redundant columns**: We also removed the derived target columns and election `year` to help avoid leaking information which can effect our final results.
- Final dataset included over 100 numeric features.

### Define the Target Variable

- As mentioned earlier, we created `target_democrat_win`, a binary column:
  - 1 for a Democratic win
  - 0 for anything else

### Train-Test Split

To evaluate the model fairly, we split the data as so:

- **Training set (50%)**: Used to train the model. Years 2008, 2012
- **Validation Set (25%)**: Used to help fine tune the model for better testing results. Year 2016.
- **Test set (25%)**: Used to evaluate how well the model performs on new data. Year 2020.

### Feature Scaling

Neural networks work best when all input features are on a similar scale. We used a technique called **standardization**, which rescales all numeric columns to have:

- Mean of 0
- Standard deviation of 1

This is done using `StandardScaler()` from the `sklearn` library.

### Building the Neural Network Model

We used the **PyTorch** library in order to help model:

- **Input Layer**: One neuron for each feature (around 100)
- **Hidden Layers**:
  - Dense layer with 64 units and ReLU activation
  - Dropout layer (to prevent overfitting)
  - Dense layer with 32 units and ReLU
- **Output Layer**:
  - Single neuron with to predict probability of Democrat win (1) or not (0)

### Compile and Train the Model

- **Loss function**: Binary Crossentropy Loss (for binary classification)
- **Optimizer**
- **Epochs**: Multiple passes over the data

We trained the model over multiple **epochs** to validated it against the test set.

### Evaluate the Model

- **Accuracy**
- **Classification report** (precision)
- **Confusion matrix**: Visual insight into what the model got right vs wrong


## Results
The model achieved strong overall accuracy in predicting county level outcomes.
- **High precision** for solid-blue counties
The model also identified important demographic correlations including:
  - Higher education levels == Democratic lean
  - Rural or lower income == Republican lean

## Concluding Analysis
This project shows how demographic probabilities can offer meaningful insight into electoral behavior. While not perfect, the model demonstrates that machine learning can discover political trends rooted in census-like data