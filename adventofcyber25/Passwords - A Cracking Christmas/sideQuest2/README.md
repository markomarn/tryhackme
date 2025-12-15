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
