
### Description
Try to be admin if you can


### Writeup


in this challenge we are not provided with the source code
when visiting the / route we got a login panel. entering `admin` as a username will return username too short 
![Alt text](image1.png?raw=true "Title")

so trying a longer username will redirect us to `/flag`

![Alt text](image2.png?raw=true "Title")

by checking the devtools we will see a token cookie that looks like a jwt

![Alt text](image3.png?raw=true "Title")

and indeed its a jwt token 
![Alt text](image4.png?raw=true "Title")
(image from http://jwt.io)

we see that the signing algorithm is HS256, so we can try to bruteforce it using `jhon the ripper`

* save the jwt token to a file `jwt.txt` : `echo "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6ImFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhIiwicGFzc3dvcmQiOiJhYWFhIiwiZXhwIjoxNzA5MDM0NDY0fQ.JlUNcUs1cTtxN-224Sm8wUk8N31eJCFxyET0msgf0wg" > jwt.txt`
* run john with format as HMAC-SHA256 and with the `rockyou.txt`  (use your own rockyou path) wordlist: `john --format=HMAC-SHA256 --wordlist=/usr/opt/SecLists/Passwords/Leaked-Databases/rockyou.txt jwt.txt`
![Alt text](image5.png?raw=true "Title")
* this HS256 secret is `wiwikiki`
* now visit http://jwt.io and modify the `username` to `admin` and use `wiwikiki` as a secret then take the generated token and put it in the cookies in devtools
* now visit `/flag` and take the flag

#### The flag
`DEFENSYS{ins3cUr3__s3cr3t5_4r3_Dangerous_31338}`
