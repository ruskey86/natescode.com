---
title: "ORMS and more"
date: 2022-08-01T00:03:46-05:00
draft: true
---

ORMs, Query Builders, sprocs and more

#

orm

#

sql

#

database

#

postgres
ORMs and Query Builders

Query Builder
Query Builder is a simple library that generated SQL from code. They don't do much else.

Sometimes they're combined with versioning like LiquiBase. ORMs do this too, making their own transactions. They have an Up() and Down() method.

The thing I like about these is that they're good for basic SQL queries and they'll automatically map the results to a type-safe object, Linq2DB was really easy to work with.

The thing I don't like is for simple queries,

SQL Injection
Honestly, pretty much everything but raw, plain SQL prevents SQL injection. Prepared Statements, Query Builders, ORMs, and stored Procedures. You have to be ignorant or drunk to allow SQL injection. Yet, I still see it regularly.

ORMs
ORMs definitely have their place. For most projects, they're super useful for migrations when the schema is changing frequently. I've used EF migrations in production without any issues. It is extremely safe and convenient to make C# model changes and have the SQL automatically figure out what needs to change. I always inspect the SQL that is generated before making changes of course. This might seem like you could easily do this yourself, sure on a small scale. Once you have multiple developers making changes then having the SQL auto-generated and then inspecting it and testing it on staging is extremely valuable.

If ORM is bad, what is good?
Bad is relative. What is better?

Manually writing SQL scripts and saving them in GIT after you run them?
I'm working for a very large client at the moment that does this. Tons of Medicare information.

This is rough to manage. Stored Procedures are generally fast, safe and easy to profile. Definitely the way to go at scale.

Leaky abstractions
All abstractions leak. Micro-orms are really, really good.

Performance
I remember a project I was doing for large bank in California. The non-technical manager heard Entity Framework was 'slow' (slow is relative) compared to Dapper. So he forged us to use Dapper.

Dapper at the time was extremely basic and didn't support migrations, and a lot of joins. Much of the reason why it was so fast.

So we had to scrap Dapper. There was zero evidence entity framework wasn't fast enough. This was fear not logic.

For 90% of cases, performance isn't much of an issue. Especially at the database access layer. For a public website, everything gets cached anyways. We aren't hitting the database for most requests.

I'd you're using a proxy like Cloud flare, chances are that 80-95% of your site is hitting the cache.

False Dichotomy
The choice isn't ALL ORM or ALL stores procedures.

ORMs generally are fine. 90-98%. Even DBAs will say this.

You CAN do migrations outside an ORM but why? Either use it or make stored procedures, NEVER business logic in them for Pete's sake.

JavaScript makes ORMs look bad
JavaScript only has doubles and not integers which can cause issues with ORMs. Most ORMS are poorly implemented in JavaScript.

Prisma doesn't wrap migrations with transactions and TypeORM had a bug that would ignore a where clause and still execute. That could potentially wipe out your whole database, no thanks.

Negatives
All abstractions leak, ORMs are no different. As I learned more SQL, the less I felt I got from heavy ORMs. Dapper is popular for a reason, it is fast, simple and closer to raw SQL.

If you need other applications to interface with your database, then what?

Large ORMs keep developers from learning SQL, well until they need to profile a query. I was guilty of this for awhile.

Conclusion
ORMs aren't bad. They're a tool to be use with caution. I've used ORMs in production on many enterprise projects for banks, credit unions, hospitals etc. I've also used Dapper and raw SQL queries. Use what works.

ORMs can and do scale for production use. Migrations are extremely helpful.