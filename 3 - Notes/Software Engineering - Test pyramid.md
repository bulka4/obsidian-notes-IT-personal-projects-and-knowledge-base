Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
The **Test Pyramid** is a guideline for how many tests of each type we should have:
```
            /\
          /   \
        /  E2E  \
       /---------\
      /Integration\
     /-------------\
    /  Unit Tests   \
   /_________________\
```
so that is:
- few E2W tests
- Some integration tests
- Many unit tests