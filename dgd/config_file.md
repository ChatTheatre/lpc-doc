---
title: DGD Configuration File
---

The first thing you'll want to specify in the configuration file is the "directory" entry.

Note that for DGD versions before August of 2020 you will ***always*** have to specify the full, absolute path to the relevant directory for any new DGD installation, including a simple "git clone", before your application will run. Later DGD versions using an absolute path for "directory" have the same requirement.

## Directory

DGD versions from September 2020 or later permit using a relative directory entry - for instance, if your DGD root is called "root" under the main directory, you could just say 'directory = "root";'.

Earlier DGD versions require you to specify an absolute path starting with "/" to the specific installed directory for DGD.

## Other configuration

The config file specified on the command line when dgd is invoked specifies some important parameters:

* objects, call\_outs, swap\_size, array\_size

Running out of objects or callouts, or making an array (or mapping) too big will cause a runtime error

Running out of swap will cause a fatal error, crash, and a core dump
