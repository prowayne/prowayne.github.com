--- 
title: python的加密工具包pycrypto
layout: post
category: python
---

## Pycrypto
#### The Python Cryptography Toolkit
项目源码托管在[github][1]上,这个模块不仅提供了变量的加解密算法(AES, DES, RSA, ElGamal,etc.),还包含了稳固的hash函数(例如SHA256 和
RIPEMD160). 更重要的是使用非常简单

[1]:https://github.com/dlitz/pycrypto "pycrypto"

## 加密解密
### 数据打包
**源数据**的长度一般是block_size的倍数,可以引入一个打包函数,保证message的长度:

```
# 打包
def pad(data, block_size=16):
    length = block_size - (len(data) % block_size)
    data += chr(length)*length
    return data
# 解包    
def unpad(data)
    return data[:-ord(data[-1])]
```

### AES
```
from Crypto.Cipher import AES
key = b'the key 16 bytes'
iv = 'This is an IV456'
aes = AES.new(key, AES.MODE_CBC, iv)
message = "some_text"
encrypted_message = aes.encrypt(pad(message))
# encrtyed_message 就为加密后的信息
aes2 = AES.new(key, AES.MODE_CBC, iv)
org_message = unpad(aes2.decrypt(encrtyed_message))
# org_message 解密后的信息,也就是原始信息
```
这里注意`AES.new(key, *args, **kwargs)`其中key只能是16,24或者32位字节,block_size=16.上面代码中的iv,在MODE_ECB 和 MODE_CTR中不需要.在MODE_OPENPGP中 加密使用block_size长度的iv,解密使用block_size +2 字节长度的iv.别的modes,iv是 block_size 字节长度,自定义是block_size长度个0.  

### DES
```
from Crypto.Cipher import DES3
from Crypto import Random
key = b'Sixteen byte key'
iv = Random.new().read(DES3.block_size)
cipher = DES3.new(key, DES3.MODE_OFB, iv)
plaintext = pad('sona si latine loqueris ', 8)
msg = iv + cipher.encrypt(plaintext)
```
DES3三重DES加密,安全性可以得到保证.

### 还有
Crypto.Cipher 还提供了ARC,CAST等多个加密算法模块

## HASH
### SHA256

```
from Crypto.Hash import SHA256
hash = SHA256.new()
hash.update('some text')
sha256 = hash.digest()
```

### MD5
```
from Crypto.Hash import MD5
h = MD5.new()
h.update(b'Hello')
md5 = h.hexdigest()
```

### 另外
Crypto.Hash 也提供了HMAC,MD4等算法,[详见官网][2]

[2]:https://www.dlitz.net 

## Random
高级一些的随机算法,比如下面这个:
```
from Crypto.Random import random
random.choice(['dogs', 'cats', 'bears'])
```
随机从list里面取一个.需要注意的是在使用os.fork()之后需要,调用Random.atfork()来保证随机性.

## 最后

pycrypto包含了丰富的加密, 随机,hash算法,使用相当方便.
