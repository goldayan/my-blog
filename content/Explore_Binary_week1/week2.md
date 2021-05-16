+++
title = "Binary Exploration Week2"
date = 2020-06-21
description = "Binary Exploration course by artikblue"
in_search_index = true

[taxonomies]
categories = ["ReverseEngineering"]
tags = ["Binary"]
authors = ["Thanga Ayyanar"]
+++

i have played more than 4 ctf that's how i met sammy then we formed a team and 
played 5 or more ctf 

Cutter

Cutter is awesome tool, love the ghidra decompiler part, but i like to explore 
r2 command line lot because i like terminal apps more.

Artik Blog

In type casting blog we learned new assembly instruction which does the casting magic
 movzx,movsx
 cvs

In Multidimenstion and Struct exploration blog i learned how to find those code 
- pf
- td
- afv-
- afvd

But tl command prints the structs we defined through td but it didn't work for me 
i use tll command to print the struct information also used tp.

Itay Cohen AKA Megabeets blogs

When i first start to explore radare2 i stumbled across his blog.
so i was thrilled to find you have included his article for this week

First blogs just explains the basics of radare2 commands.
Second blogs goes bit deep into using different radare2 tools like rarun2,.. and 
exploiting buffer overflow vulnerability with radare2 and pwntools and a nice read.

Ioli Crackme
crackme1 is pretty staright forward to find the key
crackme2 used r2 debug mode and found the key nice challenge

Practice Excerise

Explore pf command 

create a empty string in main and in next step we will fill in the string and after 1 second the value will be emptied
```c
#include<stdio.h>
#include<unistd.h>

int main() {

    char serialKey[40];

    // assign value to serial key
    strcpy(serialKey,"The secret to success is persistance");

    sleep(2);

    strcpy(serialKey,"");

    return 0;
}

```

r2 pipe automation script
```python
import r2pipe
import json
# used ast to decode json from pf, because json.loads fails
import ast

array_value = ""

def print_array(r2):
    global array_value
    array_memory = "rbp-0x30"
    new_array_json = ast.literal_eval(r2.cmd(f'pfj z @ {array_memory}'))
    new_array_value = new_array_json[0]["value"]
    if array_value != new_array_value:
        print(f"Array value: {new_array_value}")
        array_value = new_array_value


r2 = r2pipe.open('array_automate')
r2.cmd('aa;aas;doo') ## analyze all symbols and calls and open in debug mode

json_data = json.loads(r2.cmd('pdfj @ main'))

breakpoint_start = json_data["ops"][7]
breakpoint_offset = hex(breakpoint_start['offset'])
print(f"Log: Breakpoint offset: {breakpoint_offset} {breakpoint_start['disasm']}")
r2.cmd(f"dcu {breakpoint_offset}")
for index in range(8,len(json_data['ops'])):
    print_array(r2)
    r2.cmd("ds")
    print(f"Log: {json_data['ops'][index]['disasm']}")

r2.quit()
```
