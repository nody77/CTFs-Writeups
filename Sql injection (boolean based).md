# bWapp SQL Injection - Blind - Boolean Based WriteUp

When we open the challenge page, we find that their is one text box for searching and a search button.
>We know that SQL Injections is a type of web application security vulnerability that allows an attacker to inject
malicious SQL code into a web application's input field or other user inputs.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/58010d73573d815605068e02833c3213b2dde27a/Screenshot%202023-03-23%20120138.png)

So we will try to inject our code in the search text box.
First we will search for a normal movie to see what is the functionality of the website.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/58010d73573d815605068e02833c3213b2dde27a/Screenshot%202023-03-23%20120150.png)

When we press the search button, we find that the movie is in their database so let's try another movie name to see if it exists or not.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/58010d73573d815605068e02833c3213b2dde27a/Screenshot%202023-03-23%20120201.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/58010d73573d815605068e02833c3213b2dde27a/Screenshot%202023-03-23%20120230.png)

When we press the search button, we find that the movie is not in their database.
Now we can try inject our SQL code.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/58010d73573d815605068e02833c3213b2dde27a/Screenshot%202023-03-23%20120240.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/58010d73573d815605068e02833c3213b2dde27a/Screenshot%202023-03-23%20120543.png)

The code is 

```SQL
fast' or 1=1;#
```

>The explanation of the code is that we know that the fast movie is not in the database of the website so we wrote it and close the selection query
and then oring the select code with the equation `1=1` which is always true and then end the selection code with a semicolon and put the `#` sign to 
comment the rest of request.

When we press the search button we see that the code worked,so we figure out that we can retrive data from it by inject a SQL code in the text box.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/58010d73573d815605068e02833c3213b2dde27a/Screenshot%202023-03-23%20120552.png)