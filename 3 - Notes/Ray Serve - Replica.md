Tags: [[__Machine_Learning_Engineering]]

# Introduction
For each Deployment ([[Ray Serve - Deployment|link]]), Ray Serve creates one or more replicas.

Each replica is a Ray Core Actor ([[Ray Core - Actors|link]]) (a logical object) and to each Actor there is assigned a Worker process which executes deployment's code.

#MLEngineering 