### interencdec -pico ctf

![[Pasted image 20250105165055.png]]

after reading the file identified as base 64

![[Pasted image 20250105165038.png]]

after decoding with cyberchef again i got base64 value i decoded again and then got this 
`wpjvJAM{jhlzhy_k3jy9wa3k_86kl32k2}`

decoded with ceaser cipher got flag 
`picoCTF{caesar_d3cr9pt3d_86de32d2}`


### Mod 26 -picoctf

![[Pasted image 20250105165339.png]]

![[Pasted image 20250105165417.png]]

hint is ROT 13 so i searched for rot13 decoder and got the flag 
`picoCTF{next_time_I'll_try_2_rounds_of_rot13_TLcKBUdK}`


### The numbers - picoctf

![[Pasted image 20250105170116.png]]

![[Pasted image 20250105170128.png]]

For the first sequence:

- `16 9 3 15 3 20 6` → Corresponding letters in the alphabet:
    - 16 = P
    - 9 = I
    - 3 = C
    - 15 = O
    - 3 = C
    - 20 = T
    - 6 = F

So, this part becomes `PICOCTF`.

For the second sequence inside the curly braces:

- `20 8 5 14 21 13 2 5 18 19 13 1 19 15 14` → Corresponding letters:
    - 20 = T
    - 8 = H
    - 5 = E
    - 14 = N
    - 21 = U
    - 13 = M
    - 2 = B
    - 5 = E
    - 18 = R
    - 19 = S
    - 13 = M
    - 1 = A
    - 19 = S
    - 15 = O
    - 14 = N

This part becomes `THE NUMBER SAMSON`.
`**picoCTF{THENUMBERSAMSON}**`

### 13 - picoctf

![[Pasted image 20250105170312.png]]

using rot13 solved this 
![[Pasted image 20250105170340.png]]

`picoCTF{not_too_bad_of_a_problem}`

### rsa_oracle

![[Pasted image 20250105172424.png]]

slight revision based on Paulo's remark in the comments - in a public key system a [chosen _plaintext_ attack](https://en.wikipedia.org/wiki/Chosen-plaintext_attack) is pretty much part of the design - arbitrary plaintexts can be encrypted to produce ciphertexts at will - by design, however, these shouldn't give any information that will allow you to deduce the private key.

A [chosen _ciphertext_ attack](https://en.wikipedia.org/wiki/Chosen-ciphertext_attack) can be used with careful selection of the plaintext, however, to perform an attack - it's fairly straightforward on textbook RSA. Firstly, we have a piece of ciphertext we'll denote by:

C≡temodnC≡temodn

Which is RSA as we know and love. Now, Eve has CC - this is perfectly ordinary since Eve is supposed to be able to see CC. Now Eve can choose a plaintext - so, she choses 22 as her plaintext and computes Ca≡2emodnCa≡2emodn. However, to our unsuspecting victim, she sends Cb≡Ca∗CCb≡Ca∗C, so:

Cb≡C⋅2e≡te2emodnCb≡C⋅2e≡te2emodn

All good so far. Now since this is a chosen plaintext attack we're reliant on having access to the decryption of our substituted value - so now the unsuspecting victim computes:

(Cb)d≡[te2e]d≡(te)d⋅(2e)dmodn(Cb)d≡[te2e]d≡(te)d⋅(2e)dmodn

However for any plaintext xx, we know C≡xeC≡xe and x≡Cdx≡Cd; so:

(xe)d≡xmodn(xe)d≡xmodn

Therefore from the preceding result:

(Cb)d≡t⋅2modn(Cb)d≡t⋅2modn

Hence when we get that value back, we can quite easily compute tt. We simply need to halve it.

This can actually apply for any plaintext we wish to chose - I simply chose 22 because I like it as a number. [This paper](http://www.dtc.umn.edu/%7Eodlyzko/doc/arch/rsa.attack.pdf) covers the general technique and a lot more.

This **only applies** to textbook RSA. The proper application of RSA in the wild involves the use of padding schemes which defeat this attack by ensuring the ciphertext is not malleable in this way.
[](https://crypto.stackexchange.com/posts/80556/timeline)

A chosen plaintext attack means that the attacker, Eve, can encrypt the plaintext of her choice. Since in public key cryptosystems this is always possible, Eve can always acquire Bob's encryption exponent ee and encrypt any plaintext. What does this mean when the plaintext space is small?

Say Alice and Bob decide on textbook RSA and they generate the needed public and private keys. Alice sends Bob her age. Eve gets the message mm (Alice's age) as memodNmemodN. Eve knows meme decrypts to an age (plaintext space is small). Eve could launch a chosen plaintext attack by encrypting numbers 1-200 and matching it with the cipher text meme.

Here is a [SageMath](https://www.sagemath.org/) script that shows this attack on textbook RSA.

```python
from pwn import *

context.log_level='critical'
p = remote("titan.picoctf.net", 61923)

p.recvuntil(b"decrypt.")

with open("password.enc") as file:
    c = int(file.read())

p.sendline(b"E")
p.recvuntil(b"keysize): ")
p.sendline(b"\x02")
p.recvuntil(b"mod n) ")

c_a = int(p.recvline())

p.sendline(b"D")
p.recvuntil(b"decrypt: ")
p.sendline(str(c_a*c).encode())
p.recvuntil(b"mod n): ")

password = int(p.recvline(), 16) // 2
password = password.to_bytes(len(str(password))-7, "big").decode("utf-8")

print("Password:", password)
```


```
p,q = next_prime(2^50), next_prime(2^30)
N = p*q
phi = ((p-1)*(q-1))
e = randint(0, phi)
while gcd(e, phi) != 1:
    e = randint(0, phi)
e = Integers(phi)(e)
d = e^(-1)
print('p = {}\nq = {}\nN = {}\nphi(N) = {}\n'.format(p, q, N, phi))
print('Bob\'s private key: d = {}, public key: e = {}'.format(d, e))

# BLOCK: Alice sends Bob a message
m = Integers(N)(39)
c = m^e
print('Alice sends m = {} to Bob as m^e = {}'.format(m, c))

# BLOCK: Bob decrypts c
print('Bob decrypts c = {} to m = c^d = {}'.format(c, c^d))

# BLOCK: Chosen Plaintext Attack on Textbook RSA
plaintext_space = range(200)
for t in plaintext_space:
    t = Integers(N)(t)
    if t^e == c:
        print('Eve has found the message: {}'.format(t))
```

Here is the Output:

```
 ---- Bob computes his public and private key ---- 
p = 1125899906842679
q = 1073741827
N = 1208925822992387951034533
phi(N) = 1208925821866486970450028

Bob's private key: d = 663674456840375780568965, public key: e = 761705651416514555276069
 ---- Alice sends Bob a message ---- 
Alice sends m = 39 to Bob as m^e = 25719553046482356303827
 ---- Chosen Plaintext Attack on Textbook RSA ---- 
Eve has found the message: 39
```

This is a simple script that connects to the server with [pwn tools](https://docs.pwntools.com/en/stable/) to automate the process and easily send encoded text. The [context log level](https://docs.pwntools.com/en/stable/context.html#pwnlib.context.ContextType.log_level) was set to critical to remove unnecessary messages from pwntools when running. Note there is also a debug mode if needed.

First, taking in the `password.enc` text and storing it in c. Then encrypting 2 which is sent in hex and put into the c_a variable. The multiply c and c_a to where it is now in a format that the program will allow it to be decrypted. Once decrypted it takes the hex version which is why it is converted from hex with the `int(x, 16)` function. Then it uses integer division to divide by 2 to get the password.

Lastly, the password is converted to bytes and decoded to get the password that is needed to be used in the decryption.

By running this command and inputting the password after running the flag could be received:

`openssl enc -aes-256-cbc -d -in secret.enc`
passwd : 4955e

Flag: `picoCTF{su((3ss_(r@ck1ng_r3@_24bc...}`
