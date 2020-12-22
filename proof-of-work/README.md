# Proof of Work

## Prerequisites

1. Hash Functions
2. Hashed Messages
3. Chain of Hashed Messages - imposes an ordering to the messages
4. Chain of Hashed Messages with Proof of Work
   1. Think about one person building a list with Proof of Work in isolation and then presenting that list to others. Does the PoW enable anything useful in such a scenario? 
   1. Think about a network of people working in communication to build a list (of which they all retain an individual copy) who choose to accept only list entries with PoW. Does PoW enable anything useful in this scenario?
   1. In both cases the PoW demonstrates that work has been performed - that energy has been expended. In the second case, this verifiable work performed/energy expended/cost paid can be used to ensure that the network of people come to agreement on the list state. In the second case, this verifiable work performed/energy expended/cost paid brings finality/weight to state of the list. This is an ossifying or preserving effect on older (not by time but by work) entries of the list as entries are "buried under more work". The only way to modify entries, once buried, is to dig them up and rebury them deeper (VERY HARD - unless you have more shovels than the rest of the people who keep piling on more work). In the second case it also can be used to ensure that the network of people come to agreement on the list state.   
5. Build a Network which maintains the Chain of Hashed Messages (the second case from above)
6. Application to Money: What should the messages be? Transaction lists! (Blocks) -> Ordered list of transactions (Ordered chain of blocks - HOLY COW. Did he just explain blockchain without using the word blockchain?)


Require that for any message to be valid that it carry with it a valid Proof of Work. What is Proof of Work? It’s exactly what it sounds like. It is a proof that a certain amount of physical work has been done. A freshly mowed lawn or Thanksgiving table is proof that some amount of work has been performed. My message, “Hey Dad, I mowed the lawn today,” is easily verified by him looking out the window and seeing a pristine lawn. We can however construct another proof of work better suited towards building a digital money by exploiting the random nature of the cryptographic hash function mentioned previously.  

It is better suited since it lets us pass on the work to the computers. In place of human time, we use compute time. But because computers require energy to function, compute time is still tied to the physical world.

Consider a hash function with a 2 bit output space. In other words, all inputs are mapped to one of 4 values: 00, 01, 10, or 11. Notice that we have 2^2 = 4 possible outputs and that half of these begin with a zero and exactly a quarter begin with two zeroes. Expand the hash function output space to 3 bits. Now we have 2^3 = 8 outputs as follows: 000, 001, 010, 011, 100, 101, 110, 111. Again, half of these outputs begin with zero and exactly a quarter begin with two zeroes. Now imagine an N bit output space. This contains 2^N possible values, exactly half of which have a leading zero. Exactly a quarter of which have 2 leading zeroes. Exactly one eighth have 3 leading zeroes and so on. 

Our proof of work can take the form of requiring that, for a message to be valid, we produce a message whose hash output/digest contains some specified number (call it X) of leading zeroes. The greater X, the more difficult this problem becomes. We are using a function that gives output randomly distributed across its output space and restricting the number of outputs we will accept as being valid. Naturally the further we restrict this output space the more work (energy) will be required to produce a valid message (other things equal). Important also is that X is a tunable parameter which can be adjusted to set the difficulty at wherever we require. 

We can liken this scenario to throwing darts at a dart board and requiring that only a bullseye is valid. The output space of the hash function is the dart board. The smaller the size of the bullseye (the more leading zeroes), the more work will be required to produce a bullseye. This is more of a Proof of Skill perhaps, but maybe more skill == more work?? 

This frames our proof of work as a ***search*** for a hash output for our message which satisifies a specified difficulty requirement. QUESTION: Who specifies the difficulty requirement? What can we do with the ability to prove work? We can achieve consensus on state amongst participants of a global network. That is, we can get them to agree on the state of the system, however we define it.

The hash H(m) of a message m is deterministic (ie: hashing the same data twice yields the same result. The hash is randomly distributed across the output space but the hash of a specific message is a specific value. The distribution of outputs is random. The mapping of inputs to outputs is not random.). In order to calculate hashes of a message repeatedly until we successfully find a hash which satisfies our Proof of Work criterion outlined above, we need to introduce some malleability to our message. That is, we need to slightly modify our message, m, such that we can calculate a new hash `h' = H(m')` This is achieved by adding a number to the end of the message and recalculating the hash of the new message. This number is known as a nonce (number used only once) and it is the source of malleability for our messages which we increment until we can find a hash we consider to be a valid Proof of Work.

The work performed here can be verified by providing the message (including the nonce) and it's hash digest with specified number of leading 0s. The verifier then performs the hash operation on the message himself and confirms that his calculated hash matches the one prover provided.

NOTE: This form of Proof of Work is actually very efficient in the sense the time to verify any amount of work does not depend on the amount of work being verified. Whether verifying 10 or 10 trillion hashes, verification time remains constant, requiring only a single SHA-256 hash operation. Going back to our freshly mowed lawn example, this would be equivalent to saying that it would take the same amount of time to confirm that work was completed whether you are checking someone's work after they mowed your backyard or every football stadium in America. Clearly it would take much longer to verify that every grass football stadium in the country has freshly cut grass!


# The Purpose of Proof of Work \[in Bitcoin\]

In order to understand the value proposition of Proof of Work we must understand both what it is and what it brings to a network. 

Goal: Our goal is to enable participants in a large geographically distributed network to reach the same conclusion about the state of the system. The state of our system is a ledger of transactions. To agree on the state of this system is to agree on who owns what (see above). In other words, we want the people/machines in our society/network to reach consensus. Our messages are called blocks and they contain nothing more than lists of transactions.

Notes on Audience:
-	Assume that they have basic understanding/familiarity with hash functions

Open up your favorite word processing software, highlight the entirety of this blog post, press *CTRL-V* followed by *CTRL-P* in the blank document.  Great, now how much did that cost you? Such a cost is so inconsequential that you most certainly have never even paused to consider it. Technically it would cost however much energy your computer battery loses as a result of the copy operation multiplied by your cost of energy, but this is so small that it's not even worth considering. Proliferation of digital information is incredibly cheap (this is one reason the computers and the Internet are so useful), but if your aim is to construct a digital system of global money, this ease of duplication is disastrous. (Expand here … network enforced digital scarcity).

Our goal is to enable participants in a network to arrive at the same set of ordered messages. To agree on the set of messages is to agree on the state of the system. In the context of a transaction ledger, to agree on the state of the system is to agree on who owns what. If a global network can come to agree on who owns what, you have the basis for a decentralized global money, in an open (anyone can join) environment without trust. 

```
How do participants in the network agree on the state of the list?
How do participants in the network arrive at the same view on the state of the list?
How do they come to consensus on the state of the list? 
Answer: Proof of Work
```

How do we achieve this goal? 
- Require that for any message to be valid that it carry with it a valid Proof of Work.
- Establish a rule that all network participants accept the chain of hashed messages with the greatest total Proof of Work (the highest energy chain).


{ INSERT DEFINITION OF PROOF OF WORK - Consolidated from section above }


***Proof of Work imposes a cost to changing the system state and provides a way to efficiently (constant time – does not depend on the size of the cost proved) prove that cost has been paid. By requiring that nodes build on the chain of messages with the most Proof of Work (the highest energy chain) we ensure that nodes only build/work for the chain which represents the energy of the largest network.

Proof of Work ties the digital back to the physical. It gives a block physical weight. It allows any verifier to be assured that some physical work has been performed. The production of this message has X amount of energy associated with it. There is now a tangible cost to creating these messages where before there was not (recall digital messages are incredibly cheap to create). Why is this physical weight and the fact that there is a cost to produce these messages important? What does it enable us to do? 

First of all it rate limits the creation of new messages. The rate of valid updates to the system state must be limited at the very least so as to allow time for information to propagate to the network participants. Without this the system would be a jumbled mess. There would be no reaching global consensus as network nodes would all be looking at different information and have no hope at possibly reaching the same view. When you have a centralized system, the bottleneck is simply how fast you can process updates to system state (raw processing power). As your system becomes more distributed, bandwidth/information propogation speed and coordination of processing become increasingly prominent factors. 

Second, by connecting the digital back to the physical, Proof of Work provides us with a way to secure the network. Proof of Work is about achieving consensus. The cost it imposes is the very thing which allows everybody share the same view of the system state - to achieve consensus. Achieving consensus is securing the network. An unsecure system state is one subject to unauthorized unilateral change. 

   >*Said simply, Proof of Work allows us to agree on what Bitcoin is, and by doing so makes Bitcoin unforgeable.*

In an open network where particpants are pseudonymous and able to join and leave at will, how does one differentiate between candidate states? If anyone can propose their own state, what is to make one state more valid than any other?

Any individual network participant can create or accept whatever view of the system they want. Can they convince others that their view of the system state is correct? If we define "correct" as the system state with the greatest work (highest energy) then the answer is "No". Consider a dishonest network participant who creates his own set of ordered messages (his own state) favorable to himself. In the absence of Proof of Work, the validity of his system state is indistinguishable from any other. He can present his system state to another network participant and, in the absence of additional information, they will be unable to discern the validity of the candidate states. They will have to find different criteria on which to assess competing states. A metric for determining validity is needed.

What does it mean for a system state to be "correct"? What is to make one state more valid than any another? In systems with a central Authority, the correct state is determined by that Authority - the state proposed by your Bank is the valid state. In a pseudonymous distributed network of state maintainers we use work/energy. Valid states must carry Proof of Work. The most valid states carry Proof of the most Work.

   >*Valid states must carry Proof of Work. The most valid states carry Proof of the **most** Work*.

This requirement enables consensus. Given two competing views of the system state, a network participant can always select the system state endorsed by greater work. Dishonest participants are unable to present valid alternative states as they cannot forge energy (Szabo's "unforgeable costliness"). Perhaps ***Proof of Energy Expenditure*** would better describe the mechanism here. So long as one party does not control a majority of the energy in the system, they cannot convince network participants to accept any system state other than the system state constructed by the most energetic cohort of network participants. They cannot forge Bitcoin. They cannot ["double spend"](https://en.wikipedia.org/wiki/Double-spending) Bitcoin. Proof of Work turns the dishonest network views/false system states of would be usurpers into harmless individual delusions. To dishonest Bitcoin Network participants: For full credit (state acceptance), prove your work!

By constructing a system of open pseudonymous distributed with Proof of Work, Bitcoin achieves ***decentralized authority***. Allowing you to have faith that what you send and receive is valid without placing trust in any institution.

Proof of Energy Expenditure no doubt opens the consensus mechanism up to critique by those concerned with its effect on the climate. First, it should be noted that effective use of energy is the only thing separating you from a caveman sitting in his cold dark cave. It is the only reason our society is left standing amongst the countless societes and methods of human organization which came before us. The use of energy is not inherently evil. Nevertheless, it is reasonable to ask questions about what sources of energy are used and for what purpose. After reading this article you hopefully better understand the purpose... how and why energy is utilized in Bitcoin? in that PoW enables groups of people to build consistent lists in parallel. Take the journey further down the rabbit hole by digging into questions like:
- What is money?
- How does our current money work?
- What are the consequences of such a system of money?
- What other systems or institutions , methods of human organization exist to support such a system (legal, military)?

One cannot really say anything meaninful about Bitcoin's utilization of energy without attempting to grapple with the questions posed above. To do so would be little more than disingenuous emotional postulating. After having explored these, one is better equipped to understand the energy source and to make his/her own judgement as to the worth of the consumption of this source for this purpose. Link to Nic Carter, Fidelity Bitcoin Mining Report w/ Energy Composition, Bitcoin finding "stranded energy", etc.

\[ Section on State Ossification/Preservation ]

Builds an energy wall securing the historic state

## More Information

For the above explanation to make sense, the reader must understand that... Every Bitcoin network participant maintains their own list of transactions (his own state). This list of transactions, or ledger, is constructed and stored in a highly specified way designed to ensure immunity to forgery and ex-post facto data corruption and is known as a blockchain/timechain. An individual storing data in blockchain form is not special. The great power of such a storage mechanism emerges when independently verified copies of the transaction list in blockchain form are maintained by a collection of people distributed geographically - ala by a network of computers - who are able to come to agreement on one common vision of history. This is not merely data replication from a single trusted source (akin to data backup). It is independent verification that newly created data adheres to a set of agreed upon rules (law). **Information is shared. Information verification is independent.** (Don't Trust. Verify.). In such a system, each network participant is in constant communication with his peers, sharing new information (candidate state updates) he has learned and working to update his own state. We wish for each network participant's state to agree with all other network participants' states. That is, we aim to achieve consensus. This background will help the reader understand that any network participant could, in theory, create whatever state he desired (it is just a list of transactions after all), share it with his peers, and attempt to get them to adopt it as their own. Obviously if he was successfull in doing this, his state would be come the de-facto state of the network. (Unlike historical systems or institutions constructed by man) His authority to propose such a state and its correctness in the eyes of his fellow partipants does not come from wealth, political connectedness, or birthright. It instead comes from work and energy expenditure, a cost he proves paid each time he updates the state (collective). This is not a cost paid in isolation. It is a cost paid in the context of everyone attempting to solve the same problem (this is tricky to explain - the difficulty of any one state proposer to "find" a valid proof of work for the state update he is proposing, is not fixed. That is, the amount of work he is proving is not constant - difficulty adjusts but even that isn't quite what I'm trying to explain.). It is determined by the total... It is not as if all he has to do is pay some fixed cost to prove the validity of his state. It is not as if all he has to do is 2 hours of work or pay $100 to some rent seeking entity and his state shall be valid. The fact that I have a proof of work of a certain difficulty does not necessarily prove that I did all that work myself. It proves that I was part of a larger cohort of work doers who collectively completed that much work (This is a pretty incredible claim when I think about it - How does it do this? \*). The "work" completed isn't itself directly useful. It is, after all, nothing other than computing the hash digest of a message (that worker's candidate state update - a block). However, that is indirectly very useful as it is what allows us to achieve distributed/widespread consensus via decentralized emergent authority which, when used for keeping track of private property rights and securing the willful transfer of those rights, gives mankind the ability to... something very profound (Borrow language from Our Most Brilliant Idea - Robert Breedlove to finish this sentence. See Bitcoin Audible or Breedlove/Quittem Swan Signal Podcast). 

\* If the result of past work being demonstrated (proven) exceeds the quantity of work that the worker is physically capable of in the time period, then the worker must have had help. If I am proving that a new Great Pyramid of Giza has been constructed every 10 minutes, I clearly did not complete all this work myself. I instead relied upon a network of workers around the world, all pitching in toward a common goal of grandious construction. I am merely the humble presenter of our work's final product. In the context of Bitcoin, the miner with the Proof of Work for a given state update (block) is the humble presenter of the network's final product - a batch of fully validated and energy secured transactions transferring property amongst freely exchanging individuals. 

With the pyramid, I am showing you work that I am not capable of producing alone in the allotted time, so it is obvious that this is representative of the efforts of a larger group. With Bitcoin I am showing you a hash I produced but yet it is somehow indicative that a larger group of geographically distributed network participants completed more work than I myself am capable. How can this be? The random nature of finding proof of work satisfying the difficulty comes in here. My proof of work takes the form of finding a hash digest of my candidate state update (block) which satisfies a difficulty target. The difficulty target is set on a network wide basis by the Bitcoin software to an *expected* (probabalistic) 10 minutes of ***cumulative*** working power of the entire Bitcoin Network and adjusts upward or downward as the network gains or loses workers in raw number or efficiency (hash power). If the Bitcoin Network is capable of producing 1 billion hashes per minute, then the expected work required will be 10 billion hashes. The Bitcoin software will set the odds of pulling the rabbit from the hat (the network difficulty) at 1 in 10 billion. I may "find" a proof of work of the desired difficulty on my first attempt, or my 10 billionth, or even my 100 billionth. There is no memory or progress in this operation. The success of any given attempt is exactly as probable as any other, namely 1 in 10 billion. All you can be sure of is that my presenting you with a proof of work of a given difficulty, say 10 billion hash operations, likely took the network as a whole 10 billion attempts cumulatively to produce. The same way you would expect 2 friends each flipping 1 coin per second to take 10 seconds to flip 10 heads between them. The Bitcoin network is thousands of friends flipping quintillions of coins per second.

Another peculiar aspect of Bitcoin's use of Proof of Work is that proofs are said to be "found". I don't just prove my work. I find a proof of work. Moreover, that proof is testament to my work and the work of others. This process is described above and is referred to as **Mining**.

### The Purpose of Proof of Work \[ in Bitcoin]
The security of the Bitcoin network emerges from and relies upon 2 things: 
-	Proof of Work (Consensus)
-	Independent Verification. Network participants who live by the slogan “Don’t Trust. Verify”

Explain each of the above …
 
- With “Don’t Trust. Verify” but without Proof of Work, we would have a network which ensures that every message it’s participants propagate meets network defined requirements (authorized, no inflation, no double spend), but no way to ensure that every participant reaches the same view of the system state (no consensus).

- With Proof of Work but without “Don’t Trust. Verify”, we would have a network in which participants are able to reach consensus on the state of the system but are not able to say anything meaningful about whether the state is valid (as they would be verifying work only and trusting that messages are valid).

Put the above two concepts together and we can build a network which reaches consensus on the state of the system and that state will be valid as defined by a set of agreed upon rules.
 
-	State is valid because it adheres to a set of rules (called Consensus Rules)
-	One of those rules is that the state carries Proof of Work

If one of those "consensus" or system rules specifies that all Bitcoin denominations must end in 0.615, then our state that we come to consensus on will contain only Bitcoin denominations ending in 0.615. If one of those "consensus" or system rules specifies that there be no more than 21 million Bitcoin, then our state that we come to consensus on will contain no more than 21 million Bitcoin. (Link code sections which handle block subsidy and no inflation)

[Consensus Code](https://github.com/bitcoin/bitcoin/tree/master/src/consensus)
- [Proof of Work Verification](https://github.com/bitcoin/bitcoin/blob/0.20/src/validation.cpp#L3273)
- [No Inflation](https://github.com/bitcoin/bitcoin/blob/0.20/src/consensus/tx_verify.cpp#L187)
- [Block Subsidy Definition](https://github.com/bitcoin/bitcoin/blob/0.20/src/validation.cpp#L1220)
- [Subsidy Enforcement](https://github.com/bitcoin/bitcoin/blob/0.20/src/validation.cpp#L2159)
- [Difficulty Adjustment]()


### On Running a Bitcoin Node and Participating in a New World Monetary System
When you start running your own Bitcoin node you aren’t some gullible financial system participant blindly trusting the authority of a centralized financial coordinator to maintain your purchasing power. You are instead a ruthless verifier, scrutinizing the validity of all transactions in agonizing detail. When you run the Bitcoin software you instantly become a member of the best auditing firm in the world. When you arrive at the current state, you can be sure that it is valid as you have ensured so yourself. When you run the Bitcoin software ...

You join a network of those similarly dedicated to building a network for communicating value globally. (NOTE: Remember to pitch this in a way that recognizes you should run a full node for yourself, NOT for the good of the network. People respond to individual incentives. You cannot rely on people sacrificing themselves for the good of a group/commons/etc).

Working to maintain a historical record of all transactions. It is from such a record/ledger which we can build a monetary system which transcends jurisdiction and, as a result, is not possibly beholden to the interest of any one individual, corporation, or even nation.

Attempts to create money out of nothing are not recognized. Attempts to move money without proper authorization? Not recognized. This is ***Network Enforced Digital Scarcity***. This is, for the first time in modern history, a separation of money and state.


How can you trust the messages you are being sent? With. Proof of Work generates emergent authority. Authority in the absence of authority.
 

## Additional Items 

   A short story: The traveler happened upon a group of people. These people are working very intensely. The traveler observed as they piled dirt shovelful by shovelful into a a glorious mound. A mound larger than any he had ever seen before. The people worked day and night, rain or shine. Not once did they break - Not even to enjoy one of life's many pleasures. The traveler had wandered many a place near and far, but he had never seen anything like this. He simply could not contain the urge to figure out just what it was which compelled the people to work so hard. "What are you burying?", you ask. "We're burying our most prized posessions". "We're burying our life's work". The lives' work of an entire group of people buried in this hole? Crazy! 
   The mound grew higher just when you thought surely the mound, it grew higher still. A magnificent testiment to the work of these men
   Another traveler. The traveler was cunning and quick. He figured . No matter how hard the traveler and his team tried, they simply could not undo
   The cost to not be on the winning team? Death.
   The use of computers prevent the securing of the network from having to be any ones life work. Human time is replaced with Compute time, but both require energy.
   A third, heat-exhausted, near delirious traveler happened by the workers. As he drew closer he noticed they all had the letter B emblazoned in orange on their chests. And they weren't people at all, but computers? They weren't building a large mound, but rather a list of transactions which outlined the ownership and transfer of ownership of some item amongst them. A most strange hallucination, he thought.
   

A network that is global, open, neutral, censorship resistant. A monetary system that does not recognize. The most liquid scarcity is digital scarcity.
As a result of being geographically distributed we have… the participants do not reside in one legal jurisdiction and. Transcends jurisdiction

Maintaining monetary sovereignty 


You wish to define a set of rules that participants are to abide by. You can check that these rules are being followed, and so will everyone else.

You cannot stop someone from writing numbers on a piece of paper. Likewise you cannot stop someone from storing a string of bits in their computer memory. You cannot stop someone from from sharing these numbers with others. I can not stop you from writing your next blog post. What is non-physical is also non-rivalrous. Information is not physical. Information is only scarce in the absense of communication. Information is as abundant as knowledge and commmunication permit. My possession of information does not preclude you from having the same information (unless I wont share the information with you :) ). You accept the numbers written on green pieces of paper with pictures of our Founding Fathers because you recognize the Authority of the institution which wrote the number. Usually this Authority is backed by a legal or commonly accepted monopoly on force (that is permission to enforce law with threat of violence). In Bitcoin, there is no authority writing the number. There are only numbers endorsed by energy. 


Why do people choose to provide energy to securing this system? They provide energy because they are paid to do so. Bitcoin supply is created. As the price of Bitcoin rises, so does the mining reward. This drives more competition to provide energy to secure the system. The more secure system could drive additional adoption. Bitcoin pays for its own security. a positive feedback loop which incentivizes its own protection. Bitcoin is "issued" NOT from a Central Mint. It is more proper to say, that supply inflation/the issuance of new Bitcoin is only recognized in return for providing energy to the system. If Amazon provides the same product at 10% lower cost than you, they will likely win all or at least an overwhelming majority of exchanges. Bitcoin mining dynamics are not winner take all. If you have a smal

Proof of Work
- What
- Why
  - enables consensus
  - state preservation/ossification - secure information. secure the past. 
  how do you know you dont need to start over? You don't need to go back and learn how to add because you remember! How do we know the work we did yesterday remains?
- How
  - rate limits acceptance of new information
  - ties digital to physical. What does this actually mean at its core? prevents costless alteration? In a world where we want to do things as cheaply as possible why would we select such system of explicit cost. The answer is because the enemy you know is better than the enemy you dont. Our current system of money as enormous cost, a great deal of which is implicit/obfuscated. We must have cost to have security. We are looking to make something digital hard to acquire. You cannot copy Bitcoin. The value is in a consistent and verifiable ledger. You can copy the list of numbers and how they change over time transactions. Why does any one list of transactions have meaning? Because we know its the list we started working on 10 years ago, we know nobody has changed any part of the list (our work was done and our work remains), we know new additions to the list follow the laws agreed to by everyone (work continues).
  - metric of differentiation. PoW is the Authority.
- Who
  - list builders for list validators
- When
 - 24/7

How do you quantify demand? How to you quantify human desire? The market price. Historically the market price of a good has been a function of both the supply and demand for that good. With Bitcoin the supply is known to market particpants and is unchanging. Do movements in its price reflect only changes in demand?
Value created in the production of commodities channels additional capital into the production of that commodity. 
Value created/profit received in the creation of Bitcoin channels capital into production of additional network security, NOT additional Bitcoin. Such is the beauty of the difficulty adjustment.
