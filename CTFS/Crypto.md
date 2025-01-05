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

