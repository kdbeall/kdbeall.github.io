---
layout: post
title: Raw Thoughts on The Future of Hardware
---

Initially, it might seem that the CISC philosophy is dead. On the contrary, CISC is more relevant than ever because
there is a slowdown, if not the end, of Moore's law. As of 2020, there are only three major companies Intel, TSMC, and Samsung left at the bleeding-edge of semiconductor manufacturing. Previous titans such as [Global Foundries](https://www.anandtech.com/show/13277/globalfoundries-stops-all-7nm-development) are reducing their investment in newer nodes and processes. With that in mind, we can't rely on steady improvements to general purpose computing. Instead, hardware will
grow more complex to support specialized developer needs. However, what happens when specialized hardware functionality is added year-on-year to meet the current fads? It's not exactly trivial to deprecate hardware functionality. Will we have huge and bloated instruction sets? It's not hard to imagine an ISA that has upwards of 5k instructions. Thus, I feel we need to reinvestigate the CISC philosophy to make hardware complexity manageable.

### Examples of Current Complexity

* [Why do ARM chips have an instruction with Javascript in the name?](https://stackoverflow.com/questions/50966676/why-do-arm-chips-have-an-instruction-with-javascript-in-the-name-fjcvtzs)
* [Intel's RDRAND](https://en.wikipedia.org/wiki/RDRAND)
* [Intel's AVX](https://en.wikipedia.org/wiki/Advanced_Vector_Extensions)
* [Transactional memory support in IBM Power 8 Processor](https://ieeexplore.ieee.org/document/7029245)
* [Neural Engine in Apple's A11](https://www.wired.com/story/apples-neural-engine-infuses-the-iphone-with-ai-smarts/)

### Complex Hardware Blurbs and Questions
* Hardware transactional memory could simplify concurrency. It could make previously tricky [STM](https://queue.acm.org/detail.cfm?id=1454466) a reality. STM can be backed by hardware primitives for increased performance.
* NUMA-awareness (not to be confused with the Numa Numa song) will be needed. More complex processor topologies are being invented. My understanding is that many operationg systems and other systems software e.g. [Windows](https://www.youtube.com/watch?v=M-Q02b5uvfY) don't take into account differences between AMD's CCX and traditional Intel multiprocessor systems 
glued together by QPI. Additionally, exotic storage solutions e.g. [3D XPoint](https://en.wikipedia.org/wiki/3D_XPoint) can be used as [Non-volatile main memory](https://en.wikipedia.org/wiki/NVDIMM) which also change assumptions about memory.
* Will neuromorphic chips e.g. IBM's TrueNorth and Apple Neural Engine become popular?
* What APIs will be offered to access specialized hardware? My understanding is that Apple's neural engine can't be accessed
using traditional assembler instructions. You must use [CoreML](https://developer.apple.com/documentation/coreml).
* Will mainstream CPUs include a FPGA or FPGA-like coprocessor?
