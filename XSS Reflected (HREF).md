# bWAPP Cross Site Scripting Reflected (HREF) WriteUp

When we first open the challenge page, we find a text box and a continue button and a note 
says that "in order to vote we need to enter our name first"

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff6d8f0fb8014bdca5da706aaef016b10f92dee4/Screenshot%202023-03-29%20190411.png)

So I entered the name hacker so see what will happen.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff6d8f0fb8014bdca5da706aaef016b10f92dee4/Screenshot%202023-03-29%20190432.png)

Then after clicking the continue button a table of the movies name appeared for voting 

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff6d8f0fb8014bdca5da706aaef016b10f92dee4/Screenshot%202023-03-29%20190445.png)

So Let's try to insert our payload by returning to the first page to insert it in the text box.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff6d8f0fb8014bdca5da706aaef016b10f92dee4/Screenshot%202023-03-29%20190540.png)

The code is :
```javascript
<script>alert("good job")</script>
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff6d8f0fb8014bdca5da706aaef016b10f92dee4/Screenshot%202023-03-29%20190551.png)

After that we discover that the payload didn't work,so I did some researching and find out that the we need to close the tag before writing 
our script and open it again so the function of the rest of the web page can work.

So the new payload is

```javascript
><script>alert("good job")</script><
```

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff6d8f0fb8014bdca5da706aaef016b10f92dee4/Screenshot%202023-03-29%20190653.png)

![alt text](https://github.com/nody77/CTFs-Writeups/blob/ff6d8f0fb8014bdca5da706aaef016b10f92dee4/Screenshot%202023-03-29%20190702.png)

It worked!!



