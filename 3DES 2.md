3DES

```python
import pyDes
import base64


def encrypt_3des(plain_text):
    key = b"secret_key123456"
    obj = pyDes.triple_des(key=key, mode=pyDes.ECB, pad=None, padmode=pyDes.PAD_PKCS5)
    cipher_text = obj.encrypt(plain_text)
    return base64.b64encode(cipher_text).decode()


def decrypt_3des(cipher_text):
    cipher_text = base64.b64decode(cipher_text)
    key = b"secret_key123456"
    obj = pyDes.triple_des(key=key, mode=pyDes.ECB, pad=None, padmode=pyDes.PAD_PKCS5)
    plain_text = obj.decrypt(cipher_text)
    return plain_text.decode()


text = "613772bhh 3h4jh3j4"
a = encrypt_3des(text)
print(a)
b = decrypt_3des(a)
print(b)
```

