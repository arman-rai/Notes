RSA is based on:

- Two large primes: `p` and `q`
- Compute: `n = p * q`
- Compute: `phi = (p-1)*(q-1)`
- Public key: `(e, n)`
- Private key: `d`, where:  
    `d ≡ e⁻¹ mod phi`

Encryption: `c = m^e % n`  
Decryption: `m = c^d % n`
