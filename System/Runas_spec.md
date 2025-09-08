>[!Source]
>`man sudoers`

### **Runas_spec**
 A  Runas_Spec sets the default for the commands that follow it.  What this
means is that for the entry:

dgb     boulder = (operator) /bin/ls, /bin/kill, /usr/bin/lprm

The user dgb may run /bin/ls, /bin/kill, and  /usr/bin/lprm  on  the  host
boulder—but only as operator.  For example:

$ sudo -u operator /bin/ls
It  is also possible to override a Runas_Spec later on in an entry.  If we
modify the entry like so:

dgb     boulder = (operator) /bin/ls, (root) /bin/kill, /usr/bin/lprm

Then user dgb is now allowed to run /bin/ls as operator, but /bin/kill and
/usr/bin/lprm as root.

We can extend this to allow dgb to run /bin/ls with  either  the  user  or
group set to operator:

dgb     boulder = (operator : operator) /bin/ls, (root) /bin/kill,\
/usr/bin/lprm

While  the group portion of the Runas_Spec permits the user to run as com‐
mand with that group, it does not force the user to do so.  If no group is
specified on the command line, the command will run with the group  listed
in  the target user's password database entry.  The following would all be
permitted by the sudoers entry above:

$ sudo -u operator /bin/ls
$ sudo -u operator -g operator /bin/ls
$ sudo -g operator /bin/ls

In the following example, user tcm may run commands that  access  a  modem
device file with the dialer group.

tcm     boulder = (:dialer) /usr/bin/tip, /usr/bin/cu,\
/usr/local/bin/minicom

In this example only the group will be set, the command still runs as user
tcm.  For example:

$ sudo -g dialer /usr/bin/cu

Multiple  users  and  groups may be present in a Runas_Spec, in which case
the user may select any combination of users and groups via the -u and  -g
options.  In this example:

alan    ALL = (root, bin : operator, system) ALL

user  alan may run any command as either user root or bin, optionally set‐
ting the group to operator or system.

### **PASSWD and NOPASSWD**

By default, sudo requires that a user authenticate before running a com‐
mand.  This behavior can be modified  via  the  NOPASSWD  tag.   Like  a
Runas_Spec, the NOPASSWD tag sets a default for the commands that follow
it in the Cmnd_Spec_List.  Conversely, the PASSWD tag can be used to re‐
verse things.  For example:

ray     rushmore = NOPASSWD: /bin/kill, /bin/ls, /usr/bin/lprm

would allow the user ray to run /bin/kill, /bin/ls, and /usr/bin/lprm as
root  on  the  machine “rushmore” without authenticating himself.  If we
only want ray to be able to run /bin/kill without a password  the  entry
would be:

ray     rushmore = NOPASSWD: /bin/kill, PASSWD: /bin/ls, /usr/bin/lprm

### **Regular expressions**
Starting with version 1.9.10, it is possible to  use  regular  expressions
for  path  names and command line arguments.  Regular expressions are more
expressive than shell-style wildcards and are usually safer  because  they
provide  a  greater  degree of control when matching.  The type of regular
expressions supported by sudoers are POSIX extended  regular  expressions,
similar  to  those  used  by the egrep(1) utility.  They are usually docu‐
mented in the regex(7) or re_format(7) manual, depending  on  the  system.
As  an extension, if the regular expression begins with “(?i)”, it will be
matched in a case-insensitive manner.

In sudoers, regular expressions must start with a ‘^’  character  and  end
with  a ‘$’.  This makes it explicit what is, or is not, a regular expres‐
sion.  Either the path name, the command line arguments  or  both  may  be
regular expressions.  Because the path name and arguments are matched sep‐
arately,  it is even possible to use wildcards for the path name and regu‐
lar expressions for the arguments.  It is not possible  to  use  a  single
regular  expression  to match both the command and its arguments.  Regular
expressions in sudoers are limited to 1024 characters.

There is no need to escape sudoers special characters in a regular expres‐
sion other than the pound sign (‘#’).

In the following example, user john can run the passwd(1) command as  root
on  any  host  but is not allowed to change root's password.  This kind of
rule is impossible to express safely using wildcards.

john    ALL = /usr/bin/passwd ^[a-zA-Z0-9_]+$,\
			 !/usr/bin/passwd root

It is also possible to  use  a  regular  expression  in  conjunction  with
sudoedit  rules.   The  following  rule would give user bob the ability to
edit the /etc/motd, /etc/issue, and /etc/hosts files only.

bob    ALL = sudoedit ^/etc/(motd|issue|hosts)$

Regular expressions may also be used to match the command itself.  In this
example, a regular expression is  used  to  allow  user  sid  to  run  the
/usr/sbin/groupadd,         /usr/sbin/groupmod,        /usr/sbin/groupdel,
/usr/sbin/useradd, /usr/sbin/usermod, and  /usr/sbin/userdel  commands  as
root.

sid    ALL = ^/usr/sbin/(group|user)(add|mod|del)$

One  disadvantage  of using a regular expression to match the command name
is that it is not possible to match relative paths such  as  ./useradd  or
../sbin/useradd.  This has security implications when a regular expression
is  used  for  the command name in conjunction with the negation operator,
‘!’, as such rules can be trivially bypassed.  Because of  this,  using  a
negated  regular  expression for the command name is strongly discouraged.
This does not apply to negated commands that only use a regular expression
to match the command  arguments.   See  “Regular  expressions  in  command
names” below for more information.

### **EXAMPLES**
Below  are  example sudoers file entries.  Admittedly, some of these are a
bit contrived.  First, we allow a few environment variables  to  pass  and
then define our aliases:

```
# Run X applications through sudo; HOME is used to find the
# .Xauthority file.  Other programs use HOME to locate configuration
# files and this may lead to privilege escalation!
Defaults env_keep += "DISPLAY HOME"

# User alias specification
User_Alias      FULLTIMERS = millert, mikef, dowdy
User_Alias      PARTTIMERS = bostley, jwfox, crawl
User_Alias      WEBADMIN = will, wendy, wim

# Runas alias specification
Runas_Alias     OP = root, operator
Runas_Alias     DB = oracle, sybase
Runas_Alias     ADMINGRP = adm, oper

# Host alias specification
Host_Alias      SPARC = bigtime, eclipse, moet, anchor :\
			   SGI = grolsch, dandelion, black :\
			   ALPHA = widget, thalamus, foobar :\
			   HPPA = boa, nag, python
Host_Alias      CUNETS = 128.138.0.0/255.255.0.0
Host_Alias      CSNETS = 128.138.243.0, 128.138.204.0/24, 128.138.242.0
Host_Alias      SERVERS = primary, mail, www, ns
Host_Alias      CDROM = orion, perseus, hercules

# Cmnd alias specification
Cmnd_Alias      DUMPS = /usr/bin/mt, /usr/sbin/dump, /usr/sbin/rdump,\
					   /usr/sbin/restore, /usr/sbin/rrestore,\
					   sha224:0GomF8mNN3wlDt1HD9XldjJ3SNgpFdbjO1+NsQ== \
					   /home/operator/bin/start_backups
Cmnd_Alias      KILL = /usr/bin/kill
Cmnd_Alias      PRINTING = /usr/sbin/lpc, /usr/bin/lprm
Cmnd_Alias      SHUTDOWN = /usr/sbin/shutdown
Cmnd_Alias      HALT = /usr/sbin/halt
Cmnd_Alias      REBOOT = /usr/sbin/reboot
Cmnd_Alias      SHELLS = /usr/bin/sh, /usr/bin/csh, /usr/bin/ksh,\
						/usr/local/bin/tcsh, /usr/bin/rsh,\
						/usr/local/bin/zsh
Cmnd_Alias      SU = /usr/bin/su
Cmnd_Alias      PAGERS = /usr/bin/more, /usr/bin/pg, /usr/bin/less

Here  we override some of the compiled in default values.  We want sudo to
log via syslog(3) using the auth facility in all cases and for commands to
be run with the target user's home directory as the working directory.  We
don't want to subject the full time staff to the sudo lecture and we  want
to  allow them to run commands in a chroot(2) “sandbox” via the -R option.
User millert need not provide a password and we don't want  to  reset  the
LOGNAME  or USER environment variables when running commands as root.  Ad‐
ditionally, on the machines in the SERVERS Host_Alias, we  keep  an  addi‐
tional local log file and make sure we log the year in each log line since
the log entries will be kept around for several years.  Lastly, we disable
shell  escapes  for  the commands in the PAGERS Cmnd_Alias (/usr/bin/more,
/usr/bin/pg and /usr/bin/less).  This will not effectively constrain users
with sudo ALL privileges.

# Override built-in defaults
Defaults                syslog=auth,runcwd=~
Defaults>root           !set_logname
Defaults:FULLTIMERS     !lecture,runchroot=*
Defaults:millert        !authenticate
Defaults@SERVERS        log_year, logfile=/var/log/sudo.log
Defaults!PAGERS         noexec

The User specification is the part that actually determines  who  may  run
what.

root            ALL = (ALL) ALL
%wheel          ALL = (ALL) ALL

We let root and any user in group wheel run any command on any host as any
user.

FULLTIMERS      ALL = NOPASSWD: ALL

Full time sysadmins (millert, mikef, and dowdy) may run any command on any
host without authenticating themselves.

PARTTIMERS      ALL = ALL

Part  time sysadmins bostley, jwfox, and crawl) may run any command on any
host but they must authenticate themselves first (since  the  entry  lacks
the NOPASSWD tag).

jack            CSNETS = ALL

The user jack may run any command on the machines in the CSNETS alias (the
networks  128.138.243.0, 128.138.204.0, and 128.138.242.0).  Of those net‐
works, only 128.138.204.0 has an explicit netmask (in CIDR notation) indi‐
cating it is a class C network.  For the other networks in CSNETS, the lo‐
cal machine's netmask will be used during matching.


lisa            CUNETS = ALL

The user lisa may run any command on any host in  the  CUNETS  alias  (the
class B network 128.138.0.0).

operator        ALL = DUMPS, KILL, SHUTDOWN, HALT, REBOOT, PRINTING,\
			   sudoedit /etc/printcap, /usr/oper/bin/

The  operator  user may run commands limited to simple maintenance.  Here,
those are commands related to backups,  killing  processes,  the  printing
system,  shutting  down  the  system,  and  any  commands in the directory
/usr/oper/bin/.  One command in the DUMPS Cmnd_Alias includes a sha224 di‐
gest, /home/operator/bin/start_backups.  This  is  because  the  directory
containing  the script is writable by the operator user.  If the script is
modified (resulting in a digest mismatch) it will no longer be possible to
run it via sudo.

joe             ALL = /usr/bin/su operator

The user joe may only su(1) to operator.

pete            HPPA = /usr/bin/passwd [A-Za-z]*, !/usr/bin/passwd *root*

%opers          ALL = (: ADMINGRP) /usr/sbin/

Users in the opers group may run commands in /usr/sbin/ as themselves with
any group in the ADMINGRP Runas_Alias (the adm and oper groups).

The user pete is allowed to change anyone's password except  for  root  on
the  HPPA  machines.  Because command line arguments are matched as a sin‐
gle, concatenated string, the ‘*’  wildcard  will  match  multiple  words.
This  example  assumes that passwd(1) does not take multiple user names on
the command line.  On systems with GNU getopt(3), options to passwd(1) may
be specified after the user argument.  As a result, this  rule  will  also
allow:

passwd username --expire

which may not be desirable.

bob             SPARC = (OP) ALL : SGI = (OP) ALL

The  user  bob  may run anything on the SPARC and SGI machines as any user
listed in the OP Runas_Alias (root and operator.)

jim             +biglab = ALL

The user jim may run any command on machines in the biglab netgroup.  sudo
knows that “biglab” is a netgroup due to the ‘+’ prefix.

+secretaries    ALL = PRINTING, /usr/bin/adduser, /usr/bin/rmuser

Users in the secretaries netgroup need to help manage the printers as well
as add and remove users, so they are allowed to run those commands on  all
machines.

fred            ALL = (DB) NOPASSWD: ALL

The  user  fred can run commands as any user in the DB Runas_Alias (oracle
or sybase) without giving a password.

john            ALPHA = /usr/bin/su [!-]*, !/usr/bin/su *root*

On the ALPHA machines, user john may su to anyone except root  but  he  is
not allowed to specify any options to the su(1) command.

jen             ALL, !SERVERS = ALL

The  user  jen  may run any command on any machine except for those in the
SERVERS Host_Alias (primary, mail, www, and ns).

jill            SERVERS = /usr/bin/, !SU, !SHELLS

For any machine in the SERVERS Host_Alias, jill may run  any  commands  in
the  directory /usr/bin/ except for those commands belonging to the SU and
SHELLS Cmnd_Aliases.  While not specifically mentioned in  the  rule,  the
commands  in  the  PAGERS  Cmnd_Alias  all reside in /usr/bin and have the
noexec option set.

steve           CSNETS = (operator) /usr/local/op_commands/

The user steve may run any command  in  the  directory  /usr/local/op_com‐
mands/ but only as user operator.

matt            valkyrie = KILL

On  his personal workstation, valkyrie, matt needs to be able to kill hung
processes.

WEBADMIN        www = (www) ALL, (root) /usr/bin/su www

On the host www, any user in the WEBADMIN  User_Alias  (will,  wendy,  and
wim), may run any command as user www (which owns the web pages) or simply
su(1) to www.

ALL             CDROM = NOPASSWD: /sbin/umount /CDROM,\
			   /sbin/mount -o nosuid\,nodev /dev/cd0a /CDROM

Any  user  may  mount  or  unmount  a  CD-ROM on the machines in the CDROM
Host_Alias (orion, perseus, hercules) without entering a  password.   This
is  a bit tedious for users to type, so it is a prime candidate for encap‐
sulating in a shell script.

```

