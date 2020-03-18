---
layout: article
title:  "macOS: Encrypt and Decrypt File on macOS"
date:   2017-02-03 17:29:57 +0700
tags: encryption macos openssl
---

# Encrypting the file.

- Open **Terminal**.

```
$ openssl enc -aes-256-cbc -e -in INPUT-FILE -out OUTPUT-FILE
```

- OpenSSL will asks for the encryption password.
- Enter the encryption password.

```
enter aes-256-cbc encryption password:
```

- Enter the encryption password, again.

```
Verifying - enter aes-256-cbc encryption password:
```

- Done!

# Decrypting the file.

- Open **Terminal**.

```
$ openssl enc -aes-256-cbc -d -in INPUT-FILE -out OUTPUT-FILE
```

- OpenSSL will asks for the decryption password.
- Enter the decryption password.

```
enter aes-256-cbc encryption password:
```

- Done!

Source: [5 Advanced Mac Tricks You've Never Used](https://www.youtube.com/watch?v=uI4x0wvogco)
