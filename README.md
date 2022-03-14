### *@Maintenance will resume on April 2022*
# Risk Management


## Abstraction
One of the problems mostly encounter in designing trading strategies is not knowing when market doesn't behave as it used to. And this uncertainty turns out to be the greatest risk every trader faces. This research aims to design a procedure to detect and predict those unbehaves so as to prevent lossing and even winning.

## Methology
<!-- Background Investigation -->
### Background Investigation -- Deterministic Model
By conducting unsupervised classification, it's a lot easier to discriminate the degree of jeopardy about the existing position and opportunities of future dicisions. This model aims to help traders to come up with algorithmic strategies for different clusters.

* Cluster -- EM-GMM model
* Classification -- Random Forrest/Decision Tree

<!-- Anomalies within background intervals -->
### Anomalies -- Stochastic Model
To predict stochastic behavior, user can define certain amplitude of volatility as a treshold. Those greater than the threshold are defined as anomalies, and their yesterday are labeled for neural network to learn. For most cases, volatiling over 300 point within a day is recommended threshold. Hyperparameter and parameter setting still require domain-knowledge to optimise the performance of this model.

* AD -- 1DCnn approach

<!-- Usage -->
## Usage
* Download from PyPI
```sh
pip install risk-manage=1.1.3
```
```sh
import risk_manage as rm
```
* Setting up targets and days to trace
```sh
target = "^VIX"
target_u = "^TWII"
daypara = 400
```
### Clustering
* Explore optimal number of clusters 
```sh
model = rm.cluster_model(target, daypara)
model.plot_info_criteria()
```
![alt tag](https://user-images.githubusercontent.com/38639538/115183059-aaf8a200-a10d-11eb-9341-27b8d6977b5d.png)
* Fit and Plot
```sh
model.fit("cluster number")
model.plot()
```
![alt tag](https://user-images.githubusercontent.com/38639538/115183163-d9767d00-a10d-11eb-97fd-968f9d2f5ba1.png)

### Decision Boundaries
* Plot 
```sh
model2 = rm.Decision_Boundary(target, target_u, daypara, n_cluster=4)
model2.plot(depth=100, n_estimator=100, resolution=0.05, use_tree=True)
```
![alt tag](https://user-images.githubusercontent.com/38639538/116360991-1390fe80-a833-11eb-81b0-afeaccd505df.png)

* Print detail info
```sh
model2.log()
```

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
```sh
model.metrics(alert_window = 3, n_class = 3, outlier_test)
```
ps.
* alert_window is the sensitivity of detection, meaning predicting how many days before market volatiles
* n_class is the number of clusters
![alt tag](https://user-images.githubusercontent.com/38639538/115183192-e3987b80-a10d-11eb-8db5-8f73a28b6a9e.png)
![alt tag](https://user-images.githubusercontent.com/38639538/115183177-ded3c780-a10d-11eb-88db-cf9b19a4afac.png)
