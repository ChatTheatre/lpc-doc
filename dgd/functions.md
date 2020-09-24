---
title: Functions in DGD
---

There are three kinds of functions in DGD

* kfuns
* afuns
* normal funs

A kfun is a function provided by DGD itself.

An afun is a function defined by the auto object, and can mask a kfun.  Such masking is often done for security reasons and the kernel library's auto object provides a good demonstration of this concept.

Any object, clone or master, may have LPC functions defined by the source that was used to compile it.  Except for the initial cold boot for the driver and auto objects, any object can be compiled from literal source supplied to the compile_object kfun, but by default reads the source from the corresponding LPC source file.

DGD itself may call functions, called applies, which work like hooks.

Full documentation for DGD's applies can be found in the lpc-doc package.

Functions can have attributes:

* private - a private function can only be called inside the program it is defined in, is invisible to inheriting programs and external objects, and cannot be masked by an inheriting program
* static - a static function can only be called inside the object it is defined in, can be called by inheriting programs, and can be masked by an inheriting program.  it is invisible to external objects
* nomask - a nomask function cannot be masked and an attempt to do so causes a compile error
* atomic - an atomic function is guaranteed to have no side effects if it is aborted due to an error.  There are some things that are therefore not allowed inside an atomic function call

Technically, all calls to external objects from LPC are done by invoking the call\_other kfun.  Overriding this in the auto object will cause performance penalties, but may be useful.  By default, attempting to call a nonexistent (and possibly invisible due to being static or private) function in any object returns nil.  Kotaka overrides call\_other to raise a runtime error if an attempt is made to call a non-existent function.

A callout is a delayed self-call, that must be directed at a static function in the object by invoking the call\_out kfun.
