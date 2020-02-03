# Thread Safety Problems

Using 2 different browsers enter `jeff` and `dave` respectively into each browser. Click `Submit` button at the same time eg. fast switching by using "alt/cmd + tab"



It appears that both browser displays the same user's account information. This is due to thread safety problems where one process (eg. retrieving 'jeff' account) were able to interfere with other process (eg. retrieving 'dave') since both process are using the same function (retrive account information).



# Shopping Cart Concurrency Flaw

Using 2 different browsers again. 



**On Browser 1**

On the first browser, modify shopping cart with eg. `1` quantity for the first item and click `Update Cart`. (If you go to the second browser, and refresh the shopping cart page, you will observe that the item you updated in the first browser will be loaded.) We know that once you click `Update Cart` the quantity for the item gets updated in the backend (like temporarily saved).



Click `Purchase` on Browser 1 to continue which will brings us to the credit card details and summary for total costs. Now that the price is "Locked in" Don't click `Confirm` yet.



**On Browser 2**

Modify shopping cart (shopping spree) eg. add `10`quantity for each item and click`Update Cart` . This will update the backend of total cart items.



**On Browser 1**

Return back to browser 1 and click`Confirm` to make the purchase of all the items you updated into the cart earlier but for the cheap "Locked-in price".


