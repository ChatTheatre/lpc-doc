# DGD and LPC

[Dworkin's Game Driver](https://dworkin.nl/dgd) is a powerful interpreted language primarily aimed at running persistent, state-heavy applications attached to network sockets. It was originally a from-scratch reimplementation of [LPMUD](https://en.wikipedia.org/wiki/LPMud), but it has diverged significantly over time. The language of DGD's VM is called LPC, after the original LPMud language. DGD runs a fairly distinctive dialect, which might reasonably be referred to as "DGD LPC."

These pages are meant as an introduction to DGD and its LPC language, and a set of resources to learn them.

DGD forms the lower layers of [Skotos](https://skotos.net) and [ChatTheatre](https://chattheatre.com), and has done so for a number of [MUDs](https://en.wikipedia.org/wiki/MUD), at least one BitCoin exchange, and a few other assorted services.

DGD has [some unusual characteristics](dgd/unusual.md) that can be very powerful for the right application.

It also has a [long and storied history](dgd/history.md).

## Installing

Here's [how to install DGD](dgd/installing.md).

When running DGD, see also:

* [DGD's Configuration File](dgd/config_file.md)

## Using DGD

You may wish to use the [Kernellib](https://ChatTheatre.github.io/kernellib-doc) when writing a new DGD application and your existing applications may use it, as SkotOS and eOS do.

* [Error handling in DGD](dgd/errors.md)
* [Objects in DGD](dgd/objects.md)
* [Functions in DGD](dgd/functions.md)

* [DGD API Documentation for Auto and Driver objects](dgd/api_docs.md)
* [DGD's built-in editor reference](dgd/editor.md)
* [DGD's parse_string function for building grammars](dgd/parser.md)
* [DGD Kernel Functions (kfuns)](dgd/kfuns.md)

## ChatTheatre Resources

This is one of several documentation sites courtesy of [ChatTheatre](https://chattheatre.com), which aims to make DGD more straightforward to install and use.

* [Kernellib Documentation](https://ChatTheatre.github.io/kernellib-doc)
* [SkotOS Documentation](https://ChatTheatre.github.io/SkotOS-Doc)
* [eOS Documentation](https://ChatTheatre.github.io/eOS-Doc)

## DGD Resources

* The [LPC Reference Manual](./LPC.html) from DGD - very incomplete

* For many years, the Phantasmal DGD documentation site was the preferred resource for DGD documentation. You can find [the most recent versions of its source files on GitHub](https://github.com/shentino/phantasmal/tree/master/website/DGD), and ChatTheatre is attempting to adapt its most useful parts to something modern.

* The most comprehensive resource on DGD remains the [DGD email list archive](https://mail.dworkin.nl/pipermail/dgd/). The list operated from August of 1997 until July of 2019. It isn't easy to sort through, but the amount of raw DGD content is unrivalled.

## Non-DGD LPC Resources

* There is a well-known but very outdated LPC book, titled simply ["Intermediate LPC."](https://www.mars.org/home/rob/docs/IntermediateLPC/chapter1.html) It's not DGD-specific, but you may still find something useful there.
