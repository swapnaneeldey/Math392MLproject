# Predicting U.S. Presidential Elections Using Neural Networks

In this project, we set out to explore a question that blends political science and machine learning: Can we predict the outcome of the U.S. 
presidential elections using only demographic and socioeconomic data? More than just testing model accuracy, we wanted to understand why certain predictions were made and what that tells us about the electorate.

For this project, we worked with data provided by our professor, covering four election years: 2008, 2012, 2016, and 2020. The dataset included probability distributions of party outcomes for each county, alongside an extensive range of features including education levels, age distributions, household income brackets, racial demographics, and more. These inputs gave us a robust portrait of each county, and our goal was to use this data to classify which party, either Democratic or Republican, was most likely to win in a given region. But we were just as interested in why a model would reach a particular conclusion.

We decided to split the data chronologically, we trained the model on data from 2008, when the Democratic party won, and 2016, when the Republican party won, to ensure the model was exposed to instances of both major parties securing victory. This approach aimed to reduce potential bias and help the model generalize better across different political outcomes. We validated it on 2012, and using 2020 as our final test. We beleived this split would better replicate how machine learning is actually deployed: using the past to anticipate the future.

The model was implemented in PyTorch, where we focused on proper scaling and class balancing to prevent the network from simply memorizing dominant voting patterns. During training and evaluation, we used confusion matrices to visualize prediction performance and generated detailed classification reports to assess precision and recall across each class.

One of our key visual outputs was the confusion matrix from the 2020 test results. It made the strengths and weaknesses of the model immediately clear: Democratic strongholds, especially dense urban counties, were correctly classified with high confidence. Similarly, many rural counties with older populations and lower education levels, which historically lean Republican, were predicted accurately.

The most revealing plots were the ones that highlighted the gray areas, or the misclassifications. Suburban counties, places in demographic flux, and historically unpredictable regions were far more difficult for the model to handle. It was in these mistakes that we found some truths where politics isn’t static, and voters don’t always behave in ways that are easily captured by a formula.

What we learned through this process is that neural networks are powerful tools for pattern recognition, but their predictions are bound to the data we feed them. They can mirror past trends but are not built to anticipate social change or political upsets unless we account for those possibilities in the model structure or features.

This project reinforced how essential preprocessing and validation designs are to become meaningful outcomes. But more than that, it reminded us that data science isn’t just about predictions but it’s about questions and what we ask. Even with the mistakes our models can make, they become opportunities to better understand what we might want to know.
