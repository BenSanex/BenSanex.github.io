---
layout: post
title:  "Pesto and ChatGPT"
date:   2023-08-03
categories: blog post
tags: [Post, AI]
---
There's certainly no shortage of discussions about the AI revolution and ChatGPT, but today stood out as especially memorable.

At my workplace, we're in the midst of a significant database migration. Our Neo4j graph database seems to be lagging in almost every aspect imaginable. We're bound to self-hosting due to specific plugins and our version mandates hosting on an Ubuntu server that's alarmingly outdated in terms of security patches. Given that our business foundation rests on this data, the current setup is far from ideal. The team isn't well-versed in Neo4j, leading us to the decision to transition to PostgreSQL.

<!--more-->

Opting for PostgreSQL offers us several advantages, overshadowing the merits of our current graph database—even if it seemed like the ideal choice initially. In my view, the pivotal advantage is that virtually every web developer is acquainted with a relational database. This familiarity results in quicker and less error-prone feature releases. Additionally, a plethora of tools, from ORMs and cloud hosting services to general information on development and troubleshooting, become available.

To ensure the integrity of our critical data during this migration, we've been brainstorming ways to replicate our existing setup. One idea that emerged was to dispatch NServicebus messages comprising both the original request and the expected response from each controller action, retesting this in the new system. By logging any discrepancies, we hope to detect and address any issues before deploying to production. However, after testing a couple of methods, it became clear that a more generalized approach was needed. We contemplated turning to GPT-4 for insights and concluded our query with, _What do you think?_

The response began as follows:
```It sounds like you're implementing a form of request shadowing or mirroring to compare the behavior of two different implementations of your API. This is a technique often used to safely test new implementations in a production-like environment without affecting actual users.
```

What caught my attention was how it discerned the underlying pattern we were aiming for, even though we didn't really think to look for an existing one. Such insight isn't what one typically retrieves from a standard web search. While it's straightforward to query a basic topic or seek a direct answer, translating extensive descriptions into succinct concepts is often a task reserved for human experts. While Google excels when the search objective is clear, formulating a concise query that yields meaningful results can be a challenge when the end goal is ambiguous.

After a productive day, as my wife set the pasta water to boil, I had a mere 10 minutes to prepare some pesto. Sure, I was familiar with the basic ingredients: basil, pine nuts, olive oil, and garlic. What I was missing were the exact ratios. Now, I could've scoured my cookbooks and read through Kenji's detailed explanation on why freezing olive oil is the secret to a perfect pesto. Alternatively, I could embark on a web search, sifting through numerous results, some genuine, some clickbait, all the while hoping to land on a straightforward recipe without a long-winded backstory of someone's great-grandmother's culinary journey.

Instead, I posed the question to ChatGPT.

The result? Flawless pasta.



>This post was edited with ChatGPT ;)