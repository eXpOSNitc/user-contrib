## Python Script to compile all SPL files in one go saving time

### What it does.

Having to compile all the kernel spl modules after each change can be a lot time consuming to do by hand. This script basically compiles all the spl files in one go.

### How to use.

Python3 is already pre-installed on many linux distros, if not install it.

Put the `compile.py` script in `myexpos/spl` folder. 

Run `python3 compile.py` or `./compile.py` from `myexpos/spl` folder .

**Note** : This script only compiles SPL programs which are in the `myexpos/spl/spl_progs` directory and immediate subdirectories.