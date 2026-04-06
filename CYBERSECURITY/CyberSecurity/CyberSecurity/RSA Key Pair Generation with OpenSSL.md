# 🔐 RSA Key Pair Generation with OpenSSL

In this lab, you will learn about **asymmetric encryption**, also known as **public-key cryptography**. This one-way relationship is the foundation of secure communication over insecure networks.

Unlike normal encryption that uses only **one key** for both locking and unlocking messages, asymmetric encryption uses **two keys**:

- 🔓 **Public Key** → can be shared with anyone. It is used to **encrypt** messages.
- 🔐 **Private Key** → must stay secret. It is used to **decrypt** messages.

This system allows people to send secure messages without first sharing a secret key.

---

## 📌 Objectives

In this lab, you will:

- Generate an RSA key pair  
- Extract a public key from a private key  
- Encrypt a message using the public key  
- Decrypt the message using the private key  

---

## 🧰 Tools Used

- OpenSSL  
- Linux Terminal (Kali Linux)

---

## 🧪 Step 1: Generate RSA Key Pair

Run the following command:

```bash
openssl genrsa -out private.pem 2048
