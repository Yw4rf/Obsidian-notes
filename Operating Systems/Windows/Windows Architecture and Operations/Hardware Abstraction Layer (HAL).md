##### Hardware Abstraction Layer (HAL)
- Windows computers use many different types of hardware. When the OS is installed, it must be isolated from differences in hardware.
- HAL is a software that handles all the communication between the hardware and the kernel. 
- The kernel is the core of the Operative System and has control over the entire computer. it handles all of the input and output requests, memory, and all of the peripherals connected to the computer.
- Basic Windows Architecture:

![HAL](HAL.png)

- Because the Kernel still contains some hardware-specific code for these critical tasks, it is said to be **"not completely independent of the HAL."** They are tightly coupled to ensure the system is both portable and fast.
- The HAL also needs the kernel to perform some functions.