# Developing a Neural Network Regression Model

## AIM

To develop a neural network regression model for the given dataset.

## THEORY
A neural network with multiple hidden layers and multiple nodes in each hidden layer is known as a deep learning system or a deep neural network. Here the basic neural network model has been created with one input layer, one hidden layer and one output layer.The number of neurons(UNITS) in each layer varies the 1st input layer has 16 units and hidden layer has 8 units and output layer has one unit.

In this basic NN Model, we have used "relu" activation function in input and hidden layer, relu(RECTIFIED LINEAR UNIT) Activation function is a piece-wise linear function that will output the input directly if it is positive and zero if it is negative.

## Neural Network Model
![image](https://github.com/jithendra2004/basic-nn-model/assets/94226297/2b87cc95-de4e-4949-9691-0e15cd425197)


## DESIGN STEPS

### STEP 1:

Loading the dataset

### STEP 2:

Split the dataset into training and testing

### STEP 3:

Create MinMaxScalar objects ,fit the model and transform the data.

### STEP 4:

Build the Neural Network Model and compile the model.

### STEP 5:

Train the model with the training data.

### STEP 6:

Plot the performance plot

### STEP 7:

Evaluate the model with the testing data.

## PROGRAM
~~~
DEVELOPED BY:K.DEVI JHANSI
REG.NO:212221230045
~~~
~~~
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from google.colab import auth
import gspread
from google.auth import default
auth.authenticate_user()
creds, _ = default()
gc = gspread.authorize(creds)
worksheet = gc.open('ex1').sheet1
data = worksheet.get_all_values()
dataset1=pd.DataFrame(data[1:],columns=data[0])
dataset1=dataset1.astype({'input':'float'})
dataset1=dataset1.astype({'output':'float'})
dataset1.head()
X = dataset1[['input']].values
y = dataset1[['output']].values
X
X_train,X_test,y_train,y_test = train_test_split(X,y,test_size = 0.33,random_state = 33)
Scaler = MinMaxScaler()
Scaler.fit(X_train)
X_train1 = Scaler.transform(X_train)
ai_brain=Sequential([
    Dense(8,activation='relu'),
    Dense(10,activation='relu'),
    Dense(1)
])
ai_brain.compile(optimizer='rmsprop',loss='mse')
ai_brain.fit(X_train1,y_train,epochs=200)
loss_df = pd.DataFrame(ai_brain.history.history)
loss_df.plot()
X_test1 = Scaler.transform(X_test)
X_n1 = [[30]]
X_n1_1 = Scaler.transform(X_n1)
ai_brain.predict(X_n1_1)
~~~

## Dataset Information

![image](https://github.com/jithendra2004/basic-nn-model/assets/94226297/4d33094b-fd1c-4d15-abe0-94ed2f192ced)


## OUTPUT

### Training Loss Vs Iteration Plot

![image](https://github.com/jithendra2004/basic-nn-model/assets/94226297/c8a0774d-cce6-4652-9e28-aefa3a518fa0)


### Test Data Root Mean Squared Error
![image](https://github.com/jithendra2004/basic-nn-model/assets/94226297/23041bbc-2221-4744-8ac4-139582d8e3d1)


### New Sample Data Prediction

![image](https://github.com/jithendra2004/basic-nn-model/assets/94226297/1107a195-6b18-4cf3-aa47-b2959920b1dd)

## RESULT
A Basic neural network regression model for the given dataset is developed successfully.
