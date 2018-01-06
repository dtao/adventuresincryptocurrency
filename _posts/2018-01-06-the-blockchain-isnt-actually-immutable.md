---
layout: post
title:  The blockchain isn't actually immutable
date:   2018-01-06 10:29:00 -0600
---
I found a great book that's available online called [Mastering Bitcoin][mastering-bitcoin]. It looks like it was written in 2015, so I'm sure the information isn't 100% accurate anymore; but even after reading one chapter I feel it's a valuable source of information about some of the technical details of Bitcoin.

I started with [the chapter on the blockchain][the-blockchain] and found this part both surprising and enlightening:

> One way to think about the blockchain is like layers in a geological formation, or glacier core sample. The surface layers might change with the seasons, or even be blown away before they have time to settle. But once you go a few inches deep, geological layers become more and more stable.

Prior to reading this chapter I had been under the impression that the blockchain is deeply immutable in the traditional sense, meaning once data is added to the structure it can't be changed. (Actually, *true* immutability would mean you can't write data to the structure at all, only create new structures that share most of the data. For a distributed ledger this probably isn't very feasible.)

In fact, the design of the blockchain allows for mutation, but the longer the chain gets the more computationally expensive it becomes to modify old blocks. This is because the identifier for every block embeds the identifier of its parent, which is a value derived from the contents of the block (surprise: it's a hash!); so making any modification to a block requires not only recalculating the block's identifier, but recalculating the identifiers for all of its descendents as well.

I have to say, it's quite a clever design.

Next I think I'll read about [transactions][transactions].

[mastering-bitcoin]: http://chimera.labs.oreilly.com/books/1234000001802
[the-blockchain]: http://chimera.labs.oreilly.com/books/1234000001802/ch07.html
[transactions]: http://chimera.labs.oreilly.com/books/1234000001802/ch05.html
