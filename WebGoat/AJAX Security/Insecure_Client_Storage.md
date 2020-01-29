## Insecure Client Storage

### Stage 1

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

![](C:\Users\edmun\Documents\GitHub\owasp-bwa-solutions\WebGoat\AJAX Security\coupons.png)

### Stage 2

After applying the coupons, update quantity of items and see the total cost add up with the coupon discount being applied. Then right click the value of total cost and select `Inspect` , now modify the value to `$0.0` and click `Purchase` button. 

![](C:\Users\edmun\Documents\GitHub\owasp-bwa-solutions\WebGoat\AJAX Security\free.png)


