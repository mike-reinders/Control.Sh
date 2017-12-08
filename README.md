# Control.Sh
Application-Holding &amp; -Management Shell-File

# Description

Control.sh provides to start, stop and restart your application whith only one simple command line for Linux Systems.

# Installation & Usage

## Installation

Download: [control.sh](control.sh)

1. Copy control.sh into your folder, where your managed application executable is stored in.  
2. Execute `apt-get update; apt-get install screen` in your putty/console.  
3. Configure your control.sh

## Usage

1. First go into your folder with `cd /my/folder/`  
2. Execute `./control.sh help` to get all available commands.

Commands:  
`./control.sh start` *Starts the managed application*  
`./control.sh stop` *Stops the managed application*  
`./control.sh restart` *Restarts the managed application*  
`./control.sh status` *Shows running status of the managed application*  
`./control.sh console` *Gets you into the console of the managed application*

**Note:**  
When you use `./control.sh console` and you want to get out, you only can leave the screen by using **CTRL + A + D**.
Use it multiple times if it doesnt work!
if you use **CTRL + C** it **KILLS** the managed application and **ALL data is lost**

## Quick Configuration-Steps

Change following lines/variables:
```
33: SCREEN_NAME="ApplicationScreenName" # the screen name; only change it if you use multiple applications using `screen`
34: EXECUTION_FILE="startfile -parameter1 -parameter2" # your filename and parameters
35: EXECUTING_USER="root" # which user do you want to run the application
```

# Configuration

There are two types of configuration:  
- `>>> NOVICE-SETUP <<<` &nbsp; &nbsp; *for simple configurations (contains 8 variables)*  
- `>>> ADVANCED-SETUP <<<` &nbsp; &nbsp; *for advanced configurations (contains 2 variables, 1 function)*

## Simple Configuration

**Variable:** `APPLICATION_NAME="Application-Server"` (line 33)  
 &nbsp; &nbsp; **Function:**  
 &nbsp; &nbsp; &nbsp; Specifies the name of the managed application.

**Variable:** `SCREEN_NAME="ApplicationScreenName"` (line 34)  
 &nbsp; &nbsp; **Function:**  
 &nbsp; &nbsp; &nbsp; Specifies the Screen-Name which is used to identify the managed application.  
 &nbsp; &nbsp; **Variable Restrictions:**  
 &nbsp; &nbsp; &nbsp; Regular Expression: Every Character except Whitespaces, Dots and no lead with `K_`

**Variable:** `EXECUTION_FILE="startfile -parameter1 -parameter2"` (line 35)  
 &nbsp; &nbsp; **Function:**  
 &nbsp; &nbsp; &nbsp; Declares the start file and its needed parameters.

**Variable:** `EXECUTING_USER="root"` (line 36)  
 &nbsp; &nbsp; **Function:**  
 &nbsp; &nbsp; &nbsp; Declares the user which is used to run the managed application/(keeper)script  
 &nbsp; &nbsp; **Note:**  
 &nbsp; &nbsp; &nbsp; if the user to be executed is not root and not the given user in this variable,  
 &nbsp; &nbsp; &nbsp; you will get an error on execution.

**Variable:** `SCREEN_KEEPER=false` (line 38)  
 &nbsp; &nbsp; **Function:**  
 &nbsp; &nbsp; &nbsp; Indicates whether the screen-keeper will be started on `./control.sh start`  
 &nbsp; &nbsp; **Note:**  
 &nbsp; &nbsp; &nbsp; The keeper restarts your application when it closed.

**Variable:** `MIN_ELAPSED_TIME=30` (line 39)  
 &nbsp; &nbsp; **Function:**  
 &nbsp; &nbsp; &nbsp; Specifies how much seconds has to be elapsed between start (incl. restart) and close,  
 &nbsp; &nbsp; &nbsp; before the start-event of the application is considered as failed.

**Variable:** `MAXCOUNT_TIME_EXCEEDED=3` (line 40)  
 &nbsp; &nbsp; **Function:**  
 &nbsp; &nbsp; &nbsp; Specifies how much times the keeper will restart your managed application after failed start-events.

**Variable:** `RESTART_DELAY=0` (line 41)  
 &nbsp; &nbsp; **Function:**  
 &nbsp; &nbsp; &nbsp; Specifies the restart-delay  
 &nbsp; &nbsp; &nbsp; (how much seconds the keeper waits until it restarts your managed application)

## Advanced Configuration

**Variable:** `NOT_RECOMMEND_FORCE_RUN=false` (line 45)  
 &nbsp; &nbsp; **Function:**  
 &nbsp; &nbsp; &nbsp; Indicates whether the script deactivates the distribution-check.

**Variable:** `ENABLE_USERDEFINED_STOP=false` (line 47)  
 &nbsp; &nbsp; **Function:**  
 &nbsp; &nbsp; &nbsp; Indicates whether the script executes the function userdefined_stop() when `./control.sh stop` is beeing executed.

**Function:** `function userdefined_stop() {` (line 48)  
 &nbsp; &nbsp; **Function:**  
 &nbsp; &nbsp; &nbsp; Contains the code, that gets executed when `./control.sh stop` is beeing executed.    &nbsp; &nbsp;
 &nbsp; &nbsp; **Default Function:**  
 &nbsp; &nbsp; &nbsp; Command `save-all` and `stop` will be sent via STD:IN-Pipe with 1 seconds delay after each command.
 &nbsp; &nbsp; **Note:**  
 &nbsp; &nbsp; &nbsp; This method will be executed before the script tries to terminate the process or tries to killing it.  
 &nbsp; &nbsp; &nbsp; The managed application got 10 seconds before step 2 (termination) and additional 10 seconds before step 3 (killing)  
 &nbsp; &nbsp; &nbsp; gets executed.



