---
layout: post
title: Food for Thought: The Future of RISC vs CISC Philosophies
---

Initially, it might seem that CISC is dead. On the contrary, CISC is more relevant than ever because
of the slowdown of Moore's law. There are only three major companies Intel, TSMC, Samsung left at the bleeding-edge of semiconductor manufacturing, and [we're not prepared for its end](https://www.technologyreview.com/s/615226/were-not-prepared-for-the-end-of-moores-law/). Titans such as [Global Foundries](https://www.anandtech.com/show/13277/globalfoundries-stops-all-7nm-development) are reducing their investment in bleeding-edge technolgies. With that in mind,
we can't rely on steady improvements to general purpose improvements. Instead, hardware will
grow more complex to support developer needs.

### Need for Complexity

* [Why do ARM chips have an instruction with Javascript in the name?](https://stackoverflow.com/questions/50966676/why-do-arm-chips-have-an-instruction-with-javascript-in-the-name-fjcvtzs)
* [Intel's RDRAND](https://en.wikipedia.org/wiki/RDRAND)
* [Intel's AVX](https://en.wikipedia.org/wiki/Advanced_Vector_Extensions)
* [Transactional memory support in IBM Power 8 Processor](https://ieeexplore.ieee.org/document/7029245)
* [Neural Engine in Apple's A11](https://www.wired.com/story/apples-neural-engine-infuses-the-iphone-with-ai-smarts/)
* Hardware transactional memory could simplify concurrency. It could make previously tricky [STM](https://queue.acm.org/detail.cfm?id=1454466) a reality. STM backed by hardware primitives for increased performance.
* NUMA-awareness (not to be confused with the Numa Numa song) will be needed. More complex processor topologies are being invented. My understanding is that many operationg systems and other systems software e.g. [Windows](https://www.youtube.com/watch?v=M-Q02b5uvfY) don't take into account differences between AMD's CCX and traditional Intel multiprocessor systems 
glued together by QPI.
* Exotic storage solutions e.g. [3D XPoint](https://en.wikipedia.org/wiki/3D_XPoint) can be used as [Non-volatile main memory](https://en.wikipedia.org/wiki/NVDIMM)
* What APIs will be offered to access hardware? My understanding is that Apple's neural engine can't be accessed
using traditional assembler instructions. You must use [CoreML](https://developer.apple.com/documentation/coreml).

