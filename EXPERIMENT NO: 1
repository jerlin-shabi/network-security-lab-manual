### EXPERIMENT NO: 1 - IMPLEMENTATION OF SYMMETRIC KEY ALGORITHM USING AES

## AIM:
To implement the AES (Advanced Encryption Standard) symmetric key encryption and decryption algorithm in Python.

## THEORY:
AES (Advanced Encryption Standard) is a symmetric encryption algorithm widely used for securing data. It operates on fixed-size blocks of data (128 bits) and supports key sizes of 128, 192, and 256 bits. AES uses multiple rounds of substitution, permutation, mixing, and key addition transformations to ensure data security.

AES operates in different modes, including:
-ECB (Electronic Codebook)**: Simplest but less secure mode, encrypts each block independently.
-CBC (Cipher Block Chaining)**: Uses an Initialization Vector (IV) to ensure unique ciphertexts for identical plaintexts.
-CFB (Cipher Feedback)** and **OFB (Output Feedback)**: Convert AES into a stream cipher.
-GCM (Galois/Counter Mode)**: Provides authentication along with encryption.

For this experiment, we will use AES in **CBC (Cipher Block Chaining) mode**, which ensures security by chaining encrypted blocks and using an IV.

## REQUIREMENTS:
- Python 3.x
- `cryptography` library (install using `pip install cryptography`)

## PROCEDURE:
1. **Generate AES Key**: Create a random 256-bit key for encryption.
2. **Prepare Data for Encryption**:
   - Convert the plaintext into bytes.
   - Apply **PKCS7 padding** to ensure the data is a multiple of the AES block size (16 bytes).
3. **Encrypt Data**:
   - Generate a random **Initialization Vector (IV)**.
   - Encrypt the padded plaintext using **AES in CBC mode**.
   - Append IV to the ciphertext for decryption.
4. **Decrypt Data**:
   - Extract IV from the ciphertext.
   - Decrypt the data using AES and remove padding.
5. **Display Results**: Print the ciphertext and decrypted plaintext to verify correctness.

## CODE IMPLEMENTATION:
```python
from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes
from cryptography.hazmat.primitives import padding
from cryptography.hazmat.backends import default_backend
import os

def generate_key():
    """Generate a 256-bit key for AES encryption."""
    return os.urandom(32)  # AES-256 key

def encrypt(plaintext, key):
    """Encrypts plaintext using AES in CBC mode."""
    iv = os.urandom(16)  # Initialization Vector (IV)
    cipher = Cipher(algorithms.AES(key), modes.CBC(iv), backend=default_backend())
    encryptor = cipher.encryptor()
    
    # Padding to ensure block size is 16 bytes
    padder = padding.PKCS7(128).padder()
    padded_data = padder.update(plaintext.encode()) + padder.finalize()
    
    ciphertext = encryptor.update(padded_data) + encryptor.finalize()
    return iv + ciphertext  # Prepend IV to ciphertext for decryption

def decrypt(ciphertext, key):
    """Decrypts AES-encrypted ciphertext."""
    iv = ciphertext[:16]  # Extract IV from ciphertext
    actual_ciphertext = ciphertext[16:]
    cipher = Cipher(algorithms.AES(key), modes.CBC(iv), backend=default_backend())
    decryptor = cipher.decryptor()
    
    decrypted_padded = decryptor.update(actual_ciphertext) + decryptor.finalize()
    
    # Remove padding
    unpadder = padding.PKCS7(128).unpadder()
    decrypted_data = unpadder.update(decrypted_padded) + unpadder.finalize()
    
    return decrypted_data.decode()

# Example Usage
key = generate_key()
plaintext = "Hello, this is AES encryption!"

ciphertext = encrypt(plaintext, key)
print("Ciphertext:", ciphertext.hex())

decrypted_text = decrypt(ciphertext, key)
print("Decrypted Text:", decrypted_text)
```

## EXPECTED OUTPUT:
- The program should output an encrypted ciphertext (in hexadecimal format) and successfully decrypt it back to the original plaintext.

## CONCLUSION:
AES is a widely used symmetric encryption algorithm that provides high security. This experiment demonstrates secure encryption and decryption using AES in CBC mode with proper padding.

## VIVA QUESTIONS:
1. What is AES, and how does it work?
2. Why do we use padding in AES encryption?
3. What is the significance of the Initialization Vector (IV)?
4. How is AES different from DES?
5. Can AES encryption be cracked? If so, how?
