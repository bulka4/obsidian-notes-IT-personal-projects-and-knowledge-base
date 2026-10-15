Tags: [[__Software_Engineering]]
#SoftwareEngineering  

# Introduction
Recreate deployment is a deployment strategy where we stop the old version and then start the new one:
```
v1 v1 v1
 ↓
nothing
 ↓
v2 v2 v2
```

This is simple but causes downtime.