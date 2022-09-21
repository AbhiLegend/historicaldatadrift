# Historical datadrift
## Summary <br />
Historical Data Drift is used to study how the data has changed and also from that we can monitor threshold <br />
For this exercise we will be running the code from command line. <br />
Make sure you clone the github repo. <br />
### Detecting,evaluating and visualizing historical drifts in the data . <br />
Steps we need to follow: <br />
i)Make Sure python is installed.<br />
ii)I will be showing the entire process in Windows machine . <br />
iii)Make sure JSON,Pandas and Numpy are installed as weill be using these libraries . <br />
iv)We need to install plotly to visualize our drift. <br />
Using pip the process is as follows. <br />
```
pip install plotly
```
To install Evidently using pip the process is shown below. <br />
```
pip install evidently
```
Similarly to install Mlflow <br />
```
pip install mlflow
```
As we are using plotly to get the visualizations to save the visualizations as screenshots we will use the following code in python. <br />
```
fig.write_image("fig1.png")
```
To run the code in command window with mlflow following command needs to be given. <br />
To Setup mlflow server locally in the system the following code works. <br />
```
python expo.py & mlflow server --host 0.0.0.0
```
And if you want to use it with mlflow ui the following code works.
```
python expo.py & mlflow ui
```
Let's take a look at expo.py code <br />
First we import necessary libraries <br />

We define column mapping to specify the feature type. That is needed to perform the correct statistical tests using Evidently. <br />
Next we define column mapping to specify the feature type. That is needed to perform the correct statistical tests using Evidently. <br />
```
data_columns = {}
data_columns['numerical_features'] = ['weather', 'temp', 'atemp', 'humidity', 'windspeed']
```
We also define our reference data (the first month) and the following periods to evaluate for drift. We treat each month of data as an experiment. <br />
```
reference_dates = ('2011-01-01 00:00:00','2011-01-28 23:00:00')

experiment_batches = [
    ('2011-02-01 00:00:00','2011-02-28 23:00:00'),
    ('2011-03-01 00:00:00','2011-03-31 23:00:00'),
    ('2011-04-01 00:00:00','2011-04-30 23:00:00'),
    ('2011-05-01 00:00:00','2011-05-31 23:00:00'),  
    ('2011-06-01 00:00:00','2011-06-30 23:00:00'), 
    ('2011-07-01 00:00:00','2011-07-31 23:00:00'), 
]
```
Now we discuss two functions.First detects dataset drift.The other function detects feature drift. <br />
Let us visualize the feature drift.In the code we are saving the feature drift as a snapshot so that we can analyse it.We call our function for feature drift to <br />evaluate the drift for individual features. <br />
We use Plotly to visualize to view the results on heatmap.The dataset drift is showed in red color. <br />
![alt text](https://github.com/AbhiLegend/historicaldatadrift/blob/main/images/fig1.png) <br />

Not at all stable. <br />

The truth is, we took a use case with high seasonality. Our data is literally about the weather. Temperature, humidity, wind speed patterns change a lot month by month. <br />

This gives us a very clear signal that we need to factor in the most recent data and update the model often. <br />

If we want to look at it in a more granular fashion, we can plot our P-values. We set the get_pvalues as TRUE and then generate a new plot. <br />
![alt text](https://github.com/AbhiLegend/historicaldatadrift/blob/main/images/fig2.png) <br />

### Visualizing Dataset drift
Let's now call a function to calculate the dataset drift. <br />

Knowing how volatile the data is, we set our threshold high. We only call it DRIFT if 90% of features have a statistical change in distributions. <br />
```
dataset_historical_drift = []

for date in experiment_batches:
    dataset_historical_drift.append(detect_dataset_drift(raw_data.loc[reference_dates[0]:reference_dates[1]], 
                           raw_data.loc[date[0]:date[1]], 
                           column_mapping=data_columns, 
                           confidence=0.95))
```
That is how the results would look on a month-by-month basis.

![alt text](https://github.com/AbhiLegend/historicaldatadrift/blob/main/images/fig3.png) <br />

You can also set a more granular view and make a plot using the share of drifting features within each month. <br />
![alt text](https://github.com/AbhiLegend/historicaldatadrift/blob/main/images/fig4.png) <br />

### Logging the drifts using Mlflow
We use Mlflow to log the drifts.As we run the code and Mlflow together we see the resultant in either the mlflow ui or mlflow server. <br />
```
python expo.py & mlflow server --host 0.0.0.0
```
As we run the code the following things are shown in the coomand window as shown below <br />

![alt text](https://github.com/AbhiLegend/historicaldatadrift/blob/main/images/CodeCapture1.PNG) <br />

To access the mlflow ui we need to go to the browser and key in localhost : <port> for me it is running on port 5000.After logging we need to  <br />
select the experiment so that we can view the details. <br />
  
![alt text](https://github.com/AbhiLegend/historicaldatadrift/blob/main/images/mlflow1.PNG) <br />
  
For the run window we can see the parameters and the metrics for the expriments <br />
![alt text](https://github.com/AbhiLegend/historicaldatadrift/blob/main/images/mlflow2.PNG) <br />

We can view the dataset drift for the run. <br />
![alt text](https://github.com/AbhiLegend/historicaldatadrift/blob/main/images/mlflow3.PNG) <br />
We can compare more than one run to see the results for the drift <br />
![alt text](https://github.com/AbhiLegend/historicaldatadrift/blob/main/images/mlflow4.PNG) <br />
### Summary for the code and the experiment
We are able to run the code and mlflow simultaneously <br />
We are able to compare historical datadrift so that we get insight into how the dataset has been behaving <br />
Using Plotly we are able to get different insights and views into the dataset <br />
Using Mlflow we are able to log the drifts so that we can easily compare the results <br />
                                                                                                              
                                                          





  















