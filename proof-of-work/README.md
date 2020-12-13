# Proof of Work

## Prerequisites

- Hash Functions
- Hashed Messages
- Chain of Hashed Messages

Require that for any message to be valid that it carry with it a valid Proof of Work. What is Proof of Work? It’s exactly what it sounds like. It is a proof that a certain amount of physical work has been done. A freshly mowed lawn or Thanksgiving table is proof that some amount of work has been performed. My message, “Hey Dad, I mowed the lawn today,” is easily verified by him looking out the window and seeing a pristine lawn. We can however construct another proof of work better suited towards building a digital money by exploiting the random nature of the cryptographic hash function mentioned previously.  

It is better suited since it lets us pass on the work to the computers. In place of human time, we use compute time. But because computers require energy to function, compute time is still tied to the physical world.

Consider a hash function with a 2 bit output space. In other words, all inputs are mapped to one of 4 values: 00, 01, 10, or 11. Notice that we have 2^2 = 4 possible outputs and that half of these begin with a zero and exactly a quarter begin with two zeroes. Expand the hash function output space to 3 bits. Now we have 2^3 = 8 outputs as follows: 000, 001, 010, 011, 100, 101, 110, 111. Again, half of these outputs begin with zero and exactly a quarter begin with two zeroes. Imagine an N bit output space. This contains 2^N possible values, exactly half of which have a leading zero. Exactly a quarter of which have 2 leading zeroes. Exactly one eighth have 3 leading zeroes and so on. 

Our proof of work can take the form of requiring that, for a message to be valid, we produce a message whose hash output contains X number of leading zeroes. The greater X, the more difficult this problem becomes. We are using a function that gives output randomly distributed across its output space and restricting the number of outputs we will accept as being valid. Naturally the further we restrict this output space the more work (energy) will be required to produce a valid message (other things equal). Important also is that X is a tunable parameter which can be adjusted to set the difficulty at wherever we require. 

We can liken this scenario to throwing darts at a dart board and requiring that only a bullseye is valid. The output space of the hash function is the dart board. The smaller the size of the bullseye (the more leading zeroes), the more work will be required to produce a bullseye. This is more of a Proof of Skill perhaps, but maybe more skill == more work?? 

What can we do with the ability to prove work? We can achieve consensus on state amongst participants of a global network. That is, we can get them to agree on the state of the system however we define it.

The hash H(m) of a message m is deterministic (ie: non-random). In order to calculate hashes of a message repeatedly until we successfully find a hash which satisfies our Proof of Work criterion outlined above, we need to introduce some malleability to our message. That is we need to slightly modify our message, m, such that we can calculate a new hash `h' = H(m')` This is achieved by adding a number to the end of the message and recalculating the hash of the new message. This number is known as a nonce (number used only once) and it is the source of malleability for our messages which we increment until we can find a hash we consider to be a valid Proof of Work.

NOTE: This form of Proof of Work is actually very efficient in the sense the time to verify any amount of work does not depend on the amount of work being verified. Whether verifying 10 or 10 trillion hashes, verification time remains constant, requiring only a single SHA-256 hash operation. Going back to our freshly mowed lawn example, this would be equivalent to saying that it would take the same amount of time to confirm that work was completed whether you are checking someone's work after they mowed your backyard or every football stadium in America. Clearly it would take much longer to verify that every grass football stadium in the country has freshly cut grass!


# The Value of Proof of Work

In order to understand the value proposition of Proof of Work we must understand both what it is and what it brings to a network. 

Goal: Our goal is to enable participants in a large geographically distributed network to reach the same conclusion about the state of the system. The state of our system is a ledger of transactions. To agree on the state of this system is to agree on who owns what (see above). In other words, we want the people/machines in our society/network to reach consensus. Our messages are called blocks and they contain nothing more than lists of transactions.

Notes on Audience:
-	Assume that they have basic understanding/familiarity with hash functions

Open up your favorite word processing software, highlight the entirety of this blog post, press CTRL-V followed by CTRL-P in the blank document.  Great, now how much did that cost you? Proliferation of digital information is incredibly cheap (this is one reason the computers and the Internet are so useful), but if your aim is to construct a digital system of global money, this ease of duplication is disastrous. (Expand here … network enforced digital scarcity) Proof of Work

Our goal is to enable participants in a network to arrive at the same set of ordered messages. To agree on the set of messages is to agree on the state of the system. In the context of a transaction ledger, to agree on the state of the system is to agree on who owns what. If a global network can come to agree on who owns what, you have the basis for a decentralized global money, in an open (anyone can join) environment without trust. 

How do we achieve this goal? Establish a rule that all network participants accept the chain of hashed messages with the greatest total Proof of Work (the highest energy chain). In some sense this states that the valid chain is always the highest cost chain.

{ INSERT DEFINITION OF PROOF OF WORK - Consolidated from section above }

***Proof of Work imposes a cost to changing the system state and provides a way to efficiently (constant time – does not depend on the size of the cost proved) prove that cost has been paid. By requiring that nodes build on the chain of messages with the most Proof of Work (the highest energy chain) we ensure that nodes only build/work for the chain which represents the energy of the largest network.

Proof of Work ties the digital back to the physical. It gives a block physical weight. It allows any verifier to be assured that some physical work has been performed. The production of this message has X amount of energy associated with it. There is now a tangible cost to creating these messages where before there was not (recall digital messages are incredibly cheap to create). Why is this physical weight and the fact that there is a cost to produce these messages important? What does it enable us to do? 

First of all it rate limits the creation of new messages. The rate of valid updates to the system state must be limited at the very least so as to allow time for information to propagate to the network participants. Without this the system would be a jumbled mess. There would be no reaching global consensus as network nodes would all be looking at different information and have no hope at possibly reaching the same view. When you have a centralized system, the bottleneck is simply how fast you can process updates to system state (raw processing power). As your system becomes more distributed, bandwidth/information propogation speed and coordination of processing become increasingly prominent factors. 

Second, by connecting the digital back to the physical, Proof of Work provides us with a way to secure the network. Proof of Work is about achieving consensus. The cost it imposes is the very thing which allows everybody share the same view of the system state - to achieve consensus. Achieving consensus is securing the network. An unsecure system state is one subject to unauthorized unilateral change. 

Said simply, Proof of Work allows us to agree on what Bitcoin is, and by doing so makes Bitcoin unforgeable.

In an open network where particpants are pseudonymous and able to join and leave at will, how does one differentiate between candidate states? If anyone can propose their own state

***KEY QUESTION: What is to make one state more valid than any other?***

Any individual network participant can create or accept whatever view of the system they want. Can they convince others that their view of the system state is correct? If we define "correct" as the system state with the greatest work (highest energy) then the answer is "No". Consider a dishonest network participant who creates his own set of ordered messages (his own state) favorable to himself. In the absence of Proof of Work, his system state is indistinguishable from any other. He can present his system state to another network participant and, in the absence of additional information, they will be unable to discern the validity of the candidate states. They will have to find different criteria on which to assess competing states. 

What does it mean for a system state to be "correct"? What is to make one state more valid than any another? In systems with a central Authority, the correct state is determined by that Authority - the state proposed by your Bank is the valid state. In a pseudonymous distributed network of state maintainers we use work/energy. *Valid states must carry Proof of Work. The most valid states carry Proof of the **most** Work*. This requirement enables consensus.

Given two competing views of the system state, a network particpant can always select the system state endorsed by greater work. Dishonest participants are unable to present valid alternative states as they cannot forge energy (Szabo's "unforgeable costliness"). Perhaps ***Proof of Energy Expenditure*** would better describe the mechanism here. So long as one party does not control a majority of the energy in the system, they cannot convince network participants to accept any system state other than the system state constructed by the most energetic cohort of network participants. They cannot forge Bitcoin. They cannot "double spend" (link to definition) Bitcoin. Proof of Work turns the dishonest network views/false system states of would be usurpers into harmless individual delusions. To dishonest Bitcoin Network participants: For full credit (state acceptance), prove your work!

By constructing a system of open pseudonymous distributed with Proof of Work, Bitcoin achieves ***decentralized authority***. Allowing you to have faith that what you send and receive is valid

You cannot stop someone from writing numbers on a piece of paper. Likewise you cannot stop someone from storing a string of bits in their computer memory. You accept the numbers written on green pieces of paper with pictures of our Founding Fathers because recognize the Authority of the institution which wrote the number. Usually this Authority is backed by a legal or commonly accepted monopoly on force (that is permission to enforce law with threat of violence)

Proof of Energy Expenditure no doubt opens the consensus mechanism up to critique by those concerned with its effect on the Climate. First, it should be noted that effective use of energy is the only thing separating you from a caveman sitting in his cold dark cave. The use of energy is not inherently bad. Nevertheless, it is reasonable to ask questions about what sources of energy are used and for what purpose. After reading this article you hopefully understand the purpose. All that's left is to understand the source. Link to Nic Carter, Fidelity Bitcoin Mining Report w/ Energy Composition, Bitcoin finding "stranded energy", etc.

