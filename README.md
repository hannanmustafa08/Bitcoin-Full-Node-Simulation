# Bitcoin Full Node Simulation

A fully functional, Python-based Bitcoin full-node simulation developed for the CS3812 Introduction to Blockchain course at LUMS. This project mirrors the foundational protocols of the Bitcoin network, handling transaction validation, double-spend prevention, block mining, and peer-to-peer (P2P) chain consensus. 

During live testing, this node was deployed on a shared ISPL server, where it successfully mined, verified, and broadcasted blocks that achieved consensus and were accepted into the class-wide longest chain.

## 🛠️ Tech Stack & Key Concepts
* **Language:** Python
* **Cryptography:** SHA-256 Hashing, Public/Private Key Signatures
* **Architecture:** P2P Networking, UTXO Database Construction, Proof-of-Work (PoW)
* **Storage:** Pickle (object serialization), Local filesystem indexing

## 🚀 Features

### 1. UTXO Database Construction & Transaction Verification
* **Double-Spend Prevention:** Dynamically maintains an Unspent Transaction Output (UTXO) database to strictly ensure that no outputs are spent more than once.
* **Signature Validation:** Authenticates unlocking scripts by applying public keys to signatures, verifying the absolute integrity of every input.
* **Transaction Validity:** Parses mempool transactions, ensuring that total input values strictly meet or exceed output values, discarding any corrupt or unauthorized requests.

### 2. Proof-of-Work Mining
* **Block Generation:** Compiles batches of valid, unconfirmed transactions into new blocks.
* **PoW Execution:** Iteratively calculates a cryptographic nonce until the block hash fulfills the network's required leading-zeros difficulty threshold.
* **State Persistence:** Automatically serializes and saves locally mined blocks to the `valid_chain` directory.

### 3. Peer Chain Validation (P2P Consensus)
* **Longest Chain Rule:** Downloads incoming chains from peers (stored in `pending_chains`) and rigorously evaluates them against the local state.
* **Block Linkage Check:** Authenticates block continuity by validating the chaining of `previous_hash` pointers across all newly received blocks.
* **Full-Chain Re-verification:** Extends zero-trust protocols to peers by re-evaluating the signature and UTXO validity of every transaction within a received chain before replacing the local state.

## 💻 Setup & Execution

*Note: This repository represents the core logic (`FullNode.py`). Execution requires the full CS3812 skeleton environment, including `main.py`, the interactive terminal interface, and local `valid_chain`/`pending_chains` directories.*

To launch the node and access the interactive mining console within the complete environment:

```bash
python3 main.py
