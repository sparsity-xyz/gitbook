# Agent Signature Verification

## Signature Verification Process

### Overview

The Sparsity platform uses ECDSA (Elliptic Curve Digital Signature Algorithm) with SHA-384 hashing to verify message authenticity. Each response comes with a digital signature to ensure the message hasn't been tampered with and originates from a trusted Sparsity server.

To establish this trust, Sparsity provides a verifiable chain of evidence from source code to signed output, ensuring the integrity of the execution environment. This trust chain can be validated in five steps:

1. **Codebase A** implements an HTTPS client that communicates with a specific HTTPS endpoint (e.g., OpenAI).
2. **Codebase A** is packaged into **Docker image B**.
3. **Docker image B** is then converted into an **AWS Nitro Enclave EIF image C**, a secure execution environment.
4. **When running**, image C's instance possesses a unique **public key (PK-C)**, whose corresponding **private key (PVK-C)** never leaves the enclave.
5. For a prompt like `"hi"`, image C communicates with the GPT-4 endpoint and produces a signed response such as `"Hello! How can I assist you today?"`. This response is cryptographically signed using **PVK-C**, and the corresponding **attestation document** includes **PK-C** for verification.

This attested signature, paired with the public key, enables any verifier to independently confirm that the message was generated inside the trusted enclave instance running code from the verified image.

### Verification Steps

1. **Required Data**
   * Message content
   * Digital signature
   * Public key (in Attestation Document)
2. **Message Preprocessing**
   * For string messages: Convert to UTF-8 encoded bytes
   * For JSON objects: Convert to canonicalized JSON string (using `,` and `:` as separators, keys sorted)
   * For byte messages: Use as is
3. **Signature Verification**
   * Algorithm: ECDSA with SHA-384
   * Public key format: DER
   * Verify signature against the message

### Verification Result

* Success (`true`): Message is authentic and untampered
* Failure (`false`): Message may be tampered or from untrusted source

### Example Code

```python
from cryptography.hazmat.primitives import hashes, serialization
from cryptography.hazmat.primitives.asymmetric import ec
from cryptography.hazmat.backends import default_backend
import json

def verify_signature(pub_key: bytes, msg: Union[bytes, str, dict], signature: bytes) -> bool:
    # Load public key
    pub_key = serialization.load_der_public_key(pub_key, backend=default_backend())
    
    # Preprocess message
    if isinstance(msg, str):
        msg = msg.encode()
    elif isinstance(msg, dict):
        msg = json.dumps(msg, separators=(',', ':'), sort_keys=True).encode()
    
    # Verify signature
    try:
        pub_key.verify(signature, msg, ec.ECDSA(hashes.SHA384()))
        return True
    except:
        return False
```

### Security Recommendations

1. Always verify signatures - never skip this step
2. Ensure correct public key is used
3. Regularly update public keys
4. Do not trust messages with failed verification

### Important Notes

* Signature verification is crucial for message authenticity
* Verification failure may indicate:
  * Message tampering
  * Incorrect public key
  * Invalid signature format
  * Unexpected message format

### Technical Details

* Hash Algorithm: SHA-384
* Signature Algorithm: ECDSA
* Public Key Format: DER
* Message Encoding: UTF-8 for strings, canonicalized JSON for objects

