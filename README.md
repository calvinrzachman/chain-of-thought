# chain-of-thought
A collection of ideas and writings on topics in the Bitcoin space

This repository is intended to be a drafting space writing. Upcoming topics include:
- Proof of Work
- How Does Lightning Network Scale? (Global vs Local state/information)
  - Lightweight money substitutes/proxy (paper receipts with claim on gold vs. valid transaction which spend from multi-sig UTXO)
  
## Lightning Network 

How does the Lightning Network scale Bitcoin? 
What commonalities does the scaling approach share with traditional scaling methods? 
What makes it different from scaling of old?

- Brief outline on how centralization and money substitutes helped human civilization scale

  [ Reread Social Scalability by Nick Szabo ] 
  As Nick Szabo says “gold’s physicality necessitated it’s centralization”, and that centralization might one day cost us everything. Central governments used the public's faith in gold as money to bootstrap their acceptance of paper money. They made paper as good as gold.

- Explain how Lightning scales in a similar way, but with a twist. We again introduce a proxy or money substitute of sorts (signed data structures called Bitcoin transactions), but do so in such a way that we capture all of the upside of scaling with little to no downside. (Full custody, no trust, no counter-party risk, maintain user privacy)

- Think about it from a perspective of global vs. local consensus



## Understanding Bitcoin
1. Hash Functions
2. Hashed Messages
3. Chain of Hashed Messages - imposes an ordering to the messages
4. Chain of Hashed Messages with Proof of Work
   1. Think about one person building a list with Proof of Work in isolation and then presenting that list to others. Does the PoW enable anything useful in such a scenario? 
   1. Think about a network of people working in communication to build a list (of which they all retain an individual copy) who choose to accept only list entries with PoW. Does PoW enable anything useful in this scenario?
   1. In both cases the PoW demonstrates that work has been performed. In the second case it also can be used to ensure that the network of people come to agreement on the list state. In both cases it brings finality/weight to state of the list. In both cases it would lead to an ossifying or preserving effect on older (not by time but by work) entries of the list. Entries "buried under more work". The only way to modify entries, once buried, is to dig them up and rebury them deeper (VERY HARD - unless you have more shovels than the rest of the people who keep piling on more work).
   
    Require that for any message to be valid that it carry with it a valid Proof of Work. What is Proof of Work? It’s exactly  what it sounds like. It is a proof that a certain amount of physical work has been done. A freshly mowed lawn or Thanksgiving table is proof that some amount of work has been performed. My message “Hey dad I mowed the lawn today” is easily verified by him looking out the window and seeing a pristine lawn. We can however construct another proof of work better suited towards building a digital money by exploiting the random nature of the cryptographic hash function mentioned previously.
    
    It is better suited since it lets us pass on the work to the computers. In place of human time, we use compute time. But because computers require energy to function, compute time is still tied to the physical world.
    
5. Build a Network which maintains the Chain of Hashed Messages (the second case from above)
6. Application to Money: What should the messages be? Transaction lists! (Blocks) -> Ordered list of transactions (Ordered chain of blocks - HOLY COW. Did he just explain blockchain without using the word blockchain?)



## What is Bitcoin?

### Outline

- Bitcoin the asset
    - A number in a ledger
- Bitcoin the Network
    - A collection of individuals cooperatively building a ledger
- Bitcoin’s ledger
    - Blockchain/Timechain
- Decentralized Record Keeping/List Building
    - Finding Order in Chaos - Proof of Work
- Censorship Resistance and Digital Scarcity

Bitcoin is many different things to different people. For some, Bitcoin is hope, for others [Bitcoin is freedom](https://www.youtube.com/watch?v=xLYYh4aPXAM), yet others still - [Bitcoin is Time](https://dergigi.com/2021/01/14/bitcoin-is-time/). Metaphor and philosophical musing aside, for the purposes of this summary Bitcoin is two things: Bitcoin is a software protocol which forms the basis of a global, censorship resistant, monetary settlement network, and bitcoin is the accounting unit native to the ledger that software protocol maintains. The latter concerns what is owned, while the former concerns the system which enables *digital scarcity* and ownership without central authority in the first place. 

When you own a Bitcoin, what do you actually own? “A bitcoin”, is a number stored in a ledger (list). However, it is a number stored in a very specific and special kind of ledger - one unlike any you have encountered before. A ledger which, along with a geographically dispersed network of record keepers, has truly unique properties.

When you own Bitcoin, you have knowledge of a piece of information, usually just a large random number called a *private key*, which can be used to update the ledger and transfer the number to control by a different key.

   >“Money is essentially a tool to keep track of who owes what to whom. Broadly speaking, everything we have used as money up to now falls into two categories: physical artifacts and informational lists. Or, to use more common parlance: tokens and ledgers.” ~ Dergigi
 
Our money is already digital
Increasingly less reliant on physical artifacts (cash) and increasingly more reliant on informational lists. 
Consider the implications of this in a society which drifts ever farther from ...

[ Possibly draw comparison to what the reader is somewhat familiar - our current system of digital centralized ledger money. SEE: *'Comparison to Deposits'*]

Bitcoin is actually quite similar in this regard.
our current system of centralized digital ledger money.
To illucidate, I'll ask the same question of the US Dollar: When you own a US dollar, what do you actually own? Excellent follow up questions include: What defines your ownership of it? Who can take that ownership away?

When you think of yourself has having US dollars, you own information that will allow you to “control” (with permission of your bank) numbers/entries in the Bank’s ledger. It would be improper to state that you have true control, as entries may only be updated with the permission of your Bank. The pieces of information used to authorize ledger entries are personal. You must use your personal private information (name, billing address, etc.)

Another key distinction to be made is what information system users must give up to access and transact with their own funds. With a bank ledger, the user must give up their identity. There are no private bank transactions. Period.

In a world 


So, both Bitcoin and bank deposits involve controlling numbers in a ledger. The key difference lies in who owns and controls access to that ledger. With a bank, the ledger is under the full discretion of the bank. With the Bitcoin Network’s ledger(s) there is no sole controller. Bitcoin is an entry in a ledger that ONLY you can control, and you can do so WITHOUT anyone’s permission. (Answer the How? later)

The Bitcoin Network is a collection of individuals, each maintaining their own ledger and enforcing a set of agreed upon rules encoded in software, their support for which is expressed in their electing to run the software under their own free will. The [Bitcoin software](https://bitcoin.org/en/bitcoin-core/) is available for free on the Internet and is fully observable by anyone with the ability to read the [C++ reference implementation](https://github.com/bitcoin/bitcoin). When you run the software and plug in to the Bitcoin Network, you aren’t some gullible financial system participant blindly trusting the authority of a centralized financial coordinator to maintain your purchasing power. You are instead a ruthless verifier, scrutinizing the validity of all transactions in agonizing detail. When you run the Bitcoin software you instantly become a member of the best auditing firm in the world. When you run the Bitcoin software you join all others who do the same, working to build and preserve a historical record of transactions. It is from such a record which we can build an accounting/monetary system which transcends jurisdiction and is, as a result, not possibly beholden to the interest of any one individual, corporation, or even nation. Attempts to create money out of nothing are not recognized. Attempts to move money without proper authorization. Not recognized. This is network enforced digital scarcity. This is, for the first time in modern history, a separation of money and State.

So we have Bitcoin, the network, and bitcoin, the asset.

Alternative Hot Takes:
Bitcoin is cash over TCP/IP
Bitcoin is an internet native protocol for exchanging value, an Internet Value/Money Protocol (IVP/IMP) if you will. This would be referred to as Bitcoin Protocol or LP/BP.
Bitcoin is a property right that does not require the State and it’s legal monopoly on violence to enforce ownership. 
Bitcoin is absolute scarcity.
Bitcoin is digital real estate.
Bitcoin is digital gold.
Bitcoin is information.
[Bitcoin is Venice](https://allenfarrington.medium.com/bitcoin-is-venice-8414dda42070).

KEY QUESTIONS: 
- How does Bitcoin build a ledger? 
- How are you able to interact with the system without asking permission?

Bitcoin is a software protocol for cooperatively building lists/ledgers in a low trust environment. 
Bitcoin is a software protocol for cooperative list building.

So what does Bitcoin’s ledger look like? How is it built and what unique properties does it have?
In other words, where do Bitcoin’s censorship resistance and scarcity properties come from?
- Censorship Resistant
- Digital Scarcity

IMPORTANT: The unique properties do NOT come from the ledger alone, but from the ledger and the network of people which maintain it.
- Blockchain not Bitcoin takes are incorrect.
- Bitcoin is NOT just a payment network
- Bitcoin is NOT PayPal
- Bitcoin is NOT a company
- Bitcoin is NOT ...
- Central Bank Digital Currencies (CBDCs) are NOT interesting (for anyone except for governments). They are tools for mass surveillance and control. Your dollar is already digital.

That the above statements are true should be obvious if one grasps the implications of a ledger owned by no-one.
Bitcoin is rule by rules, not by rulers.


### Comparison to Deposits

Another key distinction to be made is what information system users must give up to access and transact with their own funds. With a bank ledger, the user must give up thier identity. There are no private bank transactions. Period. 

QUESTION: When you own a US dollar, what do you actually own? What defines your ownership of it? Who can take that ownership away?

You own information that will allow you to “control” (with permission of your bank) numbers/entries in the Bank’s ledger. It would be improper to state that you have true control, as entries may only be updated with the permission of your Bank. The pieces of information used to authorize ledger entries are personal. You must use your personal private information (name, billing address, etc.). What’s more, you must also give the keys to your account any time you wish to use it.

At this point, you might reasonably object: “hey, but I can withdraw my money from the bank and receive physical cash if I want to”. True, you can exchange your IOU from the Bank for physical cash, but historically this conversion has not always been honored. Formerly you could exchange the paper cash for gold - today this exchange is a digital claim on dollars for physical paper money. This is a form of counter-party risk which arises from having a trusted third party custody your assets. In a well functioning system, one might deem the risk minimal and perhaps even well worth the service provided by the custodial insitution.

Bitcoin is actually quite similar in this regard. Recall, Bitcoin is controlled by a key. The key can be held for you by a trusted 3rd party, in which case you have a claim to Bitcoin being held in you name. This claim is only as good as the institution issuing it. You also have the option to “withdraw” your Bitcoin, transferring ownership of the Bitcoin from the exchange’s key to a key that you (and you alone) control. You have just realized the digital equivalent of “stuffing your cash under your mattress”.

Except that if invaders come, turn over your mattress, there will be no cash to see. Bitcoin takes up zero space. Private keys to Bitcoin are information. Bitcoin can be stored anywhere analog (on paper), digital (bits - 01100101), and even biological memory (you can store the private keys to Bitcoin in your brain!).


## What is a blockchain? Is it important? Does it “fix everything”? 
#### Corollary: What is Bitcoin’s Blockchain?

- Consider an individual building a list in blockchain form in isolation and then presenting that list to others. Does the blockchain format enable anything useful in such a scenario?
- Consider a network of people working to build a list, of which they all retain an individual copy. Does a blockchain enable anything useful in this scenario?

A blockchain is a list
A blockchain is a …

[ TODO: High level explaination of how messages (blocks) are linked in a chain ]

- Hash Functions (Magic One Way Function: input --> output, but NOT output --> input. Ex: y=2\*x is NOT one way. 2*(2) = 4 and 4/(2) = 2)
- Hashed Messages
- Chain of Hashed Messages - Each block/message contains a reference to all messages which came before it. Concretely, this reference is the output of taking the message, representing it as a number, pumping this number through a "hash function" and observing the output number. This imposes an ordering to the messages. Message This imposes an ordering to the messages as Message A must exist before Message B if Message B refers to the Message A. Rather, message A must exist before message B if message B contains a reference to the hash of message A. The hash of message A is a value incalculable without knowledge of message A.
```
m1 ... mN ------------   mN+1 ------------       ...
         | - list data       | - more list data
         | - reference       | - reference to mN
             to m(N-1)
```
A blockchain is highly specified way of writing down or storing information in which, each time you go to update what you've written, you include a reference to all the messages which came before. Concretely, this reference is constructed by taking the the information you have already written (historical record), representing it as a number, pumping this number through a "hash function" and observing the output number. Take history, represent it as a number (encoding/serialization), pump it through a one-way function (critical - what does the one-way function do? See [Bitcoin is Time](https://dergigi.com/2021/01/14/bitcoin-is-time/)), and include this in your message to be added. 

A blockchain is a self referencing list.
A blockchain is, on its own, nothing worth getting excited about. An individual storing data in blockchain form is not special. Such an individual could show you his data cleanly written out in blockchain form. All he could prove to you was that some messages/data entries existed before other entries. He could NOT prove the wall clock time when they were created as you would have to trust that he entered the correct timestamp. All he can prove is relative existence, namely that message A existed before message B. 

You could write down your grocery lists in blockchain form. You could prove that some of your your grocery list existed before other parts of your grocery list. But that is all you could prove. A blockchain simply imposes an ordering to the messages in your list.

An individual storing data in blockchain form is not special. The great power of such a storage mechanism emerges when independently verified copies of the transaction list in blockchain form are maintained by a collection of people distributed geographically - ala by a network of computers - who are able to come to agreement on one common vision of history.

QUESTION: What great power is this? Bitcoin's properties of censorship resistance and *absolute* digital scarcity of course!

### Bitcoin's Blockchain (Building Lists)

[More on the Bitcoin Network and Decentralized Record Keeping]

The list can be copied, altered and shared by any individual. How can honest users cut through the noise and coalesce around one common vision of history?

A fundamental question:
- How do participants in the network agree on the state of the list?
- How do participants in the network arrive at the same view on the state of the list?
- How do they come to consensus on the state of the list?

With Bitcoin, Satoshi achieves distributed consensus. That is, agreement on state amongst a set of distributed and independent entities.


Blockchain does NOT fix everything, but Bitcoin might :)


## Finding Order in Chaos - Proof of Work (Extra Credit)

At the risk of getting a bit technical. Proof of Work is THE key. [A failure to understand Proof of Work is a failure to understand Bitcoin](https://twitter.com/dergigi/status/1392826448017346561)

Thoroughly understand 2 things and you will likely understand Bitcoin:
- Proof of Work and Difficulty Adjustment
- 

What is Proof of Work? It’s exactly what it sounds like. It is a proof that a certain amount of physical work has been done. A freshly mowed lawn or Thanksgiving table is proof that some amount of work has been performed. My message, “Hey Dad, I mowed the lawn today,” is easily verified by him looking out the window and seeing a pristine lawn. The Great Pyramids stand as testament to the Greatness of the ancient Egyptian civilization. 

Bitcoin uses a mechanism to demonstrate work that is better suited towards building a digital money by exploiting the random nature of the cryptographic hash function mentioned previously. It is better suited since it lets us pass on the work to the computers. In place of human time, we use compute time. But because computers require energy to function, compute time is still tied to the physical world. This is Bitcoin's tether to the physical world.


In an open network where participants are pseudonymous and able to join and leave at will, how does one differentiate between candidate states? If anyone can propose their own state, what is to make one state more valid than any other?

Any network participant could, in theory, create whatever state he desired (it is just a list of transactions after all), share it with his peers, and attempt to get them to adopt it as their own. Obviously if he was successful in doing this, his state would be come the de-facto state of the network. In the Bitcoin protocol, unlike historical institutions constructed by man, his authority to propose such a state and its correctness in the eyes of his fellow participants does not come from wealth, political connectedness, or birthright. It instead comes from work and energy expenditure, a cost he proves paid each time he updates the state (collective). Who gets to prove energy expenditure?

Any individual network participant can create or accept whatever view of the system they want. Can they convince others that their view of the system state is correct? If we define "correct" as the system state with the greatest work (highest energy) then the answer is "No". Consider a dishonest network participant who creates his own set of ordered messages (his own state) favorable to himself. In the absence of Proof of Work, the validity of his system state is indistinguishable from any other. He can present his system state to another network participant and, in the absence of additional information, they will be unable to discern the validity of the candidate states. They will have to find different criteria on which to assess competing states. A metric for determining validity is needed.

What does it mean for a system state to be "correct"? What is to make one state more valid than any another? In systems with a central Authority, the correct state is determined by that Authority - the state proposed by your Bank is the valid state. In a pseudonymous distributed network of state maintainers we use work/energy. 

  >* Valid states must carry Proof of Work. The most valid states carry Proof of the most Work.

This requirement enables consensus. Given two competing views of the system state, a network participant can always select the system state endorsed by greater work. Dishonest participants are unable to present valid alternative states as they cannot forge energy (Szabo's "unforgeable costliness"). Perhaps ***Proof of Energy Expenditure*** would better describe the mechanism here. So long as one party does not control a majority of the energy in the system, they cannot convince network participants to accept any system state other than the system state constructed by the most energetic cohort of network participants. They cannot forge Bitcoin. They cannot ["double spend"](https://en.wikipedia.org/wiki/Double-spending) Bitcoin. Proof of Work turns the dishonest network views/false system states of would be usurpers into harmless individual delusions. To dishonest Bitcoin Network participants: For full credit (state acceptance), prove your work!


Bitcoin is NOT a trusted network. This means that it. Participants are pseudonymous and can come and go as they please. This means the protocol must be designed in a way which does not assume altruism/good faith. There will be dishonest who attempt to cheat, mislead, or attack honest network participants.
Network participants can come and go as they please, 
In Satoshi's own words: "nodes can leave and rejoin the network at will, accepting the longest proof-of-work chain as proof of what happened while they were gone."

While Proof of Work was invented in the 90's, Satoshi's application to distributed consensus is novel and this is sometimes referred to as Nakamoto Consensus, in his honor. 

When combined with a proof of work, our blockchain list levels up. It becomes resistant/immune to forgery and ex-post facto data corruption. (I think it is actually the blockchain in combination with a proof of work network which achieves this).


## Building Lists

Bitcoin is a software protocol for cooperatively building lists/ledgers in a low trust environment. 

## Censorship Resistance

“The root problem with conventional currency is all the trust that’s required to make it work. The central bank must be trusted not to debase the currency, but the history of fiat currencies is full of breaches of that trust.”
 		~ Satoshi Nakamoto
    
    
  >“The root problem with conventional currency is all the trust that’s required to make it work. The central bank must be trusted not to debase the currency, but the history of fiat currencies is full of breaches of that trust.”
  > ~ Satoshi Nakamoto


- KEY IDEA: Censorship arises out of trust placed in the hands of a central authority.

Hyper-cognizance of where you place trust.
If the ledger is owned by any one individual or entity, then it can be changed by that individual or entity. Period. The only solution is to decentralize the record keeping (what does that even mean?).

Decentralization of record keeping is achieved through constructing the system of record keeping to be as lightweight and simple as possible, by constraining the amount of records to be kept, by providing a small payment to the record keepers, and by building a system in which anyone can become a record keeper without asking permission. The first item above, the constraining of information, is quite clearly at odds with expanding transactional throughput. The more information you ask participants to process, the fewer will be able to complete the task at hand. This is centralization of processing and validation in the hands of a smaller and smaller few. To do this is to destroy digital scarcity. To do this is to create yet another system of Centrally "enforced" digital scarcity. Centrally "enforced" digital scarcity is easily infringed. Network Enforced Digital Scarcity.

Decentralized record keeping? That’s it? What gives? Sometimes what sells and what explains are two different things. You will learn to love decentralized record keeping.


A system in which anyone can join without asking permission implies that there is NO authority with whom to seek permission. There is no single entity capable of controlling the system. There is no authorized set of users. ANYONE (or any programmable thing) can use Bitcoin. Bitcoin does not recognize race, gender, faith, political affiliation, or socio-economic status. It recognizes public/private key cryptography, digital signatures, and energy (proof of work).  Bitcoin eliminates sole sources of truth by design, instead achieving decentralized emergent authority through Proof of Work.

With no central coordinator or maintainer how can there be order? Decentralized emergent authority/order.


## Creating Digital Scarcity

- How can it be that Bitcoin is scarce?
- Centrally “Enforced” Digital Scarcity
- Network Enforced Digital Scarcity

I am convinced that the elusiveness of Bitcoin’s value prop stems, in large part, from a lack of understanding of how Bitcoin achieves digital scarcity. 

“Money is essentially a tool to keep track of who owes what to whom. Broadly speaking, everything we have used as money up to now falls into two categories: physical artifacts and informational lists. Or, to use more common parlance: tokens and ledgers.” ~ Dergigi

Borrowing from Gigi's article one more time:
   > "… if you have an apple and I have an apple, and we swap apples — we each end up with only one apple. But if you and I have an idea and we swap ideas — we each end up with two ideas." ~ Charles F. Brannan (1949)

Proliferation of digital information is incredibly cheap. This is one reason that computers and networks like the Internet are so useful, but if your aim is to construct a digital system of global money, this ease of duplication is disastrous (if normal citizens have the ability to duplicate that is).

Information is not physical. What is non-physical is also non-rivalrous. My possession of information does not preclude you from having the same information, unless I wont share the information with you :).

Information is only scarce in the absence of communication. Conversely, information is as abundant as knowledge and communication permit. 

The list can be copied, altered and shared by any individual. How can honest users cut through the noise and coalesce around one common vision of history?


## Where did Bitcoin come from?

## How is Bitcoin created?


## Further Reading
- Grokking Bitcoin. Kalle Rosenbaum 
- Inventing Bitcoin. Yan Pritzker
- Internet of Money - Andreas Antonopoulos
- \*Mastering Bitcoin - Andreas Antonopoulos (technical)
- Programming Bitcoin - Jimmy Song (technical)
- [Bitcoin Master Class with Michael Saylor and Ross Stevens](https://www.youtube.com/watch?v=KlXqfibqb38) (VIDEO)
- [Infrastructure Inversion](https://www.youtube.com/watch?v=KXIaILHl7Rg) - Andreas Antonopoulos (VIDEO)
- [The Fraying of the US Global Currency Reserve System](https://www.lynalden.com/fraying-petrodollar-system/), [7 Misconceptions about Bitcoin](https://www.lynalden.com/misconceptions-about-bitcoin/), [Analyzing Bitcoin's Network Effect](https://www.lynalden.com/bitcoins-network-effect/) - Lyn Alden
- [Bitcoin is the Great Definancialization](https://unchained-capital.com/blog/bitcoin-is-the-great-definancialization/) - Parker Lewis
- [The Bullish Case for Bitcoin](https://vijayboyapati.medium.com/the-bullish-case-for-bitcoin-part-1-of-4-94087a70d9e8) - Vijay Boyapati
- [Wittgenstein’s Money](https://allenfarrington.medium.com/wittgensteins-money-7cac8d0635cf), [The Capital Strip Mine](https://allenfarrington.medium.com/the-capital-strip-mine-ec627e9fe40a), [Fiat Privilege](https://allenfarrington.medium.com/fiat-privilege-3f5afae50083), [This is not Capitalism](https://allenfarrington.medium.com/this-is-not-capitalism-5ed0a9d5dfa9) - allenf32 
- [Sovereignism](https://breedlove22.medium.com/sovereignism-part-2-bitcoin-the-ultimate-offshore-bank-9a1650770202), [Our Most Brilliant Idea](https://breedlove22.medium.com/our-most-brilliant-idea-aced329f8941), [Masters and Slave’s of Money](https://breedlove22.medium.com/masters-and-slaves-of-money-255ecc93404f), [The Number 0 and Bitcoin](https://breedlove22.medium.com/the-number-zero-and-bitcoin-4c193336db5b) - Robert Breedlove
- The Bitcoin Standard - Saifedean Amous
- Mises, Rothbard, Hayek, Hazlet (Austrian School)
- [Bitcoin is Time](https://dergigi.com/2021/01/14/bitcoin-is-time/), 21 Lessons, 21 Ways - Dergigi
- Bitcoin Audible Podcast - Guy Swann (most of these articles are available in audio format here)
- Stefan Livera Podcast

Bitcoiners to Follow:
- Dergigi
- Robert Breedlove
- Nic Carter


### Misc

Bitcoin’s ledger, like any ledger, is a system for tracking private property rights and securing the willful transfer of those rights.
 
We have built institutions to defend these ownership rights. One could argue that the purpose of the legal system is to codify a rule set which can be used to resolve property disputes without resorting to violence. To establish a system of trust, a base from upon which humans feel comfortable building and exchanging with one another. They need not trust each other as long as they trust the institutions. The ultimate enforcer of such a codification of rules is an institution with a legal monopoly on violence. This institution has traditionally been called “government”. At the end of the day your ownership of any physical or informational property is protected by either yourself or the legal monopoly on violence. When trust in these institutions is high this system works well. However, when faith in our institutions falters so to do the...

Bitcoin codifies a rule set in source code. The court system is the Bitcoin Network. Human bias and subjectivity is less prevalent here. Un-equal application. The ideal of “equal justice under the law” is more faithfully executed.

Bitcoin’s blockchain is “an open source ledger which keeps track of ownership rights and permits the transfer of these rights” Jeff Tucker


Bitcoin are locked with a spending condition. The spending condition can be fairly arbitrary, but most often the condition specifies that a digital signature must be presented in order to use these bitcoin in a transaction. Transactions transfer Bitcoin from one spending condition to another, typically from one owner/key to another. 


The structure of the spending conditions are chosen by the owner of the Bitcoin (this is actually where Bitcoin really earns its label of “Programmable Money”).  The network will not process transactions attempting to update ledger entries which do not satisfy these spending conditions.

In Bitcoin, coins (UTXO) are locked with a spending condition. The mechanism used to enforce the association of Bitcoin UTXO and its spending condition is a simple scripting language that is understood and executed on every Bitcoin network node. The spending condition can be empty (allowing anyone to spend) but most commonly they bind Bitcoin to the owner of a public/private key pair. In almost all cases, the act of spending coins becomes a problem of proving knowledge of the associated private key. The most simple way to do this would be to simply announce the private key to the network. However, this is undesirable and prompts search for a better method. Digital signatures are this alternative.




We've forgotten how essential and fundamental a tool money is. Modern civilization is not possible without the division of labor/specialization enabled by indirect exchange, which is what money enables.
