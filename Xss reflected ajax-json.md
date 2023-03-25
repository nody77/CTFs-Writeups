# bWapp Cross Site Scripting Reflected (AJAX/JSON) WriteUp

When we first open the challenge page we find one text box to sereach for a movie and their is a hint saying that the master of the website 
loves marvel movies.As we can see here there in not a sereach button as it’s an AJAX web page it will update the web page without reloading 
the page and the client-server interaction will happen in the background.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/3a19a95ce3d6f0764dad48ac1f066b616d0bbdd6/Screenshot%202023-03-24%20210112.png)

First, Let's try interacting with the page to see what it can do.Let's try entering iron man moive name.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/3a19a95ce3d6f0764dad48ac1f066b616d0bbdd6/Screenshot%202023-03-24%20210127.png)

We can see that the moive is their database so let's try to inject our javascript code to see if it will work or not.
The code is 

```javascript
<script>alert("hello world")</script>
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/5f0d832c1a11dc3d7fb4436da4bb8a74146757a1/Screenshot%202023-03-25%20090800.png)

As we can see our code didn't work. So let's try to inject a simple HTML tag to see if the website is vulnerable to them or not.
I payload the following tag:

```HTML
<h1> fast </h1>
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/5f0d832c1a11dc3d7fb4436da4bb8a74146757a1/Screenshot%202023-03-24%20210526.png)

It worked!!
Now let's payload our code.

```HTML
<img src=x onerror=alert("fast")>
```

>The explanation of the code is:
we tell the web page that there is an image and its location is x which does not exist so when he can not open the image it will go to the
second part of the code which is onerror which will make an alert.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/5f0d832c1a11dc3d7fb4436da4bb8a74146757a1/Screenshot%202023-03-24%20210733.png)

It worked!!
