# bWAPP SQL Injection (Post/Select) WriteUp

When we first open the challenge web page, we see that there is a combo box for selecting a movie and there is also
an empty table for the movies.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20194627.png)

Let's try to select a movie and see what will happen.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20194642.png)

So Let's try another movie and open burpsuite to intercept the request and inject our query.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20194656.png)

Let's change the value of the movie in the last line to see how many columns we have in the displayed table, we will use `order by` function to know it

```MYSQL
0 order by 1 #
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20201153.png)

Then forward the request.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20201202.png)

We will repeat this code until it gives us an error.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20201222.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20201234.png)

So now the querey gave us an error at column number 8 which appears that it does not exist, therefore the table which we exploit the data from 
contains 7 columns.And wait we see that not all columns appear in the web page so let's try to configure out which column is on screen and which is not.

```MYSQL
0 union select 1,2,3,4,5,6,7 #
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20201300.png)

And forward the request.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20201307.png)

Now we can inject some SQL quereies to get the user from the database or the name of the database itself.
First,Let's begin to find the user of the database.

```MYSQL
0 union select 1,user(),3,4,5,6,7 #
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20201445.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20201453.png)

Second,Let's try finding the name of the database used.

```MYSQL
0 union select 1,2,3,database(),5,6,7 #
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20201530.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/9139cc74b4d085c8590da161451fb65d48a5f3ce/Screenshot%202023-03-29%20201538.png)
