## Challenge Overview

This challenge provided me with a .jpg image and a hint that something is contained within the file. The goal was to extract the flag from a .jpg file.

## Initial Analysis

My first though was to open the file and see what I was able to access. There was no password protecting the image, and the file opened and displayed an image. This ruled out the file obfuscation. Since the image appear normally, I could not rule out this being a stenography challenge quite yet. 

## Enumeration

I first moved the image into a Kali Linux Virtual Machine to untilize the kernel. The first command I tried was the `strings` command. This command is used to exrtract plaintext from a binary file/executable. There were hundreds of lines of output, so I decided to pair the `grep` command with my inital `string` command. I used words like "pico", "flag", and "ctf" to look for commonly named flags. This did not work, so I ruled out this posibility. The next command I tried is the `binwalk` command, which is used to extract any files embedded within the original. There was no output, so I ruled this route out as well. Since I have yet to rule out stenography, I decided to dive deeper into this being the solution. I used the `steghide` command, which is used to either hide or extract hidden data within image and video files. Since this command typically requires a passphrase, I attempted to guess it with a variety of common phrases (pico, admin, password, ctf, etc.). None of these were the correct phrase, so I moved onto another command. Although I did not know the password, I had yet to find any evidence that this was not the answer. The command `exitftool` is what I tried next. This is a command that is used to view the metadata of a file, which typically contains hidden information. Upon running this command, I noticed a suspicious string of characters in the "comment" section. It appeared to be a hash of some type. So, I ran it through a hash identifier which revealed it as a base64 hash. This prompted me to put this hash into a base64 decoder, which gave me an output that looked like another base64 hash. Subsequently, I rentered the new hash into the decoder, which revealed the `steghide` password. And, upon running `steghide` with the correct passphrase, the flag was revealed and the CTF was solved.


