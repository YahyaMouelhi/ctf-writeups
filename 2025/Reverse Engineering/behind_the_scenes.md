Content: This is a very easy reversing challenge from Hackthebox.

I tried to dynamically analyze the binary at first by interacting with it using ltrace and strings, but we get nothing.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1753633330568/08692539-a3f3-49cb-a1dd-36c65b0c4900.png align="center")

as we can see we hit an illegal instruction , weird right ?

When opening Ghidra, we see in main an incomplete code, which is very weird, and when examining assembly, we see the last instruction is “UD2“ and after comes a broken missing code.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1753632203244/9643b36f-a058-4896-8f78-187b7bea1ada.png align="center")

after doing some research, the UD2 instruction is a trap that stops the disassembler from disassembling the rest of the code, and it's used for testing and intentionally crashing the program. Well, no problem, after opening GDB and disassembling main, we luckily see everything, and after examining the addresses of every cmp as string, we get the password and we surround it with HTB{}.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1753632448771/51b674c3-af8d-420c-8f9c-dfb087f2eb7f.png align="center")

we can see these values and their representation as strings, and that's the flag:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1753632561228/4e44f5b8-5754-4ba8-b6db-f450a39f6bef.png align="center")

And that’s all, this challenge teaches us about the UD2 instruction and how it can obfuscate the disassembler. Hope this article was helpful!
