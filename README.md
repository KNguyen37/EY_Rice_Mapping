# Crop Type Classification with Sentinel-1 SAR Data

This project classifies crop types from multi-temporal radar imagery using machine learning approaches.

## Data

The raw data sources used were:
* Sentinel-1 C-band VV/VH backscatter intensity rasters over an agricultural site spanning 3 months
* Point vector data with 10 crop labels randomly distributed over the site's farmland

### Data Wrangling

1. **Spatial Join**: A spatial join between the crop labels and radar data extracted average VV/VH values for each farm's time series. 
2. **Preprocessing**: Reshaped to samples x timesteps. Relative vegetation index (RVI) computed for each time series.
3. **Train Test Split**: 80-20 stratified split of farms to separate train and test sets.

## Modeling

Varying ML approaches were tested:
* 1D CNN on RVI
* 1D CNN on radar backscatter 
* Random forest on backscatter
* Random forest on RVI

Hyperparameter tuning and cross validation were utilized.

Here is an updated Results section highlighting that the random forest model on RVI performed best on the EY test set:

## Results  

Multiple models were evaluated based on accuracy on a held-out EY test set consisting of Sentinel-1 SAR data over unknown crop types.

The best performing model was a **random forest classifier trained on engineered relative vegetation index (RVI) features**, which achieved **85% accuracy** at predicting crop types on the EY test data.

The next best model, a 1D CNN operating directly on the VV/VH time series, scored 10 percentage points lower at 75% accuracy.

The high performance of the RF+RVI approach can be attributed to:

* The derived polarization ratios captured in RVI provide meaningful geospatial features
* Ensemble modeling reduces overfitting  compared to deep CNNs
* Interpretability of RFs allows analysis of important variables  

Given the significant jump in accuracy on external industry data, the RF+RVI approach shows good generalization ability even with limited training samples. This model has been saved for real-world crop type mapping applications.

Future iterations could incorporate recent hyperparameter optimization techniques such as Bayesian hyperband to further improve predictive power.