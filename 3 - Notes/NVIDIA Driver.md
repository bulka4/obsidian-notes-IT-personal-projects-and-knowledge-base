Tags: [[_Hardware_abstraction]]
#HardwareAbstraction

# Introduction
An NVIDIA driver is the software that allows the operating system and applications to communicate with an NVIDIA GPU. It manages the GPU hardware and exposes APIs (like CUDA ([[CUDA|link]])) so programs can use the GPU for computation or graphics.

What it does:
- Controls the GPU hardware directly
- Handles memory, scheduling, and interrupts
- Provides API access to programs (CUDA, OpenCL, OpenGL)
	- Programs can use this API to use GPU for computations
- Monitors GPU usage, temperature, and errors