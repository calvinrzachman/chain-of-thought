# chain-of-thought
A collection of ideas and writings on topics in the crypto space

This repository is intended to be a drafting space writing. Upcoming topics include:
- Proof of Work
- How Does Lightning Network Scale? (Global vs Local state/information)
  - Lightweight money substitutes/proxy (paper receipts with claim on gold vs. valid transaction which spend from multi-sig UTXO)

## Understanding Bitcoin
1. hash function
2. data serialization and hashed messages
3. chain of hashed messages (imposes an order to the messages)
4. chain of hashed messages with proof of work (ties digital to physical. Brings finality/weight to system state)

    Require that for any message to be valid that it carry with it a valid Proof of Work. What is Proof of Work? It’s exactly  what it sounds like. It is a proof that a certain amount of physical work has been done. A freshly mowed lawn or Thanksgiving table is proof that some amount of work has been performed. My message “Hey dad I mowed the lawn today” is easily verified by him looking out the window and seeing a pristine lawn. We can however construct another proof of work better suited towards building a digital money by exploiting the random nature of the cryptographic hash function mentioned previously.

It is better suited since it lets us pass on the work to the computers. In place of human time, we use compute time. But because computers require energy to function, compute time is still tied to the physical world.


5. build a Network which maintains the hashed chain of messages
6. application to currency: What should the messages be? Transactions lists! (Blocks) -> Ordered list of transactions (Ordered chain of blocks)
