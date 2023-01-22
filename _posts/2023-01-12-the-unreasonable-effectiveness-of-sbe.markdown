---
layout: post
title:  "The Unreasonable Effectiveness of Simple Binary Encoding (SBE)"
date: 2023-01-12
tags: sbe "simple binary encoding"
---

![](/assets/img-lamppost.jpeg)

### Introduction
Simple Binary Encoding (SBE) is a codec format specified by the Financial 
Information eXchange (FIX) Trading Community for use in high-performance trading systems. 
It lives in Layer 6 (Presentation Layer) of the [OSI model][OSI model], and deals with how
trading messages between different systems are represented on the wire. 
Below, we'll see why it may make sense to leverage its compactness and performance in 
non-financial settings as well, provided its obscurity and some quirks are deemed tolerable for the
use-case.

### Why yet another codec?
For a lot of systems, passing around JSON data is perfectly suitable. It is self-describing, human-readable, and perhaps above all -- has the benefit of being easy to integrate with almost anywhere. 
It is the lingua franca of interprocess communication nowadays, and one would be hard pressed to find a 
language or a library that doesn't support it.

In some respects though, JSON is not as efficient as one would want a codec to be.

{% highlight json %}
{
    "students": [
        {
            "name": "First Last",
            ...
        },
        {
            "name": "First1 Last1"
        }
        ...
    ]
    ...
}
{% endhighlight %}

Notice in the above snippet how the key `name` is repeated for every student element in the
`students` array. If we already know the schema of the student model, there's no need 
to repeatedly have the `key=value` structure and, moreover, use that for over the wire 
transmission. Imagine how odd it'd be if we referenced the part of speech of each word 
we spoke -- something like
`Subject:I Verb:have Article:an Object:apple`.
The density of information we'd pass on to each other via spech would be so much smaller,  
and we would be wasting precious time and brain cycles speaking like that.

Instead, each language has some grammar (schema, in our case) that's learned ahead of time. And 
so when the time comes to decode some prose or speech, the receiver can infer the grammar by the 
arrangement of the different words. Of course, this leads to some ambiguity in natural languages
 like English -- which we should have no room for in computing. In similar vein, SBE schemas are shared off-channel and the data on the wire is much more compact because there's no `key=value` structure, 
 just a series of `value1|value2|...`. This leads to challenges of its own, such as:
 - How do we know where `value1` ends and `value2` begins?
 - What if there's a change in schema?
 and many others. 

 We'll address those concerns in the next installment of this post, stay tuned!







[OSI model]: [https://en.wikipedia.org/wiki/OSI_model]