# Control.Sh
A shell script for running applications in foreground or background

# Description

Control.sh is used for running applications in foreground or background.  
Simply configure it within the Control.sh-file or within a control.cfg-file

# Installation & Usage

## Installation

Download or Clone: [control.sh](control.sh)

1. Download or Clone the Control.sh-file into your folder  
2. Execute `apt-get update; apt-get install screen sudo` in your putty/console/terminal.  
3. Configure your control.sh or create a control.cfg within the folder where your control.sh is located in

## Commands
`./control.sh start` *Starts the managed application*  
`./control.sh stop` *Stops the managed application*  
`./control.sh run` *Runs the managed application in foreground*  
`./control.sh restart` *Restarts the managed application*  
`./control.sh status` *Shows running status of the managed application*  
`./control.sh	last-exit-code`		*Returns and displays the last exit code*  
`./control.sh join`  *Joins the application and exits when waittime was reached or application stops*  
`./control.sh console` *Gets you into the console of the managed application*  
`./control.sh help`  *Displays help/all commands*

**Note:**  
When you use `./control.sh console` and you want to get out, you only can leave the screen by using **CTRL + A + D**.
Use it multiple times if it doesnt work!
if you use **CTRL + C** it **KILLS** the managed application **which might leads to data loss**

## Quick Configuration-Steps

Change following lines/variables:
```
42: SCREEN_NAME="ApplicationScreenName" # change it when using multiple applications under the same user
43: EXECUTION_FILE="startfile -parameter1 -parameter2" # your commandline
44: EXECUTING_USER="root" # under which user the commandline is executed
```

# Configuration

There are two types of configuration sections:  
- `>>> NOVICE-SETUP <<<` &nbsp; &nbsp; *for simple configurations (contains 10 variables)*  
- `>>> ADVANCED-SETUP <<<` &nbsp; &nbsp; *for advanced configurations (contains 2 variables, 1 function)*

## Simple Configuration

**APPLICATION_NAME** (Line 41)  
 &nbsp; Specifies the name of the managed application.
 &nbsp; **default:** "Application-Server"

**SCREEN_NAME** (Line 42)  
 &nbsp; Specifies the Screen-Name which is used to identify the managed application.  
 &nbsp; **Note:** Every Character except Whitespaces, Dots and no lead with `K_` are allowed.

**EXECUTION_FILE** (Line 43)  
 &nbsp; Specifies the command line your managed application shall run.  
 &nbsp; **default:** "startfile -parameter1 -parameter2"

**EXECUTING_USER** (Line 44)  
 &nbsp; Specifies the user under which the managed application and its' keeper is executed.  
 &nbsp; **Note:** The specified user must be root or the user you'r going to run control.sh with.

**SCREEN_KEEPER** (Line 46)  
 &nbsp; Specifies whether the screen-keeper will be started on `./control.sh start`  
 &nbsp; The keeper restarts your application on exit.  
 &nbsp; **default:** false

**MIN_ELAPSED_TIME** (Line 47)  
 &nbsp; Specifies the time in seconds which has to be elapsed between start and exit  
 &nbsp; of the managed application to consider the start as success.  
 &nbsp; **default:** 30

**MAXCOUNT_TIME_EXCEEDED** (Line 48)  
 &nbsp; Specifies how much times the keeper will restart your managed application after a failed start.  
 &nbsp; **default:** 3

**RESTART_DELAY** (Line 49)  
 &nbsp; Specifies the restart-delay the keeper waits until the managed application is restarted.  
 &nbsp; **default:** 0
 
 **RESTART_ONFAILURE_ONLY** (Line 50)  
 &nbsp; Specifies whether the screen keeper only restarts the managed application on non-zero exit code.  
 &nbsp; **default:** true

**CONFIG_FILE** (Line 52)  
 &nbsp; Specifies the Configuration-File  
 &nbsp; **default:** control.cfg

## Advanced Configuration

**NOT_RECOMMEND_FORCE_RUN** (Line 56)  
 &nbsp; Specifies whether the script does not run a distribution-check.  
 &nbsp; **defaukt:** false

**ENABLE_USERDEFINED_STOP** (Line 58)  
 &nbsp; Specifies whether the script executes the function userdefined_stop() instead of sending a unix SIGTERM signal  
 &nbsp; when stopping the managed application.  
 &nbsp; **default:** false

**function userdefined_stop()** (Line 59)  
 &nbsp; Contains the routine which is executed when stopping the managed application.  
 &nbsp; **Note:** After execution the managed application has got 10 seconds to terminate  
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; until the normal shutdown routine is beeing executed.



