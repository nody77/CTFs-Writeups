# bWapp SQL Injection (Get/Search) WriteUp

When we first open the challenge web page, we see that there is one text box for searching and there is also
an empty table for the movies.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20225454.png)

So let's try first see what that web page do.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20225517.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20225522.png)

So when we press the search button, we see that the data for the searched movie returned in the table.
Now let's start our SQL injection, first we need to know the number of columns of the table we can access which is the table of movies.

The code is 
```SQL
iron' order by 1-- -
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20225747.png)

We can identify by using order by technique and check if there is an error come out. 
`Order by 1` is SQL query that allow you to sort the table based on the column number 1.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20225753.png)

Now we need to increase the number of the column until it gives us an error.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20225821.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20225829.png)

So now the querey gave us an error at column number 8 which appears that it does not exist, therefore the table which we exploit the data from 
contains 7 columns.And wait we see that not all columns appear in the web page so let's try to configure out which column is on screen and which is not.
by using the following code:

```SQL
iron' union select 1,2,3,4,5,6,7-- -
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20225925.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20225932.png)

Now we can inject some SQL quereies to get the user from the database or the name of the database itself.
First,Let's begin to find the user of the database.

The code is 
```SQL
iron' union select 1,user(),3,4,5,6,7-- -
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20230050.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20230057.png)

Second,Let's try finding the name of the database used.

The code is
```SQL
iron' union select 1,2,database(),4,5,6,7-- -
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20230117.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/a32adfcedc955c7b06f0c9bc9f73cd1aa422e9f0/Screenshot%202023-03-25%20230125.png)


