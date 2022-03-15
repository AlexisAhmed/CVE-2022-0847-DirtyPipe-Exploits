![Dirty Pipe](https://forum.hackersploit.org/uploads/default/original/2X/a/a3cc4ce68db810c4e24d35cb929a952363f11703.png
)

# CVE-2022-0847-DirtyPipe-Exploits
A collection of exploits and documentation for penetration testers and red teamers that can be used to aid the exploitation of the Linux Dirty Pipe vulnerability.

# About The Vulnerability
- Dirty Pipe (CVE-2022-0847) is a local privilege escalation vulnerability in the Linux kernel that could potentially allow an unprivileged user to do the following:
	- Modify/overwrite arbitrary read-only files like /etc/passwd. 
	- Obtain an elevated shell.

## Affected versions
- Linux kernel versions newer than 5.8 are affected.
- So far the vulnerability has been patched in the following Linux kernel versions:
	- 5.16.11
	- 5.15.25
	- 5.10.102
- You can learn more about the vulnerability here: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-0847

# DirtyPipe Vulnerability Scanner
- If you are not sure if a target system is vulnerable, use this really cool bash script developed by @basharkey.
- DirtyPipe Checker: https://github.com/basharkey/CVE-2022-0847-dirty-pipe-checker


 
## Compiling the exploit
- An automated compiler bash script has been provided to you to automate the compilation of both exploits.
- In order to compile the exploit succesfully, you will need to have GCC installed.

```
sudo apt-get install gcc
```

- After installing GCC, you can run the 'compile.sh" script as follows:

```
chmod +x compile.sh
```
```
./compile.sh
```


# Exploit-1 - Modifying/overwriting read only files
- This repo contains 2 exploits, the 'exploit-1.c' exploit can be used to modify or overwrite arbitrary read only files.
- This exploit is a proof of concept that was developed by Max Kellermann and has been modified to change the root password in the /etc/passwd file, consequently providing you with access to an elevated shell.



## Running the exploit binary
- The exploit code has already been configured to replace the root password with the password "piped" and will take a backup of the /etc/passwd file under /tmp/passwd.bak. Furthermore, the exploit will also provide you with an elevated root shell and will restore the original passwd file when done.

```
./exploit-1
```

# Exploit-2 - Hijacking SUID binaries
- This exploit can be used to inject and overwrite data in read-only SUID process memory that run as root.

## Finding SUID binaries
```
find / -perm -4000 2>/dev/null
```
## Running the exploit binary

```
./exploit-2 /usr/bin/sudo
```

## Important Note 
- I do not claim credit/ownership/disclosure of the vulnerability and all corresponding exploits hosted in this GitHub repo.
- All the credit goes to the awesome Max Kellerman, you can check out the official disclosure here: https://dirtypipe.cm4all.com/

## Credits
- https://github.com/febinrev/dirtypipez-exploit
- https://github.com/basharkey/CVE-2022-0847-dirty-pipe-checker
