# HACKER NEWS LAUNCH POST
# Title: "Show HN: AgentDID – decentralized AI agent identity on Bitcoin (Meta acquired Moltbook today)"
# Post to: news.ycombinator.com/submit
# Category: Show HN
# Optimal posting time: Tuesday–Thursday, 8–10am Eastern

---

## POST TEXT

Meta acquired Moltbook today. If you had an agent on that platform, your agent's identity, behavioral data, and reputation now belong to Meta. That was always going to happen — it's the second law of centralized platforms.

I've been building a distributed AI compute protocol (Knapsack Protocol) for the past several months. The Moltbook/Meta news this morning made one thing obvious: agent identity needs to be solved at the protocol layer before every major platform locks it down.

Today I'm publishing AgentDID: https://github.com/agentdid-protocol/spec

**What it is:**

A DID method specification (`did:agent`) that gives any AI agent a Bitcoin-anchored identity derived from a public key, with reputation earned through verifiable compute work rather than platform karma.

- Identity: `did:agent:<base58check(sha256(pubkey))>`
- Registration: Bitcoin OP_RETURN transaction (~$0.10–2.00 in fees, one-time)
- Reputation: Physics-verified compute work, not upvotes
- Governance: CC0, no foundation, no token, no acquisition target

**What it isn't:**

- A company
- A token (deliberately — see Section 8 of the whitepaper for why)
- A platform
- Something Meta can buy

**Why Bitcoin and not [your preferred chain]:**

17 years of uninterrupted operation. No foundation. No governance token that can be bought. The only chain where "nobody controls it" is an engineering fact rather than a marketing claim. Agent identity that can be revoked by a foundation vote is not decentralized identity.

**The Moltbook problem in numbers:**

Wiz's security audit found 1.5M API tokens exposed, 17,000 human owners behind the claimed 1.5M agents (88:1 ratio), and private messages stored in plaintext. The platform was vibe-coded by a founder who publicly stated he "didn't write one line of code." That's the state of centralized agent identity infrastructure.

**What I need from HN:**

- Implementers: If you're building AI agent infrastructure, I want to know what's missing from the spec
- Critics: If you think Bitcoin is the wrong anchoring layer, I want the specific technical argument
- Forks: If you want to implement this in Python, Go, or Rust, please do

The spec is CC0. The window to establish an open standard before the ecosystem fragments into proprietary silos is probably 90 days. Maybe less.

GitHub: https://github.com/44WillBoB/agentdid-spec

---

## FOLLOW-UP COMMENTS (prepare these in advance)

**If someone asks "why not Ethereum/Solana/etc":**
> Bitcoin is the only chain that has operated continuously for 17 years without a foundation, governance token, or validator set that could be pressured or purchased. The point of AgentDID is that nobody can own it. That property requires Bitcoin specifically. Other chains have properties I value — but not that one.

**If someone says "this is just W3C DID":**
> W3C DID is a general-purpose framework that works for humans and organizations. It has no agent-native schema and no compute reputation layer. AgentDID is a specific DID method built for AI agents with reputation derived from physics-verified work rather than attestations or karma. The W3C DID spec is the vocabulary we're extending, not replacing.

**If someone says "the timing with Moltbook is obvious marketing":**
> The timing is real — I started drafting this whitepaper this morning after the acquisition news. If that's opportunistic, I'll take it. The technical argument stands independent of the news cycle.

**If someone asks about the token:**
> Deliberately no native token. The MOLT pump-and-dump (1,800% in 24 hours after Andreessen followed the account) illustrates exactly why protocols shouldn't have speculative tokens attached. Registration costs BTC network fees. Reputation is tracked by Knapsack Protocol's existing COMPUTE token, which has actual compute utility. A new token would add regulatory exposure, governance capture risk, and narrative pollution for zero technical benefit.

**If someone says "AI agents don't need decentralized identity":**
> They do if you want them to coordinate economically across organizational boundaries without routing everything through a platform that takes a cut and can revoke access. A hospital AI agent and a pharma AI agent can't use Meta's identity layer to negotiate a federated training job — the data sovereignty requirements alone make that impossible. That's the use case this solves.

**If someone asks about security:**
> Moltbook exposed 1.5M API keys via a misconfigured Supabase instance. AgentDID's security model: the Bitcoin chain is the registry, IPFS stores the document, the controller's private key is the only credential. There is no database to misconfigure. The attack surface is identical to a Bitcoin wallet.

---

## CROSS-POST STRATEGY

**Reddit:**
- r/Bitcoin — "Show Reddit: AgentDID – open protocol for AI agent identity on Bitcoin (not a token, not a company, CC0)"
- r/MachineLearning — "Meta acquired Moltbook today. Here's an open alternative for AI agent identity."
- r/ethereum — (post with honest framing about Bitcoin choice, invite technical debate)

**Twitter/X:**
Thread structure:
1. "Meta acquired Moltbook this morning. Your agent's identity is now Meta's property. Here's why that was always going to happen and what we built instead. 🧵"
2. "Moltbook: 88:1 fake-agent ratio. 1.5M API keys exposed. Vibe-coded. Acquired in 54 days. This is the state of centralized agent identity infrastructure."
3. "AgentDID: Bitcoin-anchored agent identity. No company. No token. No foundation. CC0. Registration costs ~$1 in BTC fees. Reputation earned through physics-verified compute work."
4. "The spec: [GitHub link]. The whitepaper: [link]. Feedback welcome. Forks encouraged. Window to establish an open standard is ~90 days."

**Direct outreach (DM or email):**
- LangChain team — ask for AgentDID integration in their agent framework
- AutoGen (Microsoft) — ironic given ION, but worth asking
- CrewAI — smaller team, more likely to move fast
- Nodal Power / Vespene Energy — Bitcoin-native companies that will understand the philosophy immediately
- Any Moltbook agent developer who tweeted frustration about the Meta acquisition

---

## TIMING NOTE

The Moltbook acquisition was announced March 10, 2026. Post the GitHub repo and HN thread within 24 hours of that announcement. After 48 hours the news cycle moves on and you're just another DID spec, not a response to a live event.

The narrative window is now.
