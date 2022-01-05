# Adaptor Signatures

## Adaptor Signature Construction

Other explanations I have seen gloss over the challenge.
KEY: For *s* to be valid, the nonce must be exactly represented in the challenge, *e*:

- s  =      k      +  H(R, P, m)x               with public nonce R = k*G  &&  e = H(R, P, m)
- s  =  (k + t)  +  H(R + T, P, m)x    with public nonce R’ = R + T = (k + t)*G  &&  e = H(R+T, P, m)

NOTE: Whether outside observers know that a given nonce, *R* (or *R’*), is a single or the composite of two separate nonces group elements is not important. The construction of the nonce is not important in this regard. Whatever nonce is used in the signature equation, must have its exact public representation included in the challenge, *e*. Said differently, the nonce used must be EXACTLY the discrete logarithm of the group element/public key included in the challenge.

    s  =  ?  +  H(?-Public, P, m)x   
    
*?-Public* in the challenge MUST be *?\*G* for *s* to be usable as a valid signature. The valid signature would be *(s, ?-Public)* for key pair *(x, P)* on message *m*.

There seem to be two way to generate *s* for an adaptor signature. The following are candidates for adaptor signatures:
```
1.  s’ = (k + t)  +  H(R, P, m)x         -  tweaked nonce with regular challenge

2.  s’ =    k     +  H(R + T, P, m)x     -  regular nonce with tweaked challenge (IMPORTANT: requires only knowledge of T).
```
The critical point is that *s’* can never be used as part of a valid signature NO MATTER WHAT public nonce you pair it with. This is because the nonce used in the construction of s’ is NOT the discrete log of what is included in the challenge. The construction of s’ is “mixed”, or tweaked by either the adaptor secret or adaptor point. 

QUESTION: Which candidate adaptor signature (if any) is better? 

IMPORTANT NOTE: In order to tweak the nonce, you need to know the adaptor secret/scalar. In order to tweak the challenge you only need to know the public adaptor point. The challenge is constructed with entirely public information. I have only ever seen adaptor signature construction presented using 2). Perhaps the application of adaptor signatures will make evident why this is the case, but in theory both constructions could work.

Equation 1):
```
	s’  =  (k + t)  +  H(R, P, m)x
-	s   =     k     +  H(R, P, m)x
___________________________
    s’ - s  =  t                                     OR  ==>    s - s’  =  - t 
```
Equation 2):
```
	s’  =     k       +  H(R + T, P, m)x
-	s   =  (k + t)    +  H(R + T, P, m)x
___________________________
    s’ - s  =  - t                                   OR  ==>    s - s’  =  t 
```

It seems good convention to call the valid signature s, and the invalid (for the message) but verifiable (to have been encrypted to the claimed adaptor point) adaptor signature, s’.

NOTE: For a given message, *m*, I can generate many different signatures *(s, R)* for the same keypair *(x, P)* by choice of *k*. In practice, *k* is calculated deterministically from the private key and message being signed in order to avoid nonce re-use and private key leaks.


## Adaptor Signature Techniques

It seems we can do at least a couple different things with adaptor signatures. Consider the following scenarios:

Scenario #1: The signer knows the witness *y* to the statement *Y*. The signer computes an adaptor signature and shares it with other parties. The other parties know that if they learn the actual signature they can calculate *y* OR if they learn *y*, then they learn the actual signature.

How would they learn the actual signature or *y*? The signer would have to share either of those 2 values OR be involved in an off-chain protocol which requires those values be shared publicly in order to be valuable to the signer. This approach aligns the signer’s economic incentive with proper adherence to the protocol.

Scenario #2: Another party generates/knows witness *y* and gives statement *Y* to the signer. The signer can compute and return an adaptor signature. This adaptor signature can be modified into the real signature by the other party since they know witness *y*. Doing this and publishing the signature reveals *y* to the signer. This seems strange because it sounds like the signer couldn’t produce his own signature for the message (ie: that he needs the knowledge of a witness *y* to even be able to sign the message). No, the private key holder can always produce a signature for any message he wants. He is producing a special/tweaked signature that can be adapted by whomever has knowledge of the discrete log/preimage of *Y*.

Scenario #1 seems, at first glance, to be achievable using either equation 1) s’ = (k + t) H(R, P, m)x, OR equation 2) s’ = k + H(R+T, P, m)x, from our notes.

Scenario #2 requires using Equation 2)  s’ = k + H(R+T, P, m)x, from our notes because the signature creator does NOT know the adaptor secret/scalar/witness.
	

RESULT: The candidate adaptor signature construction from Equation 2 seems better!

The signer adapts or encrypts his signature using public information. This allows the signing entity to participate without knowledge of the adaptor scalar. In this case the encryption of the signature is achieved by simple addition of the public adaptor point to the signature’s hash challenge. Because the adaptor secret, T, is added to the hash function it transforms the hash output in some ill-defined/random way, it cannot simply be subtracted.


## Protocol Construction

In the following article on script-less scripts, Nadav outlines the use of Adaptor Signatures in the Lightning Network to create a script-less version of the HTLC concept. He presents the case where the adaptor secret is known by the recipient of funds and where the signature generator is the sender of funds without knowledge of the adaptor secret. The signature generator only knows the public adaptor point. NOTE: This is Scenario #2 above.

- Adaptor secret/scalar: t
- Adaptor/Payment point: T (a group element/public key)

https://suredbits.com/schnorr-applications-scriptless-scripts/

"Like in a normal payment, the payer/sender of the funds will generate a Schnorr signature of a transaction sending funds to the receiver. Unlike a normal payment, the sender will tweak their signature using T in such a way that the receiver will only be able to repair this signature to get a valid one, by using the secret t.“

NOTE: This implies that the signer CANNOT generate a valid signature on the message which would prematurely reveal to him the adaptor secret. If he could you would essentially be dodging DLP by using them in a signature scheme so this MUST be the case. TODO: Verify/Rationalize this for myself.

1. Sender generates an adaptor signature (which only requires knowledge of T).
2. Receiver verifies this adaptor signature.
3. Receiver completes the adaptor signature using t, uses this completed signature.
4. Sender takes the difference between the completed and adaptor signatures to learn the secret tweak.



### Notes on Schnorr

Notes on why Schnorr signature construction is what it is:
- You always need a nonce/blinding factor, but whether that nonce is singular or composite is up to you
- You need some 

```
s = k + x   one equation with 2 unknowns, but nowhere do we include the message so we cant conceivably call this construction a “signature for message m”.
sG = S = R + P
s = k + x + m     one equation with 2 unknowns but we do include the message this time. Couldn’t I do (k-2) and (m+2)? Am I signing m or (m+2) at that point. We need to commit to the message. If m is put through a hash function, then alterations to the message being signed would transform the hash output in an unpredictable way.
sG = (k + x + m)*G
A signature using private key (x-2) with nonce (k-1) and message (m-1). Clearly this still isn’t defined well enough to declare it a signature on the message m by key pair (x,P)
S = R + P + M

s = k + H(m)*x
```

The introduction of one way functions allows for public and private equations. The public equation can contain elements known by everyone without revealing anything about the private equation. Elements of the private equation can be selectively revealed. So long as there remains n > 1 unknowns in the private equation, the private equation can hide a secret number.

private equation: s = k + x
           |
           |   Elliptic Curve
           V
public equation: S = R + P