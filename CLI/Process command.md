---
updated_at: 2024-07-16T06:27:56.921+06:00
edited_seconds: 800
---

`ps`
`ps -e`
`ps -o`
`ps --forest`

`free`
`free -m`
`free -g`

`kill PID`
`killall`
`pkill`
`jobs`
`top`

`fg %JOB_ID` // process to foreground
`bg %JOB_ID` // send process to background

---
### Lab 13 History                                          
```bash
    4  ping localhost > /dev/null &                                         
    5  jobs                                                                  
    6  ping localhost > /dev/null &                                          
    7  jobs                                                                  
    8  fg %1                                                                 
    9  bg %1                                                                 
    11  jobs                                                                 
    12  ping localhost > /dev/null &                                         
    13  jobs                                                                 
    14  kill %3                                                              
    15  jobs                                                                 
    16  killall ping                                                       
    17  jobs
    18  killall ping                           
    20  kill %1 %2
    21  jobs
    22  ping localhost > /dev/null & 
    23  top
    24  sleep 888888 &
    25  jobs
    26  ps
    28  ps --forest
    29  kill 74
    30  jobs
    31  pkill -15 sleep
    32  jobs 
    33  ping localhost > /dev/null &
    34  ps
    35  ps -e
    36  ps --forest
    37  ps -e --forest
    38  ps -o pid,tty,time,%cppu,cmd
    39  ps -o pid, tty, time, %cppu, cmd
    40  ps -o pid,tty,time,%cppu,cmd 
    41  ps -o pid,tty,time,%cpu,cmd 
    42  ps -o pid,tty,time,%cpu,cmd --sort %mem
    43  ps -o pid,tty,time,%mem,cmd --sort %mem 
    44  free
    45  kill 80
    46  jobs