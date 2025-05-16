# Agent Signature Verification

## Signature Verification Process

### Overview

The Sparsity platform uses ECDSA (Elliptic Curve Digital Signature Algorithm) with SHA-384 hashing to verify message authenticity. Each response comes with a digital signature to ensure the message hasn't been tampered with and originates from a trusted Sparsity server.

### Verification Steps

1. **Required Data**
   * Message content
   * Digital signature
   * Public key
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

