# Lightning Service Authentication Token (LSAT)

March 30th 2020 - Lightning Labs announces new specification for private payments and authentication on the web, allowing users to pay for and consume resources digitally without the need for providing personal information like name, mailing address (email), and bank or credit card information.


## Initial (thought) Chain
Consider the following: I wish to purchase a resource from you (an apple let's say). I hand you $2 and you give me the apple. Transaction complete. I don't know anything about you and you don't know anything about me beyond that which we choose to voluntarily divulge in idle conversation while making the exchange.

As a merchant, the presence of the US dollar in your hand is all I need to know in order to exchange with you. This is not the case with exchanges in a digital environment. Consider now the case of a merchant selling access to a resource like an API with digital payment. The merchant must be sure that either the person accessing the API has paid, or that someone else (they need not know who) has paid. The only way this has been solved in the digital realm is by tying payment to identity. I need your name, login information, mailing address (email), and bank/credit card information in order to trust that I will be paid for offering you access to my service. 

NOTE: Typically merchant's must wait to receive funds. There is no instant settlement. 

Two thoughts:
- If payment is one time/up front and the token/credential is reusable, then you must be able to ensure that the token is not reused by parties who have not paid. (WRONG!!)

- If the payment is by use, then you don't need to provide any identity. I as the seller already have all I need, namely the money. In other words, I can now see the digital US dollar in your hand. See "Metered API"

LSAT is looking to provide a reusable token. As it is a bearer token with no association to identity (simply presenting it is all that's needed for authentication), you can even give it to a friend to use. This seems problematic as I would think that it would be the merchant's goal to ensure that parties who have not paid cannot use the resources being sold.


I am falling trap to the traditional. Tying digital payment and identity together. This is the wrong way of thinking. It is NOT a property of cash that use identifies the user. Likewise, it is (or will one day hopefully be) NOT a property of Bitcoin that use reveals information about the user. As a bare minimum requirement for sustained operation: The merchant is NOT concerned with whether the person using the resource has paid, but rather ONLY that they have been compensated by someone for the resources being consumed (ie: I can pay for my brother). 

It is (as it should be) on the server to protect itself with LSAT revocation conditions. A user exceeding the server's defined conditions (expiration date, rate or volume of usage, or more restrictively, requiring requests come from a specified IP Address) would find their LSAT revoked. They could be automatically requested to pay a new invoice for additional usage or to perform an API "tier upgrade" if the usage exceeds a specified threshold. 

Two (revised) thoughts:
- If payment is one time/up front and the token is reusable, then you must be able to ensure that the token is not indescriminantly reused. Either by taking token reuse into consideration when pricing the LSAT or

- If the payment is by use, then you don't even need a token at all. I as the seller already have all I need, namely the money. In other words, I can now see the digital US dollar in your hand. See "Metered API"


It seems that with LSAT, developers will be able to provide Apple Pay level of user experience at the point of sale with none of the trust or usual suspects (middlemen) between customer and merchant.
