Tags: [[__Machine_Learning]] [[__Machine_Learning_Engineering]] [[_Tensorflow]]
#MachineLearning #MLEngineering #Tensorflow 

# Introduction
Below sections describe how to create a custom model using Tensorflow. This is mostly used for neural networks but it can be used in general for any differentiable computation components (so instead of neural network layers we can use any other differentiable function).
# Inheriting from the `tf.keras.Model`
To define a custom model using Tensorflow, we can create a class which inherits from the `tf.keras.Model` like this:
```python
import tensorflow as tf

class MyModel(tf.keras.Model):

    def __init__(self):
        super().__init__()

        self.dense1 = tf.keras.layers.Dense(64, activation='relu')
        self.dense2 = tf.keras.layers.Dense(32, activation='relu')
        self.out = tf.keras.layers.Dense(1)

    def call(self, inputs):
        x = self.dense1(inputs)
        x = self.dense2(x)
        return self.out(x)

model = MyModel()
```
## Training function
For training, we can use functions `compile` and `fit`:
```python
model.compile(
    optimizer='adam',
    loss='mse',
    metrics=['mae']
)

model.fit(X_train, y_train, epochs=10)
```
# Custom layers
We can also create custom layers:
```python
class MyLayer(tf.keras.layers.Layer):

    def __init__(self, units):
        super().__init__()
        self.units = units

    def build(self, input_shape):
        self.w = self.add_weight(
            shape=(input_shape[-1], self.units),
            initializer='random_normal',
            trainable=True
        )

    def call(self, inputs):
        return tf.matmul(inputs, self.w)
```
# Custom training loop
To create a custom training loop, we can use:
```python
optimizer = tf.keras.optimizers.Adam()

for epoch in range(10):

    with tf.GradientTape() as tape:

        predictions = model(X_train)
        loss = tf.reduce_mean(
            tf.keras.losses.mse(y_train, predictions)
        )

    gradients = tape.gradient(loss, model.trainable_variables)

    optimizer.apply_gradients(
        zip(gradients, model.trainable_variables)
    )

    print(loss.numpy())
```
# Inheriting from `tf.keras.Model` vs `tf.keras.layers.Layer`
The `tf.keras.Model` class is a subclass of the `tf.keras.layers.Layer`. It additionally adds functions like `compile` and `fit` for training.
