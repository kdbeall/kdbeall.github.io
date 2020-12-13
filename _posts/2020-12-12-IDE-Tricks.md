---
layout: post
title: Draft Post - VS Code Tips and Tricks
---

## Command Palette

## 

## Code Snippets
They're mini-templates which make it easier to type common coding patterns.
In Go it is often pretty tedious to create a heap.

``` go
import "container/heap"

type IntHeap []int

func (h IntHeap) Len() int            { return len(h) }
func (h IntHeap) Less(i, j int) bool  { return h[i] < h[j] }
func (h IntHeap) Swap(i, j int)       { h[i], h[j] = h[j], h[i] }
func (h *IntHeap) Push(x interface{}) { *h = append(*h, x.(int)) }
func (h *IntHeap) Pop() interface{} {
	old := *h
	n := len(old)
	x := old[n-1]
	*h = old[0 : n-1]
	return x
}

```


## Further Reading

* [tldr pages](https://tldr.sh/) — ever feel frustrated by the complexity of man pages? tldr pages are a simpler version of man pages.
* [iTerm2](https://iterm2.com/features.html) upgrade your terminal emulator.
* [Git Aliases](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases) aliases for common git commands.
