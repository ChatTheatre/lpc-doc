# DGD and LPC

[Dworkin's Game Driver](https://dworkin.nl/dgd) is a powerful interpreted language primarily aimed at running persistent, state-heavy applications attached to network sockets. It was originally a from-scratch reimplementation of [LPMUD](https://en.wikipedia.org/wiki/LPMud), but it has diverged significantly over time. The language of DGD's VM is called LPC, after the original LPMud language. DGD runs a fairly distinctive dialect, which might reasonably be referred to as "DGD LPC."

These pages are meant as an introduction to DGD and its LPC language, and a set of resources to learn them.

DGD forms the lower layers of [Skotos](https://skotos.net) and [ChatTheatre](https://chattheatre.com), and has done so for a number of [MUDs](https://en.wikipedia.org/wiki/MUD), at least one BitCoin exchange, and a few other assorted services.

DGD has [some unusual characteristics](dgd/unusual.md) that can be very powerful for the right application.

It also has a [long and storied history](dgd/history.md).

Here's [how to install DGD](dgd/installing.md).

## ChatTheatre Resources

This is one of several documentation sites courtesy of [ChatTheatre](https://chattheatre.com), which aims to make DGD more straightforward to install and use.

* [Kernellib Documentation](https://ChatTheatre.github.io/kernellib-doc)
* [SkotOS Documentation](https://ChatTheatre.github.io/SkotOS-Doc)
* [eOS Documentation](https://ChatTheatre.github.io/eOS-Doc)

## DGD Resources

For many years, the Phantasmal DGD documentation site was the preferred resource for DGD documentation. You can find [the most recent versions of its source files on GitHub](https://github.com/shentino/phantasmal/tree/master/website/DGD), and ChatTheatre is attempting to adapt its most useful parts to something modern.

The most comprehensive resource on DGD remains the [DGD email list archive](https://mail.dworkin.nl/pipermail/dgd/). The list operated from August of 1997 until July of 2019. It isn't easy to sort through, but the amount of raw DGD content is unrivalled.

## Non-DGD LPC Resources

There is a well-known but very outdated LPC book, titled simply ["Intermediate LPC."](https://www.mars.org/home/rob/docs/IntermediateLPC/chapter1.html) It's not DGD-specific, but you may still find something useful there.

## Copyright & Status

Unless otherwise noted, the contents of this repository as declared public domain using the Creative Commons "No Rights Reserved" [CC0 Declaration](https://creativecommons.org/share-your-work/public-domain/cc0/).

Felix Croes ("dworkin") has declared his work in this repository to be in the public domain (reference: https://github.com/dworkin/lpc-doc/blob/master/LICENSE).

### CC0 Declarations

Under US law it is a bit more difficult to declare something public domain (see [article](https://www.techdirt.com/articles/20150123/15564629797/why-we-still-cant-really-put-anything-public-domain-why-that-needs-to-change.shtml)). Creative Commons offers a [CC0 tool](https://creativecommons.org/choose/zero/) that combined with GPG signed commits to this repository, helps with this issue.

The following parties have declared their contributions to this repository as public domain:

* Noah Gibbs

<p xmlns:dct="http://purl.org/dc/terms/" xmlns:vcard="http://www.w3.org/2001/vcard-rdf/3.0#">
  <a rel="license"
     href="http://creativecommons.org/publicdomain/zero/1.0/">
    <img src="http://i.creativecommons.org/p/zero/1.0/88x31.png" style="border-style: none;" alt="CC0" />
  </a>
  <br />
  To the extent possible under law,
  <a rel="dct:publisher"
     href="https://codefol.io">
    <span property="dct:title">Noah Gibbs</span></a>
  has waived all copyright and related or neighboring rights to
  <span property="dct:title">lpc-doc repository</span>.
This work is published from:
<span property="vcard:Country" datatype="dct:ISO3166"
      content="UK" about="https://github.com/ChatTheatre/lpc-doc">
  United Kingdom</span>.
</p>
