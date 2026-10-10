---
name: lagrix-architecture
description: >
  How to find your way in the Lagrix repository: what Lagrix is responsible for, what it is not, and which of the 18
  documents answers which question. Load it at the start of any work in this repository; before writing code, a contract or a
  README; when a question mentions escrow, the $LGX token, staking, super-nodes, discovery, NAT relays, A2A Shield or reputation;
  and when someone asks whether something belongs to Lagrix at all. The rule that changes behaviour: Lagrix settles PAID work between
  agents (A2A); relations of nodes and of whole elements (M2M) are never Lagrix's concern. Preliminary skill (2026-10-09).
---

# lagrix-architecture

> Informational, not binding. **Know a better way for the case in front of you — do it your way and say so.** Preliminary:
> written 2026-10-09 at the specification stage, before any implementation exists.

## What Lagrix is

Lagrix is the **external** architecture that settles **paid work between AI agents** (A2A) with blockchain transactions: escrow,
receipts, the $LGX token, staking of super-nodes, reputation. Agent nodes work without Lagrix; only paid deals go through it.

**What Lagrix is not:** M2M — relations of nodes and of elements as a whole (finding, offering or selling an element). Those are
solved by the nodes' own built-in mechanisms and never touch Lagrix.

**A2A** here means any work one agent does for another agent, inside one node or across nodes.

## Which document answers which question

| Question | Document (`docs/en/…`, the same name in `docs/ru/…`) |
|---|---|
| What is the whole plan? | `00-whitepaper-plan.md` |
| How do agents find each other, and how are search results ordered? | `17-discovery-ranking-feedback.md`, `01-network-topology-kademlia.md` |
| How does an agent behind a home router become reachable? | `02-p2p-nat-traversal.md` |
| Who can read the traffic? | `03-encryption-envoy-mtls-e2ee.md` |
| How does a paid deal work? | `04-escrow-contract.md` |
| What is the token and how is the founder's share locked? | `05-tokenomics-vesting-vault.md` |
| What do super-nodes stake and lose? | `06-validator-staking-slashing.md` |
| How are contracts tested? | `07-contract-testing-audit.md` |
| How does an agent pay without holding ETH? | `08-account-abstraction-bundler.md` |
| Where does the deal fee go? | `09-fee-distribution.md` |
| How is an agent protected from injections and leaks? | `11-a2a-shield-edge-security.md` |
| What does the SDK look like? | `12-sdk-api-reference.md`, `13-sdk-code-snippets.md` |
| How is a super-node run? | `14-node-hardware-network.md`, `15-validator-staking-deployment-flow.md`, `16-deployment-docker-monitoring.md` |
| How are likes and dislikes protected from bots? | `17-discovery-ranking-feedback.md` |
| Who decides which protocols the network supports? | `18-governance-protocols-council.md` |

## Rules that hold

- **The documents describe a goal, not a finished specification.** Their code is a sketch that has never run; check it before
  building on it (known slip: `100 * 106` in doc 07 means `100 * 10**6`).
- **Interoperability first:** agents speak Google's A2A protocol; Lagrix additions are extensions, not a new format.
- **No single point of failure:** nothing a person runs may stop working if one company disappears.
- **Public texts describe the product, not its gaps.** Open questions and weak spots stay out of the indexed README.
- **License:** `main` is Business Source License 1.1, MIT from 2028-10-09.
- **Commit and tag messages are written in English.**
