### Prepare the Data for Machine Learning Algorithms

It’s time to prepare the data for your Machine Learning algorithms. Instead of just doing this manually, you should write functions to do that, for several good reasons:

    [x] This will allow you to reproduce these transformations easily on any dataset (e.g., the next time you get a fresh dataset).

    [x] You will gradually build a library of transformation functions that you can reuse in future projects.

    [x] You can use these functions in your live system to transform the new data before feeding it to your algorithms.

    [x] This will make it possible for you to easily try various transformations and see which combination of transformations works best.
    

But first let’s revert to a clean training set (by copying `strat_train_set` once again), and let’s separate the predictors and the labels since we don’t necessarily want to apply the same transformations to the predictors and the target values (note that `drop()` creates a copy of the data and does not affect `strat_train_set`):

`housing = strat_train_set.drop("median_house_value", axis=1)`

`housing_labels = strat_train_set["median_house_value"].copy()`

### Data Cleaning

Most Machine Learning algorithms cannot work with missing features, so let’s create a few functions to take care of them. You noticed earlier that the total_bedrooms attribute has some missing values, so let’s fix this. You have three options:

    Get rid of the corresponding districts.

    Get rid of the whole attribute.

    Set the values to some value (zero, the mean, the median, etc.).

You can accomplish these easily using DataFrame’s 'dropna()', 'drop()', and 'fillna()' methods: