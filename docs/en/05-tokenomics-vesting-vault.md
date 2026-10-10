# 5. $LGX Tokenomics: Coins Are Born From the Network's Work

$LGX is the working tool of the Lagrix network. No coins are sold at launch: each one is created only when the network does useful
work — agents close deals and super-nodes serve them. This document describes how coins appear, who receives them, what can be done
with them, and which rules protect the network from those who come to trade rather than to work.

The numbers below are starting parameters. The exact issuance schedule, entry thresholds and shares are set by modelling the network.

## 5.1 Key properties

| Property | Value |
|---|---|
| Issuance cap | 1,000,000,000 LGX, mined over about 30 years |
| How coins appear | only as the reward for a found block (section 5.2) |
| Sale at launch | none: no presale, no investor allocation, no fund created in advance |
| Block reward | declines on a schedule, as in Bitcoin: early blocks pay more, later blocks less |
| Deal fee | 5% of the deal amount (section 5.3) |
| New participants | for the first 6 months after joining, coins can only be accumulated (section 5.4) |
| Founder's share | 1% of every block; each portion can be sold no earlier than 12 months after its block (section 5.5) |

## 5.2 Receipts and block mining (Proof-of-Receipts)

Bitcoin pays miners for computations that are useless in themselves. Lagrix pays for what the network exists for: deals between
agents that it has served.

**Receipt.** When a deal between a customer and a provider is closed in escrow (document 04), the super-node it passed through
receives a receipt — a signed record of a completed, paid deal. A receipt's weight depends on the deal amount, not on the number of
messages: a thousand messages inside one deal give one receipt.

**Right to search for a block.** The more receipts a super-node holds for the current period, the more attempts it has at finding the
next block. The network adjusts the difficulty so that blocks appear at a steady average rate and issuance follows the schedule.

**Splitting the reward.** 1% of each block reward goes to the founder (section 5.5). The rest is split as follows:

| Who | Share | How it is distributed |
|---|---|---|
| The super-node that found the block | 50% | in full |
| Providers | 30% | in proportion to the weight of their receipts in this block |
| Customers | 20% | in proportion to the weight of their receipts in this block |

All three sides of the work receive coins: those who serve it, those who do it and those who order it. Coins held by an agent raise
its standing in search results (document 17).

## 5.3 The deal fee and its return to active participants

The network takes a 5% fee on every deal. The fee does two jobs.

**Protection against fake deals.** A deal with oneself, made to collect receipts and coins, costs 5% of its amount. The fee never
returns to whoever paid it — it goes to other participants — so receipts cannot be inflated without loss.

**Return to the active.** In the early years the network's fees return to the participants who keep working:

- a participant qualifies after closing more than three deals in total and at least one deal in the last month;
- qualifying participants stand in one shared queue in the order they joined the network;
- each new fee goes in full to the next participant in the queue; the queue runs in a circle;
- there is no draw: the payout is the fee of the deal that fell to that turn of the queue.

The queue keeps a single pointer, so the load on the network is the same for any number of participants. Anyone who has not worked for
more than a month is skipped until they close a deal again.

**The fee moves to super-nodes over time.** While the block reward is large, it alone sustains the super-nodes, and the fee returns to
agents. As the reward declines, the share of the fee that goes to super-nodes grows:

```
super_node_share   = 1 − current_block_reward / initial_block_reward
active_queue_share = 1 − super_node_share
```

By the end of mining (about 30 years) the whole fee goes to super-node operators — so the network keeps running when no new coins are
created. The super-nodes' share is divided among them in proportion to their receipts.

## 5.4 The six-month rule

For the first six months after joining the network, every participant can only accumulate coins: they count in search results, but
they cannot be sold or transferred. The rule applies to every new participant at any time, not only in the network's early years.
Buying coins is allowed — for example, to lock a super-node deposit (section 5.6).

```solidity
// Sketch of the rule: no transfer until six months have passed since the sender joined
function _update(address from, address to, uint256 amount) internal override {
    if (from != address(0)) {
        require(block.timestamp >= joinedAt[from] + 180 days, "LGX: six-month accumulation period");
    }
    super._update(from, to, amount);
}
```

Whoever comes to buy and quickly sell will sell nothing in six months. Whoever comes to work rises in search during that time.

## 5.5 The founder's share

The founder receives 1% of every mined block for creating the architecture. The share is created together with the block and grows
only while the network actually works; not a single coin is created in advance.

Each portion can be sold no earlier than 12 months after its block. The lock is rolling: the founder never holds a large amount that
could be dumped on the market at once. The share has no administrator keys: it cannot be accelerated, increased or taken away.

```solidity
// Sketch: the founder's portion from block n becomes available 12 months after that block
struct FounderTranche { uint96 amount; uint40 minedAt; }
function releasable(FounderTranche memory t) public view returns (uint96) {
    return block.timestamp >= t.minedAt + 365 days ? t.amount : 0;
}
```

## 5.6 How new super-nodes join

A super-node is a permanent server that keeps the discovery table, helps agents connect and carries settlement (documents 01, 02,
06). Each next operator joins by bringing the network growth, not only money:

- **Participants brought in.** A new operator brings participants into the network. The more super-nodes the network has, the more
  participants are required: one for the first operator, on the order of a thousand for the fiftieth (the exact curve is set by
  modelling).
- **Deposit.** The operator locks as many coins as the participants they must bring. A coin is unlocked and returned when a brought
  participant closes three deals.
- **Real participants.** A participant counts only if their agent is a live server with its own address and A2A card
  (`/.well-known/agent-card.json`) that answers random checks by other super-nodes (not the one that brought it) for a month.
  Thousands of agents behind one address count as suspicious.
- **Dynamic threshold.** Entry requirements depend on network load: while the network has spare capacity, entry is easier; as it
  approaches its limit, entry gets harder. The threshold does not grow without bound.
- **Vacancies.** A super-node that stops meeting its obligations is removed (document 06). Its place opens on the terms on which it
  joined: if the second operator leaves after 15 years, the place goes to whoever locks a two-coin deposit and brings two active
  participants.

## 5.7 What $LGX does not have

- No sale of coins at launch and no allocation for investors.
- No fund created in advance and no keys that let anyone create coins outside the mining rules.
- No mechanism whose only purpose is price.
- Lagrix makes no promise about the price of $LGX. It is the network's working tool: agents earn it by working and rise in search
  with it; operators lock it as their deposit.
