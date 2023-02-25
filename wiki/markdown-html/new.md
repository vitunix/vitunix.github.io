# CryptoGraphy
## Solving Some CryptoGraphy Questions - cryptohack.org
## Installation
pip install pwn <br />
pip install base64 <br />
pip install Crypto <br />
pip install pycrypto <br />
#
### Introduction to Cryptohack

```py
# ASCII to String
a = [99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]
for i in a:
    print(chr(i), end="");

# Output = crypto{ASCII_pr1nt4bl3}
```

```py
# Hex to String
a="63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d"
print(bytes.fromhex(a))

# Output = b'crypto{You_will_be_working_with_hex_strings_a_lot}'
```

```py
#  Base64 to String
# Hex string, decode it into bytes and then encode it into Base64.

import base64
a = "72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf"
b = bytes.fromhex(a)
print(base64.b64encode(b))

#Output = b'crypto/Base+64+Encoding+is+Web+Safe/'
```

```py
# Bytes and Big Integers

from Crypto.Util.number import *
a=11515195063862318899931685488813747395775516287289682636499965282714637259206269
print(long_to_bytes(a))

# Output = b'crypto{3nc0d1n6_4ll_7h3_w4y_d0wn}'
```

```py
# XOR Starter

from pwn import *
data = 'label'
flag = ""
for i in data:
	flag += chr(ord(i) ^ 13)
	
print(f'crypto{{{flag}}}')

# Output  = crypto{aloha}
```

```py
# XOR Properties

from pwn import *
KEY1 = "a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313"
flag = "37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e"
KEY1 = bytes.fromhex(KEY1)
flag = bytes.fromhex(flag)
KEY2 = xor(KEY1, flag)
flag = "c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1"
flag = bytes.fromhex(flag)
KEY3 = xor(KEY2, flag)
flag = "04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf"
flag = bytes.fromhex(flag)
print(xor(KEY1, KEY2, KEY3, flag))

Output = b'crypto{x0r_i5_ass0c1at1v3}'

# Another Method

KEY2 = xor(bytes.fromhex("a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313"),bytes.fromhex("37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e"))

KEY3 = xor(bytes.fromhex("c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1"),KEY2)

last_flag = xor(bytes.fromhex("a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313"),KEY2,KEY3,bytes.fromhex("04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf"))

```

```py
# Favourite byte

a = "73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d"
a = bytes.fromhex(a)
b = 1
while True:
     c = xor(a,b)
     print(f'{b}. {c}')
     b += 1

# Output = b'crypto{0x10_15_my_f4v0ur173_by7e}'
```

```py
# You either know, XOR you don't

msg = "0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104"
msg = bytes.fromhex(msg)
print(f'msg = {msg}')

flag_format = b"crypto{"
key = [o1 ^ o2 for (o1, o2) in zip(msg, flag_format)] + [ord("y")]
print(f'key = {key}')

flag = []
key_len = len(key)
for i in range(len(msg)):
	flag.append(msg[i] ^ key[i % key_len])
print(f'flag = {flag}')

flag = "".join(chr(o) for o in flag)
print(f'(Flag: {flag})')

# Output = crypto{1f_y0u_Kn0w_En0uGH_y0u_Kn0w_1t_4ll}
```

### Course End

#

### Modular Arithmetic

```py
# gcd program -  Greatest Common Divisor(GCD)

def gcd(a,b):
	if(a<b):
		a,b = b,a
	while b!=0:
		print(b)
		a,b = b,a%b
	return a

a = int(input("Enter 1st number: "))
b = int(input("Enter 2nd number: "))
print(gcd(a,b))

```
```py
# Extended GCD program
from math import floor
def gcd(a,b):
	s1 = 1
	s2 = 0
	t1 = 0
	t2 = 1
	if(a<b):
		a,b = b,a
	while b!=0:
		a,b,c = b,a%b,a/b
		s1,s2 = s2, s1-(floor(c)*s2)
		t1,t2 = t2, t1-(floor(c)*t2)
		print(f'a = {a} \nb = {b} \nc = {c}\n')
		print(f'\ns1 = {s1} s2 = {s2} t1 = {t1} t2 = {t2}\n')
	
	print(f"Final Ans: gcd = {a} s = {s1} t = {t1}")

a = int(input("Enter 1st number: "))
b = int(input("Enter 2nd number: "))
print(gcd(a,b))

# Output = crypto{10245, -8404}
# Ans = -8404
```
```py
# Modular Arithmetic 1

a = 11 % 6
b = 8146798528947 % 17
print(min(a, b))

#Output = 4
```
```py
# Modular Arithmetic 2

>>> 273246787654**65536 % 65537

# Output = 1

```
```py
# Modular Inverting

a = 1
while True:
	if((3 * a) % 13 == 1):
		print(a)
		break
	a += 1

# Output = 9
```
```py
# Quadratic Residues

# a² = x mod p => a²-x =k*p
# range of k (1,100)

from Crypto.Util.number import *
from math import gcd
a = int(input("Enter the value of a: "))
p = int(input("Enter the value of p: "))
zn = [i for i in range(1,p) if gcd(p,1) == 1]
for i in zn:
	for k in range(1,100):
		if(pow(i,2)-a == k*p):
			print(i)

# Output = 8,21
```

### Course End

#

### Symmetric Cryptography

Keyed Permutations

```
What is the mathematical term for a one-to-one correspondence? 

Ans - crypto{bijection}

```

Resisting Bruteforce

```
What is the name for the best single-key attack against AES? 

Ans - crypto{Biclique}

```




