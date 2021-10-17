# Lightning Network

How does the Lightning Network scale Bitcoin? 
What commonalities does the scaling approach share with traditional scaling methods?
What makes it different from scaling of old?

THOUGHT: It is very hard to gate keep or rent seek on Lightning. When you can lay new payment infrastructure (Lightning payment channels) for the cost of a TCP connection and one global consensus (on chain channel funding transaction), any gate keeper can easily be made irrelevant by the construction of new train tracks to bypass him in a matter of seconds. Cool.

- Write a short primer piece with definitions for payment channels, payment channel networks, and possibly Bitcoin UTXO, and multi-signature UTXO (an output which requires multiple signatures in order to be spent). 
- Brief outline on how centralization and money substitutes helped human civilization scale
    ```
    [ Reread Social Scalability by Nick Szabo and Money Warehouses (Chapter 12 of What Has Government Done to Our Money - Rothbard ]
    ```
    As Nick Szabo says “gold’s physicality necessitated it’s centralization”, and that centralization might one day cost us   everything. Central governments used the public's faith in gold as money to bootstrap their acceptance of paper money. They made paper as good as gold.

- Explain how Lightning scales in a similar way, but with a twist. We again introduce a proxy or money substitute of sorts (signed data structures called Bitcoin transactions), but do so in such a way that we capture all of the upside of scaling with little to no downside. (Full custody, minimal trust, minimal counter-party risk, maintain user privacy).

- Think about it from a perspective of global vs. local consensus

NOTE: The angle presented in this writing is decidedly Austrian. I generally am susceptible to arguments from this school of thought. Their explanations seem to give careful consideration to incentives and second order effects and, as a result, sound highly plausible, but I have not had enough time to divert away from Bitcoin to fully fleshing out these economic/historical ideas.


A decentralized auditable ledger brings security and finality to our system state, but all the information replication and energy that this requires makes the system difficult to scale. Network enforced digital scarcity comes at a price. 

As mentioned previously, when you transact with Layer-1 Bitcoin, you require the attention of the entire world. The more people that want to use Bitcoin, the harder and more expensive it becomes to use. Cash does not have this property. Improving this difficulty in scaling is the subject of off-chain protocols, or so called Layer-2 solutions. By far the most popular example of such a system are Payment Channel Networks (PCN), the most popular example of which is the Lightning Network.

-----

The centralization of money storage inevitably leads to the exchange of “money substitutes” [Rothbard WHGDTOM 37]. The classic historical example of which is transacting using paper receipt’s redeemable for gold in a warehouse. The paper receipt acts as a proxy or stand-in for gold in an exchange. NOTE: You could argue that the centralization of money storage is driven by a desire to use money substitutes, either duplicitously via those seeking to control the money or honorably via desires to increase the salability of the monetary medium across space.

If you managed to find this article without first having read Robert Breedlove’s philosophical work on Bitcoin, please check out his [ link to Breedlove ]. He often highlights 5 properties of money:
- Divisibility
- Portability
- Durability
- Recognizability/Verifiability
- Scarcity

[ See sections in iPhone which talk about each ]

Problems with divisibility, portability, and verifiability of money (not really durability and DEFINITELY NOT scarcity) led to its eventual centralization and replacement with “money substitutes”. (There are likely other factors at play here such as groups of people recognizing that controlling the value system of society is incredibly powerful).

The debate is as to whether your money should be absolutely hard or contain a small backdoor enabling the value to which it entitles you to be repurposed at the whim of some central decision making body. The softness of money is monotone. What begins minimally soft, ends infinitely so. We have moved first from commodity money in the form of precious metals, to paper receipts with claim on precious metals, to most recently digital “points” apparently assignable at will by economic architects (hello Stephanie Kelton/“Modern” Monetary Theory) without any tie to the physical world whatsoever. I am not claiming your money must be physical to have value. It has to be valued by people to have value. However, Bitcoin, despite being digital, DOES have [strong ties to the physical world](https://github.com/calvinrzachman/chain-of-thought/tree/master/proof-of-work) which are KEY to its scarcity - *network enforced digital scarcity*.

Bitcoin is already near infinitely divisible, near infinitely portable, and fully verifiable. So what gives? Why do we need “more layers” to realize Satoshi’s vision (his real vision - not the shitcoin)? The very thing which gives Bitcoin the properties here outlined, is what prevents it from being used as an every day medium of exchange. 

THOUGHT: If a medium which is otherwise most suitable as a store of value cannot move frequently enough to accomodate the frequency of man's exchange, then he will divise a way to abstract that medium and exchange claims against it. These "promises to pay" weigh nothing at all and will therefore be scalable to whichever frequency man requires. As it turns out, promises are NOT infinitely scalable. Credit carries risk and requires trust in indiduals, institutions, reputation systems, etc. 

QUESTION: Why can’t you “move” Bitcoin in small amounts with high frequency? Is this not a short coming in portability?
ANSWER: A decentralized auditable ledger brings security and finality to our system state, but all the information replication and energy that this requires makes the system difficult to scale. Network enforced digital scarcity comes at a price. 

When it comes to security - we'd rather not compromise. We seek to preserve ALL of the characteristics which make Bitcoin a sound and incorruptible money. Unfortunately for B-Cashers, it looks like you can build a system for high frequency MoE on top of a rock solid SoV layer. But it does not appear as though you can build a MoE that any one wants to use :D through naive linear scaling for additional space that network demand doesn’t presently justify.


So why will this time be any different? Why should you accept payments via the Lightning Network as a stand-in for cold, hard Layer-1 digital gold? To explain why you need not worry, we must examine how a payment channel is constructed.

[ Small summary of Lightning Network ]

* What is a Payment Channel?
* How does this Payment Channel help us scale?
NOTE: I am assuming basic familiarity with payment channels and the Lightning Network.  For more information on these topics, the reader is referred to … [ Lightning Network White Paper, Bitcoin Magazine, and Why Bitcoin’s Lightning Network is Ingenious]

With the Lightning Network we are scaling once again through introduction of a monetary substitute/proxy. However, this money substitute does not arise out of centralization of the underlying monetary good (gold/Bitcoin), but instead out of centralization/localization of information. [ Link to footnote with global vs. local here ]. This time our monetary substitute/proxy takes the form of a valid, signed Bitcoin transaction which spends from a ***shared*** output, known as a ***multi-signature*** output. The shared output requires the consent of both parties (multiple signatures) to be spent. 

A payment channel is “opened”/funded by a transaction which creates this shared output. The shared output places control over the funding capital jointly between the two channel participants. This transaction is called the ***funding transaction***. 

Our money substitute is the signed transaction which spends from the funding transaction and is known as the ***commitment/update transaction***. The signed commitment transaction is a commitment to a specific division of the funding capital between the two channel participants (ie: I own 0.3 and you own 0.7 in a payment channel with 1 BTC), and channel peers continuously craft commitment transactions any time they want to update the allocation of funding capital between them.

*Why does the payment channel construction need a multi signature output upon which it can build?* Both parties need to be sure that funds cannot be moved out from underneath him - that funds cannot move without his approval. He needs to be sure that joint property rights over the channel funding capital is honored and enforced at all times and that any re-allocation of capital amongst them, once committed to by both participants, cannot be unilaterally undone (invalidation of old state). Careful construction of the off-chain protocol in combination with the Bitcoin Network provides this assurance. With a solid platform upon which we can negotiate, signed Bitcoin transactions are indeed as good as gold (as good as on-chain bitcoin).

The multi-signature ensures that the payment channel construction is *fully collateralized*, as it proves to both participants that capital has been committed specifically for negotiation with each other. In this way, the multi signature output of the funding transaction ensures that:
- The signed commitment transaction is NOT a promise
- The signed commitment transaction is NOT an IOU
- The signed commitment transaction is NOT an IOU or receipt with a claim on Bitcoin

The multi-signature underlying a payment channel gives the signed commitment transaction credibility. When you receive a signed commitment transaction, you know that your counter-party has the equity underlying your negotiations because that equity is under your joint control. The commitment transaction is a contract declaring that the specified equity is placed under your sole control and will be regonized as such by the Bitcoin Network.

Another way to think about it: Two channel participants are co-authors jointly working on a draft of a Bitcoin transaction. They continually revise the transaction in private until they feel compelled to publish, whether due to a breach of channel contract or desire to use capital elsewhere. With the publication of their final draft, they reflect the aggregate of all negotiations and once again ask for the attention of the world as a whole to bear witness.

SIDE NOTE: You and I could open a payment channel using nothing more than a vanilla UTXO under my sole control as our channel funding capital. I have full control over the UTXO and how it is spent. I could make off-chain “commitments” to allocate a portion of the funds to you, but nothing is stopping me from spending the funds elsewhere should I choose to do so, rendering my “commitments” to you null and void. Without the multi-signature construction underpinning the negotiations, any re-allocation of capital is nothing more than a PROMISE/IOU, as a channel participant cannot be sure that the money he was just pledged by his counter-party will not be spent somewhere else prior to final settlement on-chain. (Link to Breedlove tweet on how funny business goes down between payment and settlement)

In a very real sense capital is not committed solely for your channel partner, but can also be utilized for routing payments to other network participants. This does not violate statements made above as routing payments boils down to accepting commitments from one direct channel partner while simultaneously and atomically (all or nothing/IFF dynamics) extending a commitment to a different direct channel partner.

We will accept this signed transaction in exchange for the product of our labor, just as we might accept Bitcoin or USD.

With Layer 1 Bitcoin we are accepting ***space/entries (transactions) in a distributed ledger*** as payment. With the Layer 2 Lightning Network we accept ***signed transactions*** (not in a distributed ledger) as payment. The signed commitment transaction is clearly a stand-in for the preciously scarce attention of the Bitcoin Network.

[ We have comparison between Lightning and paper receipts (the OG off-ledger solution) somewhere on iPhone ] 


Substituting paper receipts for gold brought notable improvements to the portability and divisibility of money, but these improvements came at the cost of a complete destruction of the scarcity of the monetary medium. If what transpired with gold, paper receipts, and fiat is demonstrative of anything, it is that we should consider with great scrutiny attempts to substitute money, particularly those accompanied by a centralization (in the hands of third parties) of the underlying monetary good which backs the substitution. Substituting signed, valid transactions (messages) in place of immortalizing the messages in a distributed ledger, we are indeed centralizing something. We are centralizing information². Rather than storing that information in N different ledgers worldwide, you store the information in k << N dual entry (pairwise) ledgers along the payment path. Our saving grace is that the underlying Bitcoin is kept by the parties involved directly. It is NOT placed in the hands of a trusted 3rd party. This makes all the difference in the world.

We would only need concern ourselves if, in order to open a payment channel you were required to send your bitcoin to a multi-signature, or completely ruinously single-signature, with the State or some banking institution. This would clearly centralize the storage of Bitcoin. It is obvious that such an arrangement would only arise under the threat of violence OR if the State somehow becomes the primary channel counterparty chosen voluntarily by economic agents (lol).

It is not evident that LN poses any threat to destroy the scarcity of bitcoin. Payment channels are fully collateralized/“backed” by bitcoin on chain which cannot be spent or used for any other purpose other than the LN payment channel negotiations to which it has been committed.


