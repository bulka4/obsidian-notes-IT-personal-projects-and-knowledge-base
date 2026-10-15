Tags: [[__Software_Engineering]]
#SoftwareEngineering  

# Introduction
Blue-green deployment is a deployment strategy where we run the two versions simultaneously.
```
Blue:  v1  ← traffic

Green: v2  ← no traffic
```

Once v2 is ready:
```
Blue:   v1
Green:  v2  ← traffic
```

You can switch traffic back to v1 if necessary.