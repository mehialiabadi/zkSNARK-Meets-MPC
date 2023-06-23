$
\section{Introduction}
 Plonk protocol relies on a common reference string (CRS) as a public parameter for proving & verifying. The CRS is generated in advance by a trusted party. The random and private data used to create the CRS, called ‘toxic waste’ requires to be kept secure during the process an  destroyed upon the CRS is created. Otherwise, it can be used by an adversary to make false proofs.
 
The creation of public parameters for zkSNARKs is called the setup ceremony which is run by a Multi-Party Computation (MPC) protocol. 

Setup MPC ceremony is an interactive protocol involving multiple parties who contribute randomness to iteratively build the CRS. A typical ceremony consists of the number of players, the coordinator, and the verifier. The MPC protocols are always of a round-robin nature, where a player receives a  message from the previous player. Then the player adds their input to accumulated randomness before passing it into the next player. In the end, the final result is the CRS. In the intermediate state, as it is being passed between players, the message is referred to as the transcript.

In 2015, Ben-Sasson et al. in \cite{} proposed a family of MPC protocols for ZKPs. They have proven that the CRS generated with these protocols is secure as long as at least one contributing party behaves honestly. 
In other words, by increasing the number of honest and independent contributors, the probability that all participants are dishonest is reduced to the point of negligibly.

In 2017, Bowe et al. introduced another family of MPC protocols \cite{bowe2017scalable} specifically for pairing-based zk-SNARKs like Groth16. (It's out of our scope).


\subsection{Pre-requirements}

\begin{enumerate}
\item Determine the selection date, and number of members, and define the elliptic curve and its parameters. 
    \item Registration  process
    \begin{itemize}
        \item To sign up for participation, a
        The user must send a  token/coin to theAB-controlled address.
         Admin then will add their address on the mpc-server. 
        \item Here there are 3 participant groups. 
        \begin{enumerate}
            \item  Institutional participants -  They have top priority during the ceremony.
            \item Early bird individuals - They have secondary priority during the ceremony.
            \item Individuals - They have tertiary priority during the ceremony
        \end{enumerate}
        \item 
        
    \end{itemize}
    \item  Prepare Instruction for players: laptop/system preparation, how to join, generate transcript, upload their transcript to serve,r and download previous player's transcript.  
    %Prepare applications: software & hardware ISO file, software's links, docs and procedure details
   % \item Implement & Test MPC client application.
    Note: Tornadocash ran a setup ceremony that enabled users to contribute directly from the web browser, as a result around 1114participantst played a part. 
   % \item Implement ,Deploy and Test MPC server: (coordination among participants ,provide information of the  current state of ceremony)
\end{enumerate}
\begin{itemize}
    \item Selection process: 
   The selected date is governed by a predetermined Ethereum block height. The block hash of the block is used as a seed to a pseudo-random number generator which first selects several participants from tier and is then used to randomize the priority order of participants in both tier 1 and tier 2. Unselected participants and participants in tier 3 are ordered on a first come first served basis.
    
\end{itemize}
\subsection{MPC Protocol}
Once the ceremony starts,  all registered participants can simply run the open-sourced client software to participate in the ceremony. All of whom will be randomly ordered into a public queue. To reduce the waiting time of the activity, the mpc-server continuously monitors the active participant’s client software and applies a First-Come-First-Serve strategy on all active and prioritized participants.
%Then, the protocol proceeds as follows:
\subsubsection{Trusted setup algorithm}
 The underlying cryptographic algorithms for handling the computation and verification  of PLonk CRS on  the defined elliptic curve points run as follows:
 
 \begin{itemize}
     \item
     The first participant ($P_1$)runs the setup by providing the number of G1 and G2 points as input arguments. 
     Then chooses  random toxic  $z_1$ and building  $transcript_1$ as follows: 
     %the generator point h, and 
     
   $transcript_1$: $(g_1.{z_1^{0}}, ..., g_1.{z_1^{max}}) \in G1$ , 
   $z_1.g_2 \in G$
\item Participant 2 ($P_2$) receives $transcript_1$  from $P_2$ and rolls in their toxic random ($z_2$) to generate their own transcript:

  $transcript_2$:  $(g_1.z_1^{0}z_2^{0}, ..., g_1.z_1^{max}z_2^{max}) \in G1$ , 
     $z_1.z_2.g_2 \in G2$

  \item Likewise, participant n ($P_n$) takes $transcript_{n-1}$ from $P_{n-1}$ and outputs CRS:
  
    $transcript_n$:  $(g_1.z_1^{0}z_2^{0}...z_n^{0}, ..., g_1.z_1^{max}z_2^{max}...z_n^{max}) \in G1$ , 
     $z_1.z_2....z_n.g_2 \in G2$
 \end{itemize}
 
\subsubsection{Transcript file structure}
%\subsection{Post process}

\subsection{Security of  MPC Ceremony}

The security of the ceremony relies on honest participants. If there is only one participant who behaves honestly, the whole ceremony is succeeded 

 %whichcurvee? BN254 and BLS12–381.
 $

