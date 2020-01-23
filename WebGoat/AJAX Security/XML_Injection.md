## XML Injection

After submitting the given account ID, you will observe that the account balance seem to only review the first 3 rewards (out of total 5). If you check all items and submit them, intercept with burp (or other HTTP intercept tool) you could see the following POST parameters

```
accountID=836239&check1001=on&check1002=on&check1003=on&SUBMIT=Submit
```

Modify the request to include the other 2 rewards (assuming that the naming convention used is in sequential numbering eg. 1001,1002,1003,1004,1005)

```
accountID=836239&check1001=on&check1002=on&check1003=on&check1004=on&check1005=on&SUBMIT=Submit
```
