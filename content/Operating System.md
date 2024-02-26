
Lecture notes from Operating System & Experiment taught by Insik Shin - KAIST
### Introduction - 26 Feb 24

- Computer science is abstraction(making things simple)
- First design and then code
	- Divide and conquer method would be good for this lecture's project.

4 Computer system structure
1. Users
	- People who uses the computer
2. Hardware
	- provides basic computing resources
	- cpu, gpu, ram, etc.
3. Software(Application programs)
	- Defines way how to use system resources
4. Operating system
	- Controls & coordinates use of hardware
	![[Pasted image 20240226135211.png|200]] (We will consider User, Application as one)
	

Role of operating system (Similar to government)
- Facilitator
- Traffic Cop
- Example) File system(logical storage)
	- We save data physically on a disk sector(HDD).
	- However we do not care or know the disk sector -> we need a file system
	- File system is needed by everyone(Facilitator)
	- But the file system needs to be protected(Traffic Cop)
- The reason why this operating system works: People believe operating system works perfectly and also safe, but not sure with applications.
- If we want to reduce the code size(make it smaller& trustworthy)
	- Keep the traffic cop functionality, and give up the facilitator(Available at the application level).

Definition of operating system
- No universal definition
- Suggestion: Everything a vendor ships when you order an operating system
- The one program running at all times on the computer - Kernel or Operating System

