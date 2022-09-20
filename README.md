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







