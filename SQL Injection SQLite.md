# bWAPP SQL Injection (SQLite) WriteUp

When we first open the challenge page, we see that there is one text box for searching and there is also
an empty table for the movies and there is a small text written beside the text box saying that it requires PHP SQLite Module.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/bed65c42faadef83574f3f958a8b4ff8a212ae9f/Screenshot%202023-03-29%20202533.png)

So let's try first see what that web page do.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/bed65c42faadef83574f3f958a8b4ff8a212ae9f/Screenshot%202023-03-29%20202544.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/bed65c42faadef83574f3f958a8b4ff8a212ae9f/Screenshot%202023-03-29%20202551.png)

So when we press the search button, we see that the data for the searched movie returned in the table.
Now let's start our SQL injection, first we need to know the number of columns of the table we can access which is the table of movies.
But that time we nedd first to search for the syntex for PHP SQLite to do our attack.

After doing some researching for the syntex, I found out that the `order by` function is the same.

```MYSQL
iron' order by 1-- -
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/bed65c42faadef83574f3f958a8b4ff8a212ae9f/Screenshot%202023-03-29%20202855.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/bed65c42faadef83574f3f958a8b4ff8a212ae9f/Screenshot%202023-03-29%20202904.png)

Now we need to increase the number of the column until it gives us an error.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/bed65c42faadef83574f3f958a8b4ff8a212ae9f/Screenshot%202023-03-29%20203152.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/bed65c42faadef83574f3f958a8b4ff8a212ae9f/Screenshot%202023-03-29%20203157.png)

So now the query gave us an error at column number 7 which appears that it does not exist, therefore the table which we exploit the data from 
contains 6 columns.
So Let's try to know the version of the SQLite that is being used.

```SQLite
k' UNION SELECT 1,sqlite_version(),3,4,5,6,7-- -
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/bed65c42faadef83574f3f958a8b4ff8a212ae9f/Screenshot%202023-03-29%20203657.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/bed65c42faadef83574f3f958a8b4ff8a212ae9f/Screenshot%202023-03-29%20203702.png)