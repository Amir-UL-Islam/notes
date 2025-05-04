A JWT consists of three parts, separated by dots (`.`):

`HEADER.PAYLOAD.SIGNATURE`

Each part is Base64URL-encoded:

1. **Header** – Metadata about the token, including the algorithm used for signing.
    
2. **Payload** – Claims (data) like user ID, roles, expiration time, etc.
    
3. **Signature** – A cryptographic signature that ensures the token hasn't been tampered with.
    

---

### **How is the Signature Created?**

The signature is generated using a cryptographic hashing algorithm (e.g., HMAC or RSA):

#### **HMAC-based Signing (HS256, HS384, HS512)**

For **symmetric** algorithms like HMAC (`HS256`), both the issuer and the verifier use a **shared secret key**.

$$
SIGNATURE = HMAC-SHA256(     base64urlEncode(HEADER) + "." + base64urlEncode(PAYLOAD),     secretKey )
$$


### **RSA Signature Verification Formula**

The JWT signature is generated using this formula
$$
SIGNATURE = Encrypt( HASH(base64urlEncode(HEADER) + "." + base64urlEncode(PAYLOAD)), PRIVATE_KEY)
$$

When verifying, the server decrypts the signature using the public 

$$
DECRYPT(SIGNATURE, PUBLIC_KEY) == HASH(base64urlEncode(HEADER) + "." + base64urlEncode(PAYLOAD))
$$

If the hashes match, the JWT is valid. If they don’t, the token is tampered with or invalid.

**Breaking Down RSA Signature Verification in JWTs:**
#### ** Step 1: Signing the JWT (On the Auth Server)**
Before verification happens, the authentication server **creates** a JWT signature using **its private key**.
#### **Compute the Hash**
The first step in signing a JWT is creating a hash of the **header and payload**.
`HASH = SHA256(base64urlEncode(HEADER) + "." + base64urlEncode(PAYLOAD))`

This is a **fixed-length hash** (a digital fingerprint of the data).
#### **Encrypt the Hash with the Private Key**
The authentication server **encrypts** this hash using its **private key** (RSA encryption).
`SIGNATURE = ENCRYPT(HASH, PRIVATE_KEY)`

This **encrypted hash** becomes the **JWT signature**.

📌 **Key Point:**

- The **signature is NOT the raw hash** but an **encrypted** version of it.
---

#### ** Step 2: Verifying the JWT (On the API Server)**
When the JWT reaches the API server, it needs to verify the signature.
#### **Extract the Header, Payload, and Signature**

The JWT consists of three parts:

`<Header>.<Payload>.<Signature>`

The API server extracts:

- **Header** (JSON with metadata like algorithm)
    
- **Payload** (User data & claims)
    
- **Signature** (Encrypted hash)
#### ** Recompute the Hash (Independent Calculation)**
The server **ignores** the signature for now.  
It **recomputes** the hash **from scratch** using the **same algorithm**:
`EXPECTED_HASH = SHA256(base64urlEncode(HEADER) + "." + base64urlEncode(PAYLOAD))`

This should produce the **same hash** that was originally signed.
#### **Decrypt the Signature with the Public Key**
The API server **decrypts** the signature using the **public key**:

`DECRYPT(SIGNATURE, PUBLIC_KEY) = ORIGINAL_HASH`

📌 **What is the result of decryption?**

- The result is **the original SHA-256 hash** that the authentication server created.
---

#### ** Step 3: Compare the Hashes**
Now, the server has two hashes:

1. **Expected Hash** → The hash it computed from the header and payload.
    
2. **Decrypted Hash** → The hash recovered from the JWT's signature.

If these **two hashes match**, the JWT is **valid**.  
If they **don't match**, the JWT has been **tampered with** or is **invalid**.

`IF DECRYPT(SIGNATURE, PUBLIC_KEY) == EXPECTED_HASH    ✅ Signature is valid (JWT is authentic) ELSE    ❌ Signature is invalid (JWT is tampered or forged)`
