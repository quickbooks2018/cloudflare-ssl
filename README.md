# Generate Self-Signed Certificate

# Download Packages
# https://github.com/cloudflare/cfssl

curl -Lo cfssl https://github.com/cloudflare/cfssl/releases/download/v1.6.1/cfssl_1.6.1_linux_amd64

curl -Lo cfssljson https://github.com/cloudflare/cfssl/releases/download/v1.6.1/cfssljson_1.6.1_linux_amd64

# Setup CA
1. Create two files
ca-config.json
ca-csr.json

cfssl gencert -initca ca-csr.json | cfssljson -bare ca

# Certificate Signining Request CSR
cfssl gencert \
-ca=ca.pem \
-ca-key=ca-key.pem \
-config=ca-config.json \
-profile=tls \
cloudgeeks.ca-csr.json | cfssljson -bare cloudgeeks.ca

# Decode
openssl x509 -in cloudgeeks.ca.pem -text -noout
