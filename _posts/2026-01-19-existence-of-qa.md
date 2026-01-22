---
layout: post
title: "In Defense of QA"
date: 2026-01-19 10:00:00 -0600
tags:
  - Post
  - QA
featured_image: none
excerpt: >-
  An argument for dedicated QA as a distinct role and mindset from feature delivery.
---

The debate over whether we still need QA keeps resurfacing, usually framed as a question of trust in developers or belief in automation. That framing misses the point. This isn’t about capability — it’s about incentives, cognitive load, and risk.

I recently found myself in another discussion debating the merits of dedicated QA engineers. For most, if not all, of my career I was never expected to have final say in whether or not my code was ready for release. There was always someone taking a second look (or a first, if I was lazy, overconfident, etc.) at a particular feature.

So it was a surprise when I joined a new company where the mandate was simple: *we do not have QA, everyone owns their own testing.*

It felt timely that [this post](https://news.ycombinator.com/item?id=46646226) made its way to the front page of Hacker News. The underlying paper argues that while developer-owned testing is possible in theory, it often fails in practice because the surrounding organizational structure does not set the initiative up to succeed.

As far as I can tell, this debate resurfaces on Hacker News more often than I bring it up myself.

---

## Shipping vs Stopping

The logic behind developers owning their code *does* have merit. Developers should be experts in their domain and should understand expected behavior as well as anyone. Training a QA engineer on product behavior introduces another layer of communication and another potential slowdown.

In my opinion, this is a feature, not a bug.

Having more people deeply familiar with a domain, each bringing their own perspective, reduces the chance of unintended consequences. Redundancy and extra eyes are exactly how complex systems stay resilient.

At a more fundamental level, developers and QA engineers tend to optimize for different things. Developers are oriented toward shipping. QA is oriented toward stopping bad things from shipping. That tension isn’t dysfunction, it’s the safety mechanism.

---

## Incentives Matter More Than Intentions

Developers are incentivized and measured on their ability to ship features.

At monthly all-hands meetings, the big announcements aren’t about how much money was saved by preventing a null reference exception on line 52. That kind of win is hard to measure and happens far more frequently than anyone would care to admit.

New features bring excitement. They make management happy. They set PMs and engineers up for promotions.

Prevented bugs don’t.

That incentive structure doesn’t make developers careless, it makes them rational.

---

## “Tests Are Code, So Developers Should Write Them”

Another common argument is that tests are code, and developers write code, so developers should write the tests. That’s true. I can read and write tests. Most developers can.

I’m not arguing that developers should abdicate responsibility for testing. Developers should absolutely be writing unit tests and integration tests where appropriate. Depending on the feature, they should also be doing performance or load testing.

A pull request should be a statement of what changed and a defense of why those changes should be merged.

The next step, however, is for someone else to challenge that statement.

This isn’t an argument for throwing work “over the wall” to QA, or for manual testing replacing automation.

---

## Where Dedicated QA Fits

This is where end-to-end testing makes the most sense.

End-to-end tests are more time-consuming and more expensive to run. You generally don’t want them on every commit or even on every deploy to a development environment. This is also where the strongest argument against dedicated QA tends to appear: *you can and should automate these tests.*

You should... where possible.

The issue arises when automation is *not* possible.

Not every company can reliably set up test data that guarantees deterministic results for complex workflows. Many systems rely on intricate setup conditions that are difficult or impossible to fully automate. When that’s the case, you’re relying on manual testing whether you admit it or not.

If you can’t automate it, someone still has to validate it.

---

## The Cost Center Fallacy

Layoffs have been the fashionable way to pump stock prices over the past few cycles. I’ve been through them. When evaluating who to keep, it’s easy to look at a discipline that actively slows shipping and has an explicit cost attached to it and say: *this needs to go.*

That looks clean on paper.

In practice, it just shifts the cost.

If X number of features are shipped each week and validating them costs 40 hours, those 40 hours don’t disappear when QA does. They move.

Would you rather those 40 hours be spent by a senior engineer making $190k a year, or by a QA engineer who costs significantly less? Those 40 hours of validation still need to happen. In reality, they often balloon once you factor in the cognitive load required to switch from shipping happy paths to actively trying to break things.

Context switching is not free.

---

## A Different Mindset Entirely

QA work requires a fundamentally different mental posture.

It’s the difference between making something work and trying to make it fail. Between shipping and stopping.

That mindset doesn’t come naturally to most builders, and that’s fine. It’s why specialization exists.

> A QA engineer walks into a bar and orders a beer.  
> She orders 2 beers.  
> She orders 0 beers.  
> She orders -1 beers.  
> She orders a lizard.  
> She orders a NULLPTR.

I have personally witnessed well over $200k in bugs that would have been caught by QA engineers I’ve worked with in the past.

---

## When Dev-Owned Testing *Can* Work

I would prefer to work with QA engineers, but it *is* possible to succeed with developers owning their own testing.

Startups that don’t have the money or the luxury of time (usually because of money) may need to drive their cars with no brakes. They’ll get dinged up along the way, but moving fast is existential.

Larger companies can try to move in this direction too, but only if they are set up to succeed:
- Codebases must designed to be testable
- Infrastructure must make tests easy to run and maintain
- Ownership must be explicit to prevent a tragedy of the commons

If you don’t have those things, removing QA doesn’t make you faster, it just makes failure quiet until it explodes.

If that is your situation, trust the experts whose job is to think about how your system fails.
