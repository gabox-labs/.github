<div align="center">

# Gabox

**An onchain gacha for NFTs and tokenized assets, built on one primitive: the backed position.**

[![Chain](https://img.shields.io/badge/chain-Solana-9945FF)](https://solana.com)
[![Denomination](https://img.shields.io/badge/denomination-USDC-2775CA)](#protocol-at-a-glance)
[![Randomness](https://img.shields.io/badge/randomness-MagicBlock%20VRF-0A0A0A)](https://www.magicblock.gg)
[![Status](https://img.shields.io/badge/status-live%20on%20devnet-brightgreen)](#status)
[![License](https://img.shields.io/badge/license-MIT-blue)](https://github.com/gabox-labs/docs/blob/main/LICENSE)

[Documentation](https://github.com/gabox-labs/docs) · [Contact](mailto:hello@hubra.app)

</div>

---

## What is Gabox?

Gabox is a peer-to-peer gacha protocol on Solana. Depositors list real assets in shared pools, buyers pay a fixed ticket price for a verifiably random draw, and every item drawn comes with a guaranteed instant buyback offer.

The entire protocol rests on a single primitive. When a depositor lists an item, they pair it with **backing** — an amount of USDC locked alongside the asset. That one number is simultaneously the item's buyback bid, its draw weight, and the depositor's stake. Ticket pricing, draw odds, and buyback liquidity are all derived from it.

## How it works

1. **Deposit** — A depositor lists an NFT or tokenized asset and locks USDC backing next to it: their own statement of the item's value, and the price they stand ready to buy it back at.
2. **Price** — The pool's ticket price updates automatically: the draw-weighted expected value of the pool (the harmonic mean of all backings) plus a 10% surcharge.
3. **Draw** — A buyer pays the ticket. MagicBlock VRF selects exactly one position, with probability inversely proportional to its backing — cheap items are drawn constantly, richly backed grails rarely. The item is delivered immediately.
4. **Keep or sell back** — The buyer has a short settlement window to decide. **Keep** it, and the depositor's backing is returned as they exit. **Sell it back** for 90% of its backing in instant cash, and the item returns to its depositor or is automatically relisted.

## Why this design matters

Most gacha and lootbox mechanics have a house that can lose: if buybacks are promised from a shared vault, one jackpot cash-out can drain it. Gabox removes that failure mode entirely — every buyback is pre-funded by the depositor's own backing, posted before the item ever enters a pool.

| Property | How Gabox achieves it |
|---|---|
| **No insolvency risk** | Every possible payout is collateralized by depositor backing before the draw |
| **No oracle risk** | Prices derive from self-set backing, not floor-price feeds |
| **Verifiable fairness** | Draws use onchain VRF with published odds |
| **Guaranteed exit** | Every drawn item can be sold back instantly for 90% of its backing |

The protocol holds no float and no vault. It never promises a payout it does not already hold in escrow on someone's behalf — solvency is structural, not a treasury-management problem.

## Protocol at a glance

| | |
|---|---|
| **Assets** | NFTs and tokenized assets (e.g. graded cards, vaulted TCG, blue-chip PFPs) |
| **Chain** | Solana |
| **Denomination** | USDC throughout — backing, bids, tickets, and fees are all USD-denominated |
| **Randomness** | MagicBlock VRF, delivered via CPI callback |
| **Protocol take** | 1% of each ticket, plus 10% of backing on each sell-back |

## Status

The program is **code-complete and live on devnet**, with real draws settled against the MagicBlock VRF oracle end to end: backed positions with buffers, harmonic-mean pricing, keep-or-sell-back settlement, the five-rank crown board, and the full failure-path machinery.

Mainnet follows external code review and a Squads multisig upgrade authority. See the [roadmap](https://github.com/gabox-labs/docs/blob/main/roadmap.mdx) for what ships when.

## Repositories

| Repository | Description |
|---|---|
| [`docs`](https://github.com/gabox-labs/docs) | Protocol documentation: mechanism, pricing, economics, safety, and roadmap |

Additional repositories will be opened as the protocol approaches mainnet.

## Contact

Questions or feedback: [hello@hubra.app](mailto:hello@hubra.app)
