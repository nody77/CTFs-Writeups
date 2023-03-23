# bWapp Cross Site Scripting Reflected (GET & POST) WriteUp

When I first opened the challenge page it only contained two text boxes, one for the first name and the second for the last name.
So I tried to write anything in the text boxes to see what is their function and their output.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/d990837d8ed70229719eac6b5aec635f704e0640/Screenshot%202023-03-23%20115744.png)

When I pressed the Go button . Welcome hello world is written below the button. 

![alt text](https://github.com/nody77/CTFs-Writeups/blob/954b0170d90fb35b515dd4585addf9697a5adcda/Screenshot%202023-03-23%20115801.png)

We know that Cross Site Scripting (XSS) is the type of security vulnerability in web applications where attackers inject malicious code 
into a website, so let's try to inject java script code to see if the web site is secured from XSS attackes or not.

![alt text](https://github.com/nody77/CTFs-Writeups/blob/653057a9c42d38c6e4d3ad864e6ffd6694d3feb1/Screenshot%202023-03-23%20115836.png)

The code is 

``` javascript 
<script> alert ("hello world") </script>
```

Then when I pressed the Go button again, the code did not work and a message appeared saying that we must enter data in both fields,

![alt text]()

so let's split the code in the two fields.
I will write the beginnig script tag withe the alert code in the first name field and write the ending script tag in the last name field.

![alt text](https://drive.google.com/file/d/1s1SrQ6dexMla9esheICwELgD7ozZVla6/view?usp=sharing)

When pressing the Go button again we notice that the code we injected has worked and the alert message has appeared.

![alt text](https://drive.google.com/file/d/1YWYd8x0MDoWg8aLgmbJLRLicLm6fXR3C/view?usp=sharing)



