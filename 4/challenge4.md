# Challenge 4

Downloaded the challenge binary from [here](flareon2016challenge.dll).

## Start

### Overview

The binary provided is a `.dll`. It appears that this challenge has to do with dynamic libraries.

### Begin

Throwing the binary into IDA shows a number of user-defined functions with the name  starting with `flareon2016challenge`.

I'll provide a basic Python script for you to begin exploring the challenge!

```
from ctypes import *

chal = cdll.LoadLibrary('flareon2016challenge.dll')
```

This script allows you to import the dll in python, you can then call the exported functions based on the exported entry for the function.

There are 51 exported functions in total.

**[Activity]** Explore and figure out what to do with the 51 functions. :)  
***Hint: There is some order in which you have to call the functions in***

