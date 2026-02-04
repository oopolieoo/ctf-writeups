## Challenge Overview

This challenge provided me with a .jpg image and a hint that something is contained within the file. The goal was to extract the flag from a .jpg file. This CTF has a difficulty rating of easy.

## Initial Analysis

My first thought was to open the file and see what I was able to access. There was no password protecting the image, and the file opened and displayed an image. This ruled out the file obfuscation.

## Enumeration

My first inspection of the image did not reveal any anomalies, so I treated it as a potential steganography challenge. I began with the `strings` command to check for any readable data in the files binary, but found no relevant information after filtering for common flag patterns. This suggested the clues to the flag were hidden elsewhere. I then tried the `binwalk` command to identify any files embedded within the original. There was no output, so I ruled this route out as well. Since I have yet to rule out stenography, I decided to dive deeper into this being the solution. I used the `steghide extract` command, which is used to either hide or extract hidden data within image and video files. Since this command typically requires a passphrase, I attempted to guess it with a variety of common phrases (pico, admin, password, ctf, etc.). None of these were the correct phrase, so I moved onto another command. Although I did not know the password, I had yet to find any evidence that this was not the answer. The command `exiftool` is what I tried next. This is a command that is used to view the metadata of a file, which typically contains hidden information. Upon running this command, I noticed a suspicious string of characters in the "comment" section. ![IMG_0475](https://github.com/user-attachments/assets/ea5803a6-3e5e-4e9c-ba5c-de27ce5e53d0) 

It appeared to be an encoding of some type. So, I ran it through an encoder identifier which revealed it as base64. This prompted me to put this into a base64 decoder, which gave me an output that looked like another base64 encoding. Subsequently, I re-entered the new string into the decoder, which revealed the `steghide` password. And, upon running `steghide extract` with the correct passphrase, the flag was revealed and the CTF was solved.
