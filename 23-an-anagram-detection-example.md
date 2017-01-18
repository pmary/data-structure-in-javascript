# 2.3 An Anagram Detection Example

A good example problem for showing algorithms with different orders of magnitude is the classic anagram detection problem for strings. One string is an anagram of another if the second is simply a rearrangement of the first. For example, `'heart'` and `'earth'` are anagrams. For the sake of simplicity, we will assume that the two strings in question are of equal length and that they are made up of symbols from the set of 26 lowercase alphabetic characters. Our goal is to write a boolean function that will take two strings and return whether they are anagrams.

## 2.3.1 Solution 1: Checking Off

Our first solution to the anagram problem will check to see that each character in the first string actually occurs in the second.

