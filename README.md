# Merkle Tree Visualizer

An interactive Merkle tree that hashes with **real SHA-256** (via the browser's `crypto.subtle`) and rebuilds itself live as you edit the data blocks. Click any leaf to generate its **Merkle proof** — the sibling hashes needed to verify that block belongs under the root.

**Live:** [merkletree-visualizer.netlify.app](https://merkletree-visualizer.netlify.app/)

## What it does

- **Live hashing** — edit any data block and every hash up the tree recomputes instantly with real SHA-256.
- **Merkle proofs** — click a leaf and it highlights the path to the root, marks the sibling hashes you'd need, then replays them step by step to confirm they reconstruct the same root.
- **Odd-leaf handling** — when a level has an odd number of nodes, the last one is duplicated and hashed with itself (the way Bitcoin does it). Padded nodes are drawn dashed so it's visually honest.
- **Live editing** — add, remove, or randomise blocks and watch the tree restructure.

## Why Merkle trees matter

A Merkle tree lets you commit to a large set of data with a single hash (the root). To prove one item is part of that set, you don't need the whole dataset — just a handful of sibling hashes (`O(log n)` of them). This is the backbone of how blockchains verify transactions efficiently, and how systems like Git and IPFS check data integrity.

## How to use

1. Open the [live demo](https://merkletree-visualizer.netlify.app/).
2. Edit the **data blocks** on the left — the tree re-hashes on every keystroke.
3. Use **+ add block** to grow the tree or **⟳** to randomise the data.
4. Click any **leaf node** to see its Merkle proof:
   - The path to the root is highlighted in green.
   - The sibling (proof) hashes are highlighted in blue.
   - Below, each step shows whether the sibling is hashed on the `left` or `right`, then verifies the recomputed root matches.

## Implementation notes

- Pure HTML, CSS, and JavaScript — **no libraries, no build step**.
- Hashing uses the native [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Crypto/subtle) (`crypto.subtle.digest`).
- The tree layout and connector lines are drawn with absolutely-positioned nodes and inline SVG.

> **Note:** this is a teaching implementation. It hashes the two child hashes as concatenated **hex strings**, whereas Bitcoin does a double-SHA-256 over the raw **bytes**. The structure and proof logic are identical — only the byte handling is simplified for readability.

## Run locally

No build needed — just open the file:

```bash
git clone https://github.com/vhmns14/merkle-tree
cd merkletree
open index.html        # macOS
# xdg-open index.html  # Linux
# start index.html     # Windows
