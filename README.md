import matplotlib.pyplot as plt
import numpy as np
from sklearn import datasets, linear_model
from sklearn.metrics import mean_squared_error
diabetes = datasets.load_diabetes()
# print(diabetes.keys()) >> dict_keys(['data', 'target', 'frame', 'DESCR', 'feature_names', 'data_filename', 'target_filename', 'data_module'])

diabetes_X = diabetes.data[:, np.newaxis, 2]

diabetes_x_train = diabetes_X[:-30]
diabetes_x_test = diabetes_X[-30:]

diabetes_y_train = diabetes.target[:-30]
diabetes_y_test = diabetes.target[-30:]


model = linear_model.LinearRegression()
model.fit(diabetes_x_train, diabetes_y_train)

diabetes_y_prediction = model.predict(diabetes_x_test)

print("Mean squared Error is : ", mean_squared_error(diabetes_y_test, diabetes_y_prediction))

print("Weights: ", model.coef_)
print("Intercept: ", model.intercept_)

plt.scatter(diabetes_x_test, diabetes_y_test)

plt.plot(diabetes_x_test, diabetes_y_prediction)
plt.show()
