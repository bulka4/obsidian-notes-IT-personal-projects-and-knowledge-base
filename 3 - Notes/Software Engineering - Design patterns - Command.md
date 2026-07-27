Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
The command pattern is used to represent an action to perform as an object. This operation object can be stored, pass as an argument to functions etc.

So we create an object which represents an action:
```python
command = Command()
```
and we execute it:
```python
command.execute()
```

Or we can do something with different commands before we execute them:
```python
command1 = Command(x)
command2 = Command(y)

def f(commands):
	for command in commands:
		command.execute()
		
f([command1, command2])
```

The action it executes can be any method from any other class.
# Example
For example, if we have a class like this:
```python
class LightBulb:
    def turn_on(self):
        print("Light is on")

    def turn_off(self):
        print("Light is off")
```

the the object `bulb = LightBulb()` doesn't represent any action. 

So we create command classes for different operations:
```python
class TurnOnCommand:
    def __init__(self, bulb):
        self.bulb = bulb

    def execute(self):
        self.bulb.turn_on()


class TurnOffCommand:
    def __init__(self, bulb):
        self.bulb = bulb

    def execute(self):
        self.bulb.turn_off()
```

and now we can represent operations as objects which can be stored, passed as an argument to functions etc., for example we can do something like:
```python
turn_on_command = TurnOnCommand(bulb)
turn_off_command = TurnOffCommand(bulb)

def f(commands):
	for command in commands:
		command.execute()
		
commands_to_run = [turn_on_command, turn_off_command]
f1(commands_to_run)
```

Instead of:
```python
bulb = LightBulb()

f([bulb.turn_on(), bulb.turn_off()])
```
