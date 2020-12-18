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
