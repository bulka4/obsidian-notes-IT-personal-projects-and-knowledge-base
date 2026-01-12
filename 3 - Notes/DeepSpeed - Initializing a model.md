Tags: [[__Distributed_computing]], [[__Infrastructure_Engineering]], [[__Machine_Learning_Engineering]], [[_DeepSpeed]]
#DistributedComputing #InfrastructureEngineering #MLEngineering #DeepSpeed 

# Introduction
To load a model, so we can make predictions using it, we need to use `deepspeed.initialize` on every node:
```python
class MyModel(torch.nn.Module):
    def __init__(self):
        super().__init__()
        self.linear = torch.nn.Linear(10, 1)

    def forward(self, x):
        return self.linear(x)

model = MyModel().cuda()

deepspeed.initialize(
    model=model,
    model_parameters=model.parameters(),
    config="ds_config.json",
)
```