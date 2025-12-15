# SideQuest 2 🎯
 
For those who want another challenge, have a look around the VM to get access to the key for Side Quest 2! Accessible through our [Side Quest Hub!](https://tryhackme.com/adventofcyber25/sidequest)

This sidequest has the same context, namely password cracking, so we first check every file in the main directory.

```
ls -la 
```
and we see that we find .Passwords.kdbx

```
file .Passwords.kdbx
#output 
.Passwords.kdbx: Keepass password database 2.x KDBX
```

what is KeePass Password Database 2.x (KDBX)?
is an encrypted file format used by KeePass, a popular open-source password manager.
In a CTF or forensic context, finding a .kdbx file usually implies:
- The next step is password cracking or key recovery (e.g., extracting a hash and attempting a wordlist attack).
- The file likely contains credentials or flags once successfully unlocked.

Let’s crack the password from that file with john.

1. Extract the hash from the `.kdbx` file
```
cd Desktop/john/run/
ls | grep -i keepass2john 
keepass2john file.kdbx > keepass.hash
./keepass2john ~/.Passwords.kdbx >> ~/Desktop/hash_Passwords_kdbx
```
John cannot read `.kdbx` files directly. You must first convert the file into a hash format. The result is a hash representation that can be processed by John.

```
john --wordlist=/usr/share/wordlists/rockyou.txt ~/Desktop/hash_Passwords_kdbx 

```
John will attempt to match the password against the extracted hash.

output: 

```
Using default input encoding: UTF-8
Loaded 1 password hash (KeePass [AES/Argon2 256/256 AVX2])
Cost 1 (t (rounds)) is 20 for all loaded hashes
Cost 2 (m) is 65536 for all loaded hashes
Cost 3 (p) is 2 for all loaded hashes
Cost 4 (KDF [0=Argon2d 2=Argon2id 3=AES]) is 0 for all loaded hashes
Will run 2 OpenMP threads
Note: Passwords longer than 41 [worst case UTF-8] to 124 [ASCII] rejected
Press 'q' or Ctrl-C to abort, 'h' for help, almost any other key for status
Failed to use huge pages (not pre-allocated via sysctl? that's fine)
[</REDACTED>]      (.Passwords)     
1g 0:00:01:13 DONE (2025-12-15 14:30) 0.01366g/s 1.312p/s 1.312c/s 1.312C/s harrypotter..ihateyou
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

