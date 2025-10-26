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

## Puzzle T1: Zero-Sum Game - Sumcheck Protocol Double-Spending Attack
**Status**: ✅ Solved  
**Directory**: `puzzle-zero-sum-game/`

A private payments protocol vulnerability exploiting the sumcheck protocol where incorrect sum values enable double-spending attacks. This puzzle demonstrates how a prover can craft valid proofs for polynomials with non-zero sums while claiming they sum to zero.

**Key Concepts**:
- Sumcheck protocol
- Marlin polynomial commitment scheme (KZG10)
- BLS12-381 elliptic curves
- Fiat-Shamir transform
- Masking polynomials
- Double-spending attacks
- Zero-knowledge payment protocols

**Solution**: 
- **Root Cause**: The verifier uses an incorrect sum value (zero) when the actual polynomial sum over the domain is non-zero
- **Attack Strategy**: Construct masking polynomial `s(x) = -f(x)` to satisfy the verification equation
- **Mathematical Relation**: `f(ξ) + s(ξ) = ξ·g(ξ) + h(ξ)·Z_H(ξ) + sum/|H|`
- **Implementation**: 
  - Set `g(x) = 0` and `h(x) = 0` for simplicity
  - Set `s(x) = -f(x)` (non-constant as required)
  - This ensures `s(ξ) + f(ξ) = 0 = ξ·0 + 0·Z_H(ξ) + 0/|H|`
- **Fiat-Shamir Consistency**: Derived challenge `ξ` identically to the verifier
- **Batch Opening**: Created proper QuerySet and batch opening proof for all polynomials
- **Result**: Successfully passed verification despite the polynomial having a non-zero sum
- Complete working solution demonstrating how masking polynomials enable double-spending when sum verification is compromised

## Puzzle T2: Power Corrupts - Cheon Attack on Trusted Setup
**Status**: ✅ Solved  
**Directory**: `puzzle-power-corrupts/`

A cryptographic attack exploiting a vulnerable BLS12-Cheon pairing-friendly elliptic curve trusted setup. This puzzle demonstrates how the Cheon attack can recover secret parameters when the sum of SRS powers divides the group order, combined with social engineering intelligence about the secret's structure.

**Key Concepts**:
- Cheon attack on pairing-based cryptography
- BLS12 pairing-friendly elliptic curves
- Trusted setup vulnerabilities
- Baby-step giant-step (BSGS) algorithm
- Discrete logarithm problem
- Groth16 SRS exploitation
- Group order divisibility attacks

**Solution**: 
- **Root Cause**: The sum `d = d₁ + d₂ = 702,047,372` divides `q-1` where `q = 1,114,157,594,638,178,892,192,613`
- **Attack Strategy**: Exploit the mathematical relationship τ = 2^(k₀ + k₁·m) where m = (q-1)/d
- **Social Engineering Intelligence**: k₀ is 51 bits with 15 MSBs = `10111101110` (range: 1,089,478,584,172,543 to 1,089,547,303,649,280)
- **Two-Phase BSGS Attack**:
  - **Phase 1**: Find k₀ using BSGS on g^(2^d)^c = k where k = e(τ^d₁·P, τ^d₂·Q)
    - Table size: 2^20 (baby steps)
    - Search space: ~68 billion values reduced to ~1.5 million via intelligence
    - Result: k₀ = 1,089,539,821,761,426
  - **Phase 2**: Find k₁ using BSGS on g^(η^c) = h·2^(-k₀) where η = 2^m
    - Table size: 2^16 (baby steps)  
    - Search space: ~702 million values
    - Result: k₁ = 690,599,720
- **Final Calculation**: τ = 2^(k₀ + k₁·m) = 284,865,198,031,253,921,498,207
- **Performance**: 
  - k₀ recovery: ~53.5 seconds
  - k₁ recovery: ~4.8 seconds
  - Total attack time: ~58 seconds
- **Verification**: Successfully verified P·τ = τP ✅
- Complete working solution with efficient BSGS implementation and proper field arithmetic

## Puzzle T3: Bigger is Better - Inner Product Commitment SRS Leak
**Status**: ✅ Solved  
**Directory**: `puzzle-bigger-is-better/`

A soundness vulnerability in an inner-product commitment scheme (ILV) where a malicious trusted setup ceremony accidentally included an extra SRS element. This puzzle demonstrates how a single leaked cryptographic parameter can completely break the soundness of a commitment scheme.

**Key Concepts**:
- Inner-product commitment schemes
- Structured Reference String (SRS) security
- Powers-of-Tau trusted setup vulnerabilities
- BLS12-381 elliptic curves
- Polynomial commitment soundness
- Pairing-based cryptography

**Solution**: 
- **Root Cause**: The SRS contains 514 elements in `powers_of_beta_g_first` instead of the expected 513
- **Leaked Element**: β^(dim+1)·G = β^513·G is available at index 513, but should have been excluded
- **Vulnerability**: The honest protocol skips coefficient (dim+1) when constructing proofs, assuming the SRS element is unavailable
- **Attack Strategy**: 
  1. Generate an honest proof using `ILV::open(ck, a, b)` which encodes the actual inner product
  2. Compute the difference: `Δ = actual_inner_product - claimed_inner_product`
  3. Add the malicious term: `Δ · β^(dim+1) · G` to the honest proof
  4. The modified proof verifies with the fake claimed inner product!
- **Implementation**:
  ```rust
  let honest_proof = algorithms::ILV::<E>::open(&ck, &a, &b);
  let difference = actual_inner_product - claimed_inner_product;
  let malicious_term = ck.powers_of_beta_g_first[dim + 1].mul(difference.into_repr());
  let proof = Proof((honest_proof.0.into_projective() + malicious_term).into_affine());
  ```
- **Mathematical Insight**: The verification equation implicitly uses `claimed_ip · β^(dim+1)` to "fill the gap" at position (dim+1). Since the prover can explicitly add any value at this position using the leaked SRS element, they can make any claimed value verify.
- **Impact**: Complete soundness break - the attacker can forge proofs for any false inner product claim
- **Title Meaning**: "Bigger is Better" refers to the SRS being too big (514 elements instead of 513)
- **Result**: Successfully created forged proofs that verify with incorrect inner product values
- Complete working solution demonstrating elegant attack using existing honest algorithms plus one malicious modification

## Puzzle F1: Gamma Ray - Elliptic Curve Double-Spend Attack
**Status**: ✅ Solved  
**Directory**: `puzzle-gamma-ray/`

A Zcash-inspired private transaction system vulnerability where only the x-coordinate of elliptic curve public keys is stored in the Merkle tree. This design flaw enables double-spending attacks by exploiting the fact that points (x, y) and (x, -y) are both valid on the curve but produce different nullifiers.

**Key Concepts**:
- Elliptic curve cryptography
- Groth16 zkSNARKs
- MNT4-753/MNT6-753 curve cycles
- Merkle tree commitments
- Nullifier-based double-spend prevention
- Public key representation vulnerabilities

**Solution**: 
- **Root Cause**: The circuit only stores `pk.x` (x-coordinate) in the Merkle tree leaf (line 113: `let leaf_g: Vec<_> = vec![pk.x];`)
- **Vulnerability**: For any point P = (x, y) on an elliptic curve, the point -P = (x, -y) is also valid
- **Attack Strategy**: 
  1. Original spend: Uses `secret = leaked_secret` → produces `pk = G·s = (x, y)`
  2. Double spend: Uses `secret_hack = -leaked_secret` → produces `pk_hack = G·(-s) = (x, -y)`
  3. Both have the same x-coordinate, so both pass Merkle tree verification
  4. But `Hash(s) ≠ Hash(-s)`, creating different nullifiers
- **Implementation**:
  ```rust
  // Convert to MNT6 scalar field, negate, then convert back to MNT4 field
  let leaked_secret_mnt6 = MNT6BigFr::from_le_bytes_mod_order(&leaked_secret.into_bigint().to_bytes_le());
  let secret_hack_mnt6 = -leaked_secret_mnt6;
  let secret_hack = MNT4BigFr::from_le_bytes_mod_order(&secret_hack_mnt6.into_bigint().to_bytes_le());
  let nullifier_hack = <LeafH as CRHScheme>::evaluate(&leaf_crh_params, vec![secret_hack]).unwrap();
  ```
- **Technical Details**: 
  - Negation performed in MNT6 scalar field (elliptic curve group order)
  - Circuit constraint (line 98) enforces `secret <= MNT6BigFr::MODULUS`
  - Both secrets satisfy this constraint after proper field conversion
  - Poseidon hash used for nullifier generation
- **Impact**: Complete double-spend attack - same coin can be spent twice with different nullifiers
- **Fix**: Store the full public key point (both x and y coordinates) in the Merkle tree
- **Result**: Successfully created two valid proofs for the same coin with different nullifiers
- Complete working solution demonstrating a critical vulnerability in elliptic curve-based privacy systems

## Puzzle F2: Supervillain - BLS Signature Rogue Key Attack
**Status**: ✅ Solved  
**Directory**: `puzzle-supervillain/`

A BLS signature aggregation vulnerability exploiting a flawed proof-of-possession (PoP) scheme. This puzzle demonstrates how a malleable PoP scheme using per-index points enables rogue key attacks, allowing an attacker to forge aggregate signatures without knowing any private keys.

**Key Concepts**:
- BLS signature aggregation
- Proof-of-possession (PoP) schemes
- Rogue key attacks
- B-KEA assumption vulnerabilities
- Pairing-based cryptography
- BLS12-381 elliptic curves

**Solution**: 
- **Root Cause**: The PoP scheme uses different points for each index: `derive_point_for_pok(i) = (i+1) · G2`
- **Critical Flaw**: Unlike secure PoP schemes (e.g., Sapling) that use a single shared point, this per-index approach makes the scheme malleable
- **Vulnerability**: The malleability allows combining existing PoP proofs to create valid proofs for keys with unknown discrete logs
- **Attack Strategy**: 
  1. **Rogue Key Construction**: Set `new_key = -Σ(pk_i)` to cancel all existing public keys
  2. **Malleable PoP Exploit**: Create valid proof without knowing the secret key
     - For existing key at index i: `e(pk_i, (i+1)·G2) = e(G1, proof_i)`
     - This means: `e(pk_i, G2)^(i+1) = e(G1, proof_i)`
     - Therefore: `e(pk_i, G2) = e(G1, proof_i/(i+1))`
  3. **Mathematical Derivation**: For new key at index n:
     ```
     e(new_key, (n+1)·G2) = e(-Σ(pk_i), (n+1)·G2)
                          = Π e(pk_i, G2)^(-(n+1))
                          = Π e(G1, proof_i/(i+1))^(-(n+1))
                          = e(G1, Σ(-(n+1)/(i+1) · proof_i))
     ```
     Therefore: `new_proof = Σ(-(n+1)/(i+1) · proof_i)`
  4. **Aggregate Key Cancellation**: `aggregate_key = new_key + Σ(pk_i) = 0`
  5. **Signature Forgery**: Any signature on the zero key is valid, so `aggregate_signature = 0`
- **References**: 
  - [Power of Proofs-of-Possession Paper](https://rist.tech.cornell.edu/papers/pkreg.pdf)
  - [Sapling Security Analysis by Mary Maller](https://github.com/zcash/sapling-security-analysis/blob/master/MaryMallerUpdated.pdf)
- **Impact**: Complete aggregation security break - attacker can forge valid aggregate signatures without any private keys
- **Fix**: Use a single, shared point for all PoP verifications instead of per-index points
- **Result**: Successfully created malicious key with valid PoP and forged aggregate signature
- Complete working solution demonstrating why PoP scheme design is critical for BLS signature aggregation security

## Puzzle F3: Chaos Theory - ElGamal + BLS Key Reuse Attack
**Status**: ✅ Solved  
**Directory**: `puzzle-chaos-theory/`

A cryptographic vulnerability exploiting key reuse between ElGamal encryption and BLS signatures. This puzzle demonstrates how using the same secret key for both encryption and signing enables an attacker to decrypt messages using pairing-based algebraic manipulations.

**Key Concepts**:
- ElGamal encryption
- BLS signatures
- Pairing-based cryptography
- BLS12-381 elliptic curves
- Bilinear pairings
- Key separation principle
- Encrypt-then-sign schemes

**Solution**: 
- **Root Cause**: The sender's secret key `s_k` is used for both ElGamal encryption and BLS signature generation:
  - Encryption: `C_2 = R_pk · s_k + M`
  - Signature: `S = H(C) · s_k`
- **Vulnerability**: This key reuse creates an exploitable algebraic relationship via pairing bilinearity
- **Attack Strategy**: 
  1. **Starting Relationship**: Consider the pairing `e(C_2, H(C))`
  2. **Substitute C_2**: `e(R_pk · s_k + M, H(C))`
  3. **Bilinearity Split**: `e(R_pk · s_k, H(C)) · e(M, H(C))`
  4. **Scalar Move**: Move `s_k` from G1 to G2: `e(R_pk, H(C) · s_k) · e(M, H(C))`
  5. **Signature Substitution**: Replace `H(C) · s_k` with `S`: `e(R_pk, S) · e(M, H(C))`
  6. **Isolate Message**: Rearrange to solve for message term:
     ```
     e(M, H(C)) = e(C_2, H(C)) · e(R_pk, S)^(-1)
     ```
- **Mathematical Insight**: 
  - Pairing bilinearity: `e(aP, bQ) = e(P, Q)^(ab) = e(bP, aQ)`
  - The signature provides the missing piece `H(C) · s_k` to cancel out `s_k` from the encryption
  - Result is an equation that only depends on the message `M`
- **Attack Properties**:
  - No secret key recovery needed
  - Works with small message space (brute-force search)
  - Completely breaks confidentiality
  - Signature provides decryption oracle
- **Impact**: Complete confidentiality break - attacker can decrypt any message by testing candidates against the pairing equation
- **Fix**: Use separate, independent keys for encryption and signing (key separation principle)
- **Result**: Successfully recovered the encrypted message index from the blob
- Complete working solution demonstrating why **key separation** is critical in cryptographic protocols - never reuse keys across different primitives!

## Puzzle V1: Zeitgeist - Halo2 Verifier Polynomial Leakage Attack
**Status**: ✅ Solved  
**Directory**: `puzzle-zeitgeist/`

A Halo2 zero-knowledge proof vulnerability where the verifier exposes polynomial evaluations at challenge points, enabling an attacker to recover the secret witness through Lagrange interpolation. This puzzle demonstrates how information leakage during verification can completely break the zero-knowledge property.

**Key Concepts**:
- Halo2 proving system
- Poseidon hash circuits
- Polynomial commitments (KZG + SHPLONK)
- Lagrange interpolation attacks
- Verifier information leakage
- BN256 elliptic curves
- Zero-knowledge property violations

**Solution**: 
- **Root Cause**: The Halo2 verifier exposes evaluations `advice_evals[0][1]` at challenge points `x` during proof verification
- **Vulnerability**: The secret witness resides in advice column index 1 at position 3, and remains constant across all proofs (independent of the nonce)
- **Attack Strategy**: 
  1. **Data Collection**: Capture 64 verification attempts to collect polynomial evaluations
     - Each verification exposes `x` (challenge point) and `advice_evals[0][1]` (evaluation at x)
     - All proofs use the same secret but different random nonces
  2. **Polynomial Reconstruction**: Use Lagrange interpolation to reconstruct the polynomial
     ```rust
     let coeffs = lagrange_interpolate(&all_xs, &first_evals);
     ```
     - With 64 points, we can uniquely reconstruct a polynomial of degree ≤ 63
  3. **Secret Extraction**: Evaluate the reconstructed polynomial at ω²
     ```rust
     let w = Fr::from_str_vartime("12799441450189702121232122059226990287081568291547011007819741462284200902087").unwrap();
     let secret = eval_polynomial(&coeffs, w.square());
     ```
     - The value ω is the primitive root of unity for the evaluation domain
     - ω² corresponds to position 3 in the domain (where the secret resides)
- **Implementation Details**:
  - Modified `halo2_proofs/src/plonk/verifier.rs` to capture evaluation data
  - Added global storage using `Mutex<Vec<String>>` for thread-safe data collection
  - Implemented hex string parsing with proper little-endian byte ordering
  - Extracted evaluation at index 1 (not 0) as specified in the hints
- **Mathematical Insight**: 
  - The circuit uses two Poseidon hashes: one for commitment, one for nullifier
  - Commitment: `Poseidon(secret, 0)` - independent of nonce
  - Nullifier: `Poseidon(secret, nonce)` - varies with each proof
  - The secret polynomial remains the same across all proofs, while nullifier polynomials differ
- **Recovered Secret**: 
  ```
  0x066ab256379d1a0d7bd1dd54cf3f4171edbf5ca3976e8956fe0ddd10af67418d
  ```
- **Verification**: 
  ```rust
  assert_eq!(Poseidon(secret, 0), commitment); // ✅ Passed
  ```
- **Impact**: Complete zero-knowledge break - the verifier leaks enough information to reconstruct the private witness
- **Fix**: Verifier should never expose intermediate polynomial evaluations; only verify without returning sensitive data
- **Puzzle Name Insight**: "Zeitgeist" (German for "spirit of the times") hints at the time-dependent nature of collecting multiple proofs over time
- **Result**: Successfully extracted Bob's secret private key from 64 intercepted proof verifications
- Complete working solution with comprehensive documentation (ANALYSIS.md, MECHANISM_EXPLAINED.md, PUZZLE_SUMMARY.md)

## Puzzle V2: Don't Look Up - ProtoStar Lookup Protocol Attack
**Status**: ✅ Solved  
**Directory**: `puzzle-dont-look-up/`

A zero-knowledge lookup protocol vulnerability exploiting small field sizes in the ProtoStar special-sound lookup protocol. This puzzle demonstrates how to create valid proofs for values outside the intended range by exploiting the field arithmetic properties and multiplicity vector manipulation.

**Key Concepts**:
- ProtoStar lookup protocol (variant of LogUp)
- Special-sound lookup arguments
- Logarithmic derivatives
- Small field size vulnerabilities
- Multiplicity vector manipulation
- Range check bypass techniques
- Field extension security

**Solution**: 
- **Root Cause**: The protocol uses a small prime field (p = 70,937) and allows manipulation of the multiplicity vector
- **Vulnerability**: The verification equation `sum(h_i) = sum(g_i)` can be satisfied by setting all multiplicities to zero
- **Attack Strategy**: 
  1. **Witness Vector**: Create a vector of length p (70,937) where every element is 2^15 (32,768)
  2. **Multiplicity Vector**: Set all elements in the multiplicity vector m to zero
  3. **Mathematical Exploit**: Since 2^15 is not in the range [0, 2^6-1] = [0, 63], it doesn't appear in the lookup table
  4. **Verification Bypass**: The sum of multiplicities becomes 0, making the verification equation hold
- **Technical Details**:
  - Field size: p = 70,937 (≈16-bit prime)
  - Extension field: x^6 + 70897x^5 + 34941x^4 + 45405x^3 + 15086x^2 + 39025x + 3
  - Target value: 2^15 = 32,768 (outside range [0, 63])
  - Protocol: ProtoStar special-sound lookup (Section 4.3, p. 34)
- **Mathematical Insight**: 
  - The protocol verifies that witness elements are in the lookup table by checking multiplicities
  - By setting multiplicities to zero, we bypass the range check entirely
  - The small field size enables this attack by making the witness vector manageable
- **Impact**: Complete range check bypass - can prove any value is "in range" regardless of actual value
- **Security Lesson**: Small fields combined with lookup protocols can create unexpected vulnerabilities
- **Puzzle Name Insight**: "Don't Look Up" refers to not looking up values in the table (bypassing the lookup check)
- **Result**: Successfully created a valid proof that 2^15 is in the range [0, 63] when it's actually not
- Complete working solution demonstrating how field size and protocol design interact to create vulnerabilities
## Puzzle V3: Shadow - JWT.pk Identity Infrastructure Attack
**Status**: ✅ Solved  
**Directory**: `puzzle-shadow/`

A critical vulnerability in an identity infrastructure system where the identifier format allows manipulation to impersonate other users. This puzzle demonstrates how improper identifier concatenation and verification can enable account takeover attacks in zero-knowledge proof-based authentication systems.

**Key Concepts**:
- Identity infrastructure authentication
- SHA256 hashing in ZK circuits
- Identifier format vulnerabilities
- String concatenation attacks
- Account impersonation attacks
- Noir zero-knowledge proofs

**Solution**: 
- **Root Cause**: The identifier format `"{pk}_{pepper}"` uses an underscore separator without delimiting the end of the pk string
- **Vulnerability**: The circuit only verifies that Bob's public key appears *somewhere* in the identifier, not that it's in the correct position
- **Attack Strategy**: 
  1. **Construct Malicious Identifier**: Create an identifier of the form `"{ALICE_pk}_{ALICE_pepper}{BOB_pk}"`
  2. **Hash Verification**: This identifier hashes to one of the whitelisted values (Alice's registered hash), if you specify the length up to `{BOB_pk}`
  3. **Public Key Verification**: Bob's public key appears in the identifier (at the end)
  4. **Both Checks Pass**: The circuit accepts this as valid despite it containing both keys
- **Technical Details**: 
  - Alice's pk: 32 bytes (from circuit comment)
  - Alice's pepper: 32 bytes (from circuit comment)
  - Bob's pk: 32 bytes (from Prover.toml)
  - Total: 65 bytes = 32 + 1 + 32 = ALICE_pk + '_' + ALICE_pepper + ...BOB_pk appended
  - The identifier contains Bob's key at the end but hashes to Alice's registered value
- **Mathematical Insight**: 
  - SHA256 is deterministic: `SHA256(ALICE_pk_ALICE_pepper_BOB_pk)` ≠ `SHA256(ALICE_pk_ALICE_pepper)`
  - However, the first part `ALICE_pk_ALICE_pepper` alone hashes to Alice's registered digest
  - By appending Bob's key at the end, we satisfy both conditions
- **Impact**: Complete account takeover - Alice can authenticate as Bob while using her own registered identifier
- **Fix**: Verify that the public key appears only at the start of the identifier, delimited by exactly one underscore
- **Puzzle Name Insight**: "Shadow" refers to impersonating another user's identity in the authentication system
- **Result**: Successfully created a valid proof that authenticates as Bob using Alice's credentials
- Complete working solution demonstrating how identifier format vulnerabilities can break authentication systems
