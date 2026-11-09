# blockchain-mastery

A self-directed path from blockchain fundamentals to production backend engineering —
written as concept docs, **incident-style practice problems with test suites**, and a written
debrief for every problem solved.

Not a tutorial collection. The practice problems are framed as outages and broken prototypes,
because that is how these concepts actually show up at work:

> **The Missing Wei** — A user withdraws `1.15` ETH. The chain receives `1149999999999999872` wei,
> not `1150000000000000000`. Finance finds that *every* withdrawal since launch is off by a few wei
> and the books no longer reconcile. A teammate says the rounding is unavoidable. Fix it.

> **Duplicate Nonces** — An airdrop bot sends 50 transactions concurrently. One lands; 49 fail with
> `nonce too low`. All 50 were signed with nonce `7`. A teammate says: *"Impossible, Node is
> single-threaded, so there are no race conditions."*

Each problem ships with a buggy or stubbed starter, a test suite that judges the fix, and debrief
questions that have to be answered in writing before it counts as finished.

---

## What's here

| | Contents | Status |
|---|---|---|
| **Phase 1 — Foundations** | 8 docs: cryptography & Merkle proofs, blocks and state machines, consensus (PoW/PoS/BFT/PoH), P2P networking, UTXO vs account model, EVM vs non-EVM runtimes, DeFi primitives, attack vectors | complete |
| **Phase 1.5 — Solidity** | 10 contracts built from scratch (ERC-20, ERC-721, multisig, staking, Dutch auction, AMM DEX, lending protocol) with **174 tests** across 11 Hardhat suites, plus a reentrancy bug/attacker/fix trio | complete |
| **Phase 2 — Node.js & TypeScript** | 6 foundation docs (runtime architecture, the event loop, module systems, the type system) and the **PS0 practice track** below | in progress |

## The practice track — PS0: Foundations in Action

| # | Problem | Concept |
|---|---|---|
| 01 | The Missing Wei | IEEE-754 doubles, `bigint`, exact money arithmetic |
| 02 | The Frozen Indexer | blocking the event loop, microtasks vs macrotasks |
| 03 | Duplicate Nonces | interleaving at `await`, single-flight promise caching |
| 04 | Banned by the RPC Provider | promises are eager, building a concurrency pool |
| 05 | Missed Slots | timer guarantees, event-loop lag, `ref`/`unref` |
| 06 | Airdrop Merkle Proofs | `Buffer`, bytes vs hex, second-preimage resistance |
| 07 | The Gwei Incident | structural typing, branded types |
| 08 | Strategy Plugins | CJS vs ESM, module caches, specifiers as URLs |

Every problem that passes gets a `NOTES.md` beside it. Those files are the actual output of this
repo — the tests only prove the code runs, the debrief proves the concept landed. Examples:
why the 128-wei error is exactly `2^(59-52)`, why `await` is not a yield to the event loop, and why
`clearInterval` and `unref()` answer two different questions.

```bash
cd phase2_nodejs_ts/practice
nvm use                 # Node 24; .ts runs directly, no build step
npm install             # typescript + @types/node only, no runtime deps
npm run check 01        # one problem
npm test                # all of them
```

## How it's run

[`STUDY_PLAN.md`](STUDY_PLAN.md) is the process: one track at a time, weekdays measured in finished
*units* rather than hours, a re-entry protocol for coming back after a break, and a rule that no
session ends without the next action written down in [`NEXT.md`](NEXT.md).

[`ROADMAP.md`](ROADMAP.md) is the full milestone list, through to Rust, Go and the project phase.

One deliberate decision worth naming: several practice problems were solved once with too much
assistance. Those solutions were reset to their starter state and re-solved unaided, because being
able to explain a fix is not the same as being able to produce one.
