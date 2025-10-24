
Chunk 1/5
# ARCAI — ArcAgent

ARCAI is a proof-of-concept conversational AI wallet agent that helps users manage, move, and optimize USDC on the Arc network. It uses an LLM to interpret plain‑English requests, proposes explainable on‑chain actions, runs deterministic safety checks, and constructs unsigned transactions for users to sign noncustodially. This repository is prepared for rapid demos (e.g., hackathons) and local development.

## One‑sentence pitch
A conversational AI wallet agent that lets users manage, move, and optimize USDC on Arc through plain‑English chat; it recommends safe, explainable on‑chain actions and constructs transactions that users sign.

## Features (MVP)
- Wallet connect + USDC balance display (frontend stub)
- Chat UI that accepts natural-language intents (transfer, deposit, withdraw, swap, optimize)
- LLM-driven intent parsing → action plan templates
- Backend deterministic safety checks (max slippage, whitelisted adapters, max single-transfer limit)

Chunk 2/5
- Transaction construction (unsigned) using ethers.js for frontend signature (noncustodial)
- Minimal starter smart contract (StarterVault) to store deposits and hashed AI rationales
- CI workflow, README and demo plan for a 2–4 minute end‑to‑end demo on Arc testnet

## Tech stack
- Smart contracts: Solidity (Hardhat)
- Backend: Node.js + TypeScript, ethers.js, OpenAI (or chosen LLM)
- Frontend: Next.js + React (wagmi / web3modal recommended)
- Optional: The Graph for indexing, IPFS for immutable rationale storage

## Architecture (summary)
- Frontend
  - Wallet connection, chat UI, displays LLM recommendations and unsigned txs for user signature.
- Backend
  - Receives chat intent, queries on‑chain data and oracles, calls the LLM with structured prompts, runs deterministic safety checks, constructs unsigned transaction payloads (ethers.js), and returns explainable actions + tx data.
- Execution
  - Frontend requests signature from user wallet and broadcasts the signed transaction to the Arc testnet. Optionally, adapters or contracts emit events and store hashed AI rationale for auditability.

Chunk 3/5
## Quick start (local)
Prerequisites
- Node.js 18+
- npm or pnpm
- An Arc testnet RPC URL and test USDC token address
- OpenAI API key (or other LLM provider key)

Quick run (example)
1. Clone repo
   git clone https://github.com/shagarnet/ARCAI.git
2. Install dependencies
   cd ARCAI/backend && npm install
   cd ../frontend && npm install
3. Create .env files using the examples (backend/.env.example, root .env.example)
4. Start backend
   cd backend && npm run dev
5. Start frontend
   cd frontend && npm run dev
6. Open frontend, connect a testnet wallet, and try sample prompts (e.g., “Send 10 USDC to 0xABC…” or “Optimize 100 USDC for yield”)

.env.example (backend)
OPENAI_API_KEY=your_openai_api_key
ARC_RPC_URL=https://rpc.arc-testnet.example
USDC_TOKEN_ADDRESS=0x0000000000000000000000000000000000000000
PORT=4000

.env.example (frontend / root)
NEXT_PUBLIC_BACKEND_URL=http://localhost:4000

Note: Never commit real API keys or private keys. Use .env.example to show required variables.

Chunk 4/5
## Demo script (short)
1. Connect a test wallet to the frontend.
2. Ask: “Optimize 100 USDC for yield.”
3. Agent displays current options, recommends one action with rationale and risk summary.
4. Backend runs safety checks and constructs an unsigned tx.
5. User signs tx in wallet and broadcasts to Arc testnet.
6. UI shows on‑chain confirmation and the agent’s explanation; adapter/contract stores a hashed rationale for auditability.

## Security & safety
- Backend does not hold private keys — all value transfers require the user's wallet signature.
- Deterministic safety rules: max transfer limits, whitelisted adapters, max slippage bounds, and callStatic dry-run simulations.
- Rate-limit and sanitize LLM inputs, and perform preflight transaction checks.
- Log events and store hashed AI rationale (optional IPFS) for audit trails.

## Development roadmap (next commits)
- Add complete Hardhat configuration, contract tests, and deployment scripts
- Improve prompt templates and rate limiting for LLM usage
- Integrate wagmi / rainbowkit for robust wallet UX
- Add TypeScript types, unit tests for safetyChecks, and end‑to‑end demo tests
- Add a demo video and downloadable screening form

Chunk 5/5
## Contributing
- Open issues for bugs or feature requests.
- Use feature branches and open pull requests for changes.
- Do not commit secrets (private keys, real API keys, mnemonics).

## Contact
- Name: markos chala
- Email: markschala12@gmail.com
- GitHub: @markoschalaalx

## License
MIT — Copyright (c) 2025 markos chala
