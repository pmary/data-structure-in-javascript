# 2.3 An Anagram Detection Example

A good example problem for showing algorithms with different orders of magnitude is the classic anagram detection problem for strings. One string is an anagram of another if the second is simply a rearrangement of the first. For example, `'heart'` and `'earth'` are anagrams. For the sake of simplicity, we will assume that the two strings in question are of equal length and that they are made up of symbols from the set of 26 lowercase alphabetic characters. Our goal is to write a boolean function that will take two strings and return whether they are anagrams.

## 2.3.1 Solution 1: Checking Off

Our first solution to the anagram problem will check to see that each character in the first string actually occurs in the second. If it is possible to “checkoff” each character, then the two strings must be anagrams. Checking off a character will be accomplished by replacing it with the special JavaScript value `null`. However, since strings in JavaScript are immutable, the first step in the process will be to convert the second string to an array. Each character from the first string can be checked against the characters in the list and if found, checked off by replacement. An implementation of this strategy may look like this:

```js
function anagramCheckingOff (s1, s2) {
  if (s1.length !== s2.length) return false

  const s2ToCheckOff = s2.split('')

  for (let i = 0; i < s1.length; i++) {
    let letterFound = false
    for (let j = 0; j < s2ToCheckOff.length; j++) {
      if (s1[i] === s2ToCheckOff[j]) {
        s2ToCheckOff[j] = null
        letterFound = true
        break
      }
    }
    if (!letterFound) return false
  }

  return true
}

anagramCheckingOff('abcd', 'dcba') ); // true
anagramCheckingOff('abcd', 'abcc'); // false
```

To analyze this algorithm, we need to note that each of the n characters in `s1` will cause an iteration through up to _n_ characters in the list from `s2`. The number of visits then becomes the sum of the integers from 1 to _n_. We stated earlier that this can be written as
$$
\begin{split}\sum_{i=1}^{n} i &= \frac {n(n+1)}{2} \\
                 &= \frac {1}{2}n^{2} + \frac {1}{2}n\end{split}
$$
As _n_ gets large, the $$n^2$$ term will dominate the nn term and the $$\frac {1}{2}$$ can be ignored. Therefore, this solution is $$O(n^{2})$$.

## 2.3.2 Solution 2: Sort and Compare

Another solution to the anagram problem will make use of the fact that even though `s1` and `s2` are different, they are anagrams only if they consist of exactly the same characters. So, if we begin by sorting each string alphabetically, from a to z, we will end up with the same string if the original two strings are anagrams. The code below shows this solution. First, we convert each string to an array using the string method `split`, and then we use the array method `sort` which lexographically sorts an array in place and then returns the array. Finally, we loop through the first string, checking to make sure that both strings contain the same letter at every index.

```js
function anagramSortAndCompare (s1, s2) {
  if (s1.length !== s2.length) return false

  const sortedS1 = s1.split('').sort()
  const sortedS2 = s2.split('').sort()

  for (let i = 0; i < sortedS1.length; i++) {
    if (sortedS1[i] !== sortedS2[i]) return false
  }

  return true
}

anagramSortAndCompare('abcde', 'edcba'); // true
anagramSortAndCompare('abcde', 'abcd'); // false
```

At first glance you may be tempted to think that this algorithm is $$O(n)$$, since there is one simple iteration to compare the n characters after the sorting process. However, the two calls to the JavaScript array `sort` method are not without their own cost. As we will see in a later chapter, sorting is typically either $$O(n^{2})$$ or $$O(n\log n)$$, so the sorting operations dominate the iteration. In the end, this algorithm will have the same order of magnitude as that of the sorting process.

## 2.3.3 Solution 3: Brute Force

A brute force technique for solving a problem typically tries to exhaust all possibilities. For the anagram detection problem, we can simply generate a list of all possible strings using the characters from `s1` and then see if `s2` occurs. However, there is a difficulty with this approach. When generating all possible strings from `s1`, there are n possible first characters, $$n−1$$ possible characters for the second position, $$n−2$$ for the third, and so on. The total number of candidate strings is $$n∗(n−1)∗(n−2)∗...∗3∗2∗1$$, which is $$n!$$. Although some of the strings may be duplicates, the program cannot know this ahead of time and so it will still generate $$n!$$ different strings.

It turns out that $$n!$$ grows even faster than $$2n$$ as $$n$$ gets large. In fact, if `s1` were 20 characters long, there would be $$20!=2,432,902,008,176,640,000$$ possible candidate strings. If we processed one possibility every second, it would still take us 77,146,816,596 years to go through the entire list. This is probably not going to be a good solution.

## 2.3.4 Solution 4: Count and Compare

Our final solution to the anagram problem takes advantage of the fact that any two anagrams will have the same number of a’s, the same number of b’s, the same number of c’s, and so on. In order to decide whether two strings are anagrams, we will first count the number of times each character occurs. Since there are 26 possible characters, we can use a list of 26 counters, one for each possible character. Each time we see a particular character, we will increment the counter at that position. In the end, if the two lists of counters are identical, the strings must be anagrams. The code below shows this solution.

```js
function getLetterPosition(letter) {
  return letter.charCodeAt() - 'a'.charCodeAt();
}

function anagramCountCompare(s1,s2) {
  const s1LetterCounts = new Array(26).fill(0);
  const s2LetterCounts = new Array(26).fill(0);
  
  for (let i = 0; i < s1.length; i++) {
    const letterPosition = this.getLetterPosition(s1[i]);
    s1LetterCounts[letterPosition]++;
  }
  for (let i = 0; i < s2.length; i++) {
    const letterPosition = this.getLetterPosition(s2[i]);
    s2LetterCounts[letterPosition]++;
  }
  for (let i = 0; i < s1LetterCounts.length; i++) {
    if (s1LetterCounts[i] !== s2LetterCounts[i]) {
      return false;
    }
  }

  return true;
}


console.log( anagramCountCompare('apple', 'pleap') ); // true
console.log( anagramCountCompare('apple', 'applf') ); // false
```

Again, the solution has a number of iterations. However, unlike the first solution, none of them are nested. The first two iterations used to count the characters are both based on n. The third iteration, comparing the two lists of counts, always takes 26 steps since there are 26 possible characters in the strings. Adding it all up gives us $$T(n)=2n+26$$ steps. That is $$O(n)$$. We have found a linear order of magnitude algorithm for solving this problem.

Before leaving this example, we need to say something about space requirements. Although the last solution was able to run in linear time, it could only do so by using additional storage to keep the two lists of character counts. In other words, this algorithm sacrificed space in order to gain time.

This is a common occurrence. On many occasions you will need to make decisions between time and space trade-offs. In this case, the amount of extra space is not significant. However, if the underlying alphabet had millions of characters, there would be more concern. As a computer scientist, when given a choice of algorithms, it will be up to you to determine the best use of computing resources given a particular problem.

