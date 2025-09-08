# Hardware of a computer 

## CPU 

To see which *family* the **CPU** of the current system belongs to, use the `arch` command:
```bash
sysadmin@localhost:~$ arch
x86_64
```

For *more* information concerning the CPU, use the `lscpu` command:
```
sysadmin@localhost:~$ lscpu
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                4
On-line CPU(s) list:   0-3                                                   
Thread(s) per core:    1                                                     
Core(s) per socket:    4                                                     
Socket(s):             1
NUMA node(s):          1                                                     
Vendor ID:             GenuineIntel  
...
...
```

The first line of this output shows that the CPU is being used in a 64-bit mode, as the architecture reported is x86_64. The second line of output shows that the CPU is capable of operating in either a 32- or 64-bit mode, therefore, it is actually a 64-bit CPU.

## RAM

To view the amount of RAM in your system, including the swap space, execute the `free` command. The `free` command has a `-m` option to force the output to be rounded to the nearest megabyte (MB) and a `-g` option to force the output to be rounded to the nearest gigabyte (GB):
```bash
sysadmin@localhost:~$ free -m                                                
             total       used       free     shared    buffers     cached    
Mem:          1894        356       1537          0          25       177    
-/+ buffers/cache:        153       1741                                     
Swap:         4063          0       4063
```
The output shows that this system has a total of 1,894 MB and is currently using 356 MB.

The amount of swap appears to be approximately 4 GB, although none of it appears to be in use. This makes sense because so much of the physical RAM is free, so there is no need at this time for virtual RAM (swap space) to be used.

## Peripheral devices

#### PCI : Peripheral Component Interconnect
- Use `lspci` command to view all PCI devices connected to the machine.

#### USB : Universal Serial Bus 
- Use `lsusb` command to view all USB devices connected to the machine.


