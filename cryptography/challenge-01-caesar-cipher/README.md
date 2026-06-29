# Challenge 02: Caesar Cipher Decryption

> **Category:** Cryptography  
> **Difficulty:** Easy  
> **Points:** 50  
> **Author:** Coach Ay (MAPELEAD)

---

## 🎯 Objective

Decrypt the following message to find the flag.

## 📜 Challenge

```
Encrypted Message:
FLAG{pelcgb_ercynprg_zrgnkvag_pvcure}

Hint: The Romans used this technique to protect their military communications.
Each letter has been shifted by a consistent number of positions in the alphabet.
```

## 🛠️ Starter Script

```python
#!/usr/bin/env python3
"""
Caesar Cipher Decoder - CTF Challenge 02
Use this script to help solve the challenge
"""


def caesar_decrypt(ciphertext, shift):
    """Decrypt a Caesar cipher with given shift."""
    result = ""
    for char in ciphertext:
        if char.isalpha():
            ascii_offset = ord('A') if char.isupper() else ord('a')
            result += chr((ord(char) - ascii_offset - shift) % 26 + ascii_offset)
        else:
            result += char
    return result


def brute_force(ciphertext):
    """Try all possible shifts."""
    print("Trying all 26 possible shifts...\n")
    for shift in range(1, 27):
        decrypted = caesar_decrypt(ciphertext, shift)
        print(f"Shift {shift:2d}: {decrypted}")


# The encrypted flag
encrypted = "FLAG{pelcgb_ercynprg_zrgnkvag_pvcure}"

print("="*50)
print("MAPELEAD CTF - Challenge 02: Caesar Cipher")
print("="*50)
print(f"\nEncrypted: {encrypted}")
print("\nUse: caesar_decrypt(encrypted, [your_guess])")
print("Or: brute_force(encrypted) to see all possibilities")

# Uncomment to see the solution:
# brute_force(encrypted)
```

## 💡 Hints

<details>
<summary>Hint 1</summary>

The flag format is `FLAG{...}`. The word after `FLAG{` should be readable English.

</details>

## ✅ Solution

<details>
<summary>SPOILER: Click to reveal</summary>

The shift is **13** (ROT13 cipher).

**Decrypted:** `FLAG{crypto_replacement_metaknight_cipher}`

ROT13 is a special case of the Caesar cipher where the shift is 13. Applying ROT13 twice returns the original text.

```python
import codecs
result = codecs.decode("pelcgb_ercynprg_zrgnkvag_pvcure", 'rot_13')
# Result: crypto_replacement_metaknight_cipher
```

</details>

---

*Challenge created by MAPELEAD | For educational purposes only*
