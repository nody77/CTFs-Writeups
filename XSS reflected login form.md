# bWapp Cross Site Scripting Reflected (Login Form) WriteUp

When we open the challenge page, we first see two text boxes, one for the login and the other for the password, and their exist a login 
button and the page says "enter your superhero credentials"

![alt text](https://github.com/nody77/CTFs-Writeups/blob/90862b5fd2c1d01f50469deaea9964af020d0f44/Screenshot%202023-03-24%20221901.png)

So let's try entering our credentials that made us login to the bWapp.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/90862b5fd2c1d01f50469deaea9964af020d0f44/Screenshot%202023-03-24%20221943.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/90862b5fd2c1d01f50469deaea9964af020d0f44/Screenshot%202023-03-24%20221953.png)

It did not work!! 
So now we need to inject one of the text boxes with a SQL querey to get any data if possible.

```SQL
' OR 1=1;#
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/90862b5fd2c1d01f50469deaea9964af020d0f44/Screenshot%202023-03-24%20222017.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/90862b5fd2c1d01f50469deaea9964af020d0f44/Screenshot%202023-03-24%20222026.png)

Ohh! It leaked some data! 
So let's analyze it.
There is someone with the name Neo and his secret is "Oh Why Didn't I Took That BLACK Pill".
The only thing in my opinion that will be useful for us is the name of that person which is **Neo**.
So let's try to inject our script into the password box this time and write Neo in the login box.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/90862b5fd2c1d01f50469deaea9964af020d0f44/Screenshot%202023-03-24%20222311.png)

The code is 
```javascript
' 1=1; <script>alert("good job")</script>
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/90862b5fd2c1d01f50469deaea9964af020d0f44/Screenshot%202023-03-24%20222424.png)