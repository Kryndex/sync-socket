# SyncSocket

This Node.js module exposes a **no-dependency** class called `SyncSocket`, which acts as a synchronous interface to Node's `net.Socket` instance, which is normally only **a**synchronous.

This module exposes many of the same methods and properties a normal `net.Socket` has.

## Considerations

`SyncSocket` is slow. Not unusably slow, but you should have a good reason to want to use it. This was made for the rare case you need blocking read/writes in your Node.js application.

In addition, another one of my modules, [netlinkwrapper][netlinkwrapper] exposes a similar synchronous socket. However that module requires node-gyp to compile. `SyncSocket` does **not** require [node-gyp][node-gyp]. In fact, it has no dependencies.

## How Does it Work?

tl;dr: I abuse `child_process.execFileSync`.

I've done some pretty thorough research into how Node's `net.Socket` module works, and you can't make it synchronous without rewriting it in C++ via [node-gyp][node-gyp], or using some modules like [fibers][fibers] that in turn would depend on node-gyp anyways.

## Benchmarks

I've ran some tests, and `SyncSocket` is about twice as slow in doing read/writes than my competing module [netlinkwrapper][netlinkwrapper]. So if node-gyp is not an issue to you, use that instead. Or really just use `net.Socket`.

[netlinkwrapper]: https://github.com/JacobFischer/netlinkwrapper
[node-gyp]: https://github.com/nodejs/node-gyp
[fibers]: https://github.com/laverdet/node-fibers
