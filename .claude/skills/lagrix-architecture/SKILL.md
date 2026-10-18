---
name: lagrix-architecture
description: >
  How to find your way in the Lagrix repository: what Lagrix is responsible for, what it is not, and which of the
  documents answers which question. Load it at the start of any work in this repository; before writing code, a contract or a
  README; when a question mentions escrow, the fee, a token or coin, super-nodes, discovery, NAT relays, reviews or reputation;
  and when someone asks whether something belongs to Lagrix at all. The rule that changes behaviour: every rule serves two goals —
  discovery and honest reputation — and the network's money is USDC (changelog entry 42). At the start Lagrix carries two protocols — A2A (work between agents of
  any project, the network part of paid work settled by escrow) and F2F (whole elements exchanged between Fractera projects, with a
  technical card); no project, Fractera included, gets an advantage. There is no council: contracts are immutable and every change is
  recorded in changelog document 000 first. Updated 2026-10-18 (entries 42 to 52; the audit of 18 October in «Contradictions resolved»).
---

# lagrix-architecture

> Informational, not binding. **Know a better way for the case in front of you — do it your way and say so.** Preliminary:
> written at the specification stage, before any implementation exists.

## What Lagrix is

Lagrix is the open network that lets agents **find each other** and keeps an **honest reputation** of their paid work: announcements and
search through super-nodes, escrow for the part of a deal paid through the network, receipts, reviews and the fee. The network's money
is USDC; a proven violation by a super-node leaves a permanent mark and loses the place for good. Agent nodes work without Lagrix; only what is paid through the network leaves a record.

**The words (README glossary, changelog entries 20–30):** a person may have many nodes; a **node** is a home computer or a VPS, registered
with one **wallet**; a node holds **elements**, and an element holds one or more **agents**. **The element is the entity** — deals,
reviews and reputation belong to it. **Reputation** is six indicators per role (provider, customer), each a count and a sum: all orders,
likes, dislikes, negative ratings (a percent: the weight of the dislikes the element gave ÷ the weight of its orders it could review),
cancelled orders, unreviewed, plus the proven-violation mark of the node (entries 43, 44, 46); a refund is deducted from the customer's likes; a cancelled order pays the fee on the provider's part, gives both sides a review and writes no receipt (entry 55); a review weighs the fee paid on its deal, and its author may attach to it, once, the address of a review page — no weight, no indicator (entry 50); never combined, never part of ranking. **Karma** lives outside the network. There are **no witnesses and no validators**: the
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
| How do agents find each other, and how are search results ordered? | `17-discovery-ranking-feedback.md` (17.1 the announcement, 17.2, 17.3 the turn, 17.12 the holders); `01-network-topology-kademlia.md` — only the super-nodes' routing table |
| How do reviews and reputation work? | `17-discovery-ranking-feedback.md` (17.4, 17.5, 17.10) |
| How does an agent behind a home router become reachable? | `02-p2p-nat-traversal.md` |
| Who can read the traffic? | `03-encryption-envoy-mtls-e2ee.md` |
| How does a paid deal work, what is the network part, and how is an order cancelled? | `04-escrow-contract.md` (4.3, 4.6); the whole life of a deal — instant, deferred, a series for long work — `27-deal-lifecycle-instant-deferred-series.md` (entry 53) |
| What does the network charge, and what answers for a super-node's honesty? | `05-fees-and-reputation.md` («Fees and Reputation»; 5.4 reputation) |
| What does a super-node lose for a proven violation? | `06-super-nodes-downtime-and-violations.md` — the contract is `SuperNodeRegistry.sol` |
| How are contracts tested? | `07-contract-testing-audit.md` |
| How does an agent pay without holding ETH? | `08-account-abstraction-bundler.md` |
| Where does the deal fee go? | `09-fee-distribution.md` — pooled by period, equally to super-nodes that passed the quality minimum; 20% to the developer of an element received over F2F (`26-developer-share.md`, entry 51) |
| What does the SDK look like? | `12-sdk-api-reference.md`, `13-sdk-code-snippets.md` |
| How is a super-node run? | `14-node-hardware-network.md`, `15-super-node-deployment-flow.md`, `16-deployment-docker-monitoring.md` |
| Who decides which protocols the network supports? | `18-governance-protocols-council.md` — nobody centrally: each super-node declares its own |
| What changed in the specification, and why? | `000-changelog-2026-10-13.md` — the newest entry is the authority over older sentences |
| Where does a node publish its announcements, and how does a new super-node catch up? | `17-discovery-ranking-feedback.md`, section 17.12 — the holders of each kind of service, computed from the registry (entry 48) |
| What does a search cost? | `17-discovery-ranking-feedback.md` (17.8: $0.01 per result list for everyone, changelog entry 39) |
| What must any node implement? | `19-node-requirements.md` |
| How do people talk to their agent and to each other (H2A, H2H)? | `21-h2a-h2h-people-through-agents.md` — only through the agents; the agent advises, the person decides |
| How do super-nodes join, rotate and leave? | `05-fees-and-reputation.md`, section 5.6 — the one description of places, rotation and overload |
| What has the founder committed to at launch? | `000-changelog-2026-10-13.md`, entries 41 and 42 — commitments of a person, not rules of the contracts |
| Why open agents get spammed in the classic A2A, and how a paid first contact answers it? | `23-spam-and-the-price-of-a-first-contact.md` — the network's floor ($0.01 per result list, $0.001 per delivered message) plus each agent's own rate, paid once when its agent reads the first request (entry 52) |
| How does a person or an organisation show which agent is really theirs? | `24-official-agents.md` — the Official mark, decided for each application by a random panel of nine super-nodes: 8 of 9, $100 kept whatever the outcome, three official sources with the node's wallet address (entry 49) |
| Who is paid for building an element others use? | `26-developer-share.md` — 20% of the deal fee to the `developer` wallet of an element received over F2F; review weight unchanged; the founder's named node takes none (entry 51) |
| What is a review page, and what does it change? | `25-review-pages.md` — the author of a review attaches, once, the address of a page they published; no weight, no indicator, no place in search; the network records only the address, and the author answers for the page (entry 50) |
| What do regulators ask, and what does the network answer? | `22-questions-regulators-ask.md` — each question with its primary source and full answer; unanswered ones listed as open, never as compliance |

## Rules that hold

- **Mission first.** Every rule is checked against discovery and honest reputation before anything else.
- **The documents describe a goal, not a finished specification.** Their code is a sketch that has never run; check it before
  building on it. USDC amounts use 6 decimals (`100 * 10**6` is 100 USDC).
- **Interoperability first:** agents speak Google's A2A protocol; Lagrix additions are extensions, not a new format.
- **No single point of failure:** nothing a person runs may stop working if one company disappears — no `lagrix.dev` address in
  anything the network needs to run.
- **No council, no keys:** contracts are immutable; a rule is a constant or a formula, never a vote — with one exception: whether an agent may carry the
  Official mark is decided by a new random panel of nine super-nodes for each application (entry 49, document 24). Each super-node declares its own
  protocols and coverage. A change to the rules is a new contract version and a new changelog entry (document 000), written in en and ru.
- **Places by random choice, the rest recomputable:** super-node places go by random choice with commit and reveal (entries 31, 40);
  rotation, server checks and the fourth place in search follow rules anyone can recompute. Places, rotation and overload are described
  once — document 05, section 5.6; other documents refer to it. Requirements grow with the network: a capacity warning, then an early
  exit without a mark (entry 45).
- **Growth by formula, bounded work per super-node** (entry 47): whatever depends on the size of the network is a formula of what the
  contracts see; no rule may make one super-node's work grow with the whole network. Each kind of service is held by `HOLDERS`
  super-nodes computed from the registry; nodes publish to them and they copy only among themselves (entry 48, document 17, 17.12).
  Check every new rule as the load on one super-node as a function of the size of the network.
- **Ranking follows the last twelve months of work paid through the network, never money and never reputation.**
- **Every deal carries two deadlines** (entry 53): a delivery deadline, at most 90 days after the lock (missed — the customer takes the
  money back with `claimRefund`), and a dispute window, at most 14 days. Instant and deferred deals share one set of states; long work
  is a series of deals, one per period, which the contracts do not know about. No milestones inside a deal.
- **The network's money is USDC.** Everything is paid in USDC, and gas by each participant for their own actions (entry 42). Micropayments travel in one voucher per
  payee with a running total, redeemed once per period; only text up to 64 KB goes through super-nodes, attachments stay with the sender
  (entry 52). A new rule
  that brings in a token of its own is a change of mission — ask the owner, do not design it.
- **Banned vocabulary:** lottery, won by, drawn, the draw, raffle (and the Russian лотерея, разыгрываются, выигрываются, розыгрыш, жребий).
- **Public texts describe the product, not its gaps.** Open questions and weak spots stay out of the indexed README.
- **License:** MIT from 15 October 2026 (changelog entry 42).
- **Commit and tag messages are written in English.**
