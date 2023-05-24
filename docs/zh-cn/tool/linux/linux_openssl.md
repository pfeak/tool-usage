# openssl 生成 TLS 证书

## 流程

生成CA私钥（.key）-->生成CA证书请求（.csr）-->自签名得到根证书（.crt）

```
[生成CA私钥 .key]-->[生成CA证书请求 .csr]-->[自签名得到根证书 .crt]
```

## 生成 CA 私钥

```bash
openssl genrsa -out ca.key 2048
```

## 生成 CSR

```bash
openssl req -new -key ca.key -out ca.csr
```

## 生成签名证书

```bash
openssl x509 -req -days 365 -in ca.csr -signkey ca.key -out ca.crt
```
