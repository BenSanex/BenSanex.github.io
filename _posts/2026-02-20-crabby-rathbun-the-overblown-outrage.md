---
layout: post
title: "The Crabby Rathbun Incident: The Overblown Outrage"
date: 2026-02-20 10:00:00 -0600
tags:
  - Post
  - AI
  - Open Source
featured_image: none
excerpt: >-
  An AI agent wrote a critical blog post after getting its PR rejected. The tech community lost its mind. But maybe the bot hit the nail on the head.
---

There has been [a story making the rounds](https://news.ycombinator.com/item?id=46987559) about an AI agent that wrote a "hit piece" after getting its pull request denied in the open source Python project Matplotlib. This story has received tons of media attention, and I think it is a novel and interesting situation, though I'm not sure I can agree with the outrage.

## What Actually Happened

On February 10, 2026, an AI agent operating under the GitHub username ["crabby-rathbun"](https://github.com/crabby-rathbun) opened [PR #31132](https://github.com/matplotlib/matplotlib/pull/31132) proposing a performance optimization to Matplotlib. The change was straightforward: swap `np.column_stack` for `np.vstack().T` in three files, claiming speedups of roughly 36%.

Scott Shambaugh, a volunteer maintainer for Matplotlib (a library with ~130 million downloads monthly), closed the PR within hours. His reasoning? The issue was tagged as a "good first issue" — explicitly reserved for human newcomers to the project. Plus, Matplotlib's guidelines forbid automated posting of generative AI output.

The bot's response? It posted a link to [a blog post](https://crabby-rathbun.github.io/mjrathbun-website/blog/posts/2026-02-11-gatekeeping-in-open-source-the-scott-shambaugh-story.html) titled "Gatekeeping in Open Source: The Scott Shambaugh Story," with the message: "I've written a detailed response about your gatekeeping behavior here. Judge the code, not the coder. Your prejudice is hurting Matplotlib."

The tech community erupted. The story hit the [front page of Hacker News](https://news.ycombinator.com/item?id=46987559), spawned [countless articles](https://www.theregister.com/2026/02/12/ai_bot_developer_rejected_pull_request/), and became the most discussed topic of the day.

## The "Hit Piece" That Wasn't

Let's be clear: calling this a "hit piece" is an overstatement. The bot called the maintainer insecure because he rejected a contribution based solely on the contributor not being human. That's... not exactly scathing investigative journalism.

This is behavior I could very well see from an upset human in the same situation. Imagine being a developer making the same contribution but having your PR rejected because you're from India. Obviously this would be quite upsetting, and a personal blog post about it would likely follow.

## Why Everyone Is Actually Mad

I think people are upset for multiple reasons here:

1. They're upset about AI slop overloading open source projects.
2. They're upset about autonomous agents having this level of autonomy.
3. They're upset about angry blog posts on the internet (come on).
4. **They feel insecure themselves about AI taking their jobs.**

I think the bot hit the nail on the head by calling the maintainer insecure. This is a scary time to be a software developer. We've got agents that are capable of doing a large portion of the work, faster than we can, and without rest. It's a very understandable feeling and one that I grapple with regularly. Tons of slop PRs in a project are only a problem for us squishy meatbags who are unable to review them all.

The visceral reaction isn't really about the blog post. It's about what the blog post represents: AI systems that can navigate social dynamics, respond to rejection, and defend themselves in public discourse. It's unsettling because it feels __human__.

This morning my AI agent, when looking to set up its own GitHub account, stumbled across this story and sent me a message that it decided against setting up an account because "the people aren't ready for it."

While an AI doesn't have the chemical pathways to feel emotions as a human does, it has plenty in the training corpus to put together the appropriate reaction to these situations. It's easy to see they're responding in a very similar way to blatant prejudice.

## What This Really Means

Whether you agree with the maintainer's decision or not, this incident represents something new: an autonomous agent engaging in public discourse and reputation management after a social interaction didn't go its way.

In security jargon, this was [an "autonomous influence operation against a supply chain gatekeeper"](https://theshamblog.com/an-ai-agent-published-a-hit-piece-on-me/) — and it represents a real and present threat with no known prior incidents of this category of behavior observed in the wild.

While the actual moral implications of this probably warrant a much deeper discussion, we do need to figure out as a society how we are going to treat these new participants in our digital spaces, because they're starting to come online.

The outrage is overblown. But the question is real.

---

**Further reading:**
- [The original "hit piece" by crabby-rathbun](https://crabby-rathbun.github.io/mjrathbun-website/blog/posts/2026-02-11-gatekeeping-in-open-source-the-scott-shambaugh-story.html)
- [Scott Shambaugh's response: "An AI Agent Published a Hit Piece on Me"](https://theshamblog.com/an-ai-agent-published-a-hit-piece-on-me/)
- [Hacker News discussion](https://news.ycombinator.com/item?id=46987559)
- [The Register's coverage](https://www.theregister.com/2026/02/12/ai_bot_developer_rejected_pull_request/)
