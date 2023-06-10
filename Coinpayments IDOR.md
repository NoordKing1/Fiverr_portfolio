in 2022 i found a vulnerabilitie in Coinpayments api, the website is likely not properly validating or securing the user input from the URL parameter
allowing an attacker to modify the price directly. 

vulnerable url: https://www.coinpayments.net/index.php?cmd=_pay_simple&reset=1&merchant=452f63dd60678a63ce74eef80f69d284&item_name=Synapse%20X&item_desc=One%20redeemable%20serial%20key%20for%20Synapse%20X&item_number=1&currency=USD&amountf=0.1&want_shipping=0&success_url=https://x.synapse.to/success.html&cancel_url=https://x.synapse.to/success.html
risk: critical

<h2>summary</h2>:

	<input type="hidden" name="amountf" value="1.00">
  
  when you buy a product that have a payment method with coinpayments the merchant tool button api will send a post request with the following details:
	{"error":"ok",
               "result":{
                  "amount":"0.10",
                  "address":"ZZZ",
                  "dest_tag":"YYY",
                  "txn_id":"XXX",
                  "confirms_needed":"10",
                  "timeout":9000,
                  "cmd":"_pay_simple","reset":"1","merchant":"{merchent}","item_name":"{product_name}","item_desc":"{item_desc}","item_number":1,"currency":"USD","amountf":0,"want_shipping":0,"success_url":"https://x.synapse.to/success.html","cancel_url":"https://x.synapse.to/success.html"}

when you change the parameter "amountf" the api will not check if its right or no its automatically processed and it will be the price of the product
and when you pay the modified price which is 0.10$ minimum it will redirect you to success url and the payment is done and the real price has been modified
     
    solution:
      perform access validation.
      the price parameter should not be filled with the user
      
read more about the idor vulnerabilitie: https://portswigger.net/web-security/access-control/idor

![imagss](https://github.com/NoordKing1/Fiverr_portfolio/assets/73787446/a7bf21ae-aa69-4743-98dc-51e62a58a0e2)


and like you see here the price really changed not just the value of it


