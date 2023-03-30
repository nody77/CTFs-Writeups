# bWAPP Cross Site Scripting Stored (SQLiteManager) WriteUp

When we first open the challenge page we find that there is a sentence written it says that the SQLiteManager version is vulnerable to Cross Site Scrippting
and It gave us a hint which is CVE-2012-5105

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff8806afae91eaf4015ba2738a358a6280caa03f/Screenshot%202023-03-29%20193132.png)

I first started searching for that hint but I didn't find any thing useful except that there is someone said that it is a link but it might not work and wrote another 
website to visit instead of it.

So I tried to open the link in the challenge page but as he said it didn't work so I used the website he provided.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff8806afae91eaf4015ba2738a358a6280caa03f/Screenshot%202023-03-29%20193138.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff8806afae91eaf4015ba2738a358a6280caa03f/Screenshot%202023-03-29%20193147.png)

As it is written here is in the website that SQLiteManager is vulnerable to  multiple XSS vulnerabilities because it fails to properly sanitize user_supplied input.
And it gave us a payload to use so let's try to understand the payload first before inserting it.

```javascript
dbsel=&#039;"<script>alert(document.cookie)</script>
```

So here it says that we will insert the above code in `www.example.com/sqlite/main.php?` so let try to reach that address to insert the payload.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff8806afae91eaf4015ba2738a358a6280caa03f/Screenshot%202023-03-29%20193202.png)

First to reach the `www.example.com/sqlite` we press the bolded SQLiteManager word in the challenge page

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff8806afae91eaf4015ba2738a358a6280caa03f/Screenshot%202023-03-29%20193214.png)

Then open the source code of this webpage 

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff8806afae91eaf4015ba2738a358a6280caa03f/Screenshot%202023-03-29%20193305.png)

We find that there is a frame for `main.php` ,so let's click on it.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff8806afae91eaf4015ba2738a358a6280caa03f/Screenshot%202023-03-29%20193313.png)

After that we find ourselves in another view source page so let's remove this word form the url to access the webpage

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff8806afae91eaf4015ba2738a358a6280caa03f/Screenshot%202023-03-29%20193328.png)

After that we can inject our payload in the name textbox .

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff8806afae91eaf4015ba2738a358a6280caa03f/Screenshot%202023-03-29%20193506.png)

Then click save.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/bdca32c37107186206dd43591eab7729ca1c6ed0/Screenshot%202023-03-29%20193516.png)
