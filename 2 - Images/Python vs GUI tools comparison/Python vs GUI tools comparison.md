Tags: [[_Python]] [[__Programming_languages]]
#Python #ProgrammingLanguages 

# See output of different sections of code and variables values
In Python it is easy to test different sections of your code and check values of your variables.

For example here I am executing two different sql queries in two different cells of Jupyter Notebook and I can see results of both queries:
![[2 - Images/Python vs GUI tools comparison/screenshot 1.png]]

And I don’t need to run always both cells with code. I can run the first cell and then I can run multiple times the second cell without running the first cell again and all the variables created in the first cell will be still in memory.

This is very useful for debugging.
# Understanding and finding a code
Understanding Python code is easier than in case of ADF or SSIS because you don’t need to open and close all the time different windows in order to see what actions are being performed, you see everything in a single file.

Also in Python script you see only the code which you created, while in ADF or SSIS you see not only operations which you set up but also you see a lot of options and configurations which you are not using and which you don’t care about.

Also you can use search engine to find sections of code which you are looking for in a given file or to find a specific file which is for example preparing a specific table or connecting to a specific data source.

Thanks to the fact that it is easier to understand and find the code which you are looking for it is easier to maintain and debugg it.
# Tracking changes with Git
With Python it is easier to see what changes were made to the code:
![[2 - Images/Python vs GUI tools comparison/screenshot 2.png]]

In case of SSIS or ADF you would changes done to the source XML or JSON file representing the pipeline and that is not easy readable.
# Other benefits of Python
- Python is free
- There is a big community using Python so there is a lot of information about it on the internet
- Python is very flexible. Building complicated solutions in Python is much easier than using any GUI tool.
- Python scripts can be run using many different tools: ADF, Databricks, VM from any cloud provider, on prem server. So it is easier to change infrastructure for running our code than in case of pipelines build using GUI tools.