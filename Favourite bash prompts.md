
```bash
# PS1='\n\033[38;5;209m\]┌─ [$(date +%Y-%m-%d) \t] [\033[38;5;141m\]\u\033[38;5;209m\]@\033[38;5;105m\]\h\033[38;5;231m\]\W\033[38;5;209m\]]\
# \n\033[97m\]└─> \[\033[38;5;209m\]$\[\033[97m\] '

#### CYBER THEME ####
# ╭─[vagrant@localhost ~]
# ╰─> $
PS1='\n\[\033[38;5;208m\]╭─[\[\033[1;36m\]\u\[\033[0m\]@\[\033[1;35m\]\h\[\033[0m\] \[\033[1;32m\]\W\[\033[0m\]]\n\[\033[38;5;208m\]╰─> \[\033[38;5;228m\]$\[\033[0m\] '

#### Tech Minimalist ####
# PS1='\[\033[38;5;45m\]⟦\d \t \[\033[1;35m\]\u@\h\[\033[38;5;45m\]⟧\n\[\033[38;5;228m\]⟜ \w \n\[\033[38;5;15m\]⟜>'

#### Modern Blocky ####
# PS1='\n\[\033[1;33m\]┌─[\[\033[1;34m\]\d \t\[\033[1;33m\]] [\[\033[1;36m\]\u@\h\[\033[1;33m\]]\n└─[\[\033[1;37m\]\w\[\033[1;33m\]] $ \[\033[0m\]'

```


MyPrompts file
```bash
# Fancy Prompts
# -------------------------------------
# Color Codes:
# Black: \e[0;30m
# Red: \e[0;31m
# Green: \e[0;32m
# Yellow: \e[0;33m
# Blue: \e[0;34m
# Magenta: \e[0;35m
# Cyan: \e[0;36m
# White: \e[0;37m
# -------------------------------------

# Simple User@Host Prompt
# Displays username, hostname, and current directory with basic colors.
# PS1='\[\e[0;32m\]\u@\h \[\e[0;33m\]\W\[\e[m\] \$ '

# User@Host with Exit Status
# Shows exit status of the last command as a check mark or cross.
# PS1='\[\e[0;32m\]\u@\h \[\e[0;33m\]\W\[\e[m\] \[\e[0;31m\]$(if [ $? -eq 0 ]; then echo ✔; else echo ✘; fi) \[\e[m\]$ '

# User@Host with Time and Path
# Displays username, hostname, time, and current directory in different colors.
# PS1='\[\e[1;36m\]\u@\h \[\e[0;33m\]\D{%T} \[\e[0;35m\]\w\[\e[m\] \$ '

# User@Host with Current Directory
# Displays username, hostname, and current directory in a simple format.
# PS1='\[\e[0;32m\]\u\[\e[m\]@\[\e[0;36m\]\h \[\e[0;32m\]\W\[\e[m\] \$ '

# Date and Time with User@Host and Current Directory
# Displays date, time, username, hostname, and current directory.
# PS1='\[\e[0;36m\]\D{%F %T}\[\e[m\] \[\e[0;32m\]\u@\[\e[0;36m\]\h \[\e[0;34m\]\w\[\e[m\]\n$ '

# User, Host, and Path with Git Branch
# Shows username, hostname, current directory, and current Git branch if in a Git repository.
# PS1='\[\e[0;32m\]\u@\h \[\e[0;34m\]\w\[\e[m\] \[\e[0;33m\]$(__git_ps1 " (%s)")\[\e[m\] \$ '

# User@Host with Time and Exit Status
# Displays username, hostname, time, and exit status of the last command.
# PS1='\[\e[1;35m\]\u@\h \[\e[0;33m\]\D{%T} \[\e[0;31m\]$(if [ $? -eq 0 ]; then echo ✔; else echo ✘; fi) \[\e[m\] \$ '

# User@Host with Short Path and Background Color
# Shows username, hostname, and short path with a background color.
# PS1='\[\e[0;37;44m\]\u@\h:\W\[\e[m\] \$ '

```