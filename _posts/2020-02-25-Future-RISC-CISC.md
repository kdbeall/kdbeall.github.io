---
layout: post
title: Draft Post: The Future of RISC vs CISC
---

Initially, it might seem that CISC is dead. On the contrary, CISC is more relevant than ever.

Instruction sets are becoming more complex with the addition of cryptographic, transactional, vector, and
other specialized instructions.

* [Why do ARM chips have an instruction with Javascript in the name?](https://stackoverflow.com/questions/50966676/why-do-arm-chips-have-an-instruction-with-javascript-in-the-name-fjcvtzs)
* [Intel's RDRAND](https://en.wikipedia.org/wiki/RDRAND)
* [Intel's AVX](https://en.wikipedia.org/wiki/Advanced_Vector_Extensions)
* [Transactional memory support in IBM Power 8 Processor](https://ieeexplore.ieee.org/document/7029245)

[Moore's law](https://www.technologyreview.com/s/615226/were-not-prepared-for-the-end-of-moores-law/) is
dying. There are only three major competitors Intel, TSMC, Samsung left at the bleeding-edge.
Titans such as [Global Foundries](https://www.anandtech.com/show/13277/globalfoundries-stops-all-7nm-development) are 
reducing their investment in bleeding-edge technolgies.

My prediction: as Moore's law stalls there will be an increased emphasis at the intersection between
software and hardware. 

* Concurrent programming is hard and advanced ISA features such as hardware transactional memory
could make it easier.

* Need for NUMA-awareness in software. More complex processor topologies will have to be considered. 

* Exotic storage solutions e.g. [3D XPoint](https://en.wikipedia.org/wiki/3D_XPoint)
