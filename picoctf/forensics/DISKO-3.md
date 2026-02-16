## Challenge Overview
This challenge provided me with a zipped disk image with the `.dd` file extension. It asks that I find the flag within, and notes that it is "not as plain as you think it is." This challenge is rated medium difficulty. 


## Initial Analysis
After I downloaded the file, the first thing I did was unzip the folder in order to access the file properly. Upon doing so, I attempted to open the file, which did not work since it was not a mountable filesystem. I have never handled a `.dd` file before, so I did a search to find that it is a bit-for-bit disk image that captures the contents/structure of storage devices. Now knowing this, I figured I would need software to uncover the hidden data within this file. During the National Cyber League CTF competition, there was a challenge similar to this. I used a tool called Autopsy then, so I figured I would try the same with this challenge.


## Enumeration
Upon uploading the file into Autopsy, there was instant feedback in several categories. The first thing I did was look for any deleted files that may contain an artifact linked to the flag. There were two deleted files; one was a `.txt` file which appeared to contain logs from a kali terminal, while the other was a GZIP Compressed Archive. Upon opening the GZIP file, the hex in the original filename field actually translated to "flag." This was a clear indicator to me that the solution is likely here. I considered manually decompressing it in a VM using `gunzip`, but I believed that there was an easier way to find the flag through Autopsy findings. 

<img width="928" height="487" alt="Screenshot 2026-02-16 134801" src="https://github.com/user-attachments/assets/a60a8add-8f38-4b74-a57b-ae7ed712a5d0" />

Looking further, I opened the "Data Sources" tab connected to the `.dd` file and began looking through the various files. Due to Autopsy's automatic File Carving and Artifact Extraction modules, the "log" section revealed a `.gz` file named "flag.gz." Upon opening, the flag for the challenge was revealed.





## Lessons Learned
By completing this CTF, I learned valuable information about `.dd` files, their use case, and how to examine them for artifacts. Additionally, by utilizing Autopsy I found out that I can reduce the number of steps needed to find hidden information within GZIP archives.


