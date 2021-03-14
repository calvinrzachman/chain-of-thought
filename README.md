# chain-of-thought
A collection of ideas and writings on topics in the crypto space

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

Bitcoin is many different things to different people. For some, Bitcoin is hope, for others Bitcoin is freedom (link to Alex Gladstein), yet others still - Bitcoin is Time (Gigi)/Venice (lol). Metaphor and philosophical hot takes aside, for the purposes of this summary Bitcoin is two things: Bitcoin is a software protocol which forms the basis of a global, censorship resistant, monetary settlement network, and the accounting unit native to the ledger that software protocol maintains. The former concerns what is owned, while the latter concerns the system which enables digital scarcity and ownership without central authority in the first place. 

When you own a Bitcoin, what do you actually own? 

Bitcoin the emerging monetary commodity, “a bitcoin”, is a number stored in a ledger (list). However, it is a number stored in a very specific and special kind of ledger - one unlike any you have encountered before.
A ledger with truly unique properties.

When you own Bitcoin, you have knowledge of a piece of information, usually just a large random number called a private key, which can be used to update the ledger and transfer the number to control by a different key. This is not categorically different from how our current system works.



Bitcoin is an entry in a ledger that ONLY you can control, and you can do so WITHOUT anyone’s permission.

The Bitcoin Network is a collection of individuals, each maintaining their own ledger and enforcing a set of agreed upon rules encoded in software, their support for which is expressed in their electing to run the software under their own free will. The Bitcoin software is available for free on the Internet and is fully observable by anyone with the ability to read the C++ reference implementation. When you run the software and plug in to the Bitcoin Network, you aren’t some gullible financial system participant blindly trusting the authority of a centralized financial coordinator to maintain (with) your purchasing power. You are instead a ruthless verifier, scrutinizing the validity of all transactions in agonizing detail. When you run the Bitcoin software you instantly become a member of the best auditing firm in the world. [When you arrive at the current state, you can be sure that it is valid as you have ensured so yourself.] When you receive Bitcoin you can rest assured that it is authentic as you have verified this history yourself.

When you run the Bitcoin software you join all others who do the same, working to build and preserve a historical record of transactions. It is from such a record which we can build a monetary system which transcends jurisdiction and is, as a result, not possibly beholden to the interest of any one individual, corporation, or even nation. Attempts to create money out of nothing are not recognized. Attempts to move money without proper authorization. Not recognized. This is network enforced digital scarcity. This is, for the first time in modern history, a separation of money and state.

So we have Bitcoin, the network, and bitcoin, the asset.

Alternative Hot Takes:
Bitcoin is cash over TCP/IP
Bitcoin is a property right that does not require the State and it’s legal monopoly on violence to enforce ownership. 
Bitcoin is absolute scarcity.
Bitcoin is digital real estate.
Bitcoin is digital gold.
Bitcoin is information.
Bitcoin is Venice (lol).

KEY QUESTIONS: 
- How does Bitcoin build a ledger? 
- How are you able to interact with the system without asking permission?

Bitcoin is a software protocol for cooperatively building lists/ledgers in a low trust environment. 
Bitcoin is a software protocol for cooperative list building, and that list has come to be known as a blockchain.
Bitcoin is a number in a ledger.

So what does Bitcoin’s ledger look like? How is it built and what unique properties does it have?
In other words, where do Bitcoin’s censorship resistance and scarcity properties come from?

The unique properties do NOT come from the ledger alone, but from the ledger and the network of people which maintain it.





## Further Reading
- Grokking Bitcoin. Kalle Rosenbaum 
- Inventing Bitcoin. Yan Pritzker
- Internet of Money - Andreas Antonopoulos
- Mastering Bitcoin - Andreas Antonopoulos (technical)
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
- [Bitcoin is Time](https://dergigi.com/2021/01/14/bitcoin-is-time/) - Dergigi
- Bitcoin Audible Podcast - Guy Swann (most of these articles are available in audio format here)
- Stefan Livera Podcast
