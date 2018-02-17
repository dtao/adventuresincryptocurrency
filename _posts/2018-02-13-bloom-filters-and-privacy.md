---
layout: post
title:  Bloom filters and privacy
date:   2018-02-13 22:38:00 -0600
---
Well, I started reading about the bitcoin network and along the way learned how [bloom filters work][bloom-filters]! That was kind of fun.

Actually, I started writing this over a week ago; but it was late, and I got tired, so I stopped. So this will be a good exercise: let's see if I can actually remember how they work without consulting the textbook. They aren't that complicated, so I suspect I'll be fine.

First I should explain the *purpose* of a bloom filter. It's a data structure, but it differs from most conventional data structures in that it doesn't actually store the values fed to it. It is a probabilistic structure that can tell you if a value is *possibly* in a set or *definitely not* in the set. Hence the name: it's meant as a filter. It can't replace something that actually stores the values, but it can serve as a layer in front of the real data that efficiently handles a potentially large percentage of accesses, i.e. if a significant percentage of access attempts are for values not in the set.

So that's the generic scenario where you'd want a bloom filter. Now I'll try to describe how they work.

The basic players:

- A fixed size bit array (probably quite a large one, though as with any data structure it just depends on how many values you want to store)
- A set of hash functions (again, probably quite a few, depending on your needs)

To "add" a value to a bloom filter, you run it through each hash function, which should return an integer between 0 and the length of the array, and set the corresponding bit to 1. If you have 5 hash functions that means you set 5 bits to 1 (if a bit is already set to 1, leave it alone). To look up a value, you run it through each hash function and *check* the corresponding bit. If you encounter any 0s, it means the value is definitely not in the set. If you encounter all 1s, it means the value *could* be in the set.

The probability of the positive signal depends on the size of the array, the number of hash functions, and the number of values already added. The bigger the array and the more hash functions you use, the stronger the positive signal ("possibly" = "probably"). The more values already added, the weaker the signal because the array becomes saturated with 1s.

If I recall (okay, I cheated and revisited the text very briefly just now), bloom filters are used in the Bitcoin network by "SPV" nodes--simplified payment verification nodes, which do not store the entire blockchain, typically integrated into wallet apps--to represent patterns of transactions being looked up from full nodes on the network. Interestingly (to me, anyway), the application in this case is to promote privacy. Since an SPV node only requests a *pattern*, it can be difficult to discern which precise transactions it's interested in, which could give away the addresses in the user's wallet.

I've already expressed skepticism that the Bitcoin network provides as much privacy as its proponents like to think, not for technical reasons but for sociological ones, such as the fact that the average participant does not understand bloom filters and relies on something much more basic--trust in an organization, such as an exchange or financial institution--to protect them. That is not something you can solve with clever technical solutions. In fact the more clever the solution, paradoxically the more people are going to rely on trust in those who claim to understand the solution rather than the solution itself.

But I [already made that point][paradox].

[bloom-filters]: https://github.com/bitcoinbook/bitcoinbook/blob/a6a9f92/ch08.asciidoc#bloom-filters
[paradox]: {{'/2018/01/22/systems-that-require-sophisticated-users.html'|relative_url}}
