# CEFA-Pro v3.2 - Audit Ready Core

Sovereign 144,000-node deterministic identity network.

**Status:** Security Hardening Gate PASS | No private key exposure | Ed25519 verified

## What This Is
Deterministic HD wallet tree: `m/44'/144'/{node_index}'/0'/0` hardened.
Public manifest of 144k addresses. Private keys never touch disk.

Master Seed [HSM/offline] -> 144k Nodes -> Public Manifest Only -> Independent Verifier

## What You Can Verify in 10 Minutes (No Trust Required)
1. `pip install -r requirements.txt`
2. `python -m security.verifier manifest.ndjson manifest.merkle.json manifest.sig sovereign-public-key.pem`
3. Expected: PASS

No private material in repo. No API keys. No faucet.

## Architecture
- `/security/key_manager.py` - AES-GCM-256, PBKDF2 600k, AAD binding, 0o600, zeroization
- `/security/signer.py` - Ed25519 sovereign signer
- `/security/verifier.py` - Offline 3rd party verifier
- `/core/transaction_queue.py` - SQLite WAL, idempotent, dead-letter
- `/chains/` - Isolated adapters (xrpl, evm, sol)

## Security Model
- Private keys never written to disk
- Vault swap attack blocked via AAD
- Manifest authenticity via Ed25519, not HMAC
- Queue survives kill -9, resumes from WAL

## Verification Package
See `/dist/CEFA-Pro-Verification-Package-v3.2.zip` - Contains manifest, merkle root, sig, public key, and public_verifier.py

## Roadmap
v3.2 Audit Ready Core [DONE]
v3.3 Whitepaper v1 + Dashboard Demo [NEXT]
v4.0 Testnet 10k nodes

## Contact
For audit: [zbrennan716526@gmail.com]