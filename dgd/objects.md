---
title: Objects in DGD
---

This article is a stub.

## Objects and Memory Management

DGD's memory management is heavily based around objects. Each object (not array, LWO, etc.) has a memory arena of its own. At the end of a task (aka timeslice) any references to data from other objects will be copied for the object referencing it. In other words, an array passed to another object must either be discarded by that object, or it will be copied by the object at the end of the current task/timeslice.

## Object Creation

Objects are created by:

* compilation, which creates a master object
* cloning a master object

The driver and auto objects are automatically compiled by DGD on cold boot.

Objects can inherit other objects during compilation.

All objects implicitly inherit the auto object that is in service when the object is compiled.

Henceforth, the word "program" is used to refer to a particular master object.  This may refer to a given object's master, or one of its inherits any distance up the inheritance tree.  An inherited program functions the same way in LPC as a base class does in C++.
