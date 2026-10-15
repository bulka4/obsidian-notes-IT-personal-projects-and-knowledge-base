Tags: [[__Software_Engineering]]
#SoftwareEngineering  

# Introduction
Canary deployment is a deployment strategy where we send only a small portion of traffic to the new version initially.
```
v1 ← 95% traffic
v2 ← 5% traffic
```

If everything looks good:
```
v1 ← 50%
v2 ← 50%
```

Eventually:
```
v2 ← 100%
```
