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
### Clustering
* Optimal number of clusters 
```sh
model = cluster_model(target, daypara)
model.plot_info_criteria()
```
![alt tag](https://user-images.githubusercontent.com/38639538/115183059-aaf8a200-a10d-11eb-9341-27b8d6977b5d.png)
* Fit and Plot
```sh
model.fit("cluster number")
model.plot()
```
![alt tag](https://user-images.githubusercontent.com/38639538/115183163-d9767d00-a10d-11eb-97fd-968f9d2f5ba1.png)

### Anomaly Detection/Prediction
* Hyperparameters setting
```sh
LOOKBACK_SIZE = 10
THRESHOLD = 0.6
BATCH_SIZE = 32
EPOCH = 1000
PATH = "/content/save.pth"
```
* Training
```sh
model = train(LOOKBACK_SIZE, THRESHOLD, BATCH_SIZE, EPOCH, PATH)
outlier_train, loss_df_train = model.predict(load=False)
```
* Load pre-trained model
```sh
outlier_test, loss_df_test = model.predict(load=True)
```
* Metrics on test-set
* alert_window is the sensitivity of detection, meaning predicting how many days before market volatiles
* n_class is the number of clusters
```sh
model.metrics(alert_window = 3, n_class = 3, outlier_test)
```
![alt tag](https://user-images.githubusercontent.com/38639538/115183192-e3987b80-a10d-11eb-8db5-8f73a28b6a9e.png)
