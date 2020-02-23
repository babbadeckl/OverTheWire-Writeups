# Over the wire - Bandit
The Bandit wargame is aimed at absolute beginners. It will teach the basics needed to be able to play other wargames.

## **Level 0**
The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

Commands you may need to solve this level:
```
ls, cd, cat, file, du, find
```

Connect to the server via ssh:

```
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

As the description of the task says: the password is located in the ***readme*** file.

```
bandit0@bandit:~$ cat readme 
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```
----
## **Level 1**
The password for the next level is stored in a file called - located in the home directory

Commands you may need to solve this level:
```
ls, cd, cat, file, du, find
```
Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

As the description says: the password is located in a file called ***-***
```
bandit1@bandit:~$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```
----
## **Level 2**
The password for the next level is stored in a file called spaces in this filename located in the home directory

Commands you may need to solve this level:
```
ls, cd, cat, file, du, find
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

As the description of the task says: the password is stored in a file called "spaces in this filename" located in the home directory. So we simply set the file name in apostrophes ""

```
bandit2@bandit:~$ cat "spaces in this filename" 
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```
----
## **Level 3**
The password for the next level is stored in a hidden file in the inhere directory.

Commands you may need to solve this level:
```
ls, cd, cat, file, du, find
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

As the description of the task says: the password is stored in a hidden file called ***inhere***. We can show hidden files with the "ls -la" command.

```
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 Oct 16  2018 .
drwxr-xr-x 3 root    root    4096 Oct 16  2018 ..
-rw-r----- 1 bandit4 bandit3   33 Oct 16  2018 .hidden
bandit3@bandit:~/inhere$ cat .hidden 
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```
----
## **Level 4**
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

Commands you may need to solve this level:
```
ls, cd, cat, file, du, find
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

The hint says: the password is hidden in the only human-readbale file. Therefore, we check the file type of all the files in this directory. The only ASCII text file, is file07, in which the password is stored.
```
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat ./-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```
----
## **Level 5**
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:  
- human-readable
- 1033 bytes in size
- not executable

Commands you may need to solve this level:
```
ls, cd, cat, file, du, find
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

For this task, we need the find command. We can particularly set the ***-size*** parameter of **find** to only search for files that are 1033 Bytes (c for char, which is one byte) large. 

You have following size options:
- b – for 512-byte blocks (this is the default if no suffix is used)
- c – for bytes
- w – for two-byte words
- k – for Kilobytes (units of 1024 bytes)
- M – for Megabytes (units of 1048576 bytes)
- G – for Gigabytes (units of 1073741824 bytes)
```
bandit5@bandit:~/inhere$ find . -size 1033c
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

or directly execute cat in combination with find:

```
bandit5@bandit:~/inhere$ cat $(find . -size 1033c) 
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```
----
## **Level 6**
The password for the next level is stored somewhere on the server and has all of the following properties:  
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

Commands you may need to solve this level:
```
ls, cd, cat, file, du, find
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

Again, for this task we can specify the search parameters of the find command. This time we use ***-group***, ***-size*** and ***-user***. Futhermore, to get rid of all the "permission denied" outputs, we redirect the stderr (2) to /dev/null, so we dont have to search for our result within a huge text output.
```
bandit6@bandit:~$ find / -user bandit7 -size 33c -group bandit6 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```
----
## **Level 7**
The password for the next level is stored in the file data.txt next to the word millionth.

Commands you may need to solve this level:
```
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

We can use the command ***grep*** to filter only the lines of the text file that contain our searched word.
```
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ grep "millionth" data.txt 
millionth	cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```
----
## **Level 8**
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

Commands you may need to solve this level:
```
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit8@bandit.labs.overthewire.org -p 2220
```
***Uniq*** can determine unique lines from **sort**ed lists:
```
bandit8@bandit:~$ sort data.txt | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```
----
## **Level 9**
The password for the next level is stored in the file data.txt in one of the few human-readable strings, beginning with several ‘=’ characters.

Commands you may need to solve this level:
```
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit9@bandit.labs.overthewire.org -p 2220
```
***Strings*** can be used to filter only human-readable characters from the file.
```
bandit9@bandit:~$ strings data.txt | grep "="
2========== the
========== password
>t=	yP
rV~dHm=
========== isa
=FQ?P\U
=	F[
pb=x
J;m=
=)$=
========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
iv8!=
```
----
## **Level 10**
The password for the next level is stored in the file data.txt, which contains base64 encoded data

Commands you may need to solve this level:
```
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit10@bandit.labs.overthewire.org -p 2220
```
Here we can use the command ***base64*** with the decryption flag ***-d***.
```
bandit10@bandit:~$ ls
data.txt
bandit10@bandit:~$ cat data.txt 
VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==
bandit10@bandit:~$ cat data.txt | base64 -d
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```

----
## **Level 11**
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

Commands you may need to solve this level:
```
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit11@bandit.labs.overthewire.org -p 2220
```
The password has been encoded with the so called ROT13 algorithm. We can either use online tools like [this](https://cryptii.com/pipes/rot13-decoder) or decode it directly in the shell by using tr (translate).
```
bandit11@bandit:~$ ls
data.txt
bandit11@bandit:~$ cat data.txt 
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
bandit11@bandit:~$ cat data.txt | tr 'N-ZA-Mn-za-m' 'A-Za-z'
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```
----
## **Level 12**
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

Commands you may need to solve this level:
```
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit12@bandit.labs.overthewire.org -p 2220
```
This task is mostly about finding out what datatype is the current file has, as well as what tool was used to compress it.
```
bandit12@bandit:/tmp/babbadeckl$ cat data.txt | xxd -r > file
bandit12@bandit:/tmp/babbadeckl$ file file
file: gzip compressed data, was "data2.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix
```

Now we know, that the file was compressed by using the tool gzip. But before, we have to adjust the file suffix:

```
bandit12@bandit:/tmp/babbadeckl$ mv file file.gz
bandit12@bandit:/tmp/babbadeckl$ gunzip file.gz 
bandit12@bandit:/tmp/babbadeckl$ file file 
file: bzip2 compressed data, block size = 900k
```
The next layer is a bzip2 compressed file. Reading the manual of this command, it states that the files can be decompressed with the ***bzcat*** command. So let's go for it.
```
bandit12@bandit:/tmp/babbadeckl$ bzcat file > bzip2_file
bandit12@bandit:/tmp/babbadeckl$ ls
bzip2_file  data.txt  file
bandit12@bandit:/tmp/babbadeckl$ file bzip2_file 
bzip2_file: gzip compressed data, was "data4.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix
```
An other layer ... it's a gzip file again. So let's adjust the suffix and decompress it.

```
bandit12@bandit:/tmp/babbadeckl$ mv bzip2_file bzip2_file.gz
bandit12@bandit:/tmp/babbadeckl$ gunzip bzip2_file.gz 
bandit12@bandit:/tmp/babbadeckl$ ls
bzip2_file  data.txt  file
bandit12@bandit:/tmp/babbadeckl$ file bzip2_file 
bzip2_file: POSIX tar archive (GNU)
```

It wont stop.... This time it's a tar archive. We can use the ***tar*** command for it.

```
bandit12@bandit:/tmp/babbadeckl$ mv bzip2_file bzip2_file.tar
bandit12@bandit:/tmp/babbadeckl$ tar xvf bzip2_file.tar 
data5.bin
```

AAAARGH!

```
bandit12@bandit:/tmp/babbadeckl$ file data5.bin
data5.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/babbadeckl$ mv data5.bin data5.tar
bandit12@bandit:/tmp/babbadeckl$ tar xvf data5.tar 
data6.bin
bandit12@bandit:/tmp/babbadeckl$ ls
bzip2_file.tar  data5.tar  data6.bin  data.txt  file
bandit12@bandit:/tmp/babbadeckl$ file data6.bin 
data6.bin: bzip2 compressed data, block size = 900k
```

Cmon... it has to stop one day...

```
bandit12@bandit:/tmp/babbadeckl$ bzcat data6.bin > cmon
bandit12@bandit:/tmp/babbadeckl$ file cmon 
cmon: POSIX tar archive (GNU)
bandit12@bandit:/tmp/babbadeckl$ mv cmon cmon.tar
bandit12@bandit:/tmp/babbadeckl$ tar xvf cmon.tar 
data8.bin
```

uff...
```
bandit12@bandit:/tmp/babbadeckl$ mv data8.bin data8.gz
bandit12@bandit:/tmp/babbadeckl$ gunzip data8.gz 
bandit12@bandit:/tmp/babbadeckl$ ls
bzip2_file.tar  cmon.tar  data5.tar  data6.bin  data8  data.txt  file
bandit12@bandit:/tmp/babbadeckl$ file data8
data8: ASCII text
```
FINALLY!!!!!! YES!
```
bandit12@bandit:/tmp/babbadeckl$ cat data8
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```
----
## **Level 13**
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on.

Commands you may need to solve this level:
```
ssh, telnet, nc, openssl, s_client, nmap
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

This one's easy, as we can simply take the private key of bandit14 as our identity file.
```
ssh bandit14@localhost -i sshkey.private

bandit14@bandit:~$ whoami
bandit14
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```
----
## **Level 14**
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

Commands you may need to solve this level:
```
ssh, telnet, nc, openssl, s_client, nmap
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit14@bandit.labs.overthewire.org -p 2220
```

This sounds like a job for netcat (nc)
```
bandit14@bandit:~$ nc localhost 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```
----
## **Level 15**
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…

Commands you may need to solve this level:
```
ssh, telnet, nc, openssl, s_client, nmap
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit15@bandit.labs.overthewire.org -p 2220
```

For this challenge, we have to establish a secure connection (TLS) to localhost:30001. Therefore, we use the command ***openssl s_client*** as following:
```
bandit15@bandit:~$ openssl s_client -connect :30001
CONNECTED(00000003)
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
---
Certificate chain
 0 s:/CN=localhost
   i:/CN=localhost
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICBjCCAW+gAwIBAgIEYo1NxTANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjAwMTA1MTQzNTU4WhcNMjEwMTA0MTQzNTU4WjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAKF4u2eu
a8VipZPviX0hfNiCnaD2ojAffdBhKTy1bmZSNRuHPBDnU7z8rblNSknSjCITda1C
GEAI8ZktRbtLpBTbYeTgqPN/EiN5UIRMKbU6P2O93zNFPBsmyfQLrgt+DSLnsxlB
i/yYyT7WLdtNVBpgwRwkqi9K7dk9vf9waswLAgMBAAGjZTBjMBQGA1UdEQQNMAuC
CWxvY2FsaG9zdDBLBglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0
ZWQgYnkgTmNhdC4gU2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3
DQEBBQUAA4GBAJECW6IB3Ria4xG002BqD3zEbtmrDlK6nmJq+uQ4eJ6cT18o9REb
npy/lFzlv2LfcrYAnuAp6Fh89MKaYjNzJURjRQ9RkmcYgQJa1n+OBkATb7V+84/a
k9PDRkscxdNFMGBSvzFD33XZ5lbaGdrwCPyoxenoYghV/753wffN7J6H
-----END CERTIFICATE-----
subject=/CN=localhost
issuer=/CN=localhost
---
No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1019 bytes and written 269 bytes
Verification error: self signed certificate
---
New, TLSv1.2, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 1024 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: 8E0B02BDBB99FE6CA6B349B7E5EB20355DDD1075C46350F992C5DFCA9ACEAFB8
    Session-ID-ctx: 
    Master-Key: 60AF3589462E7DF60A8A190A51ABCA2F8F01D7DBBAE113BD4405C54920F006123580B3014A2F35C9C352D13762C3124A
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 56 e9 4e 87 6a 28 48 d0-13 42 5f b9 61 b0 dd d0   V.N.j(H..B_.a...
    0010 - 0f 54 18 f8 a1 70 b6 a4-e8 0a 03 64 9c 57 0e f2   .T...p.....d.W..
    0020 - e5 8f 78 e5 88 d3 a6 dd-0d 03 1c b5 d0 1a b9 4d   ..x............M
    0030 - 1f f0 20 ab 0d a9 ed bd-51 b8 d6 28 f3 dd 16 88   .. .....Q..(....
    0040 - cb 68 76 29 05 40 06 bf-15 ff 9b fd aa 82 30 db   .hv).@........0.
    0050 - 9b 8a c9 78 fd 89 fe 35-1d 8a bb d4 8e 67 1e 28   ...x...5.....g.(
    0060 - 98 5b 2f fc 2f cb 0d de-8d 3a 0e 2d 44 ee 53 ff   .[/./....:.-D.S.
    0070 - 7f 10 d4 29 a0 e3 7d 8e-18 49 9f a8 b1 93 30 ab   ...)..}..I....0.
    0080 - db d6 14 e0 04 37 72 16-08 e7 65 8e 18 e3 17 5a   .....7r...e....Z
    0090 - c9 76 04 89 21 c3 62 46-3a 84 12 5c 58 c7 81 43   .v..!.bF:..\X..C

    Start Time: 1582290335
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
BfMYroe26WYalil77FoDi9qh59eK5xNr   <- our input
Correct!                            
cluFn7wTiGryunymYOu4RcffSxQluehd   <- Password for Bandit16

closed
```
----
## **Level 16**
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

Commands you may need to solve this level:
```
ssh, telnet, nc, openssl, s_client, nmap
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit16@bandit.labs.overthewire.org -p 2220
```

As the task description says, that a port in the range between 31000 and 32000 is open, the first thing we do is to find this open port by using nmap.
```
bandit16@bandit:~$ nmap -p 31000-32000 127.0.0.1

Starting Nmap 7.40 ( https://nmap.org ) at 2020-02-21 14:14 CET
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00030s latency).
Not shown: 999 closed ports
PORT      STATE SERVICE
31518/tcp open  unknown
31790/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.09 seconds
```

Now we know, that there are indeed two ports open (31518 and 31790). So let's find out which one is the TLS one.

First one is port 31518:

```
bandit16@bandit:~$ openssl s_client -connect 127.0.0.1:31518
CONNECTED(00000003)
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
---
Certificate chain
 0 s:/CN=localhost
   i:/CN=localhost
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICBjCCAW+gAwIBAgIES250rzANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjAwMjA5MjA0NzIwWhcNMjEwMjA4MjA0NzIwWjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBANWyxh7K
T86zWM4NFe95x2KNEBUDz2XlGvU7KxUM9z1OfakmLDYCiujYdR6gI4ZBtyhEql5P
taCiNWO+ZDJCKWhjH/TyIywxjW9/PBHRC8UEzhsxc0wMHbLrlYFwzxT2KjhI3EVY
5VIWkzKrgHuON6PuBbmN0g0z5NN/xYch4kPpAgMBAAGjZTBjMBQGA1UdEQQNMAuC
CWxvY2FsaG9zdDBLBglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0
ZWQgYnkgTmNhdC4gU2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3
DQEBBQUAA4GBAFX4+KlTXWb4R/pUVt7i4FWvp3CuqgLUtgU3vRZqJ3wShIyDbsFK
a4S9uSuWcLLvyq0aa4kLhmoepyNlI3BGUSZZbRXwo/1e5IpCX3RdHhlIc3/Sd7ln
usTkejgEftWMmmBc03RY07EMxbNeXE8zzh2NP+5kVfwWG6GoGuQMXhy8
-----END CERTIFICATE-----
subject=/CN=localhost
issuer=/CN=localhost
---
No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1019 bytes and written 269 bytes
Verification error: self signed certificate
---
New, TLSv1.2, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 1024 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: 0AC27004299A2C4711FED5C6E12F04298E2E75A588C63E9AF9DC309C49178275
    Session-ID-ctx: 
    Master-Key: 075C7098E35877D1BE0BD6E993331481C1A7493350B55FE3E40DF0F4E13D24081948F1406034E4AF9B185D2E308600B9
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 26 1a 05 91 72 ce a3 a6-e5 fa 17 b1 24 c4 2b 6f   &...r.......$.+o
    0010 - 63 1c b2 1a 4e 64 48 d1-42 11 ad 40 57 f5 2f b2   c...NdH.B..@W./.
    0020 - 47 63 0a d4 7a f1 6e d8-ae 58 8b ce e9 08 a2 0e   Gc..z.n..X......
    0030 - c4 29 76 37 1a 48 08 ed-8e 41 f6 c3 64 54 0c 07   .)v7.H...A..dT..
    0040 - f6 2c ef 59 23 8e b5 fb-dc e7 7c 54 25 12 3c af   .,.Y#.....|T%.<.
    0050 - 35 c2 02 93 41 d1 5e eb-cf aa 29 75 54 9d 97 d8   5...A.^...)uT...
    0060 - f0 57 85 c7 7a 41 07 c7-56 15 2d f3 f1 74 c1 e0   .W..zA..V.-..t..
    0070 - b2 0c c4 d9 20 3d 68 c6-7d 5a 3f 99 4f 2b 98 fa   .... =h.}Z?.O+..
    0080 - 94 ac e0 2c 3f ae 4b 64-4b 7d 7b 4b 46 71 df a3   ...,?.KdK}{KFq..
    0090 - 33 eb 2b 60 cf a3 de 3d-9b c2 6f 82 1a b0 41 fc   3.+`...=..o...A.

    Start Time: 1582291050
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
cluFn7wTiGryunymYOu4RcffSxQluehd   <- our input
cluFn7wTiGryunymYOu4RcffSxQluehd   <- response
test    <- our input
test    <- response
```

So this port is not the correct one, as it simply echos whatever we send to it.
This means, the second port is our goal.

```
bandit16@bandit:~$ openssl s_client -connect 127.0.0.1:31790
CONNECTED(00000003)
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
---
Certificate chain
 0 s:/CN=localhost
   i:/CN=localhost
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICBjCCAW+gAwIBAgIEGPttrzANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjAwMjA5MjA0NzE5WhcNMjEwMjA4MjA0NzE5WjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAPiElqK1
D097ZCNDgKFxqX1ZUUpFfuoiDSP2dw5KrIruaTQMmfqCxo6dSHvkj1sF//YRI28k
BGyu9pE3zLO45uk4PrjoORYLoQjTCb61oVZLECCOIG21WQUbrhjW4zlZGmtWrqw6
zGLk7dZ8MeYHVSvK0n3Ar45hVedpsLC618ZTAgMBAAGjZTBjMBQGA1UdEQQNMAuC
CWxvY2FsaG9zdDBLBglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0
ZWQgYnkgTmNhdC4gU2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3
DQEBBQUAA4GBADJEAM0VceCYaqhfzpzkzf6dhCIWbb/8P+51Wxw24sn9iLHxdqYe
1WNfxtQb8IYb3q/6JJDJ3d6plNKmFMkFBe5AiN05PCDeMymkTv8vlKj18UNR/4GL
AH1aFGcEYVXkwX0Kl844muUrK7S0AbOvcHmzzA++qTmfB1UK264G0iAH
-----END CERTIFICATE-----
subject=/CN=localhost
issuer=/CN=localhost
---
No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1019 bytes and written 269 bytes
Verification error: self signed certificate
---
New, TLSv1.2, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 1024 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: 55F43E2344EF93880545097EC835D0BE45F7E59AFC64797AA8BB2E02B5333CC9
    Session-ID-ctx: 
    Master-Key: A78D965B4CFBD82E73785665BE869F45F09AA0E4F0B5880050690F6B5480ED182018BDC9FD0F7BC03D7B9203051E51B9
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 9f 82 12 97 ac 31 10 5b-65 4b 5d fb 71 e9 e8 02   .....1.[eK].q...
    0010 - 2e da b7 ba 71 0b 4e d0-57 10 8d ed a8 84 e0 d5   ....q.N.W.......
    0020 - 7f 67 88 3c f3 4a 9d cd-ab bf d3 33 a8 80 a3 9f   .g.<.J.....3....
    0030 - d5 27 8f cc 08 fd 84 4c-69 ae a0 46 e6 20 85 c3   .'.....Li..F. ..
    0040 - fd f0 b1 dd 0a d3 b9 b4-04 bf c8 c6 0b 93 4b 74   ..............Kt
    0050 - cd 8a 7b 1c 76 00 89 1f-f4 f8 f3 1c 3a a2 f0 2a   ..{.v.......:..*
    0060 - 6f 86 73 48 78 b1 c3 b2-fa 3a ad 14 6c bf 4b f5   o.sHx....:..l.K.
    0070 - 72 31 3b 4f c5 b9 be 51-b4 eb 4f bf 4a 11 ec 17   r1;O...Q..O.J...
    0080 - 98 b0 a7 21 fd 1a 20 64-70 1d 4a 82 17 9c a3 91   ...!.. dp.J.....
    0090 - 83 18 0a 0e bf eb 5d 32-7f 9d 70 d1 11 f4 45 3a   ......]2..p...E:

    Start Time: 1582291158
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
cluFn7wTiGryunymYOu4RcffSxQluehd
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

closed
```

Hm... no credentials for us. But hey, we got a private key. It's probably the one from Bandit17. So let's try to use it for an ssh connection.

```
bandit16@bandit:~$ echo "-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
" > /tmp/babbadeckl.key
```

Now we can use this private key file for the ssh connection.

```
ssh -i /tmp/babbadeckl.key bandit17@localhost
Could not create directory '/home/bandit16/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit16/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for '/tmp/babbadeckl.key' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "/tmp/babbadeckl.key": bad permissions
bandit17@localhost's password: 
```

This is a pretty common error for SSH connections when connecting with a key. But we can simply fix this issue by setting the permissions of the key file to 400.

```
bandit16@bandit:/tmp$ chmod 400 babbadeckl.key
bandit16@bandit:/tmp$ ssh -i babbadeckl.key bandit17@localhost

bandit17@bandit:~$ id
uid=11017(bandit17) gid=11017(bandit17) groups=11017(bandit17)

bandit17@bandit:~$ cat /etc/bandit_pass/bandit17
xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn
```

----
## **Level 17**
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

Commands you may need to solve this level:
```
cat, grep, ls, diff
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit17@bandit.labs.overthewire.org -p 2220
```

This one is super easy. Just look at the difference between both files using the ***diff*** command.

```
bandit17@bandit:~$ diff passwords.new passwords.old 
42c42
< kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd                <-- the new line
---
> hlbSBPAWJmL6WFDb06gpTx1pPButblOA                <-- the old line
```

So the password for bandit 18 is kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd

----
## **Level 18**
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

Commands you may need to solve this level:
```
ssh, ls, cat
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit18@bandit.labs.overthewire.org -p 2220
```

Let's connect to the server.
```
ssh bandit18@bandit.labs.overthewire.org -p 2220
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: 
Linux bandit 4.18.12 x86_64 GNU/Linux

Byebye !
Connection to bandit.labs.overthewire.org closed.
```

Ok, so we get directly disconnected without having the chance of executing any commands. 

"The SSH client program can be used for logging into a remote machine or server and for executing commands on a remote machine. When command is specified, it is executed on the remote host/server instead of a login shell."

As .bashrc is only loaded when we open a shell, we can circumvent this problem by using the feature of ssh as following:

```
babbadeckl@iAmRoot  ~  ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: 
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x  <-- password for Bandit19
```

----
## **Level 19**
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

Commands you may need to solve this level:
```
No commands were specified
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit19@bandit.labs.overthewire.org -p 2220
```

```
bandit19@bandit:~$ ./bandit20-do id
uid=11019(bandit19) gid=11019(bandit19) euid=11020(bandit20) groups=11019(bandit19)
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```
----
## **Level 20**
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think

Commands you may need to solve this level:
```
ssh, nc, cat, bash, screen, tmux, Unix ‘job control’ (bg, fg, jobs, &, CTRL-Z, …)
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit20@bandit.labs.overthewire.org -p 2220
```

This challenge seems to be pretty straight forward as well. The first step is to split the screen with the help of tmux. On the right side we start the listener on port 44444 as following:
```
echo "GbKksEFF4yrVs6il55v6gwY5aVje5f0j" | nc -l localhost -p 44444
```
On the left side, we then execute the suconnect and let it connect to port 44444.

```
bandit20@bandit:~$ ./suconnect 44444                                                      
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j                                                    
Password matches, sending next password 
```

On the right side, we then get the password for bandit 21: gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr

----
## **Level 21**
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

Commands you may need to solve this level:
```
cron, crontab, crontab(5) (use “man 5 crontab” to access this)
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit21@bandit.labs.overthewire.org -p 2220
```

```
bandit21@bandit:/etc/cron.d$ ls
atop  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24

bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null

bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

----
## **Level 22**
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

Commands you may need to solve this level:
```
cron, crontab, crontab(5) (use “man 5 crontab” to access this)
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit22@bandit.labs.overthewire.org -p 2220
```

```
bandit22@bandit:/etc/cron.d$ ls
atop  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
bandit22@bandit:/etc/cron.d$ /usr/bin/cronjob_bandit23.sh
Copying passwordfile /etc/bandit_pass/bandit22 to /tmp/8169b67bd894ddbb4412f91573b38db3
bandit22@bandit:/etc/cron.d$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
```

----
## **Level 23**
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

Commands you may need to solve this level:
```
cron, crontab, crontab(5) (use “man 5 crontab” to access this)
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit23@bandit.labs.overthewire.org -p 2220
```

```
bandit23@bandit:/etc/cron.d$ cat cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null

bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
	echo "Handling $i"
	timeout -s 9 60 ./$i
	rm -f ./$i
    fi
done
```

Every file in /var/spool/bandit24 gets executed once and then gets deleted. That's our chance of getting the password for this user. We simply have to write a script that writes the password from location /etc/bandit_pass/bandit24 into one of our files. Afterwards, we just copy that script into the /var/spool/bandit24 folder and wait till it gets executed by the cronjob.

```
bandit23@bandit:/tmp/babbadeckl$ cat script.sh 
#!/bin/bash

cat /etc/bandit_pass/bandit24 > /tmp/babbadeckl/password


bandit23@bandit:/tmp/babbadeckl$ touch password
bandit23@bandit:/tmp/babbadeckl$ chmod 777 password 


bandit23@bandit:/tmp/babbadeckl$ cp script.sh /var/spool/bandit24/


(wait 1 min)

bandit23@bandit:/tmp/babbadeckl$ cat password 
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```

----
## **Level 24**
A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.

Commands you may need to solve this level:
```
No commands were specified
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit24@bandit.labs.overthewire.org -p 2220
```

```bash
#!/bin/bash

password24=UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
for i in {0000..9999}; do
	echo "$password24 $i"
done | nc localhost 30002 | grep -v "Wrong" | grep -v "pincode"
```

```
bandit24@bandit:/tmp/babbadeckl25$ ./bruteforce.sh 
Correct!
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG
```

----
## **Level 25**
Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

Commands you may need to solve this level:
```
ssh, cat, more, vi, ls, id, pwd
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit25@bandit.labs.overthewire.org -p 2220
```

```
bandit25@bandit:~$ ls
bandit26.sshkey
bandit25@bandit:~$ ssh -i bandit26.sshkey bandit26@localhost

  _                     _ _ _   ___   __  
 | |                   | (_) | |__ \ / /  
 | |__   __ _ _ __   __| |_| |_   ) / /_  
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \ 
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/ 
Connection to localhost closed.
```
After trying to execute commands via ssh for a while I remembered that I've done something similar in an other CTF... So I looked up the shell of user bandit26 in the /etc/passwd file.
```
bandit25@bandit:~$ cat /etc/passwd | grep "bandit26"
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```

So instead of /bin/bash, user bandit26 uses something called /usr/bin/showtext... Let's see what it does:

```
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

more ~/text.txt
exit 0
```

There we have it! It's the same problem I had several weeks before during a CTF. When connecting to the SSH server, the ***more*** gets instantly executed. As the file that should be displayed is not large enough to actually prompt us for "more", we have to cheat a bit ... just resize your terminal as small as possible.

![small terminal](Pictures/bandit_23_02_13_38_15.png)

Now we can resize it to a larger size again. So let's take a look at the more manpage, to find out what we can do now.

```
              v         Start  up  an  editor  at current line.  The editor is taken from the environment variable VISUAL if defined, or EDITOR if VISUAL is not defined, or defaults to vi if neither VISUAL nor
                        EDITOR is defined.
```
The ***v*** key seems to be exactly what we need. Opens VIM by pressing the V key. 
And now we can simply open the password file for bandit26 within vim:

```
:e /etc/bandit_pass/bandit26
```
![](Pictures/bandit_23_02_13_41_51.png)

![](Pictures/bandit_23_02_13_42_03.png)

The password for bandit26 is 5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z

We can even spawn a shell from here by setting the shell to /bin/bash from within vim:

```
:set shell=/bin/bash
```
followed by:
```
:shell
```
![](Pictures/bandit_23_02_13_44_29.png)

----
## **Level 26**
Good job getting a shell! Now hurry and grab the password for bandit27!

Commands you may need to solve this level:
```
ls
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit26@bandit.labs.overthewire.org -p 2220
```

Now we really need the shell from the previous challenge. Aftewards, we can simply execute the program in the bandit26 directory to get the password for bandit27.
```
bandit26@bandit:~$ ./bandit27-do 
Run a command as another user.
  Example: ./bandit27-do id

bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27
3ba3118a22e93127a4ed485be72ef5ea
```

----
## **Level 27**
There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo. The password for the user bandit27-git is the same as for the user bandit27.

Clone the repository and find the password for the next level.

Commands you may need to solve this level:
```
git
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit27@bandit.labs.overthewire.org -p 2220
```
This level is pretty straight forwards, as we only have to clone the repo and see what's in there:
```
bandit27@bandit:~$ mkdir /tmp/babbadeckl27
bandit27@bandit:~$ cd /tmp/babbadeckl27
bandit27@bandit:/tmp/babbadeckl27$ git clone  ssh://bandit27-git@localhost/home/bandit27-git/repo
Cloning into 'repo'...
Could not create directory '/home/bandit27/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit27/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit27-git@localhost's password: 
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (3/3), done.

bandit27@bandit:/tmp/babbadeckl27$ ls
repo
bandit27@bandit:/tmp/babbadeckl27$ cd repo/

bandit27@bandit:/tmp/babbadeckl27/repo$ ls
README

bandit27@bandit:/tmp/babbadeckl27/repo$ cat 
.git/   README  

bandit27@bandit:/tmp/babbadeckl27/repo$ cat README 
The password to the next level is: 0ef186ac70e04ea33b4c1853d2526fa2

```

----
## **Level 28**
There is a git repository at ssh://bandit28-git@localhost/home/bandit28-git/repo. The password for the user bandit28-git is the same as for the user bandit28.

Clone the repository and find the password for the next level.

Commands you may need to solve this level:
```
git
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit28@bandit.labs.overthewire.org -p 2220
```

This challenge is pretty straight forward as well.
```
bandit28@bandit:~$ mkdir /tmp/babbadeckl28
bandit28@bandit:~$ cd /tmp/babbadeckl28

bandit28@bandit:/tmp/babbadeckl28$ git clone ssh://bandit28-git@localhost/home/bandit28-git/repo
Cloning into 'repo'...
Could not create directory '/home/bandit28/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit28/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit28-git@localhost's password: 
remote: Counting objects: 9, done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 9 (delta 2), reused 0 (delta 0)
Receiving objects: 100% (9/9), done.
Resolving deltas: 100% (2/2), done.

bandit28@bandit:/tmp/babbadeckl28$ ls
repo

bandit28@bandit:/tmp/babbadeckl28$ cd repo/

bandit28@bandit:/tmp/babbadeckl28/repo$ ls
README.md

bandit28@bandit:/tmp/babbadeckl28/repo$ cat README.md 
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```

Hm... nothing so see. But the hint says we only have to use git. So let's take a look at the logs.

```
bandit28@bandit:/tmp/babbadeckl28/repo$ git log
commit 073c27c130e6ee407e12faad1dd3848a110c4f95
Author: Morla Porla <morla@overthewire.org>
Date:   Tue Oct 16 14:00:39 2018 +0200

    fix info leak     <---- that's a big hint

commit 186a1038cc54d1358d42d468cdc8e3cc28a93fcb
Author: Morla Porla <morla@overthewire.org>
Date:   Tue Oct 16 14:00:39 2018 +0200

    add missing data

commit b67405defc6ef44210c53345fc953e6a21338cc7
Author: Ben Dover <noone@overthewire.org>
Date:   Tue Oct 16 14:00:39 2018 +0200

    initial commit of README.md

```
Now that we know that there has been a fix for "info leak", we just switch to an older state of the repo & see what the info leak was.
```
bandit28@bandit:/tmp/babbadeckl28/repo$ git reset --hard 186a1038cc54d1358d42d468cdc8e3cc28a93fcb
HEAD is now at 186a103 add missing data
bandit28@bandit:/tmp/babbadeckl28/repo$ ls
README.md
bandit28@bandit:/tmp/babbadeckl28/repo$ cat README.md 
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: bbc96594b4e001778eee9975372716b2
```

----
## **Level 29**
There is a git repository at ssh://bandit29-git@localhost/home/bandit29-git/repo. The password for the user bandit29-git is the same as for the user bandit29.

Clone the repository and find the password for the next level.

Commands you may need to solve this level:
```
git
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit29@bandit.labs.overthewire.org -p 2220
```

Let's clone the repository and see what's in there.

```
bandit29@bandit:/tmp/babbadeckl29$ git clone ssh://bandit29-git@localhost/home/bandit29-git/repo
Cloning into 'repo'...
Could not create directory '/home/bandit29/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit29/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit29-git@localhost's password: 
remote: Counting objects: 16, done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 16 (delta 2), reused 0 (delta 0)
Receiving objects: 100% (16/16), done.
Resolving deltas: 100% (2/2), done.

bandit29@bandit:/tmp/babbadeckl29/repo$ ls
README.md
bandit29@bandit:/tmp/babbadeckl29/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>     <-- big hint here
```

The hint says "no passwords in production". This means, there might be an other branch "development" that contains the password.

```
bandit29@bandit:/tmp/babbadeckl29/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
bandit29@bandit:/tmp/babbadeckl29/repo$ git checkout dev
Branch dev set up to track remote branch dev from origin.
Switched to a new branch 'dev'

bandit29@bandit:/tmp/babbadeckl29/repo$ ls
code  README.md
bandit29@bandit:/tmp/babbadeckl29/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: 5b90576bedb2cc04c86a9e924ce42faf
```

----
## **Level 30**
There is a git repository at ssh://bandit30-git@localhost/home/bandit30-git/repo. The password for the user bandit30-git is the same as for the user bandit30.

Clone the repository and find the password for the next level.

Commands you may need to solve this level:
```
git
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit30@bandit.labs.overthewire.org -p 2220
```

Let's clone the repository and see what's in there.

```
bandit30@bandit:/tmp/babbadeckl30/repo$ cat README.md 
just an epmty file... muahaha
```

Even after checking logs, branches etc, I was not able to find the password. Then I googled for further git features. I realized that "git tag" might be an other option.

```
bandit30@bandit:/tmp/babbadeckl30/repo$ git tag
secret
bandit30@bandit:/tmp/babbadeckl30/repo$ git show secret
47e603bb428404d265f59c42920d81e5
```

----
## **Level 31**
There is a git repository at ssh://bandit31-git@localhost/home/bandit31-git/repo. The password for the user bandit31-git is the same as for the user bandit31.

Clone the repository and find the password for the next level.

Commands you may need to solve this level:
```
git
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit31@bandit.labs.overthewire.org -p 2220
```

Let's clone the repository and see what's in there.

```
bandit31@bandit:/tmp/babbadeckl31/repo$ cat README.md 
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```

So let's do what it says. Create a file, commit & push it to master:

```
bandit31@bandit:/tmp/babbadeckl31/repo$ echo "May I come in?" > key.txt

bandit31@bandit:/tmp/babbadeckl31/repo$ git add key.txt -f

bandit31@bandit:/tmp/babbadeckl31/repo$ git commit -m "bandit 31 challenge"
[master 619f62a] bandit 31 challenge
 1 file changed, 1 insertion(+)
 create mode 100644 key.txt

bandit31@bandit:/tmp/babbadeckl31/repo$ git push
Could not create directory '/home/bandit31/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit31-git@localhost's password: 
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 325 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: ### Attempting to validate files... ####
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
remote: Well done! Here is the password for the next level:
remote: 56a9bf19c63d650ce78e6ec0354ee45e
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
To ssh://localhost/home/bandit31-git/repo
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'ssh://bandit31-git@localhost/home/bandit31-git/repo'
```

Password for the next level is: 56a9bf19c63d650ce78e6ec0354ee45e


----
## **FINAL CHALLENGE: Level 32**
After all this git stuff its time for another escape. Good luck!

Commands you may need to solve this level:
```
sh, man
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit32@bandit.labs.overthewire.org -p 2220
```

This challenge is rather easy if you are familiar with bash. 
When connecting to the server, you are greeted with "WELCOME TO THE UPPERCASE SHELL"..

```
WELCOME TO THE UPPERCASE SHELL
>> ls
sh: 1: LS: not found
>> id
sh: 1: ID: not found
>> cat
sh: 1: CAT: not found
```

Trying some commands but without success. However, we can simply call $0 to create a new shell, as "$0 expands to the name of the shell or shell script." [https://bash.cyberciti.biz/guide/$0]

```
>> $0
$ ls
uppershell
$ id
uid=11033(bandit33) gid=11032(bandit32) groups=11032(bandit32)
$ cat /etc/bandit_pass/bandit33
c9c3199ddf4121b10cf581a98d51caee
```

----
## **Level 33**
At this moment, level 34 does not exist yet.

Commands you may need to solve this level:
```
///
```

Connect to the server via ssh (password is the found password from the previous level):

```
ssh bandit33@bandit.labs.overthewire.org -p 2220
```

```
bandit33@bandit:~$ ls
README.txt
bandit33@bandit:~$ cat README.txt 
Congratulations on solving the last level of this game!

At this moment, there are no more levels to play in this game. However, we are constantly working
on new levels and will most likely expand this game with more levels soon.
Keep an eye out for an announcement on our usual communication channels!
In the meantime, you could play some of our other wargames.

If you have an idea for an awesome new level, please let us know!
```