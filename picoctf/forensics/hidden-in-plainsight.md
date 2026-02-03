## Challenge Overview

This challenge provided me with a .jpg image and a hint that something is contained within the file. The goal was to extract the flag from this .jpg file.

## Initial Analysis

My first though was to open the file and see what I was able to access. There was no password protecting the image, and the file opened and displayed an image. This ruled out the file obfuscation. Since the image appear normally, I could not rule out this being a stenography challenge quite yet. 

## Enumeration

I first moved the image into a Kali Linux Virtual Machine to untilize the kernel. The first command I tried was the `strings` command. 


