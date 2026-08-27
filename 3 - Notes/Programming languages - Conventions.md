Tags: [[__Programming_languages]]
#ProgrammingLanguages 

# Class internal methods
Class methods that are not supposed to be used outside of a class but rather in other methods of that class have a name starting with an underscore `_`, for example:
```python
class A:
	def _internal_method():
		...
		
	def another_method():
		...
		# OK - Using an internal method inside another method
		_internal_method()
		...
		
obj = A()
# An internal method is not supposed to be used outside of a class like this
obj._internal_method()
```