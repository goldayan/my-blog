+++
title = "Binary Exploration Week1"
date = 2020-06-21
description = "Binary Exploration course by artikblue"
in_search_index = true
draft = true

[taxonomies]
categories = ["ReverseEngineering"]
tags = ["Binary"]
authors = ["Thanga Ayyanar"]
+++

I have created a template in my github repo if anyone need to learn along.
Link to my week1 template [here](https://github.com/ThangaAyyanar/Learn-by-challenge/blob/master/Exploring%20Binary%20World/Week%201/Template.md)

Things i learned in first week 

## Basics of x64
### Read the intel x64 article
    + I got familiar with basics stuff such as register,calling convention.
    + But lacks in XMM register, I need to concentrate more on that in my free time.
### Reversing x64 basic article ( nora code article )
    + It is easy to follow along the tutorials,solved crackme that are done in that article
### Different tools used to reverse engineer binary
    + Already came across dunstri blog when i was skimming radare2 manual book.
    + Taught me that every tool has its own pros and cons.

## ArtikBlue Article
### Article 1
    + Article 1 is pretty straight forward, simple program hello world program in 32 and 64 bit.
### Article 2
    + Learning about different variable types.
    + I used a trick that i learned from liveoverflow video ( i forgot which video it is )
    + To understand assembly i write code in C with NOP code in between every line so it will easy to see in disassembly.
    ```
    #define NOP __asm__("nop;" "nop;" "nop;")

    int main(){
        int a = 5;
        NOP;
        char character = 'A';
        return 0;
    }
    ```
    In disassembly
    ```
   0x000011ed      c745e4050000.  mov dword [var_1ch], 5
   0x000011f4      90             nop
   0x000011f5      90             nop
   0x000011f6      90             nop
   0x000011f7      c645e341       mov byte [var_1dh], 0x41    ; 'A'
    ```
#### Problems we faced in Article 2
    + One thing we struggle in this article is, we tried to print double followed exactly as print float value in **rax2** but we got wrong value. we have no clue on this.

### Article 3
	+ Condition, Switch and Loop
    + I have solved few ctf challenges, and i got few knowledge about condition related things.
    + Things i learned from this article is the flag register is explained neatly.
    + I tried few program and it was pretty easy to follow.

#### Article 3 - practice (patching)
    + I used Visual mode in radare2 to patch the loop counter
    + I press 'i' and go to the respective hex code and changed the logic.
    + I also came across <shift>+a which didn't know, how to apply properly but sammy done this,I learned this from him.

### Article 4
    + Array and Strings.
    + Nora code blog also touches the array stuff slightly so i have little bit idea about array before reading this article.
    + Lot of things becomes clear to me after reading the two blog.

#### Article 4 - practice (automation)
    + First of all i don't understand why we need r2frida to automation, we can automate it easily using r2pipe as far as searched through the internet
    + If we are using r2frida we can inject into running program and manipulate it while it is running, this what expected ?
    + I tried it with r2 pipe to analyze the array binaries.
    ```
    import r2pipe
    import sys
    r = r2pipe.open(sys.argv[1])
    json = r.cmdj('iij')
    print(json)
    print(r.cmd('aaa'))
    print(r.cmd('afl'))
    print(r.cmd('s main'))
    print(r.cmd('pdf'))
    ```

## Tools
### Radare2 
    + I love command line tools, i used it lot during ctf challenges.
    + I have watched a playlist of radare2 tool usages in binaryAdventure youtube channel,He has good [playlist](https://www.youtube.com/playlist?list=PLg_QXA4bGHpvsW-qeoi3_yhiZg8zBzNwQ) on this tool.
    + I learned few new commands from your channel, such as afvn,dr 1.
### Frida
    + I already came across this tool but never used it, for anything.
    + I learned frida seperately but watched a video demonstrating using r2frida but i haven't tried.
    + came across tutorial video of frida 101 in twitter [Video](https://www.youtube.com/watch?v=CLpW1tZCblo) this a 4 hours stream he started with LD_PRELOAD and move to frida, Different ways to inject frida into the binary. He has exercise attached below, i followed along with it.The stream is bit long but learned ton.
### Ghidra
    + I used it for ctf challenges, mainly for its decompiler capability.

currently i don't have any window box, but i will keep it in my todo, i complete in my spare time.
