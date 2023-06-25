
# Introduction
 Several zkSnark protocols such as Plonk, groth1,6and Pinocchio rely on a common reference string (CRS) for proof and verification processes. The random and private data used to create the CRS, called ‘toxic waste’ requires to be kept secure during the process and destroyed upon the CRS is created. Otherwise, it can be used by an adversary to make false proofs. The CRS can be generated in advance by a trusted party, however, Multi-Party Computation (MPC) is an ideal candidate to generate CRS in a more secure way. 
 
The creation of public parameters for zkSNARKs is called the setup ceremony which is run by an MPC protocol. 
Setup MPC ceremony is an interactive protocol involving multiple parties who contribute randomness to iteratively build the CRS. A typical ceremony consists of the number of players, the coordinator, and the verifier. The MPC protocols are always of a round-robin nature, where a player receives a  message from the previous player. Then the player adds their input to accumulated randomness before passing it into the next player. In the end, the final result is the CRS. In the intermediate state, as it is being passed between players, the message is referred to as the transcript.

In 2015, Ben-Sasson et al. proposed a family of MPC protocols for ZKPs. They have proven that the CRS generated with these protocols is secure as long as at least one contributing party behaves honestly. 
In other words, by increasing the number of honest and independent contributors, the probability that all participants are dishonest is reduced to the point of negligibly.

In 2017, Bowe et al. introduced another family of MPC protocols specifically for pairing-based zk-SNARKs like Groth16. (It's out of our scope).


## Pre-requirements of ceremony
There are a bunch of requirements and processes to set up a ceremony including, participant selection, participant registration, defining the cryptographic parameters, preparing applications and hardware, preparing instructions, and so on. Following we are going to go through the actual mpc protocol that players run and achieve some randomness which will be used later in the keys (proof and verification) generation process.
```
## MPC Protocol
Once the ceremony starts,  all registered participants can simply run the open-sourced client software to participate in the ceremony. All of whom will be randomly ordered into a public queue. To reduce the waiting time of the activity, the mpc-server continuously monitors the active participant’s client software and applies a First-Come-First-Serve strategy on all active and prioritized participants.

 ```
     The first participant $P_1$ runs the setup by providing the number of G1 and G2 points as input arguments. 
     Then  she chooses random toxic  $z_1$ and build the  $transcript_1$ as follows: 
     %the generator point h, and 
     
   $transcript_1: (g_1.{z_1^{0}}, ..., g_1.{z_1^{max}}) \in G1 , z_1.g_2 \in G$
   
 Participant $P_2$ receives $transcript_1$  from $P_1$ and rolls in their toxic random $z_2$ to generate their own transcript:

  $transcript_2:  (g_1.z_1^{0}z_2^{0}, ..., g_1.z_1^{max}z_2^{max}) \in G1$ , 
     z_1.z_2.g_2 \in G2$

   Likewise, participant $P_n$ takes $transcript_{n-1}$ from $P_{n-1}$ and outputs final randomness which be used to generate proof and verification keys. 
  
    $transcript_n:  (g_1.z_1^{0}z_2^{0}...z_n^{0}, ..., g_1.z_1^{max}z_2^{max}...z_n^{max}) \in G1 , 
     z_1.z_2....z_n.g_2 \in G2$
```
## Security of  MPC Ceremony
The security of the ceremony relies on honest participants. If there is only one participant who behaves honestly, the whole ceremony is succeeded.

## Implementation

 

