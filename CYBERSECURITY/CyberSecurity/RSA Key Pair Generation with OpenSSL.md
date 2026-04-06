# 🔐 RSA Key Pair Generation with OpenSSL

In this lab, you will learn about **asymmetric encryption**, also known as public-key cryptography. This one-way relationship is the foundation of secure communication over insecure networks.

Unlike symmetric encryption that uses only **one key** for both locking and unlocking messages, asymmetric encryption uses **two keys**: a **public key** and a **private key**.

- 🔓 **Public Key** → can be shared with anyone. It is used to lock (encrypt) messages.
- 🔐 **Private Key** → must stay secret. It is used to unlock (decrypt) messages.

This system lets people send secret messages without needing to share a secret key first.

In this lab, we will use the popular **RSA** method and the `openssl` tool. You will learn how to:
- Create your own pair of keys
- Lock a message using the public key
- Unlock the message using the private key

## 🧰 Tools Used

- OpenSSL
- Linux Terminal (Kali Linux)

---

## Step 1: Generate RSA Key Pair

Run this command to create your RSA key pair:

```bash
openssl genrsa -out private.pem 2048
Explanation

openssl → The tool we are using
genrsa → Command to generate an RSA private key
-out private.pem → Saves the key to a file named private.pem
2048 → Makes a 2048-bit key (a common secure size)

You can view the content of the private key file with:
Bashcat private.pem
The output will look similar to this:
text-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQE...
...
-----END RSA PRIVATE KEY-----

Step 2: Extract the Public Key
The private.pem file contains both the private and public parts. Now extract the public key so others can use it:
Bashopenssl rsa -in private.pem -pubout -out public.pem
You should see a message like:
textwriting RSA key
This is a good sign — everything worked correctly.
Explanation

openssl rsa → Tool for working with RSA keys
-in private.pem → Uses your private key file
-pubout → Outputs only the public key
-out public.pem → Saves it as public.pem

After this step, you should see both files in your directory:
Bashls
Expected output:
textprivate.pem  public.pem

Step 3: Encrypt a Message with the Public Key
First, create a simple secret message:
Bashecho "This is my secret message!" > message.txt
Now encrypt it using the public key:
Bashopenssl pkeyutl -encrypt -pubin -inkey public.pem -in message.txt -out encrypted.bin
Explanation

openssl pkeyutl → Tool for public key operations (encrypt/decrypt)
-encrypt → We want to encrypt
-pubin → Tells OpenSSL we are using a public key
-inkey public.pem → Uses your public key
-in message.txt → The message to encrypt
-out encrypted.bin → Saves the encrypted result

If you try to view the encrypted file, it will show unreadable binary data:
Bashcat encrypted.bin

Step 4: Decrypt the Message with the Private Key
Decrypt the encrypted file using your private key:
Bashopenssl pkeyutl -decrypt -inkey private.pem -in encrypted.bin -out decrypted.txt
Explanation

-decrypt → We want to decrypt
-inkey private.pem → Uses your private key
-in encrypted.bin → The encrypted file
-out decrypted.txt → Saves the result as text

Now check the decrypted message:
Bashcat decrypted.txt
You should see:
textThis is my secret message!

✅ Summary
You have successfully completed a full asymmetric encryption cycle:

Generated an RSA key pair
Encrypted a message with the public key (anyone can do this)
Decrypted it with the private key (only you can do this)

This is how secure communication works on the internet — for example, in HTTPS websites, secure email (PGP/S/MIME), SSH, and digital signatures.

🔍 Bonus Tips

Never share your private.pem file.
2048-bit RSA is currently considered secure for most uses, but 4096-bit is even stronger.
In real-world applications, RSA is often used to encrypt a symmetric key (hybrid encryption) for better performance.
