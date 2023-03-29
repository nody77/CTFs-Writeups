# bWAPP SQL Injection (CAPTCHA) WriteUp

When we first open the challenge page ,we see a text box to enter the CAPTCHA to enter the challenge page.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20201645.png)

Then when we get inside, we see that there is one text box for searching and there is also an empty table for the movies.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20201802.png)

So let's try first see what that web page do.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20202138.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20202144.png)

So when we press the search button, we see that the data for the searched movie returned in the table.
Now let's start our SQL injection, first we need to know the number of columns of the table we can access which is the table of movies.

We can identify by using order by technique and check if there is an error come out. 
`Order by 1` is SQL query that allow you to sort the table based on the column number 1.

```MYSQl
iron' order by 1-- -
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20202156.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20202201.png)

Now we need to increase the number of the column until it gives us an error.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20202217.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20202223.png)

So now the querey gave us an error at column number 8 which appears that it does not exist, therefore the table which we exploit the data from 
contains 7 columns.And wait we see that not all columns appear in the web page so let's try to configure out which column is on screen and which is not.
by using the following code:

```MYSQL
iron' union select 1,2,3,4,5,6,7-- -
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20202246.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20202252.png)

Now we can inject some SQL quereies to get the user from the database or the name of the database itself.
First,Let's begin to find the user of the database.

The code is 
```MYSQL
iron' union select 1,user(),3,4,5,6,7-- -
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20202305.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20202309.png)

Second,Let's try finding the name of the database used.

The code is
```MYSQL
iron' union select 1,2,database(),4,5,6,7-- -
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20202318.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/cebf7285fb3e30c5c61588750238d455c006f75a/Screenshot%202023-03-29%20202323.png)