Below is a list of exit codes and explanations for each code.

to see the exit code you can activate `./gameserver dev-debug`

# Pass
* **Code:** 0
* **Description:** This code is returned when all is well.
* **On Screen:** [ OK ]
* **Logfile:** PASS

# Fatal
* **Code:** 1
* **Description:** Fatal errors occur when LGSM is prevented from completing its task. e.g it was unable to start a server.
* **On Screen:** [ FAIL ]
* **Logfile:** FATAL

# Error
* **Code:** 2
* **Description:** An error occurs when LGSM can complete its task however something went wrong. In many cases LGSM will attempt to resolve errors itself.
* **On Screen:** [ ERROR ]
* **Logfile:** ERROR

# Warning
* **Code:** 3
* **Description:** Warnings happen when there is somthing mis-configured or not setup correctly. LGSM may still work but not do as expected.
* **On Screen:** [ WARN ]
* **Logfile:** WARN

# Info
* **Code:** N/A
* **Description:** Useful information about what LGSM is currently doing.
* **On Screen:** [ INFO ]
* **Logfile:** INFO

# For Developers

An exit code is generated when you specify a logfile message _e.g fn_script_log_fatal_.
When you want the script to exit you must use core_exit.sh rather than just the exit command. core_exit.sh will then handle the exit. Each time you have a new variable for writing to the log file the code will change to that code. For example if LGSM experiences and error with code 2 then resolves the issue and passes the final code will be 0.

Examples
--------

    fn_script_log_fatal "RCON password is not set"
    core_exit.sh

This will exit with code 1

    fn_script_log_error "RCON password is not set"
    core_exit.sh

This will exit with code 2

    fn_script_log_error "SteamCMD is missing"
    LGSM installs SteamCMD
    fn_script_log_pass "SteamCMD has been installed"
    core_exit.sh

This will exit with code 0