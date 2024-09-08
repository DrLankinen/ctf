# ctf

## Common commands
1. `strings file.txt`
    1. Print the sequences of printable characters in files
1. `file file.txt`
    1. Determine file type

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

### General Skills
#### Binary Search
- [Link](https://play.picoctf.org/practice/challenge/442)
- From: PicoCTF 2024
- Difficulty: Easy
- Completed: 2024/08/24

Description:

Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses. Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools! You can download the challenge files here: [challenge.zip](https://artifacts.picoctf.net/c_atlas/18/challenge.zip)

Solution:

1. The challenge.zip contained a shell script which asked to guess a number between 1 and 1000 and it said if the correct number is lower or higher. Like the challenge name suggest, the idea is to use binary search and always guess the number between known lower and higher end.

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
