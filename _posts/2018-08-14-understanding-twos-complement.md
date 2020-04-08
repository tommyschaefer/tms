---
layout: post
title: Understanding Two's Complement
link: https://labs.teecom.com/2018/08/14/understanding-twos-complement.html
originally_posted_on: TEECOMlabs blog
---

Our team likes to do weekly
[team coding sessions](http://teecom.com/team-coding-software-techniques/) and
the occasional programming challenge. This week,
[Jake](https://teecom.com/people/jake-tesler) led the team in a challenge
borrowed from a previous college course. I come from a non-traditional computer
science background, so this challenge was particularly challenging and fun for
me!

One of the challenges that made me learn the most was:

```c
// isTmin - returns 1 if x is the minimum, two's complement
// number, and 0 otherwise
//
// Legal ops: ! ~ & ^ | +
// Max ops: 10
int isTmin(int x) {
  return 0;
}
```

If you’re anything like me, you reacted to that problem with “What the hell is
a two’s complement?!”

## Two’s Complement

A number is represented in binary by a string of ones and zeros called bits.
The number of bits used to hold a number is dependent on the particular language
or system, but 32-bit and 64-bit integers are very common.

Two's complement is a way of representing negative numbers in binary. In a
string of bits, the left most bit is often referred to as the “most significant
bit”, and the right most is called the “least significant bit”.

![](https://dl.dropboxusercontent.com/s/6bzpmw6rrakx0kr/2018_08_14_significance.jpg?dl=0)

For a number in two's complement, the most significant bit represents the sign.

![](https://dl.dropboxusercontent.com/s/3o5h8adiqgu7maj/2018_08_14_signs.jpg?dl=0)

Unfortunately, this isn’t quite enough on its own. If we just used the left most
bit as a sign with no other changes, addition would yield incorrect results.

![](https://dl.dropboxusercontent.com/s/20njw9gnkgsoklk/2018_08_14_adding_error.jpg?dl=0)

In order to preserve addition for negative numbers, we need to satisfy a rule:
**any number plus its negative must be zero**. How could we satisfy this rule?
The answer lies in the idea of "overflows". Because a number is only given a
certain amount of space, the range of possible values is limited. When a number
outgrows the container set aside for it, the bits that overflowed are lost.

To force an overflow, leaving all zeros behind, we first need to determine what
to add to a number to reach the integer maximum. For a 32 bit integer, the
largest possible integer is:

```
1111 1111 1111 1111 1111 1111 1111 1111
```

For any number `n`, we can arrive at the maximum representable integer by
inverting each bit in `n`, an operation commonly called the bitwise inversion,
and adding it to itself. Everywhere there was a zero in our original number,
there’s now a one.

![](https://dl.dropboxusercontent.com/s/va58bc9o73a5pp0/2018_08_14_adding_inverse.jpg?dl=0)

If we were to add one to that number, we would force an overflow, leaving only
zeros behind.

![](https://dl.dropboxusercontent.com/s/hyc2a1mfc7nmzke/2018_08_14_overflow.jpg?dl=0)


Using this process, we can now negate any binary number and still preserve the
rules of addition.

![](https://dl.dropboxusercontent.com/s/i0g0gik7xtam695/2018_08_14_full.jpg?dl=0)
