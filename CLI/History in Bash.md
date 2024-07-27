---
updated_at: 2024-07-22T21:50:14.713+06:00
edited_seconds: 1040
---
# History in Shell

When a command is executed in the terminal, it is stored in a history list, allowing easy re-execution without retyping. Here's how you can utilize this feature:

- **Navigating History**:
  - **Up Arrow (↑)**: Press to display the previous command.
  - **Down Arrow (↓)**: Press to move forward in the command history (after using the Up Arrow).
  - **Enter**: Press to re-execute the displayed command.
  - **Left Arrow (←)** and **Right Arrow (→)**: Use to position the cursor for editing the command.
  - Additional keys like **Home**, **End**, **Backspace**, and **Delete** can also help in command editing.

### Viewing Command History

```BASH
sysadmin@localhost:~$ date                                       
Wed Dec 12 04:28:12 UTC 2018 

sysadmin@localhost:~$ ls                                           
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos       
sysadmin@localhost:~$ cal 5 2030                                  
     May 2030                                                                
Su Mo Tu We Th Fr Sa                                                         
          1  2  3  4                                                         
 5  6  7  8  9 10 11                                                         
12 13 14 15 16 17 18                                                         
19 20 21 22 23 24 25                                                         
26 27 28 29 30 31                                                            
```

To see the list of previously executed commands, use the `history` command:

```bash
sysadmin@localhost:~$ history
    1  date
    2  ls
    3  cal 5 2030
    4  history
```

This lists all commands run in the current session.

### Re-executing Commands

- **By History Number**:
  - You can execute a command from the history list by typing `!` followed by the command's number:
    ```bash                                                   
	sysadmin@localhost:~$ !3                                        
	cal 5 2030                                                        
	     May 2030                                                            
	Su Mo Tu We Th Fr Sa                                            
	          1  2  3  4                                                   
	 5  6  7  8  9 10 11                                                    
	12 13 14 15 16 17 18                                                    
	19 20 21 22 23 24 25   
    ```

- **Most Recent Command**:
  - Type `!!` to re-execute the most recent command:
	```bash
	sysadmin@localhost:~$ date                                               
	Wed Dec 12 04:32:36 UTC 2018                                             
	
	sysadmin@localhost:~$ !!                                             
	date
	Wed Dec 12 04:32:38 UTC 2018
	```

- **By Command Name**:
  - Use `!` followed by the command name to execute the most recent occurrence of that command:
    ```bash
    sysadmin@localhost:~$ !ls
    ```

### Showing Specific History

- **Last N Commands**:
  - To display the last `N` commands, use `history N`:
    ```bash
	sysadmin@localhost:~$ history 3
	    6  date                                                              
	    7  ls /home                                                          
	    8  history 3
	```

- **Nth Command from the Bottom**:
  - Use `!-n` to run the `n`th command from the bottom of the history list:
    ```bash
	sysadmin@localhost:~$ !-3                                                
	date                                                                     
	Wed Dec 12 04:31:55 UTC 2018 
	```

### Search in History 

- Simply type: `Ctrl + R` ; then enter the search keyword. 
- Then navigate using `Ctrl + R`

### Add `date` and `time` in history file

- & Add `HISTTIMEFORMAT="%Y-%b-%d %T"` or `HISTTIMEFORMAT="%Y-%m-%d %T"` in the `.bashrc` file.

### Example Session

Consider the following terminal session:

```bash
sysadmin@localhost:~$ date
Wed Dec 12 04:28:12 UTC 2018

sysadmin@localhost:~$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos

sysadmin@localhost:~$ cal 5 2030
     May 2030
Su Mo Tu We Th Fr Sa
          1  2  3  4
 5  6  7  8  9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30 31

sysadmin@localhost:~$ history
    1  date
    2  ls
    3  cal 5 2030
    4  history
```

- Re-run the `cal` command using `!3`:
  ```bash
  sysadmin@localhost:~$ !3
  ```

- Execute the most recent command (`history`) using `!!`:
  ```bash
  sysadmin@localhost:~$ !!
  ```

By leveraging these history features, you can efficiently recall and reuse commands in your terminal sessions.