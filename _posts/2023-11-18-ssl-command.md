---
title: Certificate Conversion Command
date: 2023-11-18 18:22:00 +1000
categories: []
tags: []
pin: true
math: false
mermaid: false
---

## create ssl cert and CA

``` shell
# create CA key
openssl genrsa -des3 -out myCA.key 2048

# create CA cert
openssl req -x509 -new -nodes -key myCA.key -sha256 -days 1825 -out myCA.pem

# create service key
openssl genrsa -out hellfish.test.key 2048

# create CSR
openssl req -new -key hellfish.test.key -out hellfish.test.csr

# convert key in pem format
openssl rsa -in myCA.key -text > myCAKey.pem

# create config
cat > hellfish.test.ext << EOF 
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = hellfish.test
EOF

# sign by CA
openssl x509 -req -in hellfish.test.csr -CA myCA.pem -CAkey myCA.key \
-CAcreateserial -out hellfish.test.crt -days 825 -sha256 -extfile hellfish.test.ext

# view website certificate
openssl s_client -showcerts -connect www.cisco.com:443
```

## File Format

OpenSSL command line tool has pkcs12 and x509 toolkit to work with SSL certificate and key. 

PKCS#12 is a format that could contain both private key and public certificate. File formats are PFX (for windows) and P12 (for unix).

X509 is the public certificate standard. File formats are PEM (base64 encoded string) and DER (binary file). CER and CRT format only mean certificate, the actual format need to check file content.

``` shell
# export key and cert from pfx / p12 file
openssl pkcs12 -in app.pfx -out app_cert.pem -nodes -nokeys
openssl pkcs12 -in app.pfx -out app_key.pem -nodes -nocerts
openssl pkcs12 -in app.p12 -out app_cert.pem -nodes -nokeys
openssl pkcs12 -in app.p12 -out app_key.pem -nodes -nocerts

# create P12, PFX file
openssl pkcs12 -export -in app_cert.pem -inkey app_key.pem -name app > app.p12

# inspect P12, PFX file
openssl pkcs12 -info -in app.p12

# convert format PEM <-> DER
openssl x509 -inform PEM -in cert.pem -outform DER -out cert.cer
openssl x509 -inform DER -in cert.der -outform PEM -out cert.pem
```

## Java KeyStore and TrustStore

``` shell
# inspect keystore
keytool -list -keystore app.truststore.jks
keytool -list -rfc -storepass changeit -keystore app.truststore.jks

# change alias
keytool -changealias -alias <old-alias> -destalias <new-alias> -keystore app.truststore.jks -storepass changeit

# import cert
keytool -import -noprompt -truststore -alias <alias> -file app.pem -keystore app.truststore -storepass changeit

```
