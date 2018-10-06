---
layout: post
title: Where's Python's bag data structure?
---

I got stuck on an online coding challenge today. I needed a [bag](https://en.wikipedia.org/wiki/Set_(abstract_data_type)#Multiset) data structure. For quick reference, a bag is a generalization of a set. Think of it as a set that may have multiple entries of the same value. I searched Python's documentation for both bag and multiset. I couldn't find what I wanted. So, I wasted a lot of time rolling my own.

Back to the challenge. The goal of the challenge was to find the minimum number of substitutions, without replacement, to make a string into an anagram of another. For example, if we have strings "ab" and "aa" we'd need to make one substitution. If we had strings "abc" and "aaa" we'd need to make two substitutions. The order of the letters does not matter. A bag makes sense for this problem because we need to find out the difference in the amount of each letter. For example, in "ab" there is one a and one b, but in "aa" there are two a's and one b. A bag allows us to easily compute the difference between the two. 

It turns out that Python does have its own implementation of the bag data structure. It is called [Counter](https://docs.python.org/3.7/library/collections.html#collections.Counter). I'm scratching my head as to why I did not know about it earlier because using Counter makes this problem extremely concise.

    from collections import Counter


    def min_character_difference(str_a, str_b):
        """
            Determine the minimum number of characters
            to change, without deletion, to make the two strings into anagrams of
            each another. Return -1 if the two strings cannot be made into
            anagrams of one another.
        """
        if len(str_a) != len(str_b):
            return -1
        ctr_a = Counter(str_a)
        ctr_b = Counter(str_b)
        ctr_a.subtract(ctr_b)
        counts = ctr_a.values()
        min_diff = sum(count for count in counts if count > 0)
        return min_diff


    if __name__ == "__main__":
        assert min_character_difference("", "a") == -1, "Different length."
        assert min_character_difference("", "") == 0, "Same characters."
        assert min_character_difference("a", "a") == 0, "Same characters."
        assert min_character_difference("abc", "abb") == 1, """One character
                                                            different."""
        assert min_character_difference("bcba", "accb") == 1, """One character
                                                            different."""
        assert min_character_difference("bb", "aa") == 2, """Two characters
                                                        different."""
        assert min_character_difference("bcb", "acc") == 2, """Two characters
                                                            different."""
        assert min_character_difference("abdb", "accc") == 3, """Three characters
                                                            different."""

