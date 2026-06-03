# 🔗 Blockchain from Scratch

A simple blockchain implementation in Python, built by following Daniel van Flymen's [Learn Blockchains by Building One](https://hackernoon.com/learn-blockchains-by-building-one-117428612f46) tutorial on HackerNoon.

---

## 📖 About

This project is a minimal, educational blockchain built to understand the core mechanics behind distributed ledgers. It exposes a simple HTTP API (via Flask) so you can interact with the chain, mine new blocks, and register nodes in a decentralized network.

**What I learned building this:**
- How blocks are structured and chained together using SHA-256 hashes
- How Proof of Work (PoW) prevents trivial block creation
- How consensus is achieved across multiple nodes
- How transactions are broadcast and included in blocks

---

## ✨ Features

- **Block creation** — each block stores an index, timestamp, list of transactions, proof, and the previous block's hash
- **Proof of Work** — a simple PoW algorithm that requires finding a hash with a leading number of zeros
- **Transaction broadcasting** — add new transactions to be included in the next mined block
- **Node registration** — register multiple nodes to simulate a peer-to-peer network
- **Consensus algorithm** — resolves conflicts by replacing the local chain with the longest valid chain in the network
- **REST API** — interact with the blockchain via HTTP endpoints

---

## 🛠️ Tech Stack

- **Python 3.6+**
- **Flask** — lightweight web framework for the HTTP API
- **requests** — used for inter-node communication

---

## 🚀 Getting Started

### Prerequisites

```bash
python3 --version   # 3.6 or higher required
pip3 --version
```

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
   cd YOUR_REPO_NAME
   ```

2. Install dependencies:
   ```bash
   pip3 install flask requests
   ```

   Or if a `requirements.txt` is present:
   ```bash
   pip3 install -r requirements.txt
   ```

### Running the Node

Start a blockchain node on port 5000:

```bash
python3 blockchain.py
```

To simulate a network, run additional nodes on different ports in separate terminals:

```bash
python3 blockchain.py --port 5001
python3 blockchain.py --port 5002
```

---

## 🔌 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/mine` | Mine a new block |
| `POST` | `/transactions/new` | Create a new transaction |
| `GET` | `/chain` | Return the full blockchain |
| `POST` | `/nodes/register` | Register new peer nodes |
| `GET` | `/nodes/resolve` | Run the consensus algorithm |

### Example Requests

**Create a new transaction:**
```bash
curl -X POST http://localhost:5000/transactions/new \
  -H "Content-Type: application/json" \
  -d '{"sender": "address-a", "recipient": "address-b", "amount": 5}'
```

**Mine a new block:**
```bash
curl http://localhost:5000/mine
```

**View the full chain:**
```bash
curl http://localhost:5000/chain
```

**Register peer nodes:**
```bash
curl -X POST http://localhost:5000/nodes/register \
  -H "Content-Type: application/json" \
  -d '{"nodes": ["http://127.0.0.1:5001"]}'
```

**Resolve conflicts (consensus):**
```bash
curl http://localhost:5000/nodes/resolve
```

---

## 🧱 How It Works

### The Block

Each block in the chain looks like this:

```json
{
  "index": 1,
  "timestamp": 1506057125.900785,
  "transactions": [
    {
      "sender": "address-a",
      "recipient": "address-b",
      "amount": 5
    }
  ],
  "proof": 324984774000,
  "previous_hash": "2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824"
}
```

### Proof of Work

The PoW algorithm finds a number `p'` such that `hash(pp')` starts with four leading zeros, where `p` is the previous proof:

```
hash(p * p') starts with "0000"
```

### Consensus

When nodes disagree on the chain, the **longest valid chain wins**. Calling `/nodes/resolve` will check all registered peers and replace the local chain if a longer valid one is found.

---

## 📚 Reference

- Tutorial: [Learn Blockchains by Building One — Daniel van Flymen](https://hackernoon.com/learn-blockchains-by-building-one-117428612f46)
- Original source code: [dvf/blockchain on GitHub](https://github.com/dvf/blockchain)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
