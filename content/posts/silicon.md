---
title: "Silicon"
date: 2015-01-01T00:03:46-05:00
draft: true
---

Silicon: Adventures in Programming Language Design and Compiler Development

#

compiler

#

computerscience

#

plt

#

advanced
"One Language to rule them all, One Language to write them, One Language to bring them all and in the bytecode compile them." -- Nate of NatesCode

"If you don't know how compilers work, then you don't know how computers work" -- Steve Yegge

I'm not saying that quote is 100% accurate but that sure got me thinking. How do programming languages work?

Silicon
So, years ago I wanted to learn how programming and computers actually work. Well we use programming languages...but who makes the programming languages? How?

From Silly to Serious
Originally, it was called Sillyscript (well Sindyscript briefly because of my ex wife)

It was a toy. I thought about how I'd parse text. I figured out a tree structure would work. I was pleasantly surprised when Google confirmed my guess. It was easy to get a basic math parser to do arithmetic with precedence but I wanted more, a lot more.

Eventually, it was named Silicon. I'll admit I don't have a ton of code as I've spent years learning and tinkering with concepts. So far it is in Typescript which surprisingly is a decent fit for an initial compiler. OCaml is the standard.

I used Go to follow along to make an Interpreter and Compiler in Go. Thorsten Ball's "Writing an Interpreter in Go" and "Writing a Compiler in Go" really helped a lot. I highly recommend his books.

I read this paper by Johnathan Goodwin about gradual memory management. Just like how Typescript allows you to start with dynamic typing and gradually add static typing, you could gradually adopt lexical or manual memory management. You could start with a typical mark-and-sweep garbage collector then move to ephemeral (generational) and for critical parts use lifetimes like Rust. Silicon seeks to combine both gradual typing and gradual memory management. One language that could act like Typescript, Rust and everything in-between.

You can start writing code like JavaScript, add types as needed and later, wrote blazing fast, memory efficient and safe low-level code, only where needed without switching programming languages!

I don't have a BS in CS so I had to do some reading. I bought the Dragon Book as it's called and many others to get up to speed.

Learning
Designing a Programming Language
Naming things is hard
Originally Silicon was going to be a lot like Perl with tons of little symbols (sigils) that denoted things. I.E. '$' would precede all variable names. I eventually dropped most of the sigils but liked the name. So Sigil is the name of the compiler and toolchain while Silicon is the name of the language and grammar. I strive to create my own specification around the Silicon language that anyone can implement as they see fit, just how there are many JavaScript engines: V8, Spider monkey etc. all based off the ECMAScript specification.

Grammar
There are several factors to Silicon's grammar: features, familiarity. Both Typescript and Rust are inspired by ML languages and Silicon is simply their love-child.

The Basics
\\ single-line comment \* multi-line
comment _\
@let name = "Nate" #3'400'000,00
@let nickname : @str = "Radar"
I don't do C-style comments because // is actually the log operator. If _ for multiplication becomes \*\* for exponents then / for division should become // for logarithms.

Since using bitwise operations is so rare now, I've also inverted the symbols. & is the same as && in C-like languages etc.

ALL keywords are prepended with @ or the keyword sigil. This has a few benefits.

Prevents future clashing of keywords and custom identifiers
Allows for multi-lingual keywords: i.e. @if @Если إذا@ @如果
Editor suggestions are a bit clearer.
Other Features
automatic semi-colon insertion
strong type inference (gradually typed like Typescript)
union types
pattern matching
Negative array indexes are supported but use the IEEE 754-2019 floating point -0 to index to the last item in an array. So the first and last indices always count from 0 but starting from the end the numbers are negative (makes more sense than -1).

Let's write the timeless Fibonacci function in idiomatic Silicon (I will show several other approaches later.)

@let fib n = ~[0,1,@[-1]+@[-2]..n-1]

Yes, it is that short. This is tail-call optimized too! This is like Python list comprehensions but cleaner.

Basically we're creating a list and starting with the first two values, like we usually do in Fibonacci. Then we show how to calculate the next values. In our case we're indexing, relative to where we currently are, and using those values to calculate the next and next and next...until the provided max index. To save memory, we don't want to have the WHOLE array in memory so we use the tilde sigil to say we only want as much of the array as needed to calculate the values. In this case this is two.

@let fib n = : declare function fib that takes parameter n (type is inferred by usage)

~ sigil means we do NOT want the WHOLE array except for the indexes we need to do the calculations. In this case we'll always have 2 in memory to do the calculation for the next.

[0,1, The rest is the initial array values.

@[-1]+@[-2] Then we can use @[n] to refer to the index inside of the array. Where n is a integer less than or equal to 0. So we calculate the next value of the Fibonacci sequence.

.. range operator like C# and other languages before it. This means to continue the calculation until the next provided value.

n-1 the index to calculate to. Hence n-1 since if we want the 10th Fibonacci number, that's the index of 9.