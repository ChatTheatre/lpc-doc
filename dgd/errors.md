---
title: Error Handling in DGD
---

## Exception handling

Errors can happen either by explicit request with the error kfun, or from DGD itself if things go wrong

Errors cause the LPC call stack to unwind until the error is either caught or escapes the top call on the stack, at which point the task/event is terminated.

An error that escapes an atomic function call will cause that call to be rolled back.  Atomic function calls can be nested if desired and each atomic layer will be rolled back separately as the error goes up the stack.

Attempting to catch an "out of ticks" error will fail if the context where it is caught also is out of ticks.

## Fatal errors

Some conditions are fatal in DGD

* running out of memory, detected when malloc fails
* running out of stack, and thusly causing the OS to raise a segmentation fault
* running out of sectors in the swap file
* DGD attempting to call a function that does not exist in the driver object

All fatal errors cause dgd to abort and probably dump core, and cannot be caught by LPC exception handlers
