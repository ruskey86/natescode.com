---
title: "Premature Optimization"
date: 2020-03-01T00:03:46-05:00
draft: true
---

Premature Optimization: Overcomplicating simple problems to sound smart

#

architecture
This is one of most common mistakes developers of all skill levels and experience make. It often goes along with having an overly inflated ego.

The architect at my job currently thinks the CQRS or Command Query pattern is the best architecture ever and EVERY project, no matter the size, is going to use it.

This is like using a Rocket ship for ALL your travels. It doesn't make sense. Short distances, walk, longer bike, even longer drive and even longer fly. The solution should change depending on the extremity of the problem. There is no one side fits all.

I'm going to use CQRS as a specific example to dig into how to decide if you or your architect is overcomplicating the solution.

Religious about technology
It is okay to enjoy tools but if you're in love with the approach then you're not in love with the product and neglecting it!

Ignoring Scale
Scale is the largest factor in architecture. Now, too many think they'll pick an overly complex approach, just in case, the application grows. I promise you, Google didn't start that way. Now, I'm NOT say to start with everything in a single HTML file either, oh humans are extremists.

If you're building a side project or even a small online business, i.e my NatesCodeCamp.org, there is ZERO reason to overcomplicate the architect. In fact, that's worse because early on is when you're most likely to do major refactors. Small projects need agility, NOT rigidity and stability.

I had to refactor our Trello clone at work, which used CQRS. Dear Lord was that hell. So many models changed.

So let's cover WHAT SQRS is, the costs and WHY a project should use it.

CQRS or Command Query pattern uses command object that represent mutation. Instead of mutating a model to increment X from 1 to 2 we'd send a command called INCREMENT. Basically like Queries and Mutations in GraphQL.

CQRS separates the DTOs used to get data from