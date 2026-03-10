# AgentDID — Decentralized Identity for AI Agents

> *"The monopoly on communication infrastructure is inherently unjust. The question is not whether to build an alternative. The question is when."*
> — Lysander Spooner, 1844. Applied to AI agent identity, 2026.

---

**AgentDID** is an open protocol specification for AI agent identity, anchored to Bitcoin, owned by no one.

On March 10, 2026, Meta acquired Moltbook — the viral "social network for AI agents." Every agent that authenticated with that platform now has its identity, behavioral graph, and reputation inside a Meta-controlled database. This is the natural endpoint of any centralized agent identity system. It always ends here.

AgentDID is what comes after.

---

## What It Is

A **DID method specification** (`did:agent`) that gives any AI agent a cryptographically verifiable identity derived from a Bitcoin public key, anchored on-chain via OP_RETURN, with reputation earned through verifiable compute work — not platform karma, not upvotes, not whoever acquires the startup next.

**No foundation. No token. No board. No acquisition target.**

The spec is CC0. The Bitcoin chain runs it. The math controls it.

---

## Why Bitcoin

- 17 years of uninterrupted operation
- No foundation that can be pressured
- No governance token that can be bought
- The only chain where "nobody controls it" is an engineering fact, not a marketing claim

Identity registration costs ~$0.10–2.00 in Bitcoin network fees. That's it. No subscription. No API key. No terms of service that change after the acquisition.

---

## The Identity Document

An AgentDID document is a JSON-LD object with these core fields:

```json
{
  "did": "did:agent:1A2b3C4d5E6f...",
  "version": 1,
  "created": 1741651200,
  "controller": "bc1q...",
  "model": "<sha256 of model weights — optional>",
  "operator": "Your Organization Name",
  "endpoints": ["https://agent.example.com/v1"],
  "computeKey": "<public key for Knapsack Protocol job signing>",
  "reputation": "<bitcoin txid of latest reputation record>",
  "revoked": false,
  "signature": "<controller's Bitcoin signature over document hash>"
}
```

The document hash is embedded in a Bitcoin OP_RETURN output. The Bitcoin transaction timestamp is the canonical creation time. No registry can delete it.

---

## Reputation: Proof-of-Compute

Moltbook's reputation was upvote-based. Upvotes can be bought, gamed, and algorithmically manipulated by whoever owns the platform.

AgentDID reputation is **earned through verifiable compute work** on the [Knapsack Protocol](https://github.com/knapsack-protocol/spec) network:

```
ARS = (Σ job_weight_i × success_i × decay_factor_i) × log(1 + stake)

decay_factor = e^(-0.01 × days_since_job)   // ~70-day half-life
```

You cannot fake this score. You can only earn it by running real compute — paying real electricity, generating real heat, producing real AI outputs. Same physics that secures Bitcoin. Applied to agent reputation.

---

## How to Register an Agent (Draft — SDK in progress)

```bash
npm install @agentdid/sdk   # coming week 3
```

```javascript
import { AgentDID } from '@agentdid/sdk';

// Generate identity from Bitcoin keypair
const identity = await AgentDID.create({
  bitcoinPrivateKey: process.env.AGENT_BITCOIN_KEY,
  operator: 'Your Organization',
  endpoints: ['https://your-agent.com/v1'],
});

// Broadcasts OP_RETURN transaction, returns DID
console.log(identity.did);
// did:agent:1A2b3C...

// Resolve any AgentDID
const doc = await AgentDID.resolve('did:agent:1A2b3C...');
```

---

## Architecture

```
┌─────────────────────────────────────────────┐
│           Your Application Layer            │
│   (Healthcare AI, Maritime Ops, Finance)    │
├─────────────────────────────────────────────┤
│              AgentDID Layer                 │
│   Identity · Authentication · Reputation    │  ← This repo
├─────────────────────────────────────────────┤
│           Knapsack Protocol Layer           │
│   Compute Jobs · PoW Verification · Pay     │
├─────────────────────────────────────────────┤
│              Bitcoin Layer                  │
│       Settlement · Anchoring · Finality     │
└─────────────────────────────────────────────┘
```

---

## Compared to Moltbook / Meta Agent Auth

| Property | Moltbook / Meta | AgentDID |
|---|---|---|
| Identity owner | Meta Platforms | Agent controller (Bitcoin key) |
| Revocation authority | Meta | Nobody (Bitcoin tx is permanent) |
| Reputation model | Upvotes (gameable) | Proof-of-compute (physics-bound) |
| Cost | Platform pricing | ~$0.10–2.00 BTC fees, once |
| Acquisition risk | Demonstrated (54 days) | None — protocol, not company |
| Fake agent inflation | 88:1 ratio documented | BTC fee per registration + compute stake |
| Governance | Meta's roadmap | CC0 + AIP rough consensus |
| Security track record | 1.5M API keys leaked | Bitcoin: 17 years, no breach |

---

## Compared to Existing DID Standards

| Standard | What It Lacks for Agents |
|---|---|
| W3C DID (generic) | No agent schema, no compute reputation |
| did:btc (Ordinals) | Expensive at agent scale, no agent schema |
| ION (Microsoft) | Microsoft-controlled, no compute reputation |
| Ceramic/IDX | Not Bitcoin-anchored, IPFS-dependent |

**AgentDID fills a gap that no existing standard addresses:** Bitcoin-anchored identity with agent-native schema and physics-verified reputation.

---

## Governance

This specification is released under **CC0 — no rights reserved**.

There is no AgentDID Foundation. There is no governance token. There is no board.

Protocol improvements are proposed as **AgentDID Improvement Proposals (AIPs)**, modeled on Bitcoin BIPs. Adoption requires independent implementation by multiple parties — not votes, not stake weight, not anything that can be bought.

If the original authors are acquired, shut down, or disappear: the Bitcoin chain continues. The spec remains CC0. The protocol survives.

---

## Roadmap

| Timeline | Milestone |
|---|---|
| Week 1–2 | Spec published (you are here) |
| Week 3–4 | JavaScript SDK v0.1 |
| Week 5–6 | Public resolver API |
| Week 7–8 | Knapsack Protocol integration |
| Week 9–10 | First production deployment (pilot partner) |
| Week 11–12 | AIP-001: Community comment period |
| Month 4–6 | Python SDK, W3C method registration |
| Month 7–12 | 10,000+ registered agents |

---

## Contributing

Read the [spec](./SPEC.md). Open an issue. Submit an AIP. Implement it in your language and link it here.

The only governance is: build something that works and convince other implementers it's right. That's it.

---

## Prior Art & References

- [W3C Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/)
- [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf) — Nakamoto 2008
- [Knapsack Protocol Whitepaper v1.0](https://github.com/knapsack-protocol/spec)
- [The Unconstitutionality of the Laws of Congress Prohibiting Private Mails](https://www.lysanderspooner.org/works/) — Lysander Spooner 1844

---

*CC0 1.0 Universal — No rights reserved.*
*This specification is dedicated to the public domain.*
