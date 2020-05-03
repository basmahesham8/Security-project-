# Security-project-
computer security assignments for E/Mahmoud Ramadan 

## Assignment2
solveing the problem (https://cybertalents.com/challenges/cryptography/genfei) on  (https://cybertalents.com/) <br/>
### Prerequistes:
* Create an account on (https://cybertalents.com/)
* download and setup some python version as **python2** or **python3** from (https://www.python.org/downloads/)
* you may use some editor as **Anaconda** or **Pycharm** ..... you can aid with this link (https://www.youtube.com/watch?v=5mDYijMfSzs&t=299s)
### Deliverables:
*  Screenshot from your profile at (https://cybertalents.com/account/profile/me)
* Publish your source code to a folder called “Assignment 2” in the GitHub
repository that your created in the assignment 0.
* Write a writeup that describes how you solved the challenge and publish it
with the source code

### for Beginners,How to solve the challenge step by step?
1. unzip the downloaded file from the challenge 
2. write your own code to decrypt the encrypted code in **flag.enc** 
##### Encrypt.dy
```
import sys
from struct import pack, unpack

def F(w):
	return ((w * 31337) ^ (w * 1337 >> 16)) % 2**32

def encrypt(block):
	a, b, c, d = unpack("<4I", block)
	for rno in xrange(32):
		a, b, c, d = b ^ F(a | F(c ^ F(d)) ^ F(a | c) ^ d), c ^ F(a ^ F(d) ^ (a | d)), d ^ F(a | F(a) ^ a), a ^ 31337
		a, b, c, d = c ^ F(d | F(b ^ F(a)) ^ F(d | b) ^ a), b ^ F(d ^ F(a) ^ (d | a)), a ^ F(d | F(d) ^ d), d ^ 1337
	return pack("<4I", a, b, c, d)

pt = open(sys.argv[1]).read()
while len(pt) % 16: pt += "#"

ct = "".join(encrypt(pt[i:i+16]) for i in xrange(0, len(pt), 16))
open(sys.argv[1] + ".enc", "w").write(ct)
```
