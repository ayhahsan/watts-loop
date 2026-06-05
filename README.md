# Watt's Loop

**A Framework for Cross-Domain Analogical Innovation in Continually-Exposed AI Assistants**

*Ayhahsan Ansari — Independent Researcher, Delhi, India*

---

> **Status:** This is a research *proposal* — an architecture and a set of testable predictions. There is no implementation or empirical result yet. It is published openly to share the idea and invite critique.

## What is this?

James Watt didn't derive the separate-condenser steam engine from first principles. He spent months noticing how pressure behaved across unrelated everyday contexts — kettles, distillation gear, demonstrations he happened to see — and then recognized that the same structure solved a completely different problem: the wasteful Newcomen engine. That move — taking a pattern from domain A and dropping it into domain B — sits behind a huge fraction of major breakthroughs (Kekulé's benzene ring, Darwin borrowing from Malthus, Velcro from burrs).

Modern AI assistants are continuously exposed to wildly heterogeneous streams — your messages, social feeds, papers, news, whatever you browse. They have the *raw material* Watt had. What they lack is an explicit architectural commitment to **opportunistic cross-domain transfer**.

**Watt's Loop** proposes building that habit in on purpose: a background process that continuously turns exposure into domain-agnostic patterns, and quietly checks whether any of those patterns happen to solve a problem the user is currently stuck on — then verifies the connection before surfacing it.

## The four stages

1. **Pattern extraction** — heterogeneous inputs (text, audio, vision, conversation) are summarized into their *underlying mechanism*, with surface details stripped out.
2. **Domain-agnostic abstraction** — those structural summaries become embeddings in a shared space, so the same idea from different domains lands close together.
3. **Cross-domain matching** — active user problems are matched against stored patterns, with *larger* domain gaps boosted, to avoid collapsing into ordinary retrieval.
4. **Computational verification** — proposed analogies are tested (sandboxed code, formal prover, or a falsifiable user-mediated prediction) *before* anything reaches the user. Bad analogies die quietly in a log.

## The core loop (pseudo-code)

This is Algorithm 1 from the paper — the central cycle.

```
Algorithm 1: Watt's Loop Main Cycle

Input:      threshold theta, exposure stream E, user problem set P
Persistent: pattern store M, problem cache C, verification log V

while system active:
    e  <- Observe(E)                       # ingest one exposure observation
    phi_e <- Phi(e)                         # abstract to domain-agnostic form
    Insert phi_e into M with temporal index

    P_active <- ActiveProblems(C)
    for each p in P_active:
        phi_p <- Phi(p)                     # cached when possible
        sigma <- mu(phi_e, phi_p)           # structural similarity

        if sigma > theta:
            h <- HypothesisGen(phi_e, phi_p)   # candidate adaptation
            v <- Verify(h, p)                  # sandbox / prover / user test
            if v.success:
                Report(user, <e, p, h, v>)     # surface verified analogy
            Append <e, p, h, v> to V           # log all attempts (incl. failures)
```

Three properties matter:

- **Persistent & asynchronous** — a match may occur long after either the exposure or the problem entered the system.
- **Verification before reporting** — LLMs hallucinate plausible-but-false analogies; only verified ones are surfaced.
- **Full logging** — every attempt, including failures, is retained to support meta-learning over the system's own analogical performance.

### Domain-distance boosting

To stop the matcher from collapsing into ordinary retrieval, matches that span a larger domain gap are prioritized:

```
sigma'(phi_e, phi_p) = mu(phi_e, phi_p) * (1 + lambda * d_dom(phi_e, phi_p))
```

where `d_dom` is a categorical distance over coarse domain labels (e.g. "biology" vs. "software engineering") and `lambda` is a tunable weight favoring distant transfer.

## What's in this repo

- `Watts_loop_paper.pdf` — the full paper (formal definition, architecture, three case studies, the proposed Distant-Domain Transfer Benchmark, limitations, ethics, and roadmap).

## Honest limitations

- **Novelty ceiling** — it can only connect patterns it has actually been exposed to. Exposure breadth is the whole ballgame.
- **Hallucinated analogies** — verification catches a lot, not everything, especially claims needing real-world evidence.
- **Mirrors your bubble** — feeds encode a cultural/demographic distribution; "novel" connections may just be routine in traditions the system never sees.
- **Not new ground** — cross-domain analogy is a decades-old research area. The contribution here is a specific *architecture* for always-on assistants, not the underlying idea.

## Feedback

If you think this is wrong, or already done better somewhere, open an issue — that's exactly the feedback I'm looking for.

## Citation

```
@misc{ansari2026wattsloop,
  author = {Ansari, Ayhahsan},
  title  = {Watt's Loop: A Framework for Cross-Domain Analogical Innovation in Continually-Exposed AI Assistants},
  year   = {2026},
  note   = {Independent research preprint}
}
```
