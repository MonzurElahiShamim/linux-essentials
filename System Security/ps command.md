---
updated_at: 2024-08-17T00:47:18.028+06:00
edited_seconds: 40
---
# `ps` command


>[!gemini]+ Gemini
>The `ps` command (process status) displays information about running processes. The output of the command includes the process ID (PID), process name, % of CPU and memory usage, command line arguments, and more.
> 
> **Syntax:**
> 
> ```bash
> ps [options]
> ```
> 
> **Options:**
> 
> * **-a:** Show all processes, including processes not owned by the current user.
> * **-e:** Show the entire environment for each process.
> * **-f:** Show full process information, including user ID, group ID, start time, and more.
> * **-l:** Show additional information, including scheduling policy, thread information, and more.
> * **-t:** Specify a process group ID or session ID to display information about only those processes.
> * **-u:** Show information about processes owned by a specific user.
> 
> **Example:**
> 
> ```bash
> # Display brief information about all running processes
> ps -ef
> 
> # Show full information about the current shell
> ps -fl $$
> ```
 