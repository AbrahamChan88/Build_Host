### Generating a new CA
`cfssl gencert -initca ca-csr.json | cfssljson -bare ca`

### Generating new Server certs
`cfssl gencert -ca=ca.pem -ca-key=ca-key.pem -config=ca-config.json -profile=givemeaname server-csr.json | cfssljson -bare server`
