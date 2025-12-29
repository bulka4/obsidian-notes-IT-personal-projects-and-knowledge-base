Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[_Docker]] 

# Introduction
Every time Docker has an instruction to perform during building an image, it checks that instruction has been built before.

If yes, then it using a layer which was already built before (a cached layer).

If not, then it executes this instruction to create a new layer.

In order to decide whether to use a cached layer or not Docker checks:
- If the instruction text has changed
- If the files used in the instruction has changed (for example in the ‘COPY’ instruction)
-  Any files in the build context (the directory where we run ‘docker build’) has changed (even those not mentioned in the dockerfile)

If we change an instruction in a Dockerfile, then all the next instructions will be reexecuted (caching will not be used).

#DevOps #InfrastructureEngineering #Docker 