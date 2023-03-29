# bWAPP Cross Site Scripting Stored (Cookies) WriteUp

When we first open the challenge page we find a combo box and a like button

![alt text](https://github.com/nody77/CTFs-Writeups/blob/1c85445bdfe6d4b41277ee0266c4fb39c6cca514/Screenshot%202023-03-29%20190805.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/1c85445bdfe6d4b41277ee0266c4fb39c6cca514/Screenshot%202023-03-29%20190857.png)

We find that there is exist three kinds of movies which are Action,Horror and Sci-Fiction.
And when I inspected the page I found that there is a cookie and it contain the movie genre and it is one of the choices.

So Let's try inject the cookies with a value that does not exist in the combo box.
But first we need to open burpsuite to help us edit the http request header.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/1c85445bdfe6d4b41277ee0266c4fb39c6cca514/Screenshot%202023-03-29%20190907.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/1c85445bdfe6d4b41277ee0266c4fb39c6cca514/Screenshot%202023-03-29%20190913.png)

So let's change the genre value in the get request which is the first line.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/8525c025610cfbc99419275230eaeb5f0cbf2c56/Screenshot%202023-03-29%20190958.png)

And then we can forward the request and open the inspect page to if the cookie value have changed or not.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/8525c025610cfbc99419275230eaeb5f0cbf2c56/Screenshot%202023-03-29%20191026.png)

It changed!!
Now We can store a javascript code in the cookie.