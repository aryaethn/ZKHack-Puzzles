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

### Puzzle 3: Double Trouble - Inner Product Proof Attack
**Status**: ✅ Solved  
**Directory**: `zkhack-double-trouble-solution/`

A zero-knowledge inner product proof vulnerability where the prover uses linearly dependent random vectors instead of independent ones. This demonstrates how poor randomness can completely break zero-knowledge properties.

**Key Concepts**:
- Zero-knowledge inner product proofs
- Fiat-Shamir transform
- Pedersen commitments
- Linear dependence attacks
- Randomness requirements in ZK proofs

**Solution**: 
- Complete Rust implementation that exploits the relationship `r₂ = 2 * r₁`
- Mathematical attack using the equations: `s₁ = a + γ₁r₁` and `s₂ = a + γ₂r₂`
- Recovery of both the secret vector `a` and randomness `α`
- Clean, production-ready code with comprehensive analysis tools

### Puzzle 4: Hidden in Plain Sight - Polynomial Commitment Deanonymization
**Status**: ✅ Solved  
**Directory**: `zkhack-hidden-in-plain-sight/` (submodule)

A shielded pool deanonymization attack exploiting polynomial commitment blinding schemes. This puzzle demonstrates how mathematical relationships in blinded polynomial commitments can be exploited to recover hidden recipient addresses.

**Key Concepts**:
- KZG polynomial commitments
- BLS12-381 elliptic curves
- Polynomial blinding schemes
- Evaluation domains
- Linear algebra attacks on blinded polynomials
- Deanonymization techniques

**Solution**: 
- Complete analysis of the challenge data structure
- Mathematical solution using linear algebra to recover blinding factors
- Brute-force approach to find the target account (index 535)
- Successful reconstruction of the blinded polynomial
- Full verification that the solution matches the given commitment and openings

## Repository Structure

```
ZKHack-Puzzles/
├── zkhack-bls-pedersen/                # Puzzle 1: BLS Pedersen Hash Forgery
├── zkhack-trusted-setup/               # Puzzle 2: Trusted Setup Attack
├── zkhack-double-trouble-solution/     # Puzzle 3: Inner Product Proof Attack
├── zkhack-hidden-in-plain-sight/       # Puzzle 4: Polynomial Commitment Deanonymization (submodule)
└── bls-signatures/                     # BLS signature library (dependency)
```

## Submodules

This repository uses git submodules for some puzzles to maintain clean separation and allow independent development:

- `zkhack-hidden-in-plain-sight/` - A submodule containing the solution to Puzzle 4

To clone this repository with all submodules:
```bash
git clone --recursive https://github.com/aryaethn/ZKHack-Puzzles.git
```

To update submodules after cloning:
```bash
git submodule update --init --recursive
```

## Links

- [ZKHack](https://zkhack.dev/)
- [BLS Signatures](https://github.com/Chia-Network/bls-signatures)
- [BLS12-381](https://hackmd.io/@benjaminion/bls12-381)
