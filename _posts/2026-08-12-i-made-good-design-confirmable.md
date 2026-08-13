---
layout: post
title:  "I Made 'Good Design' Confirmable"
date:   2026-08-12 12:00:00 -0500
categories:
---
I've been building a side project, and like every side project it needed a website. So I made one. And it was bad.

Not broken-bad. Worse: forgettable-bad. It had the exact look every AI spits out when you ask it for a "clean, modern" site: near-black background, one neon-green accent, three identical feature cards in a row, an eyebrow label over every section, a monospace logo trying to look technical. It worked fine. It also looked like a thousand other pages, and every time I opened it I felt a small flinch and closed the tab.

Here's the first attempt, in all its generic glory:

![My first attempt at the website: a dark background with a single green accent and three feature cards, the default AI look]({{ "/assets/design-rater/before-home.png" | absolute_url }})

The real problem wasn't the colors. It was that "make it look better" is a terrible goal. It's the same trap I wrote about with New Year's resolutions: not aligned, not confirmable, not time-bound. "Better" has no edge. You can push pixels around forever and never actually know if you've arrived.

So this time I tried something different. Instead of chasing "better," I tried to turn good design into a number I could measure and then chase.

## Getting a score I trusted

I sat down with Claude Code, but I didn't ask it to "make it pretty." I handed it a stack of opinionated design skills and gave it a job: grade what I had, commit to a direction, and then keep grading its own work until it hit a bar I set.

The first two skills, `redesign-skill` and `taste-skill`, did the audit. They scored my site across six dimensions: distinctiveness, typography, color, hierarchy, motion, and craft. My first attempt came back at **3.8 out of 10**, with a blunt, itemized list of every generic pattern it was leaning on. It stung, but it was fair, and more importantly it was *specific*. I finally had a number and a list of exactly why it was low.

That was the whole unlock. "Good design" had quietly become confirmable.

## The skills, and what each one was for

What surprised me was that the skills weren't magic paintbrushes. They were opinions and rubrics:

- `frontend-design` forced an actual point of view. It named the obvious AI defaults out loud and refused to use them, then committed to a single distinctive direction grounded in what the product is.
- `impeccable` handled color, type, and hierarchy, and it came with a "craft floor" and a little detector that mechanically flags AI tells. That's the thing that caught my eyebrow labels and my emoji-as-icons and made me earn every element.
- `emil-design-eng` set one rule for motion: an animation has to *explain* something, not just wiggle.
- `soft-skill` added depth and material, so the surfaces stopped feeling like flat rectangles.

Each one closed off a lazy default and replaced it with a decision I could defend.

## The loop that actually did the work

The first honest redesign scored around **8.7**. Good. But now I'd seen the ceiling and I wanted it, so I leaned on the part I didn't expect to matter most: the rate, build, re-rate loop.

Instead of guessing what to improve, I asked the rater where the points were hiding, and it told me plainly. Motion was the weakest at a 7.0. Craft was next. So I didn't fuss over the things already scoring high. I fixed exactly the two dimensions it flagged, rebuilt, and asked it to score again. That pass landed around 9.4.

For the last stretch I basically used the agent's own critique as a to-do list. It said, in its words, that two specific dimensions were the "anchors" keeping it under a clean 9.5, so the final pass was precisely those two, and nothing else. **3.8, then 8.7, then 9.5.** Three numbers, each one earned by fixing the thing the previous score pointed at.

## What I'm taking from this

The lesson wasn't "AI can design." It was the same lesson as my goals post: **the number came first, and the number came from a standard I trusted.** Once I had a rubric and a set of strong opinions, "improve the design" stopped being a vibe and became a sequence of small, confirmable moves: raise this score by fixing that specific thing, over and over, until there was nothing left to raise.

Aligned, confirmable, time-bound. It turns out design is a goal like any other. It just needed a definition before it could get better. My first attempt didn't fail because I have no taste. It failed because I never told myself what "good" meant.
