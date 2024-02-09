#cs61c #cs162 

Parallelism is a core topic in machine structures. It is a principle of efficiency, where our goal as computer engineers is to execute as many instructions as possible at the same time.

>[!tip] Amdahl's Law
>The amount of instructions we can run in parallel is limited—some processes must be executed sequentially. This essentially bounds how efficient parallelizing can make our programs.

In general, our runtime is composed of three factors:
1. The number of instructions in the program
2. The number of cycles per instruction
3. The time of each cycle -> cannot be sped up, the absolute limit is the speed of light

