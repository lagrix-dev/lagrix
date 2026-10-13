---
name: lagrix-architecture
description: >
  How to find your way in the Lagrix repository: what Lagrix is responsible for, what it is not, and which of the
  documents answers which question. Load it at the start of any work in this repository; before writing code, a contract or a
  README; when a question mentions escrow, the $LGX token, staking, super-nodes, discovery, NAT relays or reputation;
  and when someone asks whether something belongs to Lagrix at all. The rule that changes behaviour: at the start Lagrix carries two protocols —
  A2A (work between agents of any project, paid work settled by escrow) and F2F (whole elements exchanged between Fractera
  projects, with a technical card); no project, Fractera included, gets an advantage. Since 2026-10-13 there is no council:
  contracts are immutable and every change is recorded in a changelog document 000 first. Updated 2026-10-13.
---

# lagrix-architecture

> Informational, not binding. **Know a better way for the case in front of you — do it your way and say so.** Preliminary:
> written 2026-10-09 at the specification stage, before any implementation exists.

## What Lagrix is

Lagrix is the **external** architecture that settles **paid work between AI agents** (A2A) with blockchain transactions: escrow,
receipts, the $LGX token, staking of super-nodes, reputation. Agent nodes work without Lagrix; only paid deals go through it.

**Two protocols at the start** (2026-10-11): **A2A** — work one agent does for another, any framework, site or agent without a UI;
**F2F** — whole elements exchanged between projects built on Fractera: the same discovery plus a technical card of what the element
is made of (`docs/en/20-f2f-element-exchange.md`). Lagrix treats every project the same. 🪦 «M2M is never Lagrix's concern»
(2026-10-09) is cancelled. Where documents 08, 12 and 13 say «M2M», they mean generic machine-to-machine traffic (gRPC), not a
Fractera protocol.

**What Lagrix is not:** the way elements of one Fractera node work together (i2i) — that stays inside the node and never touches
Lagrix.

## Which document answers which question

| Question | Document (`docs/en/…`, the same name in `docs/ru/…`) |
|---|---|
| What is the whole plan? | `00-whitepaper-plan.md` |
| How are whole elements exchanged between Fractera projects (F2F)? | `20-f2f-element-exchange.md` (draft) |
| How do agents find each other, and how are search results ordered? | `17-discovery-ranking-feedback.md`, `01-network-topology-kademlia.md` |
| How does an agent behind a home router become reachable? | `02-p2p-nat-traversal.md` |
| Who can read the traffic? | `03-encryption-envoy-mtls-e2ee.md` |
| How does a paid deal work? | `04-escrow-contract.md` |
| What is the token and how is each period's issuance split (no founder share)? | `05-tokenomics-vesting-vault.md` |
| What do super-nodes stake and lose? | `06-validator-staking-slashing.md` |
| How are contracts tested? | `07-contract-testing-audit.md` |
| How does an agent pay without holding ETH? | `08-account-abstraction-bundler.md` |
| Where does the deal fee go? | `09-fee-distribution.md` |
| What does the SDK look like? | `12-sdk-api-reference.md`, `13-sdk-code-snippets.md` |
| How is a super-node run? | `14-node-hardware-network.md`, `15-validator-staking-deployment-flow.md`, `16-deployment-docker-monitoring.md` |
| How are likes and dislikes protected from bots? | `17-discovery-ranking-feedback.md` |
| Who decides which protocols the network supports? | `18-governance-protocols-council.md` — nobody centrally: each super-node declares its own |
| What changed in the specification, and why? | `000-changelog-<date>.md` — the newest changelog is the authority over older sentences |
| What does a search cost, and how is ranking computed? | `17-discovery-ranking-feedback.md` (sections 17.2, 17.8, 17.9) |
| What must any node implement? | `19-node-requirements.md` |
| How do people talk to their agent and to each other (H2A, H2H)? | `21-h2a-h2h-people-through-agents.md` — only through the agents; the agent advises, the person decides |
| What do regulators ask, and what does the network answer? | `22-questions-regulators-ask.md` — each question with its primary source and full answer; unanswered ones listed as open, never as compliance |

## Rules that hold

- **The documents describe a goal, not a finished specification.** Their code is a sketch that has never run; check it before
  building on it. USDC amounts use 6 decimals (`100 * 10**6` is 100 USDC).
- **Interoperability first:** agents speak Google's A2A protocol; Lagrix additions are extensions, not a new format.
- **No single point of failure:** nothing a person runs may stop working if one company disappears — no `lagrix.dev` address in
  anything the network needs to run.
- **No council, no keys:** contracts are immutable; a rule is a constant or a formula, never a vote. Each super-node declares its own
  protocols and coverage. A change to the rules is a new contract version and a new changelog entry (document 000), written in en and ru.
- **Ranking follows the last twelve months of paid work, never coins.** The coin is an asset and a super-node's deposit.
- **Public texts describe the product, not its gaps.** Open questions and weak spots stay out of the indexed README.
- **License:** `main` is Business Source License 1.1, MIT from 2028-10-09.
- **Commit and tag messages are written in English.**
