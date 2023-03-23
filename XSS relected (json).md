# bWapp Cross Site Scripting Reflected (JSON) WriteUp

When we first enter the challenge page, we can see one text box for searching for a movie in the database of the website,
and there is a hint that the master of the website loves marvel movies.So we can begin investigating the web site to see its 
functionality to inject our XSS code in it.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/4295bfa06fec3cf5b2b78990d4e7c45d2cdfcf14/Screenshot%202023-03-23%20120901.png)

First, Let's search take advantages of the hint written and search for a marvel movie, for example iron man movie.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/4295bfa06fec3cf5b2b78990d4e7c45d2cdfcf14/Screenshot%202023-03-23%20120910.png)

Then press the search button and see what we will get.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/4295bfa06fec3cf5b2b78990d4e7c45d2cdfcf14/Screenshot%202023-03-23%20120917.png)

Ohh! We see that the movie is in their database, let's try another movie, for example fast movie.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/4295bfa06fec3cf5b2b78990d4e7c45d2cdfcf14/Screenshot%202023-03-23%20120935.png)

Then press the search button again.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/4295bfa06fec3cf5b2b78990d4e7c45d2cdfcf14/Screenshot%202023-03-23%20120943.png)

We see that it is not in their database. So let's begin our attack!
First we will try to inject our javascript alert code in the text box and see if it will work or not.

The code is
```javascript
<script> alert("good job") </script>
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/4295bfa06fec3cf5b2b78990d4e7c45d2cdfcf14/Screenshot%202023-03-23%20121129.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/4295bfa06fec3cf5b2b78990d4e7c45d2cdfcf14/Screenshot%202023-03-23%20121136.png)

When we press the search button we get unexpected message about the JSON response.
The meaning of it is that when the master of the website was writting the source code of the page, he forgot to write the end tag of the script of 
sending the json file.
So before writting our malicious code we need to close it by writting `"}]}';` and then write the alert code as following 

```javascript
"}]}';alert("hello world")</script>
```

- NOTE we did not write the starting tag of the script because it is alerady been written by the master of the web site.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/4295bfa06fec3cf5b2b78990d4e7c45d2cdfcf14/Screenshot%202023-03-23%20121157.png)

Then press the search button to see if it will work or not.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/4295bfa06fec3cf5b2b78990d4e7c45d2cdfcf14/Screenshot%202023-03-23%20121205.png)

It worked! 


