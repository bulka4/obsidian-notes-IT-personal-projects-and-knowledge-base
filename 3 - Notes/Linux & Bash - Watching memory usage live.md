Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
To watch memory usage by processes live, we can use a few commands:
- `htop`
```bash
# Install htop
apt update
apt install htop
# Run it to see memory usage
htop
```
- `top`
  Run:
	```bash
	top
	```
	Then press `shift + M` to sort by memory
- `ps aux`:
	```bash
	# Install propcs to get watch command
	apt update
	apt install procps -y
	# Watch memory usage
	watch -n 1 'ps aux --sort=-%mem | head'
	```
	It updates every second