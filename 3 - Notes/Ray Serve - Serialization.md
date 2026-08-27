Tags: [[__Machine_Learning_Engineering]], [[_Ray]]
#MLEngineering #Ray 

# Introduction
When we create a Ray Serve application, Ray serializes the deployment definition and the objects it needs to reconstruct the deployment
# What gets serialized
As an example, let's consider such an application:
```python
@serve.deployment
class MyModel:
    def __init__(self):
        self.model = load_model()

    def __call__(self, request):
        ...
        
app = MyModel.bind()
```

In the below subsections it is described what Ray can serialize.
## 1. The `Application` / deployment graph is serialized
`MyModel.bind()` doesn't instantiate `MyModel`. It creates a deployment graph / DAG-like object describing:
```
MyModel
   └── constructor args
```

Ray serializes this graph so that it can be transferred to the Serve controller and eventually used to create replicas.
## 2. The deployment class/function is serialized
Ray needs to make the deployment code available where the replica runs.

This is where cloudpickle comes into play. Ray can serialize Python functions/classes (the code), including many things that standard `pickle` cannot.

Conceptually:
```
MyModel class
constructor arguments
deployment configuration
        ↓
     cloudpickle
        ↓
Ray cluster
```
## 3. Constructor arguments can also be serialized
For example:
```python
@serve.deployment
class MyModel:
    def __init__(self, model_path):
        self.model = load_model(model_path)

app = MyModel.bind("/models/my-model")
```

The string `"/models/my-model"` is serialized as part of the deployment graph.

But importantly, the `self.model` object isn't serialized here, because it doesn't exist yet.

Each replica effectively does:
```python
replica = MyModel("/models/my-model")
```

and therefore loads its own model.
## 4. Global variables
Global variables outside of the Ray Serve deployment class, for example:
```python
x = 'a'

@serve.deployment
class MyModel:
	def __init__(self, x):
        self.x = x
```
are also serialized if they are later used in the deployment class.

Thus we should avoid creating big variables or variables difficult to serialize outside of the deployment class.