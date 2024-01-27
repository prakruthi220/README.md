- 👋 Hi, I’m @prakruthi220
- 👀 I’m interested in cryptography.

<!---
prakruthi220/prakruthi220 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import secrets

def generate_one_time_pad(message_length):
    return ''.join(secrets.choice('01') for _ in range(message_length * 8))

def encrypt(message, one_time_pad):
    # Convert the message and one-time pad to binary strings
    message_binary = ''.join(format(ord(char), '08b') for char in message)
    one_time_pad_binary = ''.join(format(int(bit), '08b') for bit in one_time_pad)

    # XOR the message and one-time pad
    ciphertext = ''.join(str(int(m_bit) ^ int(k_bit)) for m_bit, k_bit in zip(message_binary, one_time_pad_binary))

    return ciphertext

def decrypt(ciphertext, one_time_pad):
    # XOR the ciphertext and one-time pad to recover the original message
    decrypted_message_binary = ''.join(str(int(c_bit) ^ int(k_bit)) for c_bit, k_bit in zip(ciphertext, one_time_pad))

    # Convert the binary string back to characters
    decrypted_message = ''.join(chr(int(decrypted_message_binary[i:i+8], 2)) for i in range(0, len(decrypted_message_binary), 8))

    return decrypted_message

def main():
    # Get user input
    message = input("Enter the message to encrypt: ")

    # Generate a one-time pad
    one_time_pad = generate_one_time_pad(len(message))

    # Encrypt the message
    ciphertext = encrypt(message, one_time_pad)

    print(f"\nGenerated One-Time Pad: {one_time_pad}")
    print(f"Encrypted Message (in binary): {ciphertext}")

    # Decrypt the message
    decrypted_message = decrypt(ciphertext, one_time_pad)
    print(f"Decrypted Message: {decrypted_message}")

if __name__ == "__main__":
    main()

git rebase -i HEAD~0

