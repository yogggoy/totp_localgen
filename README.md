# TOTP Code Generator - Test Secrets

This repository contains examples and references for generating **Time-based One-Time Passwords (TOTP)** from predefined secrets.  
It is intended **only for testing and development**.

> **Do NOT use these secrets in production.**  
> All secrets in this repository are public and insecure by design.

---

## What is TOTP?

TOTP (RFC 6238) is a time-based one-time password algorithm commonly used for 2FA/MFA.  
A code is generated from:

- a shared secret (Base32)
- the current Unix time
- fixed parameters (algorithm, digits, time step)

---

## Default Parameters Used

Unless stated otherwise, examples assume:

| Parameter  | Value |
|-----------|-------|
| Algorithm | SHA1 |
| Digits    | 6 |
| Period    | 30 seconds |

These defaults are compatible with Google Authenticator, Authy, Microsoft Authenticator, etc.

---

## Test Secrets Examples(Base32)

### Basic Test Set

```text
JBSWY3DPEHPK3PXP
KRSXG5DSMFZWK3TQ
MZXW6YTBOI======
ONSWG4TFOQ======
GEZDGNBVGY======
```

### Longer Secrets (Closer to Real-World Length)

```text
IFBEGRCFIZDUQSKKJBEQ====
KRUGS4ZANFZSAYJAON2XEZJO
MFRGGZDFMZTWQ2LKNRXW45DF
```

---

## Example otpauth URI

You can import a secret into any authenticator app using an `otpauth://` URI.

Example:

```text
otpauth://totp/Test:user1?secret=JBSWY3DPEHPK3PXP&issuer=Test&algorithm=SHA1&digits=6&period=30
```

This can be encoded as a QR code if needed.

---

## Generating Codes in script - Examples

### Python (pyotp)

```python
import pyotp

totp = pyotp.TOTP("JBSWY3DPEHPK3PXP")
print(totp.now())
```

Install dependency:

```bash
pip install pyotp
```

---

### CLI (oathtool)

```bash
oathtool --totp -b JBSWY3DPEHPK3PXP
```

---
