# ctf

## Common commands
1. `strings file.txt`
    1. Print the sequences of printable characters in files
1. `file file.txt`
    1. Determine file type
1. `exiftool file.txt`
    1. Outputs metadata about a file

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
- [Link]()
- From: Beginner picoMini 2022
- Difficulty: Easy
- Completed: 2024/09/19

Description:

Can you crack the password to get the flag? Download the password checker [here](https://artifacts.picoctf.net/c/10/level1.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/10/level1.flag.txt.enc) in the same directory too.

Solution:

1. The program has condition `user_pw == "691d"` so giving input `691d` to the program reveals the flag




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
