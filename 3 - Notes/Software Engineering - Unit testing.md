Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
In unit testing, we test small pieces of code without using external dependencies like databases or APIs. Instead, we use test doubles ([[Software Engineering - Test doubles|link]]) to mimic the behavior of those external dependencies.

For example, we might create manually a Pandas dataframe in Python to create a table we need instead of populating it with data from a real external database.