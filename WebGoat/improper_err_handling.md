# Fail Open Authentication Scheme

Key in the username and password with `webgoat` and use burp suite to intercept traffic upon submit.

Observe the following 

`Username=webgoat&Password=webgoat&SUBMIT=Login`

Now remove the `&Password=webgoat` and forward the request below instead`Username=webgoat&SUBMIT=Login`
