---
title: How to generate strong passwords with quantum random data
categories:
  - Help File
tags:
  - Linux
  - Python
  - Tools
---

A number of years ago I wrote a little utility that generates [Diceware][1] passwords. "Big deal!", you might think. But my utility has a unique feature. It generates passwords using quantum random data from cosmic microwave background radiation.

*"Okay, so, it sounds like something from a Superman movie, but why does it matter?"*

A truly random number is something that is surprisingly difficult to generate. Computers can only generate pseudo-random data. The data may *look* random, but in fact follows a predictable sequence. Anything that is predictable is repeatable and therefore subject to attack. To create strong passwords that are not predictable, we need truly random data.

![XKCD](/assets/images/password_strength.png)

## What is Diceware?

Diceware is a method for generating strong but easy to remember passwords.

For example:

```
    ella trout canna beryl mabel bold
```

It is designed to be used with paper and six-sided dice. It is secure because it is done offline, uses truly random data, is fully transparent in the generating process, and is easy to remember. You can read more about it [here][2].

The downside is that it can take upwards of six to ten minutes to generate one password, as each word requires six rolls of the dice (or one roll of six dice).

## What does QDG do?

As previously explained, QDG generates Diceware passwords with truly random data. You can use it to instantly generate any number of passwords.

To get started with QDG, you first need to install it with pip:

```sh
    $ pip3 install quantumdiceware
```

Then you can simply execute the utility to generate passwords. Here is an example with output:

```sh
    $ qdg -c 5
    88 vital gawk 1950 xl spade
    dey ul still ooze 39th moen
    62nd aloha find race shine tabula
    reign wx 234 togs rsvp cain
    moll trick foot soar pile irs
```

I will often generate multiple passwords as we did above and then combine them to create my own.

For example:

```
    aloha still find race trick foot
```

Easy to remember and truly random, but exceedingly difficult to brute force.

But some accounts require a certain amount of complexity for passwords, or do not allow the use of spaces. A requirement for two uppercase letters, two lowercase letters, two numbers, and two special characters is common.

Luckily, QDG is ready-made to tackle these requirements.

To generate a password without spaces, you can replace the space with something else:

```sh
    $ qdg --char -
    vend-grist-hobby-mark-enamel-job
```

Or remove the spaces altogether:

```sh
    $ qdg --char ""
    vendgristhobbymarkenameljob
```

Another method is to generate a two-word password with the requirements sandwiched in the middle:

```sh
    $ qdg --char "AA22##" -w 2
    pencilAA22##ward
```

Anytime you need to update your password, you can keep the part in the middle and simply generate two more words.

As a general rule, you want your password to be as long as is allowed by the account. Password strength comes from *length*, not complexity.

So this was just a quick explanation of how I generate strong passwords. You can learn more about QDG by [reading the docs][3].

[1]: https://theworld.com/~reinhold/diceware.html
[2]: https://theworld.com/~reinhold/diceware.html
[3]: http://qdg.readthedocs.io/
