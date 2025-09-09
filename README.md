# ZKHack Puzzles

A collection of my solutions to ZKHack puzzles, demonstrating various cryptographic attacks and zero-knowledge proof vulnerabilities.

## Overview

This repository contains my solutions to ZKHack puzzles that explore different aspects of zero-knowledge proofs, cryptographic primitives, and their potential vulnerabilities. Each puzzle demonstrates important concepts in cryptography and helps understand the security considerations in zero-knowledge proof systems.

## Puzzles

### Puzzle 1: BLS Pedersen Hash Forgery
**Status**: ✅ Solved  
**Directory**: `zkhack-bls-pedersen/`

A demonstration of how to forge BLS signatures by exploiting the Pedersen hash function. This puzzle shows the importance of using secure hash functions in signature schemes.

**Key Concepts**:
- BLS signature scheme
- Pedersen hash function vulnerabilities
- Signature forgery techniques
- Hash function security requirements

**Solution**: The puzzle involves creating a collision in the Pedersen hash function to forge valid BLS signatures.

### Puzzle 2: Trusted Setup Attack
**Status**: ✅ Solved  
**Directory**: `zkhack-trusted-setup/`

A discrete logarithm attack on a BLS12-381 trusted setup ceremony. This puzzle demonstrates how weak generators in trusted setups can be exploited to recover the secret.

**Key Concepts**:
- BLS12-381 elliptic curve
- Trusted setup ceremonies
- Discrete logarithm attacks
- Chinese Remainder Theorem (CRT)
- Cofactor exploitation

**Solution**: 
- Python script (`solve_trusted_setup.py`) that performs the discrete logarithm attack
- Modified Rust code that reads the recovered secret from a file
- Complete working solution with secret recovery

## Repository Structure

```
ZKHack-Puzzles/
├── zkhack-bls-pedersen/     # Puzzle 1: BLS Pedersen Hash Forgery
├── zkhack-trusted-setup/    # Puzzle 2: Trusted Setup Attack
└── bls-signatures/          # BLS signature library (dependency)
```

## Links

- [ZKHack](https://zkhack.dev/)
- [BLS Signatures](https://github.com/Chia-Network/bls-signatures)
- [BLS12-381](https://hackmd.io/@benjaminion/bls12-381)
