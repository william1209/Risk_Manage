# Risk Management

<!-- Background Investigation -->
## Background Investigation -- Expected patterns
For most winning cases, having knowledge of the timing when market volatiles or not is a must. Thus we pry into the VIX index which reflects fluctuations the most. Applying cluster algorithm, we may have a glimpse at the silhouette of the market's true nature, but yet not enough. To solve this, classification algorithm/method yields a very good solution. Also the process is the so-called "Unsupervised Classification"

* Cluster -- EM-GMM model
* Classification -- Random Forrest

In a nutshell, find each cluster and draw a distinguishing line between each one.

<!-- Anomalies within background intervals -->
## Anomalies within background intervals -- Unexpected patterns
The max amplitude of fluctuations is limited in each cluster, theoretically. As a matter of fact, it does refresh records. To say there are 2 categories of this series... up-trend and down-trend, anomalies are something between, which are unable to be classified.

* AD -- 1DCnn approach

<!-- Usage -->
## Usage
* Setting up targets and days to trace
```sh
target = "^VIX"
target_u = "^TWII"
daypara = 400
```
### Dive in
* Optimal number of clusters 
```sh
model = cluster_model(target, daypara)
model.plot_info_criteria()
```
* Fit and Plot
```sh
model.fit("cluster number")
model.plot()
```
