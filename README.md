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

### Puzzle 3: Hidden in Plain Sight - Polynomial Commitment Deanonymization
**Status**: ✅ Solved  
**Directory**: `zkhack-hidden-in-plain-sight/` (submodule)

A shielded pool deanonymization attack that exploits the mathematical structure of polynomial commitments with blinding factors. This puzzle demonstrates how seemingly secure cryptographic primitives can be vulnerable when the underlying mathematical relationships are not properly understood.

**Key Concepts**:
- KZG-like polynomial commitments
- BLS12-381 elliptic curve
- Polynomial blinding schemes
- Evaluation domains and vanishing polynomials
- Deanonymization attacks on privacy-preserving systems

**Solution**: 
- Complete Rust implementation that solves the system of linear equations for blinding factors
- Mathematical attack using the relationship: `Q(x) = P(x) + (b₀ + b₁x) · Z_H(x)`
- Recovery of the target account (index 535) and blinding factors
- Analysis tools for understanding the data structure and attack methodology

### Puzzle 4: Double Trouble - Inner Product Proof Attack
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

## Repository Structure

```
ZKHack-Puzzles/
├── zkhack-bls-pedersen/                # Puzzle 1: BLS Pedersen Hash Forgery
├── zkhack-trusted-setup/               # Puzzle 2: Trusted Setup Attack
├── zkhack-hidden-in-plain-sight/       # Puzzle 3: Polynomial Commitment Deanonymization (submodule)
├── zkhack-double-trouble-solution/     # Puzzle 4: Inner Product Proof Attack
└── bls-signatures/                     # BLS signature library (dependency)
```

## Links

- [ZKHack](https://zkhack.dev/)
- [BLS Signatures](https://github.com/Chia-Network/bls-signatures)
- [BLS12-381](https://hackmd.io/@benjaminion/bls12-381)
