# h1-212

OK here is my write up 


so first i start brute force and crawl directory to check if possible to get some files there

then i used virtual-host-discovery tool to get all virtual host there 

Found: www.acme.org (200)

Found: dev.acme.org (200)

Found: local (200)

Found: localhost (200)

Found: status.acme.org (200)

Found: status (200)

Found: staging.acme.org (200)

Found: staging (200)

Found: development (200)

Found: development.acme.org (200)

Found: uat (200)

Found: uat.acme.org (200)

Found: acme.org (200)

Found: beta (200)

Found: beta.acme.org (200)

Found: secure (200)

Found: secure.acme.org (200)

Found: mobile (200)

Found: mobile.acme.org (200)

Found: 127.0.0.1 (200)

Found: m.acme.org (200)

Found: m (200)

Found: admin (200)

Found: admin.acme.org (200)

Found: old (200)

Found: old.acme.org (200)

Found: v1.acme.org (200)

Found: v1 (200)

Found: v2.acme.org (200)

Found: v2 (200)

Found: v3.acme.org (200)

Found: v3 (200)

Found: alpha (200)

Found: alpha.acme.org (200)

so as description said : admin.acme.org this is the one :D 
(An engineer of acme.org launched a new server for a new admin panel)
```
root@ip-172-31-20-83:/home/ubuntu# curl -I http://admin.acme.org
HTTP/1.1 200 OK
Date: Sat, 18 Nov 2017 22:59:11 GMT
Server: Apache/2.4.18 (Ubuntu)
Set-Cookie: admin=no
Content-Type: text/html; charset=UTF-8
```
next i start get 406 

![image](https://user-images.githubusercontent.com/7364615/32996613-4079913c-cd85-11e7-8b8c-6ba8b8aa1192.png)

so i get some stackoverflow solution which ask to look for good content-type
```
https://stackoverflow.com/questions/14251851/what-is-406-not-acceptable-response-in-http
```

brute force all type possible get that application/json is the one :d

![image](https://user-images.githubusercontent.com/7364615/32996624-64af4498-cd85-11e7-8b15-b046b0d6b4de.png)


THEN START PLAY WITH JSON DATA 

![image](https://user-images.githubusercontent.com/7364615/32996628-6e864b56-cd85-11e7-9749-30779d47e516.png)

Until fix that output 


And after send domain 
![image](https://user-images.githubusercontent.com/7364615/32996636-7dab1698-cd85-11e7-8a26-a8c27b0cfab0.png)

so when domain is valid we get data base64

![image](https://user-images.githubusercontent.com/7364615/32996640-8aa5e800-cd85-11e7-80e4-04356e646d68.png)

which is the source code of that website

:D its look ssrf here guys :D


lets bypass .com and 212 containe

after read alot from here (thx orange ) and other article 
https://www.blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf 

i notice i can use "feed line" to make 2 request or more !!

```
{"domain":"localhost/flag\n212.test.com"} 
{"domain":"localhost/server-status\n212.test.com"} 
```

with this data it will increment id+2

id+1 for localhost and id+2 for 212.test.com


So just get request of the id+1 get make us read the flag 

then base64 flag data and pwn it :D


Amazing ctf :D
