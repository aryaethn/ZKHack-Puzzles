# Puzzles

## Puzzle 1: BLS Pedersen Hash Forgery
**Status**: ✅ Solved  
**Directory**: `zkhack-bls-pedersen/`

A demonstration of how to forge BLS signatures by exploiting the Pedersen hash function. This puzzle shows the importance of using secure hash functions in signature schemes.

**Key Concepts**:
- BLS signature scheme
- Pedersen hash function vulnerabilities
- Signature forgery techniques
- Hash function security requirements

**Solution**: The puzzle involves creating a collision in the Pedersen hash function to forge valid BLS signatures.

## Puzzle 2: Trusted Setup Attack
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

## Puzzle 3: Double Trouble - Inner Product Proof Attack
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

## Puzzle 4: Hidden in Plain Sight - Polynomial Commitment Deanonymization
**Status**: ✅ Solved  
**Directory**: `zkhack-hidden-in-plain-sight/`

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
- Brute-force approach to find the target account
- Successful reconstruction of the blinded polynomial
- Full verification that the solution matches the given commitment and openings

## Puzzle 5: Strong Adaptivity - Fiat-Shamir Vulnerability
**Status**: ✅ Solved  
**Directory**: `zkhack-strong-adaptivity/`

A zero-knowledge proof vulnerability exploiting the Fiat-Shamir transform's independence from witness messages. This puzzle demonstrates how an attacker can generate valid proofs for commitments with the same message while claiming different messages in the witness.

**Key Concepts**:
- Fiat-Shamir transform vulnerabilities
- Pedersen commitments
- Sigma protocols
- Strong adaptivity attacks
- Challenge independence from witness
- Message equality proofs

**Solution**: 
- Implemented `fake_prove()` function that exploits the vulnerability
- Attack works by computing the challenge independently of the witness message
- Generates valid proof for commitments with same message
- Creates fake witness claiming different messages
- Successfully demonstrates the strong adaptivity vulnerability
- Complete working solution with verification and test cases

## Puzzle 6: Soundness of Music - Zero-Knowledge Proof Soundness Attack
**Status**: ✅ Solved  
**Directory**: `zkhack-soundness-of-music/`

A zero-knowledge proof soundness vulnerability where the prover can generate valid proofs for mathematically impossible statements. This puzzle demonstrates how to exploit the verification system to prove that 1+1+1+1=1, which is impossible in normal arithmetic.

**Key Concepts**:
- Zero-knowledge proof soundness
- BLS12-381 elliptic curve groups
- Arithmetic circuit constraints
- Trusted setup exploitation
- Proof verification bypass techniques
- Mathematical impossibility proofs

**Solution**: 
- Implemented `fake_prove()` function that generates fake proofs
- Exploits the verification system by manipulating proof elements
- Uses negative public inputs for private input polynomials
- Sets critical proof elements to zero to bypass constraints
- Successfully proves the impossible statement 4×1=1
- Complete working solution with data analysis tools

## Puzzle M1: There is Something in the AIR - Semaphore Double-Vote Bug Fix
**Status**: ✅ Solved  
**Directory**: `zkhack-there-is-something-in-the-AIR/`

A critical vulnerability in a Semaphore-style AIR (Algebraic Intermediate Representation) that allowed users to create multiple valid signals with different nullifiers on the same topic. This puzzle demonstrates the importance of proper constraint enforcement in zero-knowledge proof systems.

**Key Concepts**:
- Semaphore protocol implementation
- AIR (Algebraic Intermediate Representation) constraints
- Rescue Prime hash function
- Merkle tree verification
- Nullifier generation and uniqueness
- STARK proof systems
- Double-vote prevention mechanisms

**Solution**: 
- **Root Cause**: Nullifier capacity columns (12-15) were being reset to `[0,0,0,0]` instead of maintaining `[8,0,0,0]`
- **AIR Fixes**: Added boundary constraints to enforce nullifier capacity at first row
- **Prover Fix**: Removed buggy code that reset nullifier capacity columns
- **Constraint Fixes**: Fixed duplicate constraint indices and reorganized constraint evaluation
- **Testing**: Added comprehensive tests to verify deterministic nullifier generation
- **Result**: Fixed the double-vote bug, ensuring each user can only vote once per topic
- Complete working solution with proper constraint enforcement and verification

## Puzzle M2: Can You Turn Up the Heat - STARK FRI Vulnerability
**Status**: ✅ Solved  
**Directory**: `zkhack-can-you-turn-up-the-heat/`

A STARK proof system vulnerability exploiting the FRI (Fast Reed-Solomon Interactive Oracle Proofs) folding mechanism. This puzzle demonstrates how to create fake proofs that pass verification by manipulating the polynomial degree in FRI layer folding.

**Key Concepts**:
- STARK proof systems
- FRI (Fast Reed-Solomon Interactive Oracle Proofs) protocol
- Polynomial degree manipulation
- Fibonacci sequence verification
- Degree-respecting projection (DRP)
- Polynomial interpolation attacks
- FRI layer folding vulnerabilities

**Solution**: 
- **Root Cause**: FRI folding mechanism allowed manipulation of polynomial degrees
- **Hint 3 Implementation**: Modified the `apply_drp` function to force degree 3 polynomial in first FRI layer
- **Attack Strategy**: Used 4 anchor points to interpolate a cubic polynomial and backfill remaining points
- **Fake Proof Generation**: Created valid-looking proofs claiming incorrect Fibonacci results (123 instead of 832040)
- **Verification Bypass**: Exploited the FRI query system to ensure verification succeeds
- **Technical Details**: 
  - Folded domain from 128 to 32 elements with folding factor 4
  - Selected base index 5 and stride 8 for anchor points
  - Used Lagrange interpolation to create consistent polynomial evaluations
  - Implemented degree forcing mechanism in FRI layer 1
- Complete working solution with successful fake proof verification