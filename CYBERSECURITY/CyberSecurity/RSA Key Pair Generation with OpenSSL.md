````markdown
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
````

### 🔍 Explanation

* `openssl` → The tool we are using
* `genrsa` → Generates an RSA private key
* `-out private.pem` → Saves the key as *private.pem*
* `2048` → Key size (secure standard)

### 📄 View the Private Key

```bash
cat private.pem
```

---

## 🔑 Step 2: Extract the Public Key

Now extract the public key from the private key:

```bash
openssl rsa -in private.pem -pubout -out public.pem
```

### 🔍 Explanation

* `openssl rsa` → Works with RSA keys
* `-in private.pem` → Input private key
* `-pubout` → Extract public key
* `-out public.pem` → Save as *public.pem*

✔️ If you see:

```
writing RSA key
```

It means the operation was successful.

### 📁 Verify Files

```bash
ls
```

You should see:

* `private.pem`
* `public.pem`

---

## 🔒 Step 3: Encrypt a Message with the Public Key

### ✍️ Create a Message

```bash
echo "This is a secret message" > message.txt
```

### 🔐 Encrypt the Message

```bash
openssl pkeyutl -encrypt -pubin -inkey public.pem -in message.txt -out encrypted.bin
```

### 🔍 Explanation

* `openssl pkeyutl` → Tool for key operations
* `-encrypt` → Encryption mode
* `-pubin` → Using a public key
* `-inkey public.pem` → Public key file
* `-in message.txt` → Input message
* `-out encrypted.bin` → Encrypted output

📌 The output file will contain unreadable binary data.

---

## 🔓 Step 4: Decrypt the Message with the Private Key

### 🔑 Decrypt the File

```bash
openssl pkeyutl -decrypt -inkey private.pem -in encrypted.bin -out decrypted.txt
```

### 🔍 Explanation

* `-decrypt` → Decryption mode
* `-inkey private.pem` → Private key
* `-in encrypted.bin` → Encrypted file
* `-out decrypted.txt` → Decrypted output

### ✅ Verify Decryption

```bash
cat decrypted.txt
```

You should see:

```
This is a secret message
```

---

## 🎉 Lab Summary

You have successfully completed a full asymmetric encryption cycle:

* ✅ Generated an RSA key pair
* 🔐 Encrypted a message using the public key
* 🔓 Decrypted it using the private key

---

## 🌐 Real-World Applications

This is how secure communication works in:

* HTTPS websites 🔒
* Secure email 📧
* Digital signatures ✍️

---

## 📚 Conclusion

Asymmetric encryption is a powerful method that enables secure communication without prior key exchange. Understanding RSA and tools like OpenSSL is essential for cybersecurity, networking, and modern web security.

---

## 🏷️ Tags

`RSA` `OpenSSL` `Encryption` `Cybersecurity` `Linux` `Cryptography`

```
```
