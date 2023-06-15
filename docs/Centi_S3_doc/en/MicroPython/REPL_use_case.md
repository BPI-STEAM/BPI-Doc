## REPL Use Case

### REPL shortcut keys

1. Copy `ctrl + shift + c`.
2. Paste `ctrl + shift + v`.
    Use the left mouse button to drag and select the command to be copied in the REPL, press the copy shortcut key on the keyboard, and then press the paste shortcut key to copy and paste the command.
3. Soft reset `ctrl + d`.
4. Interrupt `ctrl + c`, interrupt the currently executing program, but will not restart and reset.

### View built-in modules

1. Entering `help("modules")` in the REPL will list all modules in the current CircuitPython development board.
2. After importing the module, you can use the `help()` function to view the function names or variable names available inside the module. 
```py
import machine
help(machine)
```