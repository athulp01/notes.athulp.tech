# Link Layer

Link layer is implemented in the NIC in each and every host.

---

## Service Provided
1. Framing - Almost all link-layer protocols encapsulate each network-layer datagram within a link-layer
frame before transmission over the link.
2. Link access - A medium access control (MAC) protocol specifies the rules by which a frame is
transmitted onto the link.
3. Reliable Delivery - When a link-layer protocol provides reliable delivery service, it guarantees to
move each network-layer datagram across the link without error but,  many wired link-layer protocols do not provide a reliable delivery service.
4. Error detection and correction - Because there is no need to forward a
datagram that has an error, many link-layer protocols provide a mechanism to detect such bit errors.


## Modulation
* Shannon limit - Theoretical limit for error free data transmission.
* PAM and ASK is used in wired systems due to constant signal strength
    * PAM-5 used in 100BASE-T and 1000BASE-T Ethernet(cat-5 cables)
    * PAM-16 in 10GBASE-T 
* PSK is used in wireless due to significant variation in signal strength during propagation.
    * BPSK used in 802.11b 1 and 2 Mbps
    * QPSK used in 802.11b 5.5 and 11 Mbps
* QAM is also used for wireless(HSPDS, LTE, WiMAX, 802.11abgn) 16-QAM and 64-QAM
* Symbol is the unit of transfer at the physical layer. Symbol can contain more than one bit.
   * BPSK 1bit/symbol, QPSK 2b/s

## Coding
* Adding redundancy at physical layer will greatly improce the link layer throughtput
* Coding gain = ratio of bits at link layer to at physical layer.

## Clocks
* Data is transmitted using a clock
* The receiver need to know when to sample the data.
* Asynchronous communication use start bit and end bit to avoid the encoding clock with the signal. But number of bits in a frame should be less because the clock will get out of unison if we need to sample more bits in a frame.
* Synchronous communication enocodes the data with the signal. Different block encoding schemes are
    * Manchester encoding, 4b5b encoding etc

## MAC Protocols
Regulate the access the medium which is shared by a number of nodes.
1. High utilization
2. Fair
3. Simple and low cost to implement
4. Robust to errors.

> Thera are two types of links, point-to-point and broadcast

Three broad classes:
1. channel partitioning
2. random access
3. taking turns

### Channel partitioning
**TDMA**
* access to channel in "rounds" 
* each node get fixed length slots in each round

**FDMA**
* Channel spectrum divided into frequency bands
* Each station is assigned a fixed frequency band

**Aloha**
* all frames same size
* time divided into equal size slots
* nodes are synchronized
* nodes are synchronized only slot beginning
* if 2 or more nodes transmit in slot, all nodesdetect collision.
* Maximum efficieny 37%

### Random access protocol 
**CSMA/CD**
* listen before transmit
* if channel is not busy, then transmit otherwise backoff.

### Taking turns
* Token ring
* Polling

### MAC address and ARP
* MAC addr -> 48-bit address
* ARP -> protocol to determine the mac address from the IP address.
    * Each node stores a table whoose entries are < IP, MAC, TTL>
    * If an mapping is not in ARP then will send a ARP query to broadcast MAC addr.
    * Then the required host would reply with its MAC addr.

## Ethernet
### Ethernet MAC Protocol
![Ethernet Frame](https://www.gatevidyalay.com/wp-content/uploads/2018/10/Ethernet-Frame-Format-IEEE-802.3.png)
* Preamble - for receiver clock synchronisation
* DA - destination MAC addr
* SA - Source addr

**Ethernet Standards**
* 100BASE-TX
    * CAT-5 cable, RJ45
    * Full duplex, one pair
    * 4b5b encoding
    * 100Mbps in each direction
    * 100m max distance
* 100BASE-FX - Optical Fibre version
* 1000BASE-T
    * CAT-5, RJ45
    * Four pairs of cable
    * Complex coding
    * 100m distance
    * 1Gbps
* 1000BASE-FX - Optical fibre version
### Ethernet Switch
* Link layer device
* transparent - host are unaware of switches
* self learning
* full duplex
* Have switch table
* switches can be interconnected

**Frame forwarding**
1. Forward the frame to corresponding interface according to the DA.
2. If DA is not present in the forwarding table, then broadcast and then learn.



