Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# For loop
Iterate over a list:
```bash
for item in one two three; do
	echo "item: $item"
done
```
Iterate over a sequence of numbers:
```bash
for i in {1..5}; do
	echo "number: $i"
done
```
Iterate over a sequence of numbers with specified step:
```bash
for i in {1..10..2}; do
	echo "Number $i"
done
```
It will print 1, 3, 5, 7, 9
# While loop
Syntax for the while loop:
```bash
while [ condition ]; do
	commands
done
```