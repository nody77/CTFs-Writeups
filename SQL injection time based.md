# bWapp SQL Injection - Blind - Time - Based WriteUp 

When we first open the challenge page, we can see one text box for sereaching for a movie and a sereach button and it the web page says theat
the result will be sent by email (which we didn't provide and will not :) ).

![alt text](https://github.com/nody77/CTFs-Writeups/blob/2fca59d7978e968948de7d72539f2710c6e9e319/Screenshot%202023-03-24%20223239.png)

First let's try sereaching for a movie, for example iron man.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/1912d59c664241e10662b01a0a8f004f08db923c/Screenshot%202023-03-24%20223253.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/2fca59d7978e968948de7d72539f2710c6e9e319/Screenshot%202023-03-24%20223322.png)

As we can see it did not do anything, so let's payload our code to see what is done.

The code is 
```SQL
x' or 1=(select sleep(2));#
```

>The explanation of the code:
we inserted a sql querey for sereaching `x`, if he did not find it,he will excute the second part which is making the web site sleep for 
two seconds and then respond again

![alt text](https://github.com/nody77/CTFs-Writeups/blob/bdad3a4254a72ada43f7709301e1686d2a870182/Screenshot%202023-03-24%20223615.png)

As we can see at the top of the page that after payloading the code the website was loading and it continued to do it for the time we inserted 
in the payload.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/bdad3a4254a72ada43f7709301e1686d2a870182/Screenshot%202023-03-24%20223628.png)
