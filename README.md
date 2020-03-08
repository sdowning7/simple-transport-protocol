# simple-transport-protocol

Approach: 


Sender:
- Have window of 5 packets
- Sender sends first 5 packets immediately
- Keeps track of seqn on acks it should get back
- Once an ACK is received for 1 of the packets it sends the next one
- If packet does not get ACK and 3 new packets are sent and ACK'd then the packet is retransmitted

Receiver:

- Assume seqn begins at 0
- When receiving a packet:
    - if it's the next packet from current seqn then print it to stdout, log, send the ack, increment seqn, and throwaway
    - if not the next packet, then store in list of received packets sorted by seqn and send ack.
    - if seqn of received packet is less than current seqn or seqn is already in store, then it's a duplicate packet and should be thrown away. ack should still be sent in case sender needs it.
    