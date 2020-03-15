# Proof of Work

Require that for any message to be valid that it carry with it a valid Proof of Work. What is Proof of Work? It’s exactly what it sounds like. It is a proof that a certain amount of physical work has been done. A freshly mowed lawn or Thanksgiving table is proof that some amount of work has been performed. My message “Hey dad I mowed the lawn today” is easily verified by him looking out the window and seeing a pristine lawn. We can however construct another proof of work better suited towards building a digital money by exploiting the random nature of the cryptographic hash function mentioned previously.  

It is better suited since it lets us pass on the work to the computers. In place of human time, we use compute time. But because computers require energy to function, compute time is still tied to the physical world.

Consider a hash function with a 2 bit output space. In other words, all inputs are mapped to one of 4 values: 00, 01, 10, or 11. Notice that we have 2^2 = 4 possible outputs and that half of these begin with a zero and exactly a quarter begin with two zeroes. Expand the hash function output space to 3 bits. Now we have 2^3 = 8 outputs as follows: 000, 001, 010, 011, 100, 101, 110, 111. Again, half of these outputs begin with zero and exactly a quarter begin with two zeroes. Imagine an N bit output space. This contains 2^N possible values, exactly half of which have a leading zero. Exactly a quarter of which have 2 leading zeroes. Exactly one eighth have 3 leading zeroes and so on. 

Our proof of work can take the form of requiring that, for a message to be valid, we produce a message whose hash output contains X number of leading zeroes. The greater X the more difficult this problem becomes. We are using a function that gives output randomly distributed across its output space and restricting the number of outputs we will accept as being valid. Naturally the further we restrict this output space the more work will be required to produce a valid message. Important also is that X is a tunable parameter which can be adjusted to set the difficulty at wherever we require. 

We can liken this scenario to throwing darts at a dart board and requiring that only a bullseye is valid. The output space of the hash function is the dart board. The smaller the size of the bullseye (the more leading zeroes) the more work will be required to produce a bullseye. This is more of a Proof of Skill perhaps, but maybe Skill == more work?? 

What can we do with the ability to prove work? We can achieve consensus on state amongst participants of a global network. That is, we can get them to agree on the state of the system however we define it.


NOTE: This form of proof of work is actually very efficient in the sense the time to verify any amount of work does not depend on the amount of work being verified. Whether verifying 10 or 10 trillion hashes, verification time remains constant, requiring only a single SHA-256 hash operation


# The Value of Proof of Work

In order to understand the value proposition of Proof of Work we must understand both what it is and what it brings to a network. 

Goal: Our goal is to enable participants in a large geographically distributed network to reach the same conclusion about the state of the system. The state of our system is a ledger of transactions. To agree on the state of this system is to agree on who owns what (see above). In other words, we want the people/machines in our society/network to reach consensus. 
Our messages are called blocks and they contain nothing more than lists of transactions.

Notes on Audience:
-	Assume that they have basic understanding/familiarity with hash functions

Open up your favorite word processing software, highlight the entirety of this blog post, press control V followed by control P in the blank document.  Great, now how much did that cost you? 
Proliferation of digital information is incredibly cheap (this is one reason the computers and the internet are so useful), but if your aim is to construct a digital system of global money this ease of duplication is disastrous. (Expand here … network enforced digital scarcity) Proof of Work

Our goal is to enable participants in a network to arrive the same set of ordered messages. To agree on the set of messages is to agree on the state of the system. In the context of a transaction ledger, to agree on the state of the system is to agree on who owns what. If a global network can come to agree on who owns what, you have the basis for a decentralized global money. In an open (anyone can join) environment without trust. 

How does it achieve this goal? Establish a rule that all network participants accept the chain of hashed messages with the greatest total proof of work (the highest energy chain). In some sense this states that the valid chain is always the highest cost chain 

***Proof of Work imposes a cost to changing the system state and provides a way to efficiently (constant time – does not depend on the size of the cost proved) prove that cost has been paid. By requiring that nodes build on the chain of messages with the most proof of work (the highest energy chain) we ensure that nodes only build/work for the chain which represents the energy of the largest network.


Proof of Work ties the digital back to the physical. It gives a block physical weight. It allows any verifier to be assured that some physical work has been performed. The production of this message has X amount of physical work associated with it. There is now a tangible cost to creating these messages where before there was not (digital messages are incredibly cheap to create). Why is this physical weight and the fact that there is a cost to produce these messages important? What does it enable us to do? 

Proof of Work is about achieving consensus. This cost is the very thing which allows us to have everybody share the same view of the system state. To achieve consensus.

First of all it rate limits the creation of new messages. The rate of valid updates to the system state must be limited at the very least so as to allow time for information to propagate to the network participants. Without this the system would be a jumbled mess and there would be no hope of ever reaching global consensus as network nodes would all be looking at different information and have no hope at possibly reaching the same view. 

Second, by connecting the digital back to the physical, proof of work provides us with a way to secure the network. 

