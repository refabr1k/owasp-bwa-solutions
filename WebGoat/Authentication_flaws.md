# Password strength


---


# Forgot password

Since the prompt mentioned `See the OWASP admin if you do not have an account.` the hint is the user name `admin`. When submitted, you will be asked the same question `What is your favorite color?`. Try different colors since there isnt any lock-out mechanism. To complete challenge input `green`.

---

# Basic Authentication

## Part 1
Using burp suite, click on any links within webgoat app and observe that there is a field `Authorization: Basic cm9vdDpvd2FzcGJ3YQ==` in your HTTP request. If you highlight `cm9vdDpvd2FzcGJ3YQ==` > `Convert Selection` > `Base64` > `decode` you will see `root:owaspbwa`

The name of authentication header is `Authorization`
The decoded value of the authentication header the base64 decoded value for previous exercise `webgoat:webgoat` 

## Part 2
The next challenge requires us to force WebGoat to reauthenticate us as `basic:basic`. 

If you make a GET request for the same page you are at, use burp suite and modify the field `Authorization: Basic` to base64 encoded of `basic:basic` It prompts you that you are almost there!

Deleting your cookies makes the server create a new session for us, didn't work because webapp will check to see if you are first authenticated, if not a prompt will ask for your login. If it checks that you are authenicated before, it just creates a new session id.


    Official solution: To access WebGoat as the user basic, you need to corrupt the existing JSESSIONID and the Authorization header. You can do this in WebScarab. Intercept the request and delete a character from the JSESSIONID value and the Authorization header.
    WebGoat will require you to authenticate, so you now enter for the user name basic and for the password basic. This logs you on as the user basic.



---

# Multi Level Login 2

Login as 'Joe'. When prompted for TAN # input, turn on burp suite to intercept traffic on submitting the form. You will see `hidden_user=Joe&tan2=15161&Submit=Submit`.

You should observe that there is a `hidden_user` parameter that can be tweaked to `Jane`.

# Multi Level Login 1

Login as 'Jane' and Input TAN #. If use burp suite to intercept request for submiting TAN #, you will observe the following (I had a prompt for entering TAN #3) `hidden_tan=3&tan=15648&Submit=Submit` 

Since we have TAN #1, we could modify it from value `3` to `1` as shown  `hidden_tan=1&tan=15648&Submit=Submit` 