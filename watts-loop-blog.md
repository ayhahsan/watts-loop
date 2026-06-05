---
title: "Watt's Loop: Can an AI Assistant Have a Eureka Moment?"
published: false
tags: ai, machinelearning, llm, research
---

## The question that started this

James Watt didn't invent the separate-condenser steam engine by sitting down and deriving it from physics. He'd spent months noticing pressure behaving in kettles, in distillation gear, in random demonstrations he happened to walk past. The actual breakthrough reportedly hit him during a walk in Glasgow Green. He took a *structure* he'd seen in one place and dropped it into a completely different problem.

That pattern - seeing something in domain A and recognizing it solves a problem in domain B - is behind a huge fraction of the big leaps in science. Kekule's benzene ring, Darwin borrowing from Malthus, Velcro coming from burrs stuck to a dog. We call it a "eureka moment," but it's really just cross-domain pattern transfer.

So here's the question I got stuck on: today's AI assistants are *constantly* exposed to wildly different streams of information - your messages, social feeds, papers, news, whatever you're browsing. They have the raw material Watt had. What they're missing is the *habit* of deliberately moving a pattern from one domain into another.

What if we built that habit in on purpose?

I wrote up a framework for it. I'm calling it **Watt's Loop**. This post is the plain-language version.

> Upfront honesty: this is a **proposal**, not a finished system. No experiments yet, no results. It's an architecture and a set of testable predictions. I'm publishing it to get the idea out and find out where it breaks.

## The core idea in one line

> An AI assistant that runs a background process continuously turning everything it's exposed to into abstract patterns, and quietly checks whether any of those patterns happen to solve a problem you're currently stuck on.

The key word is **opportunistic**. Most analogy systems work inside a single problem-solving session: you ask, it answers. Watt's Loop is meant to run in the background and surface a connection *days* after you mentioned a problem, the moment a useful pattern floats by in your feed.

## How it actually works (four stages)

**1. Pattern extraction.** Everything coming in - text, your conversations, audio, images - gets run through a small local model that writes a short description of the *underlying mechanism*, with the surface details stripped out. Not "ants leave pheromone trails" but "agents balance exploiting known good spots against exploring new ones, guided by feedback-weighted memory."

**2. Abstraction.** That stripped-down description gets turned into an embedding and stored. Now it's domain-agnostic - the "ant" version and a "network routing" version of the same idea land near each other.

**3. Cross-domain matching.** Your active problems are compared against the stored patterns. The trick: matches that cross a *bigger* domain gap get boosted. We don't want the system collapsing into ordinary search ("you asked about Python, here's a Python answer"). We want the weird, distant jumps - that's where the eureka lives.

**4. Verification.** This is the part that keeps it honest. LLMs hallucinate plausible-but-wrong analogies all day. So before anything reaches you, the proposed connection gets *tested* - run the code, check it against a prover, or hand you a clear falsifiable prediction to try. Only verified connections get surfaced. The bad analogies die quietly in a log.

## What it might look like in practice

You're building a web scraper that keeps getting rate-limited and banned. Last week you watched a few videos about how ants forage - balancing going back to known food sources vs. scouting new territory.

A week later the system connects the two: your scraper is an exploration-vs-exploitation problem over URL space. It adapts the foraging strategy into a scheduling policy, tests it in a sandbox against your current scraper, and only then tells you: *"Those ant videos suggest a scheduling approach that improved yield and cut bans in offline testing - want to try it?"*

That's the eureka pattern, engineered.

## Where it breaks (the honest part)

- **The novelty ceiling.** It can only connect patterns it has actually been exposed to. Analogies from domains it never saw are just unavailable. Exposure breadth is the whole ballgame.
- **Hallucinated connections.** Verification catches a lot, but not everything - especially claims that need real-world evidence. Some surfaced ideas will turn out to be nonsense.
- **It mirrors your bubble.** If your feeds are all Western English-language tech content, the "novel" connections it finds may just be things that are routine in traditions it never sees.
- **It's not actually new ground.** Cross-domain analogy is a decades-old research area. My contribution is a specific *architecture* for it in always-on assistants, not the underlying idea.

## Why I wrote this

I'm an independent dev building a personal AI assistant under tight resource constraints. This framework came out of exactly the kind of cross-domain reflection it describes - a historical story, a current technical opening, and a problem I was personally chewing on. If it ends up working, the people it helps most are independent builders, the same group that's historically punched above its weight on cross-domain insight while sitting outside formal research labs.

Full write-up with the formal definition, pseudo-code, case studies, and a proposed benchmark is here: [link to GitHub repo / PDF].

If you think this is obviously wrong or obviously already done better somewhere, tell me - that's exactly the feedback I'm looking for.
