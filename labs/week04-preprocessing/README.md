# Week 04 Lab

Build a reusable preprocessing pipeline (sklearn Pipeline/ColumnTransformer); PCA as a worked stateful-transform example.

Starter files for this week's lab will be added here before the lab session
(pulled into your repo via `git fetch upstream && git merge upstream/main`,
as introduced in the Week 1 lab).

# REFLECTION

### train.py's original accuracy and your final pipeline's accuracy turned out close to each other. Given everything from lecture, why doesn't that mean the leak was harmless?

The leak could be harmful. If the test data leaks into training then it knows some knowledge about the test set. It would in a nutshell mean that the model havent learned some of the patterns of the testing data from the training data. Leakage can show increase in accuracy but might struggle against unseen real data. There been cases where a good hardcoded values for mean and std while normalization gave a better results for images. 

### Which exact line(s) caused the leak? What did you actually compare to prove it was happening — not just "the accuracy changed"?
   ```python
   imputer = SimpleImputer(strategy="mean")
   X[NUMERIC_FEATURES] = imputer.fit_transform(X[NUMERIC_FEATURES])
   scaler = StandardScaler()
   X[NUMERIC_FEATURES] = scaler.fit_transform(X[NUMERIC_FEATURES])
   ```

   These line before the `train_Test split` has caused the data leakage. 

   We proved it by comparing the leakyscalar mean which is [mean of training data + testing data] to correct scalar mean [mean of just the training data]. This inconsistency proves that the data got leaked.

### Suppose this model went to production, and the serving code recomputed its own StandardScaler from whatever requests happened to be in the last hour, instead of loading the one saved during training. Which lecture topic does that describe, and how is it different from the bug you just fixed here?
The lecture topic would be Train/Serve Skew which comes from the independent implementations of same features. for eg: the model is trained on a different mean and during production a new mean is recomputed.

### What does PCA's "state" mean in this pipeline? What would go wrong if serving code ran a fresh PCA().fit_transform() on incoming requests instead of reusing the fitted pca object from training?

PCA "state" has the feature means and other principal components that used during training, from the training data. if serving code ran a fresh PCA().fit_transform() may produce new principal components which might cause train / serve Skew issue. 

