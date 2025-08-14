RSA is based on:

- Two large primes: `p` and `q`
- Compute: `n = p * q`
- Compute: `phi = (p-1)*(q-1)`
- Public key: `(e, n)`
- Private key: `d`, where:  
    `d ≡ e⁻¹ mod phi`

- **RSA Encryption**: C = M^e mod N (where C=ciphertext, M=plaintext, e=public exponent, N=modulus)
- **RSA Decryption**: M = C^d mod N (where d=private exponent)

- **Homomorphic Property**: RSA has a multiplicative homomorphic property:
    - E(M1 × M2) = E(M1) × E(M2) mod N
    - D(C1 × C2) = D(C1) × D(C2) mod N




# RSA Oracle Challenge - A High School Math Problem Approach

Let's frame this as a math problem like you'd see in algebra class:

## **The Problem**

We have a special machine (the Oracle) that can:
- Encrypt any number using the formula: **C = M^e mod N**
- Decrypt any number using the formula: **M = C^d mod N**

Where:
- **M** is your original message (a number)
- **C** is the encrypted message (a number)
- **e** and **N** are public numbers (we know e is usually 65537)
- **d** is a secret number (we don't know it)

**The Challenge**: We have a secret password encrypted as **C_target**. The Oracle refuses to decrypt this specific number for us. How can we find the original password?

## **The Mathematical Solution**

### **Step 1: Choose a Simple Number**

Let's pick a simple number we know, like **M₁ = 2**.

### **Step 2: Encrypt Our Simple Number**

Ask the Oracle to encrypt our simple number:
```
C₁ = M₁^e mod N
C₁ = 2^e mod N
```

The Oracle gives us the value of **C₁**.

### **Step 3: Create a Special Number to Decrypt**

Now we create a special number **C₂** using this formula:
```
C₂ = (C_target × C₁) mod N
```

### **Step 4: Ask the Oracle to Decrypt Our Special Number**

We send **C₂** to the Oracle for decryption:
```
M₂ = C₂^d mod N
```

### **Step 5: The Magic of Algebra**

Watch what happens when we substitute our expressions:

```
M₂ = (C₂)^d mod N
M₂ = [(C_target × C₁) mod N]^d mod N
M₂ = (C_target × C₁)^d mod N
M₂ = (C_target^d × C₁^d) mod N
M₂ = (C_target^d mod N) × (C₁^d mod N) mod N
M₂ = (C_target^d mod N) × (C₁^d mod N) mod N
```

But we know:
- **C_target^d mod N** is the original password we want (let's call it **M_target**)
- **C₁^d mod N** is our original simple number **M₁ = 2**

So:
```
M₂ = (M_target × M₁) mod N
M₂ = (M_target × 2) mod N
```

### **Step 6: Solve for the Password**

Now we can solve for **M_target**:
```
M_target = M₂ ÷ M₁
M_target = M₂ ÷ 2
```

## **Example with Numbers**

Let's say:
- **C_target** = 123456789 (our encrypted password)
- **M₁** = 2 (our chosen simple number)
- Oracle encrypts **M₁** and gives us **C₁** = 987654321

Now we calculate:
```
C₂ = (C_target × C₁) mod N
C₂ = (123456789 × 987654321) mod N
C₂ = 121932631112635269 mod N
```

We send **C₂** to Oracle for decryption, and it returns:
```
M₂ = 243865262225270538
```

Now we find our password:
```
M_target = M₂ ÷ M₁
M_target = 243865262225270538 ÷ 2
M_target = 121932631112635269
```

Finally, we convert this number to text to get our password!

## **Why This Works**

This works because of the special property of RSA:
```
Decrypt(Encrypt(A) × Encrypt(B)) = A × B
```

In our case:
```
Decrypt(Encrypt(Password) × Encrypt(2)) = Password × 2
```

So if we divide the result by 2, we get the password!

## **The Complete Math Problem**

**Given:**
- An Oracle that computes C = M^e mod N and M = C^d mod N
- A target ciphertext C_target that the Oracle won't decrypt
- e = 65537 (public exponent)

**Find:**
- The original message M_target where C_target = M_target^e mod N

**Solution:**
1. Choose M₁ = 2
2. Compute C₁ = Oracle_Encrypt(M₁)
3. Compute C₂ = (C_target × C₁) mod N
4. Compute M₂ = Oracle_Decrypt(C₂)
5. Compute M_target = M₂ ÷ M₁
6. Convert M_target to text to get the password

This is like having a special calculator that won't tell you what's in a locked box, but will tell you what's in two locked boxes multiplied together. By putting your box together with a box you know the contents of, you can figure out what's in your original box!