## JSON Injection

From: 'BOS'

To: 'SEA'

You will see there are 2 radio buttons, select the one with 0 stops priced at $600 and click submit with burp (or other HTTP intercept tools)

`travelFrom=BOS&travelTo=SEA&radio0=on&SUBMIT=Submit&price2Submit=%24600`

We observe that it is submitting `%24600` which translates to `$600`. Modify the following to make the flight priced cheaper (real cheap at $1!)

`travelFrom=BOS&travelTo=SEA&radio0=on&SUBMIT=Submit&price2Submit=%241`
