# Private Lightning Network Gossip

Lightning Network gossip protocol is the process by which we dynamically expand our network graph used for routing!! A lighning node receives & validates gossip messages, dynamically updating its routing information base (RIB), aka routing graph.

Presently a [channel announcement]() points ***directly*** to the UTXO which funds it.
- This is bad for privacy as it allows network observers to associate UTXO with persistent network identifiers (LN Node ID).
- This is good for spam prevention/anti-DOS as you must have funds in order to send channel announcment messages.
- Moreover, the amount/capacity advertised is ***EXACTLY*** the capacity owned (ie: no credit/inflation), because the mapping from channel to UTXO is explicit.
- Verifiers (LN Nodes) can enforce that channel gossip accurately reflects on chain capacity.

GOAL: We would like to remove the mapping from channel to UTXO while retaining the ability to enforce a direct link between advertised and on-chain capacity. In this way we preserve privacy without opening up new attack vectors.

QUESTION: Is this even possible? Privacy preserving prevention of denial of service. https://reyify.com/blog/riddle#motivation

Adam Gibson's (JoinMarket) blog contains many interesting ideas some of which may be of use here: https://reyify.com/blog/little-riddle


## Initial Chain of Thought

```console
Current Gossip: Node ---> Channel ---> UTXO

Channel —> UTXO:
- Liquidity/capital exists (gossip DOS/spam prevention) and is claimed to be used in the LN protocol.
- Amount trivially verifiable. Nodes cannot advertise larger channels than they actually have the liquidity to backup.
- UTXO re-use trivially avoidable. A node cannot use UTXO A to as the funding capital for both channel A and channel B.
- Not ideal for privacy.

NOTE: It does not make any sense to spend time trying to obscure the association between node and channels (Node --X-> Channel). The ability to construct a routable network graph depends entirely on knowledge of a mapping between a node and its payment channels. 

Private Gossip: Node ---> Channel --X-> UTXO

Most specifically we require Channel ---> one out of a group of UTXOs. We do not know which UTXO specifically, but it is one which we know has not been used previously.
```

### Linkable Spontaneous Anonymity Groups (LSAG/UTXO Ring Signatures)

Monero has the idea of a *`key image`* which prevents double spending. What if we had a `*UTXO image*` to prevent liquidity reuse, "repledging", rehypothecation, fractional reserve lightning?

The key image is an alternate public key computed on a second base point, specifically Hp(P), instead of G. It is required in a traceable ring signature construction to ensure multiple signatures with the same real key are linked (and thus rejected by the Monero protocol). https://monero.stackexchange.com/a/2889


“One important thing to remember with that is if I have for example, as Monero does now, a ring containing 11 one-time-use keys and I'm spending one of those, I want to make sure that I can't use one of those keys in a future transaction and double spend. Remember a given one-time [UTXO Taproot Pub]key might appear in many different rings but it can only be spent [used as proof of channel funding liquidity] once. Every transaction has well you can kind of think of as like a one-way representation of the actual spending one-time key called the key image.”

“It's important to note that you cannot look at a transaction look at its key image which is completely out there and publicly posted and determine from that which of the ring members [UTXO Taproot Public keys] was used. However, if the person who made that transaction attempts to spend [use as proof of channel funding liquidity] the same you know Apriori unknown one time [UTXO Taproot Pub]key in a later transaction, they will share the same key image. The signature construction makes sure that when you're doing this you can't lie about how you constructed the key image mathematically, so it is an effective double spend protection. If you look at two transactions and if they have the same key image then you know that the exact same one time ring input was used as the sender in that although you ideally should not be able to determine which it is [though you can reject that gossip].” https://www.youtube.com/watch?v=6CVcirD90pg

“Monero ring signatures include a term in each hash commitment that deals with the key image. The construction is such that the signature proves both that you knew the private key for one of the ring members, and that you computed the key image for that ring member correctly. Alice can sign a transaction with ring ABC when she controls A, and Bob can sign a transaction with ring ABC when he controls B; the key images will be different. An outside observer can look at a key image and be assured that provided the signature validates and the key image was not used elsewhere in a valid signature, a double-spend did not occur on that chain.”

- Is requiring LN nodes to keep their own list of UTXO key images a non-starter?
- Is this protocol affected by address reuse? It could be that funds received to an address/key already used on LN would not be useful for opening channels as peers would drop your channel announcement since its key image would match a previously used key image.
- Is the requirement that the amounts in the UTXO-Taproot Key ring be the same a non-starter? How is the protocol affected by varying amounts in the key ring (at first glance negatively?

What are the consequences of a node not having a full key-image list?
- In Monero: It is unable to determine whether a transaction is double spending an output. Money can be spent more than once —> CRITICAL PROTOCOL FAILURE.
- In Lightning Network w/ UTXO-Taproot-PubKey images: It is unable to correctly identify a UTXO as having been reused in channel proofs and accepts channel gossip it should reject. Only in the case where nodes fail to keep UTXO key images stores do we recover the state where the same on chain capital can be used to gossip multiple channel edges. Otherwise we correctly accept only a single channel edge per UTXO key, and we do so without knowing what that UTXO key is. 

QUESTION: When presented with a key image I, how does one know that it was constructed properly using x and P?
ANSWER: https://monero.stackexchange.com/a/12390

- What happens when other UTXO in ring are spent?
- What happens when your UTXO is spent (channel close)? Can we shrink the UTXO image set? Can we prune the LN channel graph?

### Attacks

Under the current system I am not able to resuse the same funds to increase the size of the channel graph.
If I were to spend this 2/2 to a new 2/2 in an effort to increase the size of the channel graph, LN node's would notice that the funding output to the channel has been spent. They could then prune the old channel from the channel graph and add the new channel.