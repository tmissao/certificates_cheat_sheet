# Certificates Cheat Sheet

These commands allow you to convert certificates and keys to different formats to make them compatible with specific types of servers or software.

## General
---

- Convert a DER file (.crt .cer .der) to PEM
```bash
openssl x509 -inform der -in certificate.cer -out certificate.pem
```

- Convert a PEM file to DER
```bash
openssl x509 -outform der -in certificate.pem -out certificate.der
```

- Convert a PKCS#12 file (.pfx .p12) containing a private key and certificates to PEM
```bash
openssl pkcs12 -in keyStore.pfx -out keyStore.pem -nodes

# You can add -nocerts to only output the private key or add -nokeys to only output the certificates.
```

- Convert a PEM certificate file and a private key to PKCS#12 (.pfx .p12)
```bash
openssl pkcs12 -export -out certificate.pfx -inkey privateKey.key -in certificate.crt -certfile CACert.crt
```

- Convert PEM to CRT (.CRT file)
```bash
openssl x509 -outform der -in certificate.pem -out certificate.crt
```

## OpenSSL Convert PEM
---

- Convert PEM to DER

```bash
openssl x509 -outform der -in certificate.pem -out certificate.der
```

- Convert PEM to P7B

```bash
openssl crl2pkcs7 -nocrl -certfile certificate.cer -out certificate.p7b -certfile CACert.cer
```

- Convert PEM to PFX

```bash
openssl pkcs12 -export -out certificate.pfx -inkey privateKey.key -in certificate.crt -certfile CACert.crt
```

## OpenSSL Convert DER

- Convert DER to PEM

```bash
openssl x509 -inform der -in certificate.cer -out certificate.pem
```

## OpenSSL Convert P7B

- Convert P7B to PEM

```bash
openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer
```

- Convert P7B to PFX

```bash
openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer

openssl pkcs12 -export -in certificate.cer -inkey privateKey.key -out certificate.pfx -certfile CACert.cer
```

## OpenSSL Convert PFX

- Convert PFX to PEM

```bash
openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes
```
