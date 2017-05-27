In order to make LinuxGSM as coherent as possible, we adopted some code conventions to follow.  
Here are some of them.


# Variables

## Naming variables

Variables should be made of lowercase letters only.

## Defining variables

Any variable should be defined through double quotes

````bash
var="value"
````

## Calling variables

Variable should always be called between brackets and double quotes to prevent globbing and word splitting.

````bash
echo "${var}"
````

## Directories

Directories are called using LinuxGSM directories variables, or relative to those.

Examples:

````bash
cp "config.cfg" "${servercfgfullpath}"
find "${executabledir}/bin"
````

# Conditional checks

## Syntax

- The `if [ statement ]; then` should be a one-liner operation.
- Signs comparators like ==; <; <=; etc. are prefered to -eq -le -lt.
- Anything within an if statement must be tabulated one step deeper.

Example:

````bash
if [ "${test}" == "${var}" ]; then
	mycheck="true"
fi
````

## Checks to avoid

### `! -z`and `! -n`

A `-z` check returns true if a variable is not defined.  
A `-n` check returns true if a variable is defined.

For that matter, you should use `-n` rather than `! -z` and use `-z` rather than `! -n`.

# Loops

- Loops should be a one liner statement.
- Anything withing a loop must be tabulated one step deeper.

````bash
while [ "${var}" < "${cap}" ]; do
	echo "This is tabulated"
	let var=var+1
done
````

# Functions

- Function should be named starting with `fn_` and using lowercase letters only.
- Any recurrent task should be put into a function.
- Anything within a function must be tabulated one step deeper.

Example:
````bash
fn_myfunction(){
	echo "This is tabulated"
}
````

# Messages

- Messages should be given using core_messages.sh forms
- Additional information messages are given in the form of echo " * Message here"