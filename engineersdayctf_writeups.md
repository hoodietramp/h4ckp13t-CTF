
# Sanity Check

**There's a flag hidden in 345y Discord Server.**

**Join the server - [345y Server](https://discord.h00dy.me/)**

**[https://discord.h00dy.me](https://discord.h00dy.me/)**
##### solution 
Head over to rules channel, in the title there's the flag 
![[Pasted image 20240912195745.png]]

**flag{W3lc0m3_t0_h4ckp13T_CTF}**

---
# RECON

**There is a flag hidden on this website!**

##### solution

As per the challenge title we gonna do some Recon here 
- so lets look in the source code of this website pressing `Ctrl+U` so get to the home page of site with is  https://ctf.h00dy.me
- upon looking into source code we found 2 png images which were not reflecting on the page . interesting right ? because there display was none in css

![[Pasted image 20240912195940.png]]

lets see what's in there 

  damn you found it !!!
  merge them 
  **flag{j1ngl3_b3ll_j1ngl3_all_th3_w4y}**
  
---
# Extension

**it may not be what it looks like**
(and a rar file is given)
##### solution

So a rar file is given and we can see the challenge name is extension then it must be related to the file extension

let's move to the terminal, and check filetype using `file` command

![[Pasted image 20240912200132.png]]

We can see it's a png image, let's change the extension and open it again.

`mv hidden_melody.rar hidden_melody.png`

![[Pasted image 20240912200224.png]]
**flag{n07_ev3ryth1ng_1s_Wh47_1t_s33ms}**

---
# Locksmith

**Jane you forgot your pattern again, can you help her out?
Flag format - flag{pattern}**
("gesture.key" file is given)
##### solution

we have a gesture.key file, a normal google search for gesture key file would tell you it's related to android pattern lock config file. After that we can just search gesture key file decoder and grab any tool from github to give us the pattern.

we can also use one of the tool called androidpatterndecoder - https://github.com/bolisettynihith/android-pattern-decoder.git there is no rocket science in it, all you need is to google it

clone the github repo and lets decode the gesture.key

here i am using this repo https://github.com/sch3m4/androidpatternlock.git you can get it by just googling a bit 
command to clone : `git clone https://github.com/sch3m4/androidpatternlock.git`

now lets decode it
you will see aplc.py is there which is the tool
to run this tool we will use this command 
`python2 aplc.py gesture.key

![[Pasted image 20240912202013.png]]

so the flag would be 
**flag{214307856}**

---
# PWN 1

**Hah! you really are brave. Analyze the attached binary source code and see if you can overflow the buffer and get the flag?

> Connect to the challenge using the netcat command below

`nc 143.110.182.106 1024`
##### Solution 

upon reading the code we can say its a buffer overflow 
Here’s a breakdown :

- The `color` array is declared with a size of 30 characters.
- The `gets()` function reads input into `color` without bounds checking, making it possible to input more than 30 characters and overwrite the adjacent memory, including the `name` variable.
- If an attacker manages to overwrite `name` to be non-zero, the condition `if (name != 0)` becomes true, and the `system("cat /home/ctf/flag.txt")` command will be executed, revealing the flag.

now lets exploit it, first let's review the source code -
![[Pasted image 20240912202222.png]]

here the color array has size of 30. if we input data more that takes more than 30 space in memory it'll result in segmentation fault, consult your C teacher (:

lets connect with the netcat with given command  and get the flag

`nc 143.110.182.106 1024`

it is asking for an input here's the hacker's part kicks in 
lets spam the input field with 'A' which will lead to buffer overflow 

![[Pasted image 20240912202410.png]]

seeee we got the flag 

**flag{b0f_m4st3r}

---
# Base Is Strong

**Base Knowledge should be strong, to get ahead and get the flag

> Get the flag?

#### NNXTIUSMJBKGCMCHON3FKY2LMR4TM5RX

##### solution

First we will identify the format of the encoded text
for the we will use a website called https://www.dcode.fr/cipher-identifier
![[Pasted image 20240912202609.png]]

upon checking we found it is **BASE32** encoding

there are many ways to decode the encryption either you can use any online decoder or terminal with command 
`echo "NNXTIUSMJBKGCMCHON3FKY2LMR4TM5RX" | base32 -d`

or we can get it using cyberchef 
![[Pasted image 20240912202653.png]]
after decoding we got 
**ko4RLHTa0GsvUcKdy6v7**
looks like its another encoding now we will again repeat the process 
upon checking it identifies as base62
![[Pasted image 20240912202720.png]]
again we will decode it with the same process 
also you can use the same website to decode it or you can use cyberchef also 
![[Pasted image 20240912202738.png]]
**flag{b4s3_armY}**

---
# Geronimo

**Remember, when you last time fall on your head and felt like you jump off a roof, feeling geronimo? get the flag hidden inside different encodings**
 (geronimo.txt file is given)
##### solution
upon checking the file we found 
```
++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>>+++++++++++++++.++++++.-----------.++++++.<<+++++++.>---------------.++++++++++++++++++++++++.>---.<<++++++++++++++.>>-.<<---.>>+.<<+++.>>------------.------.+++++++++++++++.<<++++.>>---------------.<<------.++++++.>>+++++++.-------.++++++++++++++++.<<----.>>---------.+.<<--------------.++++++++++++++++++.>++```
```

 looks like an encoding 
 
 again we gonna use https://www.dcode.fr/cipher-identifier for the cipher identification 

![[Pasted image 20240912202915.png]]
and we got to know that its a BrainFuck 
lmao thats what the real name of this cipher 

lets use the same website to decode it https://www.dcode.fr/brainfuck-language
you will find this like within the website 
also upon identification you can use any website or tool to decode it
![[Pasted image 20240912202943.png]]
we got 
**synt%7Oq3p0q3e_n7_17f_o3fg%7Q**
again another encoding you know the drill now lets identify this one 
![[Pasted image 20240912203016.png]]
its a shift cipher basically rot13 and url encoded the curly brackets, alphabets are shifted in respective to their 13th alphabet and we found after decoding it from cyberchef -

![[Pasted image 20240912203111.png]]

**flag%7Bd3c0d3r_a7_17s_b3st%7D**
again this does't look like actual flag format but we can read the content but its not in proper format also we can see that it contains %7B and %7D which are actually url encoded 
lets decode it with cyberchef https://cyberchef.org
lets bring URL Decode in recipe 
and we got the flag !!!!!!

**flag{d3c0d3r_a7_17s_b3st}**

---
#  Key Is Clear

**It's simple or clear??? Take a guess, but it still remains clear**

> Get the flag ?

**xtmv{g1k3f3z3_o1es3v_ut34d3s}

##### Solution

lets identify  the cipher from the site https://www.dcode.fr/cipher-identifier
and we found its Vigenere Cipher 

![[Pasted image 20240912203200.png]]

lets decode it but we need a key for decoding the vigenere cipher
lets try CLEAR as key cause why not but we didn't found the flag 
lets try SIMPLE this time
yeah i know it worked 
![[Pasted image 20240912203222.png]]
**flag{v1g3n3r3_c1ph3r_cl34r3d}**

---
#  Naked Eye

**The beauty we see with our naked eyes has always amazed me
(penguin.png is given)

##### Solution 

So we are greeted with a penguin image which is in .png format
 so lets see the metadata of the image we can get the matadata by using exiftool 
 command : `exiftool penguin.png`


there you go there is a binary data in the image lets see the data 
lets check the stings of the image
command : `strings penguin.png`
damn there is something odd in the end of the strings 
can you identify it? 
![[Pasted image 20240912204121.png]]

you can open the png file in notepad and at the last you will see this long string of numbers and alphabets, it's basically hex encoded string. we can use cyberchef to decode the same.
`666c61677b76317331626c335f737472316e67737d0a`
looks like some kind of encoding lets check it on https://www.dcode.fr/cipher-identifier

![[Pasted image 20240912204218.png]]

its HEX/2 ASCII encoding lets decode it from same site or any as per your choice
and we have the flag
**flag{v1s1bl3_str1ngs}**

---
# JPG Got txt

**Do you know how real world brute force attack vectors came in handy, when they have all the needed info on their public facing website. can you get the flag hidden and protected inside this jpg image.**

**Password Format - <3 capital alphabets>iot<4 numbers> (e.g. - ABCiot1234)**

**rockyou aint r0cking here!**

##### Solution

- lets start with exiftool cause its a good practice to check the metadata well we found nothing interesting 
- lets check the file details by using file command : `file mrrobot.jpg` and we got to know that its a JPEG file 
- so we gonna use steg tool for this one (steg tools is having many stenography related tools  ) so we gonna use stegseek for it 

You can use chatgpt with the challenge description and it will guide you through the challenge (:

   command: `stegseek mrrobot.jpg wordlist.txt`
   
yes we will make our own cause we have the password  format which is 
Password Format - <3 capital alphabets>iot<4 numbers>

so lets make a wordlist using crunch 
command:  `crunch 10 10 -t ,,,iot%%%% -o word.txt`
(using 3 commas for 3 capital letters and 4 % for 4 numbers and iot is wil be in middle as described in the ctf challenge description) 

now lets run the stegseek with this wordlist

![[Pasted image 20240912204931.png]]

command: `stegseek mrrobot.jpg word.txt`

there you go it extracted the file outta it check the file type with the file command its an ASCII text
just cat it 

![[Pasted image 20240912204948.png]]
**flag{iM4g3_s73Gan0gR4pY_y4Y}**

---
# OSINT 1

**locate the city and that is your flag

> Flag format - flag{city}

##### Solution 
Image is given just search it  on google 

looks like we found it
visit that site and we got to know its in mysuru (mysore)

![[Pasted image 20240912205551.png]]

![[Pasted image 20240912205606.png]]
just submit it 
 **flag{mysore}**

---
# Osint 2

**The story goes back to the creation of h4ckp13t. Find the flag posted in one of the social profile of the original creator of h4ckp13t

> flag format is flag{this_is_a_test_flag}

##### Solution

upon checking Instagram page of h4ckp13t we got to know about it was created by H00dy
so now we will search flag in h00dy's social media 
![[Pasted image 20240912205848.png]]

we searched h00dy on google where i found his website where he mentioned his all social's 
lets check one by one but we found flag in his reddit account 

![[Pasted image 20240912205908.png]]

![[Pasted image 20240912205924.png]]
**flag{5e8a5709f662f8d401f7a00e6137f9ca}**

****
# Bionic

**Internet Bots Always Remember To Check Me... Do you remember???**

##### Solution 

Hmmm.... interesting question as you can notice it is taking about bots more like Robots
well if you do directory search you will find robots.txt in most of the sites
lets check that directory. You can just use chatgpt it'll give you the filename -
https://ctf.h00dy.me/robots.txt

![[Pasted image 20240912210034.png]]

there you go 

**flag{y0u_k33p_g01ng!}**

****
# Injectable

**I heard you don't like login pages, me neither...**

> Click on the link below to access the challenge

[http://143.110.182.106:8080](http://143.110.182.106:8080/)

##### Solution 

Aah!!! login page 
well lets try injecting sqli payloads in login form

i am using `admin' --` here in username 
and will type random stuff in password because 
`--` commented out the next statement in the code 
so code will ignore password and it will only read the username in this case username is admin so it code will  consider admin as true and will not read next line no code will not get any false error and it will let us to get in
![[Pasted image 20240912210107.png]]

![[Pasted image 20240912210117.png]]
aaaannnndddd we are in

**flag{SQLi_ftw}**

-----
# Osint 3

We can find the mac address of wifi on sn1ff's twitter

![[Pasted image 20240912211012.png]]

we can use https://wigle.net to get the wifi's ssid (name of the wifi) by registering an account, and going to view and basic search

![[Pasted image 20240912210635.png]]

----
# Txt got Flag

We got a zip file, that contains a packet capture file `capture.pcapng` we can use a tool called wireshark to view the network traffic captured in that pcapng.

We can search for http requests and find a request to flag.txt
![[Pasted image 20240912211809.png]]
![[Pasted image 20240912211838.png]]

We can right click and follow http stream to view the flag

![[Pasted image 20240912211905.png]]

---
# Dial up Era

In this challenge we got an `audio.wav` file which are basically dtmf tones the sounds which old phones made when pressing any number on the keypad.

We can search for dtmf tones decoder online and can use the first tool -

![[Pasted image 20240912212327.png]]

![[Pasted image 20240912212519.png]]

SO, this is the flag - flag{0123456789}

---
# E-commerce

Here we got an e-commerce website, where we can add products to the cart

![[Pasted image 20240912212720.png]]

![[Pasted image 20240912212732.png]]

It'll show up in the Cart, but there's also a donation page where we can enter negative amount because there is no input sanitization

![[Pasted image 20240912212842.png]]

It just shows us a warning that amount must be greater than zero, but if we head over to the cart page, the amount is updated

![[Pasted image 20240912212911.png]]

There we go we can checkout with ruppee 0, and can get the flag

![[Pasted image 20240912212931.png]]

---
# Cake Shop

Here we got a website where we can buy cakes, but we have zero money, here cookie comes in play, if we go to inspect and check cookies of the website we found a cookie called - `userinfo` which is being used to track the amount of money we have, and it's looking like its base64 encoded.

![[Pasted image 20240912213122.png]]

![[Pasted image 20240912213147.png]]

We can go over to Cyber Chef to decode the cookie -

![[Pasted image 20240912213219.png]]

`%3d%3d` were just url encoded characters, we can remove them, so we can see a zero, let's try encoding 100 in base64 and change the cookie value to that and refresh the page.

![[Pasted image 20240912213323.png]]

![[Pasted image 20240912213409.png]]

You can see we still have 0 rupees, Let's hit refresh

![[Pasted image 20240912213442.png]]

Now, we can buy any cake we want and get the flag (:

![[Pasted image 20240912213513.png]]

> These were all the CTF Challenges guys. Thank you again for playing <3

Much love 
h00dy