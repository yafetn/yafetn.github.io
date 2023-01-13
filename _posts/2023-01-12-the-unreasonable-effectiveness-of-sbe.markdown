---
layout: post
title:  "The Unreasonable Effectiveness of Simple Binary Encoding (SBE)"
date: 2023-01-12
tags: sbe "simple binary encoding"
---

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






[OSI model]: [https://en.wikipedia.org/wiki/OSI_model]