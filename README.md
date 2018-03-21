# Automatically Identifying Prediction Errors of Home Mortgage Loans

## Abstract
When issuing loans, mortgage sellers are interested in protecting themselves against large forecasting errors. Although advances in statistical methods have allowed analysts to achieve relatively low prediction errors, exceptionally large and unlikely errors are still pervasive threats to otherwise sound portfolios. However, given a dataset of loans, it is possible to develop a machine learning model to foresee such exceptionally large errors, termed “hotspots”, in advance. In this paper, I demonstrate an ensemble machine learning model that performs exceptionally well at identifying prediction hotspots for loan defaults, balances, and prepayments. Scores for each class generate precision, recall, and accuracy levels that are nearly prefect. Furthermore, unlike popular methods like deep learning, the model is developed in such a way that intuition is not lost in a black box.


The prediction error can be calculated for each hotspot class by subtracting the predicted amount from the actual amount.
Unless data problem has no noise whatsoever, prediction errors will always exist. However, noise almost always exists in real world data, so prediction errors are inevitable. The error term e is assumed to be independent and normally distributed around a mean of zero. The error distributions seem to illustrate this assumption.

I explore 2 separate routes to developing a classifier. First, I develop a random forest regressor that is trained on each class of hotspot errors—prepayment, default, and balance errors. This model performs exceptionally well when predicting hotspots in the validation set. Next, for the purposes of visual legibility I develop an unsupervised clustering model. Although this model is more visually demonstrable, the model performs poorly at drawing distinct decision boundaries between hotspots and normal errors.

## Random forest

The random forest regressor was chosen for this problem for two reasons: Performance and interpretability. Unlike other continuous variable estimation models like support vector regression and ridge regression, random forests train and perform very quickly (within a few seconds versus several minutes). Additionally, random forests allow analysts to examine which features are prominently used by the model.
 
Two sets of random forests are trained for this problem. The first set is trained as a generalized regressor that can estimate any error, and the second set is trained as a binary classifier solely used to identify hotspots. For the regressor, the R squared score is high ranging from 0.86-0.89. For the classifier, the precision, recall, and precision scores are almost perfect for each error ranging from 98%-100%. The random forest is trained using 75% of the total dataset and validated using the remaining 25%.


## T-SNE
To demonstrate visual intuition surrounding the problem, I also illustrate a clustered representation of the model. The model is trained on 29 separate features, so to plot, some dimensionality reduction techniques must take place. For this, I used Principal Component Analysis (PCA) as a built-in initializer when creating a 2D representation using T-distributed Stochastic Neighbor Embedding (T- SNE). T-SNE converts similarities between data points to joint probabilities and minimizes the Kullback- Leibler divergence between the joint probabilities of the low dimensional embedding and the high dimensional data.

Although T-SNE is an excellent tool, it is not useful for this case since no clear distinction can be made between non-hotspot samples and hotspot samples. Around 20-30% (give or take) of the plotted samples can be estimated to be hotspots but not reliably.

## Conclusion
Given the difficulty of identifying large prediction errors known as hotspots, I have successfully developed a model capable of predicting when a sample is likely to cause a large prediction error. This model incorporates a random forest where the prominent decision features are easily accessible to an analyst. Furthermore, the precision, accuracy, and recall scores indicate that this model is neither overfit nor underfit to the data.
