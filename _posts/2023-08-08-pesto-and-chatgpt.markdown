---
layout: post
title:  "Pesto and ChatGPT"
date:   2023-08-02 19:57:57 -0500
categories: blog post
---
I think there has probably been plenty written about the AI revolution and ChatGPT but today was a particularly fun day. 

We are currently going through a major database migration at work. We have a Neo4j graph database that is falling behind in pretty much everything you can think of. We have to self host it because of some plugins that we use and the version we are on requires it to be hosted on an Ubuntu server that is about 5 years out of date on security patches. Considering this data is what the business is built on it's not an optimal setup. None of us are particularly savvy with Neo4j so we decided to convert the data to PostgreSQL. 

This gives us advantages in a few areas that outweigh the benefits of the graph db even though it's a good use case. Most importantly, I'm my opinion, just about every web dev in existence is familiar a relational db. This makes turnaround time on new features much faster and less error prone. There are also a lot more tools available, such as ORMs, cloud hosting services and just general information on developing and troubleshooting.

As part of this migration, since it is such a mission critical store of data we are looking for ways to make sure that the new implementation is going to match what we currently have. After a few brainstorming sessions we came up with the idea to send NServicebus messages containing the original request and the response we are going to return out from each controller action and then try it again in the new implementation. We can then log differences and hopefully trace errors before we get to production. After starting to implement this, after about two methods it was obvoius there was more generic way then having a unique message and handler for each action. After a little more discussion it seemed like a fun idea to describe to GPT4 the potential solution and ask for advice. I ended my prompt saying _What do you think?_

This is how the response started 
```It sounds like you're implementing a form of request shadowing or mirroring to compare the behavior of two different implementations of your API. This is a technique often used to safely test new implementations in a production-like environment without affecting actual users.
```

It proceeded to then lay out some examples on message implementations, what a handler would look like, etc. The part that stuck out to me was that it recognized that there is an established pattern that we were following. This is essentially the opposite of what you would normally get from a traditional web search. Its easy to ask a question or search for a simple subject or idea, but going from paragraph long descriptions to a single concept is something that was normally reserved for asking human experts. Google is good for if you know what you're looking for, but if you don't it can be really hard to come up with a search query short enough that will give you actual useful results.

On the other side of the spectrum after I finished for the day my wife started boiling the pasta water for dinner, and I had basically 10 minutes to make some pesto. I knew basically the ingredients and had them in stock: basil, pine nutes, olive oil, garlic. What I needed was basically what ratios and everything to put them into the food processor. I could look in my cookbook and then read 3 pages from Kenji on the science of why you should freeze your olive oil before you put it in the food processor. I could also do a web search, decide if I want to look at one of the big recommended posts (which may or may not be monetized clicks) or search through a few links until I find one that appears to be reputable enough to know how to make a pesto, hope it has a jump to recipe button, and then pray they're not a vegan or something as I read the recipe because I am not reading about how their great grandmother invented pesto when they floated to America on the Mauritania.

So I asked ChatGPT.

My pasta turned out perfect.