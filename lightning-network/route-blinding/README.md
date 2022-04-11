# Route Blinding

```console
“Route blinding is a lightweight technique to provide recipient anonymity by
blinding an arbitrary amount of hops at the end of an onion path. 
It's more flexible than rendezvous [routing] because it lets senders arbitrarily update
amounts and lock times, and reuse a blinded route multiple times (which is 
useful when retrying a failed route or using multi-part payments).”
```

Trying to wrap my head around the [`route blinding` proposal](https://github.com/lightning/bolts/pull/765) from t-bast. There are some subtleties which I do not feel like I completely understand yet. Below is an attempt to try and square what is going on in the proposal:

## Initial Chain of Thought

Typically Lightning Network routes are constructed entirely by the sender. The sender establishes a secret shared between itself and each intermediate hop in the route by way of ECDH between an ephemeral key (chosen by the sender for each hop in the route) and the hop’s persistent node ID public key, call it *`N(i)`*. Obviously this will not be possible if we wish to blind part of the route. With route blinding the sender instead does ECDH with the blinded node ID key, *`B(i)`*?? Intermediate hops are able to calculate the private key for this blinded node ID key, so it can still be used to establish a shared secret with the sender. NOTE: This allows the sender to retain the ability to select various onion parameters as they can modify and encrypt onions using the shared secret established via ECDH with the blinded node ID key.

Usually the onion encryptor encrypts the onion using a shared secret established via ECDH between an ephemeral key and a routing node’s persistent ID public key (aka: node ID). The onion encryptor need only communicate which ephemeral key he used. This is the key which usually arrives in the onion packet. This is not the case for blinded routing. Instead the onion encryptor encrypts using a shared secret established via ECDH between his ephemeral key and a routing node’s blinded ID public key. This is done so that the onion encryptor does not know to whom he is sending onions. 

Here’s a twist: The routing node does NOT know “its” blinded ID public key. This key is selected for the routing node by the blinded route builder (BRB?). NOTE: It is still correct to refer to the routing node as the owner of the blinded ID public key since the routing node is the ONLY party with knowledge of the associated private key. As a result, BOTH the onion encryptor’s ephemeral key AND this blinded key must be communicated to the routing node (OR the information needed to calculate the blinded key needs to be communicated to the routing node) in order for the routing node to decrypt the onion.

As always, a routing node in a blinded route needs the ability to compute the shared secret between himself and the onion encryptor. In that respect nothing has changed. What has changed is that a routing node in a blinded route must become aware of its own blinded node ID. This he can only do with knowledge of an encryptor key and this blinded key used by the party which encrypted the onion. Is this blinded key in the onion packet? (NO! The node’s blinded key is computed locally/privately by each intermediate processing node in the blinded portion of the route.) Is the onion encryptor’s ephemeral key still in the onion packet? (YES! This key remains in the usual location) Both need to be communicated to the routing nodes in the blinded route.

IMPORTANT NOTE: If the onion is indeed encrypted to a key (the blinded routing node key) that the routing node does not know, then it needs a way to compute or learn that key. Moreover the routing node needs a way to compute or learn the key ***BEFORE*** it decrypts the onion. So either the onion packet itself (NOT the per hop TLV payload) must be modified to hold an additional key OR the routing node has to come by knowledge of the key by some other means (ex: the proposed TLV extension in *`Update_Add_HTLC`*).


NOTE: The “introduction node” really is special.  The introduction node is able to to use the sender’s (onion encryptor’s) ephemeral key included in the onion packet to establish a secret shared between itself and the sender and decrypt the onion just as is done in normal LN onion routing.  However, the information contained within the node’s TLV payload will differ from prior nodes in the route.  This is the start of the blinded portion of the route.  The onion payload will NOT have the channel ID over which the HTLC should be forwarded in the introduction node’s TLV payload directly, as is usual with normal LN onion routing.  Rather, this information will be buried one layer deeper inside the encrypted route blinding payload (introduced expressly for this scheme).  The blinded route builder selects his ephemeral keys in a well-defined way such that they form a chain of keys.  The introduction node receives the first key, *`E(0)`*, in the chain of recipient generated ephemeral keys. It receives this key in its TLV onion hop payload (NOT in the onion packet directly). With this key the introduction node is able to calculate a secret shared between itself and the blinded route builder.  This shared secret enables the introduction node to decrypt its special route blinding TLV payload.  The introduction node can also compute the next ephemeral key in the chain for the next node in the blinded route.  This enables the “handoff” between the portion of the route constructed by the sender and the blinded portion constructed by the recipient. 

Further processing nodes in the blinded portion of the route receive the BRB chosen ephemeral key in a different way. 

**NOTE: A routing node in the blinded portion of the route receives the onion encryptor’s ephemeral key from its usual place in the onion packet. The routing node receives the blinded route builder’s ephemeral key from a TLV extension in the *`Update_Add_HTLC` message. Together it has what it needs to decrypt the onion and decrypt the internal route blinding TLV payload. More specifically the routing node can then establish a shared secret between itself and the blinded route builder (which can be used to compute the node’s blinded ID priv/public key, decrypt the onion, further decrypt the encrypted TLV data, discover the real channel ID to use for forwarding…).

**NOTE: Only E(i) needs to be communicated to the intermediate processing node. From this, the processing node can locally compute the secret shared between itself and the blinded route builder AND his blinded node ID public and private keys. The blinded route constructor picks this blinded node ID public key, but does so in a clever way such that the processing node can compute the key himself AND is the sole owner of the private key!! He can also compute the ephemeral key which the NEXT processing node will need!


The ***`update_add_htlc`*** message:
	
	[channel_id:channel_id]
	[u64:id]
	[u64:amount_msat]
	[sha256:payment_hash]
	[u32:cltv_expiry]
	[1366*byte:onion_routing_packet]

    // Route Blinding Scheme adds the ephemeral key, E(i),
    // chosen by the blinded route builder (BRB) here!!!
    // NOTE: This key is also referred to as the "blinding_point".
    [point:public_key]    // E(i>0)

The ***`onion_packet`*** format:

    * [byte:version]
    * [point:public_key]    // used for computation of shared secret between processing/routing node
                            // and onion encryptor (usually the payment sender).
                            // NOTE: This is onion encryptor (sender) chosen ephemeral public key.
                            // Call it EPK_S(i)? This is NOT E(i).
    * [1300*byte:hop_payloads]
    * [32*byte:hmac]

The onion packet holds a `single` public key. The key is used to establish a shared secret between the node processing the onion packet and another party, namely the party which encrypted the onion. Once the onion packet payload is decrypted by a processing node, it MAY contain arbitrary TLV data which itself may contain additional keys. In the Route Blinding scheme, we have encrypted data for the processing node from TWO parties, both the sender AND the blinded route constructor (recipient). We have recipient encrypted data nested within sender encrypted onion data.

The ***`tlv_payload`*** format:

    1. tlv_stream: tlv_payload
    2. types:
        * type: 2 (amt_to_forward)
        * data:
            * [tu64:amt_to_forward]
        * type: 4 (outgoing_cltv_value)
        * data:
            * [tu32:outgoing_cltv_value]
        * type: 6 (short_channel_id)
        * data:
            * [short_channel_id:short_channel_id]
        * type: 8 (payment_data)
        * data:
            * [32*byte:payment_secret]
            * [tu64:total_msat]

        // New TLV Payload Fields Added by Route Blinding Scheme
        * type: 10 (encrypted_recipient_data)
        * data:
            * [...*byte:encrypted_data]
        * type: 12 (blinding_point)
        * data:
            * [point:blinding]


Perhaps the most critical requirement of a blinded route:
**We MUST provide the onion encryptor with a key which allows him to establish a shared secret with each routing node, and we must do so WITHOUT the onion encryptor knowing the persistent ID of the routing node.

In order for sender to encrypt the onion it needs a shared secret with the intermediate node. In order for the blinded route constructor to encrypt the data which includes the actual channel/node to forward to it also needs a shared secret with the intermediate node. To establish shared secrets we need public keys.

A shared secret is generated between 2 public keys, (PK_A, PK_B, ss_AB). These public keys may be persistent (ex: LN Node ID) or ephemeral (ex: blinded LN node ID, or one time key for onion routing). The private key associated with each public key needs to be exclusively known by a distinct single party.


### Normal LN Onion Routing:
```console
(EPK_S, NPK_I, ss_SN) // This is used to (en/de)crypt the onion.

EPK_S: Sender chosen ephemeral public key. Private Key Owner: Sender
NPK_I:  Node ID Public Key. Known publicly via LN gossip. Private Key Owner: Node
ss_SN: Shared secret between sender and processing node.
```

### Route Blinding:
```console
(EPK_S, BNPK_I, ss_SN)    // shared secret between node and sender without sender knowing the true persistent node ID! This is used to (en/de)crypt the onion! The routing node MUST calculate "its" blinded ID key, BNPK_I, in order to decrypt! 
(EPK_R, NPK_I, ss_RN)     // shared secret between node and recipient used to decrypt special route blinding TLV payload. This is also used by routing nodes to derive their blinded node ID, BNPK_I, which is needed to decrypt the onion!

EPK_S: sender chosen ephemeral public key. Private Key Owner: Sender
EPK_R: recipient chosen ephemeral public key. NOT known by sender. Private Key Owner: Recipient
BNPK_I:  blinded node ID public key. Known by recipient, node, and sender. Originally chosen by recipient, but computable by the node given EPK_R. Private Key Owner: Node
ss_RN: shared secret between recipient and processing node.
```

## Misc. Thoughts

Alice and Bob CANNOT establish a shared secret using a public key (ephemeral or otherwise) owned by Carol.

Route Blinding Translation: Sender and Hop CANNOT establish a shared secret (needed to decrypt sender encrypted onion) using a public key owned by Recipient.

Carol CAN compute a public key owned by Bob which can be used to establish a shared secret between Bob and Alice, Xavier, or any other party. How? Assume Bob has a public identifying key pair *`(b, B)`*. Carol can generate an ephemeral key pair *`(e, E)`*, use it to establish a secret shared *`ss`* between herself and Bob. Then she can tweak Bob’s public key using that shared secret such that the associated private key is known by Bob only (ie: *`ss*B = (ss*b)*G`*, where Bob knows both *`ss`* and *`b`*). This gives Bob the ability to reconstruct the tweaked key as long as he learns Carol’s ephemeral public key, *`E`*. 

Route Blinding Translation: Recipient CAN compute a public key for Hop which can be used to establish a shared secret (needed to decrypt sender encrypted onion) between Hop and Sender. How? Assume Hop has a public identifying key pair *`(h, H)`*. Recipient can generate an ephemeral key pair *`(e, E)`*, use it to establish a secret shared between herself and Hop. Then she can tweak Hop’s public key using that shared secret such that the associated private key is known by Hop only (ie: *`B = ss*H = (ss*h)*G`*, where, with knowledge of *`E`*, Hop can compute *`ss`* and thus knows both *`ss`* and *`h`*). This gives Hop the ability to reconstruct the tweaked key, `B`, as long as she learns the recipient’s ephemeral public key, *`E`*. 