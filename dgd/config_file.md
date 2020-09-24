---
title: DGD Configuration File
---

The first thing you'll want to specify in the configuration file is the "directory" entry.

Note that for DGD versions before August of 2020 you will ***always*** have to specify the full, absolute path to the relevant directory for any new DGD installation, including a simple "git clone", before your application will run. Later DGD versions using an absolute path for "directory" have the same requirement.

## Directory

DGD versions from September 2020 or later permit using a relative directory entry - for instance, if your DGD root is called "root" under the main directory, you could just say 'directory = "root";'.

Earlier DGD versions require you to specify an absolute path starting with "/" to the specific installed directory for DGD.

## Other Configuration

telnet_port (mapping)
: A mapping containing host:port pairs, where the host
        or    string is a name, an IP number or "\*", and the port
        number  number is a port on which to accept telnet connections.
        Alternatively, a telnet port number.

binary_port (mapping)
: A mapping containing host:port pairs, where the host
        or    string is a name, an IP number or "\*", and the port
        number  number is a port on which to accept raw TCP/IP
        connections.  Alternatively, a binary port number.

datagram_port (mapping)
: A mapping containing host:port pairs, where the host
        or    string is a name, an IP number or "\*", and the port
        number  number is a port on which to accept datagram
        connections.  Alternatively, a datagram port number. (optional)

directory (string)
: The base directory for the system.

modules (mapping)
: A mapping containing module:config pairs, where the 
        module string is the path of a runtime extension
        module, and the config string is used to initialize it.
        (optional)

users (number)
: The maximum number of active telnet and binary connections.

datagram_users (number)
: The maximum number of active datagram connections. (optional)

editors (number)
: The maximum number of simultaneously active editor instances.

ed_tmpfile (string)
: The proto editor temporary file (actual files will have a number appended).

swap_file (string)
: The name of the swap file.

swap_size (number)
: The total number of sectors in the swap file.

cache_size (number)
: The number of sectors in the swap cache in memory.

sector_size (number)
: The size of a swap sector in bytes.

swap_fragment (number)
: The fragment of all objects to swap out at the end of
        each task (e.g. with a swap_fragment of 32, 1/32th
        of all objects will be swapped out).

static_chunk (number) and dynamic_chunk (number)
: The size in bytes of a static or dynamic chunk of memory.
        Memory is divided into static memory
        and dynamic memory; static memory is never freed.
        Both are allocated in chunks of the specified size.
        Setting the size of the static chunk to 0 will
        cause the system never to swap out everything to
        make more room for static memory, but will also
        increase fragmentation.

dump_file (string)
: The name of the snapshot file.

dump_interval (number)
: The expected interval between snapshots, in seconds.
        Effectively, the time during which the swapfile will be
        fully recreated.

hotboot (string\*)
: Program, with arguments, to execute during hotboot. (optional)

typechecking (number)
: If zero, only functions with a declared type are typechecked.
        If one, all LPC functions are typechecked.
        If two, additionally, nil (the value of an uninitialized
        string, object, array or mapping variable) is a value
        distinct from integer 0.

include_file (string)
: The standard include file, which is always
        included automatically for each compiled object
        (relative to the base directory).

include_dirs (string\*)
: The standard system include directories (relative
        to the base directory).  In the first of those,
        the include files which are automatically
        generated on startup will be placed.

auto_object (string)
: The file name of the auto object (relative to the base directory).

driver_object (string)
: The file name of the driver object (relative to the base directory).

create (string)
: The name of the create function.

array_size (int)
: The maximum array and mapping size.

objects (int)
: The maximum number of objects.

call_outs (int)
: The maximum number of simultaneously active callouts.
