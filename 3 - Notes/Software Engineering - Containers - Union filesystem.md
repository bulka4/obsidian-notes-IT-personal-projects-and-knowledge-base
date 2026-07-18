Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A Union Filesystem is a filesystem that combines filesystem changes from multiple layers ([[Docker - Layers|link]]) into a single view.

It is the technology behind Docker image layers.

The idea:
> Multiple read-only layers are stacked together, and the user sees them as one filesystem.
