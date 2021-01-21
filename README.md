# ROP Emporium Callme 64-bit

----------
#### Goal: Call All Callme() Functions With Parameters:
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) 0xdeadbeefdeadbeef
- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) 0xcafebabecafebabe
- ![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) 0xd00df00dd00df00d

### Information Gathering
![alt text](https://i.imgur.com/x4TzV9V.png)
### List Of Functions Within The Callme Executable
![alt text](https://i.imgur.com/Nv7ec3b.png)
## Simple Reverse-Engineering
### Disassembly Of The main() Function
![alt text](https://i.imgur.com/4JqkiDn.png)
### Disassembly Of The UsefulFunction() Function
![alt text](https://i.imgur.com/V5lCcbY.png)

- Calls all 3 functions with the inputs from EDX, ESI & EDI
- We need to give these functions the inputs: 0xdeadbeefdeadbeef, 0xcafebabecafebabe & 0xd00df00dd00df00d
- example: callme_one(0xdeadbeefdeadbeef, 0xcafebabecafebabe, 0xd00df00dd00df00d)
### Disassembly Of The Callme() Functions

![alt text](https://i.imgur.com/FXes7OV.png)

- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) moves 0xdeadbeefdeadbeef into RAX
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) then compares RBP to what's in RAX
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) then after that does a conditional jump to see if you'll move onto the next function 
- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) then moves 0xcafebabecafebabe into RAX
- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) then compares what's in RBP to whatever is in RAX
- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) then after that does a conditional jump to see if you'll move onto the next function 
- ![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) moves 0xd00df00dd00df00d into RAX then compares what's in RBP to RAX
- ![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) after that preforms a conditional jump to get the final flag
- ![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) here it will either get the encrypted flag or fail completely

# Exploitation
+ let's give the program 44 B's to see if we can make it seg-fault
![alt text](https://i.imgur.com/2oQXXoM.png)
  
- We see that in RIP we overwrite it 4 times with our B's so that means we can safely assume our offset is 40

# Exploit Development
#### First we will grab a needed rop gadget to give inputs to RDI, RSI & RDX

![alt text](https://i.imgur.com/IHpKDLs.png)
- We see that at 0x000000000040093c we have our needed gadget to complete the challenge

--- 
![alt text](https://i.imgur.com/4YomEck.png)
- We see all the memory addresses for the functions we must call here
---

![alt text](https://i.imgur.com/6xNjgEN.png)
- we first import everything from pwntools
- then we will set up our inputs to give to the program
- after doing that we will grab our memory addresses for the callme() functions
- then we grab our gadget and start crafting our payload
- we now start to sort of make our own stack to give to the program
- we fill the buffer with 40 A's and then set up our gadget then call callme() one
- after that we do the same thing with the last two callme() functions
- then we will finally start our process ( the callme executable )
- then send the payload to the programs input
- we will simply receive until the little > input suggestion
- then we will print the result

![alt text](https://i.imgur.com/KoIKRnw.png)

- after that we're done! we got the flag!
----------

 ### ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) Credits: R2LC

 ### ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) Challenge: https://ropemporium.com/challenge/callme.html ( 64-bit )
