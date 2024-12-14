# PatriotCTF 2024

### <u>Category:</u> 	*Forensics*

### <u>Difficulty:</u>	Medium

<img src="./ctf_img/ctfsubject.png" style="width:300px; height:400px;" />

### We are given an AD1 image and an eml email to investigate and several questions to answer.
```txt
tmqrx@TMQ:~$ nc 154.26.136.227 62055



 ___       __   ________  ________   ________   ________  ___       __     _____  ________
|\  \     |\  \|\   __  \|\   ___  \|\   ___  \|\   __  \|\  \     |\  \  / __  \|\   ___  \
\ \  \    \ \  \ \  \|\  \ \  \  \  \ \  \  \  \ \  \|\  \ \  \    \ \  \|\/_|\  \ \  \  \  \
 \ \  \  __\ \  \ \   __  \ \  \  \  \ \  \  \  \ \   __  \ \  \  __\ \  \|/ \ \  \ \  \  \  \
  \ \  \|\__\_\  \ \  \ \  \ \  \  \  \ \  \  \  \ \  \ \  \ \  \|\__\_\  \   \ \  \ \  \  \  \
   \ \____________\ \__\ \__\ \__\  \__\ \__\  \__\ \__\ \__\ \____________\   \ \__\ \__\  \__\
    \|____________|\|__|\|__|\|__|\ |__|\|__| \|__|\|__|\|__|\|____________|    \|__|\|__| \|__|



    Complete 9/9 questions to get the flag.


[1]. What is the URL used in the phishing email that contains the malware?
Format: http://example.com/
==> https://drive.google.com/file/d/1tmOG4Lg-Li9HSsZl4_r0-RTEWDBQqd6H/view
CORRECT!✅
[2]. When was the malware finished downloading by the victim? (UTC)
Format: YYYY-MM-DD HH:MM:SS
==> 2024-12-12 17:08:37
CORRECT!✅
[3]. When was the malware first executed by the victim? (UTC)
Format: YYYY-MM-DD HH:MM:SS
==> 2024-12-12 17:08:44
CORRECT!✅
[4]. The first file acted as a dropper for the final malware. What is the MD5 hash of the dropped file?
==> 8eaa25eb8b77ac0157e1f3a04ad47e93
CORRECT!✅
[5]. What is the token used by the malware to access the private repository and the name of the private repository?
Format: token:username/repo. Example: 123456abcdef:user1337/repo1337
==> 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:velbail/contimtanvo
CORRECT!✅
[6]. What is the email address of the culprit?
Format: email@domain
==> belvail@proton.me
CORRECT!✅
[7]. How many extensions did the malware try to encrypt?
Format: number. Example 1: 04. Example 2: 12
==> 52
CORRECT!✅
[8]. The malware tried to delete itself using a batch file. What is the MD5 hash of the batch file?
==> e0d005db63a75fbcd6c8fa85040095aa
CORRECT!✅
[9]. Recover the content of 'password.xlsx' file. What is the username and password of the fifth record?
Format: username:password
==> user38:hch89as9821y3
CORRECT!✅
Congrats! Here is your flag: W1{https://www.youtube.com/shorts/lQrTMX1YaPE_b98800dfbe7853eba944677bc3d29548}
```
## Question 1: What is the URL used in the phishing email that contains the malware ?

#### we have a email message in this message has a zip file attached
#### this is the link : ```https://drive.google.com/file/d/1tmOG4Lg-Li9HSsZl4_r0-RTEWDBQqd6H/view```

### Question 2: When was the malware finished downloading by the victim? (UTC)

#### To know when the malware was downloaded, we can check the download history in the browser.
<img src="./ctf_img/History_file.png" style="width:500px; height:150px;" />

#### We can get it at Appdata/Local/Microsoft/Edge/Default/History and use sqlite viewer to check.
<img src="./ctf_img/end_time.png" style="width:950px; height:150px;" />

#### We can see the end time is the time when the malware was successfully downloaded, it is in the form of Chromium timestamp. So we need to calculate it based on epoch time. After calculating, the exact timestamp is ```2024-12-12 17:08:37```

### Question 3: When was the malware first executed by the victim? (UTC)
#### Using PECmd, we can see that the first time this malicious file was executed was ```2024-12-12 17:08:44```
