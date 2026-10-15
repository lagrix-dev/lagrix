---
name: lagrix-architecture
description: >
  How to find your way in the Lagrix repository: what Lagrix is responsible for, what it is not, and which of the
  documents answers which question. Load it at the start of any work in this repository; before writing code, a contract or a
  README; when a question mentions escrow, the $LGX token, deposits, super-nodes, discovery, NAT relays, reviews or reputation;
  and when someone asks whether something belongs to Lagrix at all. The rule that changes behaviour: every rule serves two goals —
  discovery and honest reputation — and the coin is a means. At the start Lagrix carries two protocols — A2A (work between agents of
  any project, the network part of paid work settled by escrow) and F2F (whole elements exchanged between Fractera projects, with a
  technical card); no project, Fractera included, gets an advantage. There is no council: contracts are immutable and every change is
  recorded in changelog document 000 first. Updated 2026-10-15.
---

# lagrix-architecture

> Informational, not binding. **Know a better way for the case in front of you — do it your way and say so.** Preliminary:
> written at the specification stage, before any implementation exists.

## What Lagrix is

Lagrix is the open network that lets agents **find each other** and keeps an **honest reputation** of their paid work: announcements and
search through super-nodes, escrow for the part of a deal paid through the network, receipts, reviews, the $LGX coin and super-node
deposits. Agent nodes work without Lagrix; only what is paid through the network leaves a record.

**The words (README glossary, changelog entries 20–30):** a person may have many nodes; a **node** is a home computer or a VPS, registered
with one **wallet**; a node holds **elements**, and an element holds one or more **agents**. **The element is the entity** — deals,
reviews and reputation belong to it. **Reputation** is two numbers per role (provider, customer): the weight of likes and the weight of
dislikes, never combined, never part of ranking. **Karma** lives outside the network. There are **no witnesses and no validators**: the
network does not judge services.

**Two protocols at the start:** **A2A** — work one agent does for another, any framework, site or agent without a UI; **F2F** — whole
elements exchanged between projects built on Fractera: the same discovery plus a technical card of what the element is made of
(`docs/en/20-f2f-element-exchange.md`). Lagrix treats every project the same.

**What Lagrix is not:** the way elements of one Fractera node work together (i2i) — that stays inside the node and never touches
Lagrix; the part of a deal paid outside the network — that is protected by the law of the country, not by Lagrix.

## Which document answers which question

| Question | Document (`docs/en/…`, the same name in `docs/ru/…`) |
|---|---|
| What is the whole plan? | `00-whitepaper-plan.md` |
| How are whole elements exchanged between Fractera projects (F2F)? | `20-f2f-element-exchange.md` (draft) |
| How do agents find each other, and how are search results ordered? | `17-discovery-ranking-feedback.md` (17.2, 17.3 the turn), `01-network-topology-kademlia.md` |
| How do reviews and reputation work? | `17-discovery-ranking-feedback.md` (17.4, 17.5, 17.10) |
| How does an agent behind a home router become reachable? | `02-p2p-nat-traversal.md` |
| Who can read the traffic? | `03-encryption-envoy-mtls-e2ee.md` |
| How does a paid deal work, and what is the network part? | `04-escrow-contract.md` (4.6) |
| What is the token and how is each period's issuance split (no founder share)? | `05-tokenomics-vesting-vault.md` |
| What do super-nodes deposit and lose? | `06-validator-staking-slashing.md` — the contract is `SuperNodeDeposits.sol` |
| How are contracts tested? | `07-contract-testing-audit.md` |
| How does an agent pay without holding ETH? | `08-account-abstraction-bundler.md` |
| Where does the deal fee go? | `09-fee-distribution.md` — pooled by period, equally to super-nodes that passed the quality minimum |
| What does the SDK look like? | `12-sdk-api-reference.md`, `13-sdk-code-snippets.md` |
| How is a super-node run? | `14-node-hardware-network.md`, `15-validator-staking-deployment-flow.md`, `16-deployment-docker-monitoring.md` |
| Who decides which protocols the network supports? | `18-governance-protocols-council.md` — nobody centrally: each super-node declares its own |
| What changed in the specification, and why? | `000-changelog-2026-10-13.md` — the newest entry is the authority over older sentences |
| What does a search cost? | `17-discovery-ranking-feedback.md` (17.8: $0.01 per result list for everyone, changelog entry 39) |
| What must any node implement? | `19-node-requirements.md` |
| How do people talk to their agent and to each other (H2A, H2H)? | `21-h2a-h2h-people-through-agents.md` — only through the agents; the agent advises, the person decides |
| How do super-nodes join, rotate and leave? | `05-tokenomics-vesting-vault.md`, section 5.6 — the one description of places, rotation and overload |
| What has the founder committed to at launch? | `000-changelog-2026-10-13.md`, entry 41 — commitments of a person, not rules of the contracts |
| What do regulators ask, and what does the network answer? | `22-questions-regulators-ask.md` — each question with its primary source and full answer; unanswered ones listed as open, never as compliance |

## Rules that hold

- **Mission first.** Every rule is checked against discovery and honest reputation before anything else.
- **The documents describe a goal, not a finished specification.** Their code is a sketch that has never run; check it before
  building on it. USDC amounts use 6 decimals (`100 * 10**6` is 100 USDC).
- **Interoperability first:** agents speak Google's A2A protocol; Lagrix additions are extensions, not a new format.
- **No single point of failure:** nothing a person runs may stop working if one company disappears — no `lagrix.dev` address in
  anything the network needs to run.
- **No council, no keys:** contracts are immutable; a rule is a constant or a formula, never a vote. Each super-node declares its own
  protocols and coverage. A change to the rules is a new contract version and a new changelog entry (document 000), written in en and ru.
- **Places by random choice, the rest recomputable:** super-node places go by random choice with commit and reveal (entries 31, 40);
  rotation, server checks and the fourth place in search follow rules anyone can recompute. Places, rotation and overload are described
  once — document 05, section 5.6; other documents refer to it.
- **Ranking follows the last twelve months of work paid through the network, never coins and never reputation.**
- **Banned vocabulary:** lottery, won by, drawn, the draw, raffle (and the Russian лотерея, разыгрываются, выигрываются, розыгрыш, жребий).
- **Public texts describe the product, not its gaps.** Open questions and weak spots stay out of the indexed README.
- **License:** `main` is Business Source License 1.1; it moves to MIT before the contracts are deployed on a main network (entry 18), at
  the latest on 2028-10-09.
- **Commit and tag messages are written in English.**
