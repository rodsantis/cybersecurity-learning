# OverTheWire: Bandit

**Game:** Bandit - Linux Command Line Basics  
**Difficulty:** ⭐ Beginner  
**Total Levels:** 34  
**Status:** 🟢 Completed  
**Completed:** 34/34 
**Start Date:** December 15, 2025  
**Last Updated:** March 25, 2026

---

## 📖 Overview

Bandit is an introductory OverTheWire game. It teaches Linux command 
line basics through increasingly challenging challenges. No exploitation 
required—just solid Linux fundamentals that form the foundation for all 
cybersecurity work.

---

## 📊 Progress Tracker

| Level Range | Status | Concept | Difficulty |
|-------------|--------|---------|-----------|
| 0-5 | Completed | Basic Commands | ⭐ |
| 6-10 | Completed | File Operations | ⭐ |
| 11-15 | Completed | Text Processing | ⭐⭐ |
| 16-20 | Completed | Data Filtering | ⭐⭐ |
| 21-25 | Completed | Advanced Concepts | ⭐⭐⭐ |
| 26-34 | Completed | Complex Challenges | ⭐⭐⭐ |

---

### Level 0 → 1: SSH & File Reading

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 3 minutes  
**Date Completed:** December 15, 2025  
**Concept:** SSH connection and basic file reading

**Challenge Goal:**
Log into the Bandit server using SSH and read the password for the next level 
from a file called "readme".

**Solution:**

Step 1: Connect via SSH
```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

When prompted for password, enter: `bandit0` as per challenge information.

Step 2: List files in the directory
```bash
ls -la
```

Step 3: Read the readme file and get the password
```bash
cat readme
```
**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- SSH connection syntax: `ssh -p [port] [user]@[host]`
- `ls` shows files, `ls -la` shows detailed info including hidden files
- `cat` command reads and displays file contents
- Files can contain passwords/credentials

---

### Level 1 → 2: Dashed Filenames

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 3 minutes  
**Date Completed:** December 16, 2025  
**Concept:** Special character handling in filenames

**Challenge Goal:**
There is a file in the home directory called "-". Read this file.

**Solution:**

Step 1: Connect and list files
```bash
ssh -p 2220 bandit1@bandit.labs.overthewire.org
# used the password found in the previous level

ls -la
```
Step 2: Try to read the file "-"
```bash
cat -
# it failed as the dash (-) has a special meaning it can be used for stdin or stdout
```

Step 3: Use the correct syntax
```bash
cat ./-  # treats the "-" file as a relative path, not an option
# or
cat < -
```
**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- Special characters in filenames need escaping or special handling
- `./-` makes the path explicit
- Understanding command line parsing is crucial
- When a command doesn't work, think about how the shell interprets it

---

### Level 2 → 3: Spaces in Filenames

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 3 minutes  
**Date Completed:** December 16, 2025  
**Concept:** Handling spaces and escaping

**Challenge Goal:**
There is a file in the home directory called "--spaces in this filename--". 
Read it.

**Solution:**

Step 1: Connect and list files
```bash
ssh -p 2220 bandit2@bandit.labs.overthewire.org
# used the password found in the previous level

ls -la
# found the searched file: --spaces in this filename--
```

Step 2: from my knowledge and the learnings from the past dashed (-) challenge used quotes "" to group the spaces as one name, and used < to redirect the contents of the file as input for cat.
```bash
cat < "--spaces in this filename--"
```

Step 3: tried other solutions:
```bash
cat ./--spaces\ in\ this\ filename--
# or
cat ./"--spaces in this filename--"
# or
cat ./'--spaces in this filename--'
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- Spaces are special characters in bash (field separators)
- Escape with `\` or use quotes (single or double)
- Double quotes allow variable expansion, single quotes don't
- Best practice: use quotes for clarity
- Running cat and giving the contents of the file in quotes through the operator `<`

---

### Level 3 → 4: Hidden Files

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 3 minutes  
**Date Completed:** December 16, 2025  
**Concept:** Hidden files in Linux

**Challenge Goal:**
There is a hidden file in the inhere directory.

**Solution:**

Step 1: Connect and search
```bash
ssh -p 2220 bandit3@bandit.labs.overthewire.org
# used the password found in the previous level

ls
# it showed the directory ~/inhere
```

Step 2: Searched for the file inside the directory
```bash
cd inhere/

ls  # no results shown
ls -la  # found the searched file
```

Step 3: Got the password from the file
```bash
cat .hidden_filename
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- Files starting with `.` are hidden in Linux
- `ls` doesn't show hidden files by default
- `ls -a` shows all files including hidden
- `ls -la` shows detailed info for all files
- Hidden files are regular files, just with special naming

**Linux Convention:**
Dot files are used for:
- Configuration files (`.bashrc`, `.profile`)
- Cache directories (`.cache`)
- Version control (`.git`)
- Application data (`.ssh`)

---

### Level 4 → 5: File Types

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 3 minutes  
**Date Completed:** December 16, 2025  
**Concept:** Identifying file types

**Challenge Goal:**
There are several files in the inhere directory. One of them is human-readable. 

**Solution:**

Step 1: Connect and navigate
```bash
ssh -p 2220 bandit4@bandit.labs.overthewire.org
# used the password found in the previous level

ls
cd inhere
ls -la  # shown all available files
```

Step 2: Check file types
```bash
file ./-file*
#   they had same name with different versions, running it provided narrowed answer
```

Step 3: Read the human-readable file
```bash
cat ./-file_number
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- `file` command identifies file types
- File extensions don't always match actual type
- Can use wildcards (`*`) with `file` command
- "ASCII text" = human-readable
- "data" = binary data

---

### Level 5 → 6: File Properties

**Difficulty:** ⭐⭐ (2/5)  
**Time Spent:** 30 minutes  
**Date Completed:** December 17, 2025  
**Concept:** Using find with multiple conditions

**Challenge Goal:**
There is a file in the inhere directory with the following properties:
- Human-readable
- Size 1033 bytes
- Not executable

**Solution:**

Step 1: Connect and navigate
```bash
ssh -p 2220 bandit5@bandit.labs.overthewire.org
# used the password found in the previous level

cd inhere
```

Step 2: List all files
```bash
ls -la
# found out that there are multiple directories and files within it
```

Step 3: Use find with multiple conditions and my step by step
```bash
find -name ".*" -o -type f  # the output here was still a lot to check manually, used more conditions by looking into the man page
find -name ".*" -o -type f -size 1033c  # noticed that the output had only hidden files
find -name ".o" -size 1033c # located the only one file
find -type f -size 1033c # tried this way to check on results and found the same and only file of step 3
find . -size 1033c ! -executable # checked this way of searching also as per condition that shouldn't be executable and for learning purpose, found again same file
```

Step 4: Read the file
```bash
cat the_found_file
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- `find` command is powerful for locating files
- `-size [size]` filters by file size
- `c` suffix = bytes, `k` = kilobytes, `M` = megabytes
- `! -type` negates conditions (means NOT)
- Combining multiple conditions narrows results
- File properties include size and permissions

**Find Command Common Options:**
```bash
find . -size 1033c        # Exact size
find . -size +1033c       # Larger than
find . -size -1033c       # Smaller than
find . ! -executable      # NOT executable
find . -type f            # Regular files
find . -type d            # Directories
find . -user [username]   # Owner filter
find . -group [groupname] # Group filter
```

**Reflection:**
Finding files by properties is very useful. I can use this for:
- Locate configuration files
- Finding recently modified files
- Searching by permissions
Security audits often start with finding files with specific properties:
```bash
find / -perm -4000       # Find setuid files
find / -size 0           # Find empty files
find / -mtime -1         # Modified in last day
```

---

### Level 6 → 7: System-Wide Search

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 15 minutes  
**Date Completed:** December 18, 2025  
**Concept:** Finding files across entire system with filters

**Challenge Goal:**
There is a file somewhere on the server owned by user bandit7 and group bandit6 
with size 33 bytes.

**Solution:**

Step 1: Connect
```bash
ssh -p 2220 bandit6@bandit.labs.overthewire.org
# used the password found in the previous level
```

Step 2: Search entire filesystem
```bash
find / -size 33c -user bandit7 -group bandit6 2>/dev/null
```

Step 3: Read the file
```bash
cat /found_directory
# or
cat $(find / -size 33c -user bandit7 -group bandit6 2>/dev/null)
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- `find /` searches entire system (takes time)
- `-user` and `-group` filter by ownership
- `2>/dev/null` redirects errors to /dev/null (suppresses output)
- Combining multiple filters narrows results dramatically
- `-size 33c` searches in this case for exactly 33 bytes
- System-wide searches are slow; narrow criteria first

**Error Handling:**
- `2>` redirects standard error (file descriptor 2)
- `/dev/null` is a special file that discards input
- `2>/dev/null` hides "Permission denied" errors, which were a lot without

**Reflection:**
In security audits, you often need to find files with specific ownership/permissions:
```bash
find / -user root -perm -4000 2>/dev/null  # Setuid root files
find / -writable -type f 2>/dev/null       # World-writable files
```

---

### Level 7 → 8: Searching File Contents

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 5 minutes  
**Date Completed:** December 21, 2025  
**Concept:** Searching inside files with grep

**Challenge Goal:**
Use grep to find a line containing the word "millionth" and display the 
password next to it.

**Solution:**

Step 1: Connect
```bash
ssh -p 2220 bandit7@bandit.labs.overthewire.org
# used the password found in the previous level
```

Step 2: List files
```bash
ls -la
```

Step 3: Search for "millionth" using grep
```bash
grep millionth [file]
# or
cat [file] | grep millionth
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- `grep` searches for lines containing a pattern
- Format: `grep [pattern] [file]`
- Another commom way of using `cat [file] | grep [pattern]`
- Returns entire line(s) containing the pattern
- Case-sensitive by default
- `-i` flag for case-insensitive search
- `-n` shows the line in which we have the match
- `-r` search recursively if we don't know exactly the path
- `-c` the count of appearances

**Grep Examples:**
```bash
grep "password" file.txt           # Find "password"
grep -i "PASSWORD" file.txt        # Case-insensitive
grep -v "admin" file.txt           # Lines NOT containing "admin"
grep "^start" file.txt             # Lines starting with "start"
grep "end$" file.txt               # Lines ending with "end"
grep -c "pattern" file.txt         # Count matching lines
```

---

### Level 8 → 9: Removing Duplicates

**Difficulty:** ⭐⭐ (2/5)  
**Time Spent:** 15 minutes  
**Date Completed:** December 22, 2025  
**Concept:** Sorting and removing duplicate lines

**Challenge Goal:**
There's a file with many lines; one line appears only once. Find it.

**Solution:**

Step 1: Connect
```bash
ssh -p 2220 bandit8@bandit.labs.overthewire.org
# used the password found in the previous level
```

Step 2: List files
```bash
ls -la
# found the file that needed to be searched
```

Step 3: View the file (shows many identical lines)
```bash
head [file]
```

Step 4: Sort and remove duplicates
```bash
cat [file] | sort | uniq -c
# or
cat [file] | sort | uniq -u
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- `uniq` only works on sorted data (sorts first)
- `-u` flag = show only unique lines
- `-d` flag = show only duplicates
- `-c` flag = count occurrences
- `-i` flag = case insensitive

**Commands:**
```bash
sort file.txt | uniq           # Remove consecutive duplicates
sort file.txt | uniq -c        # Count occurrences
sort file.txt | uniq -d        # Show only duplicates
sort file.txt | uniq -u        # Show only unique lines
```

**Real Example:**
```bash
cat access.log | cut -d ' ' -f1 | sort | uniq -c | sort -rn | head
# Shows most active IP addresses in a log file
```

---

### Level 9 → 10: Finding Strings

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 15 minutes  
**Date Completed:** December 22, 2025  
**Concept:** Extracting human-readable strings from binary files

**Challenge Goal:**
Find the password which is human-readable in a file containing mostly binary data.

**Solution:**

Step 1: Connect
```bash
ssh -p 2220 bandit9@bandit.labs.overthewire.org
# used the password found in the previous level
```

Step 2: List files
```bash
ls -la
# found the file that needed to be searched 
```

Step 3: Try to read normally
```bash
cat data.txt | head
# and
grep "=" | head
# output: binary garbage
```

Step 4: Extract human-readable strings
```bash
strings [file]    # was able to locate just like this
# and/or
strings [file] | grep "="   # this narrowed down the result
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- `strings` extracts human-readable text from binary files
- Useful for examining compiled binaries or corrupt data
- Pipe with `grep` to find specific text
- Binary files can contain readable strings
- Minimum string length is usually 4 characters

**Strings Command:**
```bash
strings file.bin              # Extract all readable strings
strings file.bin | grep pwd   # Find password strings
strings file.bin | wc -l      # Count readable strings
```

**Real Example:**
```bash
strings /bin/ls | grep -i "password"  # Check for hardcoded passwords in binaries
strings malware.bin | head              # See what strings malware contains
```

---

### Level 10 → 11: Quoted Strings

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 10 minutes  
**Date Completed:** December 22, 2025  
**Concept:** Base64 encoding/decoding

**Challenge Goal:**
The password is encoded in Base64.

**Solution:**

Step 1: Connect
```bash
ssh -p 2220 bandit10@bandit.labs.overthewire.org
# used the password found in the previous level
```

Step 2: List and view file
```bash
ls -la
cat [file]
# output were in base64
```

Step 3: Decode Base64
```bash
cat [file] | base64 --decode
```

**Output:** Got the necessary password to advance to the next level.

**Reflection:**
- Base64 is encoding (not encryption)
- `base64 -d` decodes Base64
- `base64` encodes to Base64
- Base64 is easily decoded; use encryption if you need security

**Base64 Commands:**
```bash
echo "hello" | base64                    # Encode
echo "aGVsbG8=" | base64 -d              # Decode
cat file.txt | base64                    # Encode file
cat file.txt | base64 -d > output.txt    # Decode to file
```

---

### Level 11 → 12: Text Transformation

**Difficulty:** ⭐⭐ (2/5)  
**Time Spent:** 15 minutes  
**Date Completed:** December 22, 2025  
**Concept:** Using tr for text transformation

**Challenge Goal:**
The password is encoded with ROT13 (rotate letters by 13).

**Solution:**

Step 1: Connect
```bash
ssh -p 2220 bandit11@bandit.labs.overthewire.org
# used the password found in the previous level
```

Step 2: List and view file
```bash
ls -la
cat [file]
# output looked like a scrambled text
```

Step 3: Apply ROT13 transformation
```bash
cat [file] | tr [a-zA-Z] [n-za-mN-ZA-M]
# or
cat [file] | tr "a-zA-Z" "n-za-mN-ZA-M"
```

**Output:** Got the necessary password to advance to the next level.

**Reflection:**
- ROT13 rotates each letter by 13 positions
- A→N, N→A, etc.
- `tr` command does character translation
- `tr 'a-zA-Z' 'n-za-mN-ZA-M'` applies ROT13
- ROT13 is simple obfuscation, not encryption
- Understanding Caesar ciphers helps identify patterns

---

### Level 12 → 13: Decompressing Files

**Difficulty:** ⭐⭐⭐ (3/5)  
**Time Spent:** 60 minutes  
**Date Completed:** January 14, 2026  
**Concept:** Identifying and decompressing various archive formats

**Challenge Goal:**
A file is hexdumped. Decompress it to find the password.

**Solution:**

Step 1: Connect
```bash
ssh -p 2220 bandit12@bandit.labs.overthewire.org
# used the password found in the previous level
```

Step 2: View the file
```bash
cat data.txt
# noticed the hexdump pattern
```

Step 3: Convert hex to binary
```bash
xxd -r data.txt > data.bin
```

Step 4: Identify file type
```bash
file data.bin
# gzip file
```

Step 5: Renamed and Decompress
```bash
mv data.bin data.bin.gz
gunzip data.bin.gz
file data2.bin
```
Step 6: Kept on decompressing until done
```bash
# kept always checking the file type
file datanumber.bin
# checked the compression type and used
bzcat datanumber.bin > datanumber.bin
gunzip datanumber.bin.gz
tar -xf datanumber.bin
```

The file might be:
- gzip → `gunzip`
- bzip2 → `bunzip2`
- tar → `tar -xf`
- zip → `unzip`

Eventually:
```bash
cat datanumber.bin
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- `xxd -r` converts hexdump back to binary
- `file` identifies file types
- Different compression formats need different tools
- Files might be compressed multiple times
- `tar` is used for archiving (not compression)

**Compression Tools:**
```bash
gzip file              # Compress
gunzip file.gz         # Decompress

bzip2 file             # Compress (better)
bunzip2 file.bz2       # Decompress

tar -cf file.tar dir   # Archive
tar -xf file.tar       # Extract

zip file.zip dir       # Archive & compress
unzip file.zip         # Extract

xxd file > hex.txt     # Create hexdump
xxd -r hex.txt > file  # Restore from hex
```
---

### Level 13 → 14: SSH Keys

**Difficulty:** ⭐⭐⭐ (3/5)  
**Time Spent:** 60 minutes  
**Date Completed:** January 15, 2026  
**Concept:** Using SSH private keys for authentication

**Challenge Goal:**
Use the provided SSH private key to log in as bandit14.

**Solution:**

Step 1: Connect and check key
```bash
ssh -p 2220 bandit13@bandit.labs.overthewire.org
# used the password found in the previous level
ls -la
# found the sshkey.private file
```

Step 2: Tried to manipulate the file but the server wouldn't allow a connections between Bandit13 and Bandit14 as they were in localhost. So using the ssh from within didn't work. I got to the understanding of `scp` command and at first was trying to use from within the Bandit13, but as it wasn't work due to permissions, I had to reverse it and download from my local VM using always `scp`, as follows:
```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private /home/username
```

Step 3: Check key permissions
```bash
ls -la sshkey.private
# had to update the permission as follows:
chmod 600 sshkey.private
# it was too permissive for a ssh file
```

Step 4: SSH using the key
```bash
ssh -p 2220 -i sshkey.private bandit14@bandit.labs.overthewire.org
```

Step 4: Get the password
```bash
cat /etc/bandit_pass/bandit14
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- SSH keys are alternative to passwords
- Private keys must have 600 permissions (read/write owner only)
- `-i` flag specifies private key file
- Public key authentication is more secure than passwords
- `scp` Secure Copy Protocol that uses SSH

---

### Level 14 → 15: Submitting Passwords

**Difficulty:** ⭐⭐ (2/5)  
**Time Spent:** 30 minutes  
**Date Completed:** February 5, 2026  
**Concept:** Network communication and localhost connections

**Challenge Goal:**
Submit the current password to localhost:30000 and receive the next password.

**Solution:**

Step 1: Connect
```bash
ssh -p 2220 bandit14@bandit.labs.overthewire.org
# used the password found in the previous level
```

Step 2: Get the password for next level on localhost:30000
```bash
echo password_level_14 | nc localhost 30000
```
or 
Step 3: Connect to the service on localhost:30000
```bash
telnet localhost 30000
#or
nc localhost 30000
```

Step 3.1: Send the current password
Type or paste: password_level_13
Then press Enter.

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- `telnet` connects to ports (legacy)
- `nc` (netcat) is modern networking tool
- Localhost (127.0.0.1) is your own machine
- Services listen on ports
- Manual network communication tests services

**Network Tools:**
```bash
telnet host port                   # Connect to service
nc host port                       # Netcat (better than telnet)
curl http://host:port              # HTTP requests
wget http://host:port              # Download files
nmap -p port host                  # Scan ports
ss -tlnp                           # Show listening ports
```
---

### Level 15 → 16: SSL/TLS Connections

**Difficulty:** ⭐ (1/5)
**Time Spent:** 30 minutes
**Date Completed:** February 13, 2026
**Concept:** Network communication and localhost connections

**Challenge Goal:** 
Submit the current password to localhost:30001 using SSL/TLS and receive the next password.

**Solution:**
Step 1: Connect
```bash
ssh -p 2220 bandit15@bandit.labs.overthewire.org
# used the password found in the previous level
```

Step 2: Get the password for next level on localhost:30001 using ssl
```bash
echo password_level_15 | openssl s_client -connect localhost:30001 -quiet
or
echo password_level_15 | ncat --ssl localhost 30001
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- there should be a server listening `openssl s_server`
- the request will come from `openssl s_client`
- `-quiet` will hide the construction handshake
- `ncat` comes from the `namp` suite and is used by sysadmins

---

### Level 16 → 17: SSL/TLS Connections

**Difficulty:** ⭐ (1/5)
**Time Spent:** 30 minutes
**Date Completed:** February 13, 2026
**Concept:** Network communication and localhost connections

**Challenge Goal:** 
Mapping a specific range of ports, finding the ones that are listening to SSL communications and submit the current password to localhostusing:port_found SSL/TLS and receive the next password.

**Solution:**
Step 1: Connect
```bash
ssh -p 2220 bandit16@bandit.labs.overthewire.org
# used the password found in the previous level
```

Step 2: Mapping the network
```bash
nmap -p start_port-finish_port localhost
# found all the open ports no more info shared
```

Step 3: Further investigating ports
```bash
nmap -p start_port-finish_port -sV localhost
# probing the ports and identifying the services I was able to find the right one
```

Step 4: Sending the current level password to that port
```bash
echo password_level_16 | ncat --ssl localhost found_port
# got a Private Key RSA as reply
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- `nmap` is a very powerful tool for mapping the network and active reconnaissance
- `nmap` has some very powerful flags that used correctly give us a lot of info
- passwords are not only strings to access servers but also RSA PK
- `nmap` is also used in Security auditing

---

### Level 17 → 18: Comparing File Contents

**Difficulty:** ⭐ (1/5)
**Time Spent:** 15 minutes
**Date Completed:** February 13, 2026
**Concept:** Searching for specific information on a file by comparing them

**Challenge Goal:** 
Need to get the password from a new_file and that password is the only line that have changed from the old_file.

**Solution:**
Step 1: Connect
```bash
ssh -p 2220 -i bandit16_key.private bandit17@bandit.labs.overthewire.org
# used the RSA PK saved on local machine from past level
```

Step 2: Searched for files
```bash
ls
# found the old_file and new_file
```

Step 3: Comparing both of them
```bash
diff old_file new_file
# got the new password for the next level
```

**Output:** Got the nec
essary password to advance to the next level.

**Key Learnings:**
- `diff` is used to compare 2 files and show their differences
- useful to check on what was changed from logs

---

### Level 18 → 19: File Contents

**Difficulty:** ⭐ (1/5)
**Time Spent:** 5 minutes
**Date Completed:** February 14, 2026
**Concept:** Getting information from a file without connecting to host

**Challenge Goal:** 
Password is in a README file, but the .bashrc was changed so that if we connec through SSH it will automatically log us out.

**Solution:**
Step 1: Connect
```bash
ssh -p 2220 bandit18@bandit.labs.overthewire.org
# used the password and got kicked out
```

Step 2: Searched for files
```bash
ssh -p 2220 bandit18@bandit.labs.overthewire.org ls
# found the needed file
```

Step 3: Comparing both of them
```bash
ssh -p 2220 bandit18@bandit.labs.overthewire.org cat readme
# got what I needed
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- we don't need to strictly connect to the Host in order to see what is in there
- after the connection command we can use other commands

---

### Level 19 → 20: SUID usage

**Difficulty:** ⭐ (1/5)
**Time Spent:** 10 minutes
**Date Completed:** February 17, 2026
**Concept:** Using setuid file to gain privileged information

**Challenge Goal:** 
Password is in the /etc location where the password for the next level is owned by the next level user and can't be accessed by the current level user. Through a suid file we should get it.

**Solution:**
Step 1: Connect
```bash
ssh -p 2220 bandit19@bandit.labs.overthewire.org
```

Step 2: Searched for files
```bash
ls  # found the file
ls -la  # it is owned indeed by the level 20 user and has a SUID
```

Step 3: Using file to understand what it does
```bash
./executed_file # gave me the next level user privileges
```
Step 4: Using file to gain access to next password
```bash
./executed_file cat /etc/bandit_pass/bandit20
```
**Output:** Got the nec
essary password to advance to the next level.

**Key Learnings:**
- SUID can be a whole in security
- SUID gives us the privileges of the owner of the file
- it's a best practce to check if our system have unexpected SUID or GUID set by:
    `find -perm /6000`

---

### Level 20 → 21: SUID and port usage

**Difficulty:** ⭐⭐⭐ (3/5)
**Time Spent:** 40 minutes
**Date Completed:** February 23, 2026
**Concept:** Connect to a port using a seuid program

**Challenge Goal:** 
I need to use a setuid program left there to make a connection (TCP) to a port that I specify and if the password from the previous level (Level 19 -> 20) is correct I'll get the new one.

**Solution:**
Step 1: Connect & Search for file
```bash
ssh -p 2220 bandit20@bandit.labs.overthewire.org
ls  # found the file
```

Step 2: namp ports
```bash
nmap -p- -A -sV -T4 localhost
# I have mapped the ports as I had no clue where to send the password to, to get the new one
# found some possible solutions and invested on them
```

Step 3: Using file on ports
```bash
# I have used this file in the following ways which I later discovered the real solution
# I'm leaving here to register my reasoning and learning path
echo password_20 | ./file port_number
cat /etc/bandit_pass/bandit20 | ./file port_number
./file port_number < $(cat /etc/bandit_pass/bandit20)
# while doing this attempts I have opened a different terminal and simulate connection
# found out that using the file the message wasn't transferred, but using a simple nc command it was
```
Step 4: Tried on a server created by myself
```bash
cat /etc/bandit_pass/bandit20 | nc -l portchoosen &
# I was doing it to undertand what would happen when I connect to it using the file
./file portchoosen
# got the password for the next level
# it turns out that the file wanted me to connect and check the password that the server was sending and making sure it was from the level 19 -> 20 then provide the new one by elevating its privilages to Bandit21
# I originally thought I had to send the password to get a new one from the server
```
**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- SUID binary behavior
- Network Reconnaissance
- TCP interaction
- Process management
- Debugging

---

### Level 21 → 22: Cron jobs

**Difficulty:** ⭐⭐ (2/5)
**Time Spent:** 30 minutes
**Date Completed:** February 24, 2026
**Concept:** Get information from a cron file

**Challenge Goal:** 
There is a job running automatically at regular times that I need to get information from it to locate the new password.

**Solution:**
Step 1: Connect & Search for file
```bash
ssh -p 2220 bandit21@bandit.labs.overthewire.org
ls /etc/cron.d/ # found the files
```

Step 2: Examin the files
```bash
ls -la /etc/cron.d/ # got information on all the files that I could check and started checking
cat /etc/cron.d/file_name   # checked like this and found the jobs running within them
```

Step 3: Checked on the jobs path
```bash
# Once located the right file with the right path, I simply went to its path and check on the contents
cat /path/found/for/the/job #got the new password
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- CRON jobs
- read when the job will be executed as per crontab(5)
- CRON jobs might show us paths and files that doesn't have the right permissions set to exploit

---

### Level 22 → 23: Cron jobs

**Difficulty:** ⭐ (1/5)
**Time Spent:** 10 minutes
**Date Completed:** February 25, 2026
**Concept:** Get information from a cron file

**Challenge Goal:** 
There is a job running automatically at regular times that I need to get information from it to locate the new password. This time I need to understand what the script is doing in order to get the password.

**Solution:**
Step 1: Connect & Search for file
```bash
ssh -p 2220 bandit22@bandit.labs.overthewire.org
ls /etc/cron.d/ # found the files
```

Step 2: Examin the files
```bash
ls -la /etc/cron.d/ # got information on all the files that I could check and started checking
cat /etc/cron.d/file_name   # got the script, understood what it was doing and runned on my terminal to get the password
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- CRON jobs
- read and understand script written by others

---
### Level 23 → 24: Cron jobs and escalating privilages

**Difficulty:** ⭐⭐⭐ (3/5)
**Time Spent:** 30 minutes
**Date Completed:** March 13, 2026
**Concept:** Using a cron job to gain information of next level password

**Challenge Goal:** 
There is a job running automatically at regular times that I need to use it to gain privilages of the next level. With Bandit24 privilages I get the new password.

**Solution:**
Step 1: Connect & Search for file
```bash
ssh -p 2220 bandit23@bandit.labs.overthewire.org
ls /etc/cron.d/ # found the files
```

Step 2: Examin the files
```bash
ls -la /etc/cron.d/ # got information on all the files that I could check and started checking
cat /etc/cron.d/file_name   # got the script, understood what it was doing
```

Step 3: Went in the location of the running scrip
```bash
cat /usr/bin/script_name # understood what it was doing and where to look next
ls -ld /var/spool/bandit24/foo
# initialy I broke my head on how to write a script there as I couldn't CD or LS inside there
# understood that I could use my /tmp dir to make a file and the CP the file there instead of going there and creating from there
```

Step 4: Created my script
```bash
vim /tmp/script_23.sh # created my script as per the following:

#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/gotit24.txt
chmod 644 /tmp/gotit24.txt
```

Step 5: Getting it from Bandit23
```bash
# By understanding that /tmp is world-writable (1777) I could access it there from the Bandit23 by knowing the name of the file and doing
cat /tmp/gotit24.txt
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- We should audit CRON jobs as we could allow a scheduled escalation
- `/tmp` is a shared scratch space
- if a dir doesn't show us what is in there due to permissions, we might still be able to drop a file in there via CP

---
### Level 24 → 25: Brute forcing a PIN code via connection

**Difficulty:** ⭐⭐ (2/5)
**Time Spent:** 30 minutes
**Date Completed:** March 16, 2026
**Concept:** Create a connection to a port and brute force an unknown PIN code

**Challenge Goal:** 
There is a daemon listening on port 30002 which is waiting for the bandit24 password plus a 4 digit pin that I will neet to brute force it.

**Solution:**
Step 1: Connect
```bash
ssh -p 2220 bandit24@bandit.labs.overthewire.org
```

Step 2: Understand connection
```bash
nc localhost 30002  # it showed me the prompt and what it was expeting
```

Step 3: Created a script to work on the bruteforce
```bash
vim /tmp/script_24.sh   # created the necessary loops to work on it
chmod 777 /tmp/script_24.sh  # made it executable
```

Step 4: Used the script
```bash
/tmp/script_24.sh | nc localhost 30002  # got the password
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- Greater understand on daemon work and TCP connection
- paying attention to the format expected
- protocol awareness and piping

---
### Level 25 → 26: Working with Shell

**Difficulty:** ⭐⭐⭐ (3/5)  
**Time Spent:** 40 minutes  
**Date Completed:** March 20, 2026  
**Concept:** Logging to a different shell and changing it to Bash

**Challenge Goal:**
Loggin to Bandit26 that is using a different shell, force the /bin/bash and get the password for next level.

**Solution:**

Step 1: Connect and check key
```bash
ssh -p 2220 bandit25@bandit.labs.overthewire.org
# used the password found in the previous level
ls -la
# found the bandit26.sshkey file
```

Step 2: Downloaded the sshkey to my VM as per previous challenges:
```bash
scp -P 2220 bandit25@bandit.labs.overthewire.org:/home/bandit25/bandit26.sshkey /home/username
```

Step 3: Check key permissions
```bash
ls -la sshkey.private
# had to update the permission as follows:
chmod 600 sshkey.private
# it was too permissive for a ssh file
```

Step 4: SSH using the key
```bash
ssh -p 2220 -i bandit26.sshkey bandit26@bandit.labs.overthewire.org
# didn't work as I was kicked out of the session
```

Step 5: Checked further on Bandit25
```bash
grep bandit26 /etc/passwd # found the shell file
cat /usr/bin/showtext   # checked the shell file and discovered that it was using more with the shell
```

Step 6: Understand how the more behave and act on it.
```bash
# Shrink my terminal very very small and runned
ssh -p 2220 -i bandit26.sshkey bandit26@bandit.labs.overthewire.org
# soon after pressed:
v
# that opened VIM
```

Step 7: Spawn a shell from VIM
```bash
:set shell=/bin/bash
:shell
#   the next line in VIM was the bandit26 Bash shell
cat /etc/bandit_pass/bandit26
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- /etc/passwd -> logging information also about the used shell
- we can use script as shell if want
- more is interactive and dependent on the size of the terminal window
- VIM command interface and the ability of spawn shells

---
### Level 26 → 27: Working with Shell & SUID

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 10 minutes  
**Date Completed:** March 23, 2026  
**Concept:** The same as the previous level but I used a SUID withing the VIM terminal

**Challenge Goal:**
The challenge was to use the VIM terminal that I was on for the previous level and do normal tasks like using the privileged SUID to get the next level password.

**Solution:**

Step 1: Connect and check key
```bash
ssh -p 2220 bandit25@bandit.labs.overthewire.org
# used the password found in the previous level
ls -la
# found the bandit26.sshkey file
```

Step 2: Used the downloaded sshkey to log back in
```bash
ssh -p 2220 -i bandit26.sshkey bandit26@bandit.labs.overthewire.org
# didn't work as I was kicked out of the session
```

Step 3: Spawn a shell from VIM
```bash
:set shell=/bin/bash
:shell
#   the next line in VIM was the bandit26 Bash shell
./bandit27_suidfile cat /etc/bandit_pass/bandit27
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- /etc/passwd -> logging information also about the used shell
- we can use script as shell if want
- more is interactive and dependent on the size of the terminal window
- VIM command interface and the ability of spawn shells
- within VIM I can do everything a normal terminal could include using SUID files

---
### Level 27 → 28: Copying a repository using GIT command

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 10 minutes  
**Date Completed:** March 23, 2026  
**Concept:** Using SSH and GIT command I should get a Repo with the password

**Challenge Goal:**
It was given the repository and the port to which I should connect to get it. The password is there.

**Solution:**

Step 1: Connect and cloned the repo
```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
#   used the password from previous level
```

Step 2: Inspected the repo
```bash
cd /repo
ls
cat README
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- how to use ports on git ssh commands

---
### Level 28 → 29: Working with GIT and log investigation

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 15 minutes  
**Date Completed:** March 23, 2026  
**Concept:** Investigating past logs for information

**Challenge Goal:**
It was given the repository and the port to which I should connect to get it. The password is there.

**Solution:**

Step 1: Connect and cloned the repo
```bash
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
#   used the password from previous level
```

Step 2: Inspected the repo
```bash
cd /repo
ls
cat README  # the password wasn't there
```

Step 3: Inspect repository
```bash
git log     # found some changes on it
git log -p  # checked in the changes for what happened and the password was there
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- the importance of checking for the logs in git files
- logs contain important information that should be audited
- patch option in the git log command show detailed info of those changes made in the commit

---
### Level 29 → 30: Working with GIT and branches

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 20 minutes  
**Date Completed:** March 24, 2026  
**Concept:** Investigating branches

**Challenge Goal:**
It was given the repository and the port to which I should connect to get it. The password is there.

**Solution:**

Step 1: Connect and cloned the repo
```bash
git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo
#   used the password from previous level
```

Step 2: Inspected the repo
```bash
cd /repo
ls
cat README  # the password wasn't there but a message that mention password isn't in production
```

Step 3: Inspect repository
```bash
git log     # found some changes on it
git log -p  # checked in the changes for what happened and the password wasn't there
```

Step 4: Checked for branches
```bash
git branch -a     # found some branches including a dev one
git switch remotes/origin/dev --detach
#   here I located another README file and the password was in there
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- the importance of checking for the logs and branches
- understood that messages like "<no password in production>" is not a dead end message, but a hint. Understood that I should ask "What is this trying to tell me"

---
### Level 30 → 31: Working with GIT and TAG

**Difficulty:** ⭐⭐ (2/5)  
**Time Spent:** 20 minutes  
**Date Completed:** March 24, 2026  
**Concept:** Investigating GIT and TAGs

**Challenge Goal:**
It was given the repository and the port to which I should connect to get it. The password is there.

**Solution:**

Step 1: Connect and cloned the repo
```bash
git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
#   used the password from previous level
```

Step 2: Inspected the repo
```bash
cd /repo
ls
cat README  # the password wasn't there
```

Step 3: Inspect repository
```bash
git log     # only one commit
git log -p  # nothing special there
```

Step 4: Checked for branches
```bash
git branch -a     # found only one branch the main
```

Step 5: Checked for TAGs
```bash
#   I had to search and learn about ways information could be found in GIT and found TAGs
git tag # discovered a tag that said "secret"
#   Learned also that in GIT I can read a file like this:
git show [name]
git show secret # got the password
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- the importance of checking for the logs, branches, and Tags
- understood that there are four ways to check for information on GIT they are:
- Commits (git log -p)
- Branches (git branch -a)
- Tags (git tag + git show tag)
- Blobs & Trees (git cat-file -p <hash>)

---
### Level 31 → 32: Working with GIT

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 15 minutes  
**Date Completed:** March 25, 2026  
**Concept:** Investigating GIT and pushing to it

**Challenge Goal:**
It was given the repository and the port to which I should connect to get it. The password is there.

**Solution:**

Step 1: Connect and cloned the repo
```bash
git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo
#   used the password from previous level
```

Step 2: Inspected the repo
```bash
cd /repo
ls
cat README  # the password wasn't there but got instructions to create a file and push it to get the password
```

Step 3: Created file and pushed
```bash
touch key.txt
vim key.txt     # edited the file as specified
#   I have tried the normal commands to check it and push but wasn't working, here is the commands:
git status
git add .
git commit -m "pushing the requested file"
#   didn't work, so investigated:
ls -la  # found a .gitignore
cat .gitignore  # it was rejecting the *.txt
echo "" > .gitignore
#   repeated the steps above and worked fine
git status
git add .
git commit -m "pushing the requested file"
git push    # got the password
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- always do basic checks as per past levels, commit, log, tag
- check the folder also > ls -la 
- check .gitignore files as it might be the issue

---
### Level 32 → 33: Shell and terminal

**Difficulty:** ⭐⭐ (2/5)  
**Time Spent:** 15 minutes  
**Date Completed:** March 25, 2026  
**Concept:** Working with running shell

**Challenge Goal:**
It was given a shell that was translating any char to uppercase. I had to escape that and move on.

**Solution:**

Step 1: Connect
```bash
ssh -p 2220 bandit32@bandit.labs.overthewire.org
#   used the password from previous level
```

Step 2: Worked on the shell
```bash
ls  # it was translated to LS and didn't work
cntr + z    # didn't work also as it got upper cased
```

Step 3: Working with non char like symbols, numbers, etc
```bash
~   # tried but said that can't go to home directory
# studied a bit and understood that $0 points to the shell running
$0  # worked and I got out of the uppercase script
#   understood the concept that even if a shell script is running the $0 will be pointing to the underlying real shell
# from here got the password
cat /etc/bandit_pass/bandit33   # got the password
```

**Output:** Got the necessary password to advance to the next level.

**Key Learnings:**
- $0 holds the name or path of the currently running shell or script
- $0 was pointing to the real shell binary underneath it
- A restricted shell is only as strong as what it restricts

---
### Level 33 → 34: Finish line!

**Difficulty:** ⭐ (1/5)  
**Time Spent:** 3 minutes  
**Date Completed:** March 25, 2026  
**Concept:** Game-Over!

**Challenge Goal:**
There is no more levels and here the games were completed.

**Solution:**

Step 1: Connect
```bash
ssh -p 2220 bandit33@bandit.labs.overthewire.org
#   used the password from previous level
ls  # found a README.txt file
cat README.txt  # prompted a messaged that there is no more level and I completed the Bandit game.
```
---

## 📊 Skills Developed

### By Phase

**Phase 1: Basic Commands**
- ✅ SSH connection
- ✅ File reading and listing
- ✅ Special character handling
- ✅ Hidden file discovery
- ✅ File type identification

**Phase 2: File Operations**
- ✅ System-wide searching
- ✅ Content searching with grep
- ✅ Duplicate removal
- ✅ String extraction
- ✅ Piping basics

**Phase 3: Text Processing**
- ✅ Base64 encoding/decoding
- ✅ Text transformation (ROT13, sed, tr)
- ✅ File compression/decompression
- ✅ SSH key authentication
- ✅ Network communication

**Phase 4: Advanced Filtering**
- ✅ SSL/TLS connections
- ✅ Port scanning
- ✅ File comparison
- ✅ SSH configuration
- ✅ Permission modification

**Phase 5: Complex Concepts**
- ✅ Advanced piping
- ✅ Scripting basics
- ✅ Binary analysis
- ✅ Network protocols
- ✅ System administration

---

## 🔑 Key Commands Reference

| Command | Purpose | Example |
|---------|---------|---------|
| `ssh` | Remote connection | `ssh -p 2220 user@host` |
| `cat` | Display file | `cat filename` |
| `ls -la` | List detailed | `ls -la` |
| `find` | Search files | `find . -size 1033c` |
| `grep` | Search content | `grep pattern file` |
| `sort` | Order lines | `sort file.txt` |
| `uniq` | Remove duplicates | `uniq file.txt` |
| `strings` | Extract text | `strings binary.bin` |
| `base64` | Encode/decode | `base64 -d encoded.txt` |
| `tr` | Translate chars | `tr 'a-z' 'n-za-m'` |
| `sed` | Stream editor | `sed 's/old/new/g'` |
| `xxd` | Hexdump | `xxd -r hex.txt > file` |
| `gunzip` | Decompress gzip | `gunzip file.gz` |
| `tar` | Archive files | `tar -xf file.tar` |
| `telnet/nc` | Connect port | `nc localhost 30000` |

---

## 🎓 Learning Reflection

### What This Game Teaches

Bandit teaches the **foundation** of all cybersecurity work. You cannot do advanced 
security work without mastery of:

- **Linux command line** - Every tool, script, and technique uses it
- **File system navigation** - You'll spend hours finding files
- **Pattern matching** - grep, regex, and filtering are constant
- **Text processing** - Analyzing logs, output, and data
- **Piping and chaining** - Combining tools for powerful results

---

⭐ **Bandit is the perfect start to cybersecurity learning.** 🔒
```