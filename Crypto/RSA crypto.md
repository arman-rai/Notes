https://muirlandoracle.co.uk/2020/01/29/rsa-encryption/

- Two large primes: `p` and `q`
- Compute: `n = p * q`
- Compute: `phi = (p-1)*(q-1)`
- Public key: `(e, n)`
- Private key: `d`, where:  `d ≡ e⁻¹ mod phi`

- **RSA Encryption**: C = M^e mod N (where C=ciphertext, M=plaintext, e=public exponent, N=modulus)
- **RSA Decryption**: M = C^d mod N (where d=private exponent)

- **Homomorphic Property**: RSA has a multiplicative homomorphic property:
    - E(M1 × M2) = E(M1) × E(M2) mod N
    - D(C1 × C2) = D(C1) × D(C2) mod N

