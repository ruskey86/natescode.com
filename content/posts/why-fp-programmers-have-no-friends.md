---
title: "Why FP programmers have no friends"
date: 2015-01-01T00:03:46-05:00
draft: true
---

This is a bit of a satirical post but with some serious points about my struggles learning functional programming.

Like most programmers, I started with procedural coding. It is arguably more intuitive. I learned on a TI-84 using TI-BASIC. No
functions, no loops, just GOTO and labels and global variables. Later, I learned C++. I learned to embrace object-oriented programming. Eventually, I learned OOP well enough to see it's flaws and drawbacks. I started to look for a challenge and other paradigms that could help me write better code.

I stumbled upon functional programming. and languages like F#, OCaml, Haskell, Elm, Rescript and Purescript.

I enjoy mathematics and already knew some very basics of category theory. FP takes it to a whole different level of course.

Now let's get into my main non-technical struggles with FP and the community at large.

## Egotistical, not humble

The largest and most annoying barrier to learning and appreciating FP is the ego of FP's evangelists. I've found many FP developers to be extremely cocky, egotistical and narcissistic. I understand how being intelligent can give someone a false sense of superiority. Many come from an academic and mathematical background. Unfortunately they think IQ = superiority. Their precious FP code is blessed by the code gods and anything else is impure (pun intended) and evil. Of course they'll never change their ways because they don't believe in mutability. They'll never learn OOP and are stuck in an infinite recursion because they don't have a base-case.

Seriously, though. Even my F# book constantly needs to remind the reader of the superiority of F# over C#, and F# isn't completely pure or consistent (due to compatibility with .NET).

## Academics, not Teachers

The other barrier is that FP is born from higher level mathematics and academia. They're not software engineers or teachers, they're mathematicians and theorists. Their mind focuses on abstractions and concepts, not necessarily practical usage to solve client or developer problems. The fact that no one seems to explain Monads very well is a great example (Ironically, I'm working on my own Monad tutorial). Haskell has purposely been created for exploration over actual practial development.

This makes learning FP without a PHD in mathematics feel nearly impossible.

## Domain Focused, not General Purpose

Functional Programming has some amazing advantages and concepts. This post isn't knocking the paradigm but more the attitude and community. Unfortunately, languages like Haskell aren't used nearly as much for general purpose development and don't have the ecosystem for it.

## JavaScript, not Haskell

JavaScript originally was a Scheme implementation so not OOP to begin with. It uses prototypal inheritance instead of classical inheritance. JavaScript, the ecosystem and the culture at large as begun to embrace a lot of FP concepts. I think this is a good thing. React, from Facebook (now Meta), was originally written in StandardML after all. So the FP evangelists failed where Facebook succeeded. Instead of trying to prove superiority or talk about category theory, Facebook made a great UI library with practical applications and shared it. This is how you get adoption, through love and practical use, not proselytizing. React nor Javascript are anywhere near purely functional languages. React added hooks which breaks referential transparency, (so no THEO you're not a FP nerd. You're a FP faker that writes procedural code).

## Conclusion

Functional Programming has been a blast to learn. It has challenged so much of the OOP concepts that I first learned. I don't think FP, OOP, AOP, Functional Reactive Programming(FRP) or whatever paradigm is inherently the best. Most approaches have their pro's and con's. I highly recommend learning FP.