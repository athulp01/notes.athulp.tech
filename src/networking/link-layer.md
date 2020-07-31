# Link Layer and Physical Layer

## Physical Layer
### Modulation
* Shannon limit - Theoretical limit for error free data transmission.
* PAM and ASK is used in wired systems due to constant signal strength
    * PAM-5 used in 100BASE-T and 1000BASE-T Ethernet(cat-5 cables)
    * PAM-16 in 10GBASE-T 
* PSK is used in wireless due to significant variation in signal strength during propagation.
    * BPSK used in 802.11b 1 and 2 Mbps
    * QPSK used in 802.11b 5.5 and 11 Mbps
* QAM is also used for wireless(HSPDS, LTE, WiMAX, 802.11abgn) 16-QAM and 64-QAM
* Symbol is the unit of transfer at the physical layer. Symbol can contain more than one bit.
   * BPSK 1b/s, QPSK 2b/s

### Coding
* Adding redundancy at physical layer will greatly improce the link layer throughtput
* Coding gain = ratio of bits at link layer to at physical layer.

### Clocks
* Data is transmitted using a clock
* The receiver need to know when to sample the data.
* Asynchronous communication use start bit and end bit to avoid the encoding clock with the signal. But number of bits in a frame should be less because the clock will get out of unison if we need to sample more bits in a frame.
* Synchronous communication enocodes the data with the signal

## Link Layer
### Service Provided
1. Framing - Almost all link-layer protocols encapsulate each network-layer datagram within a link-layer
frame before transmission over the link.
2. Link access - A medium access control (MAC) protocol specifies the rules by which a frame is
transmitted onto the link.
3. Reliable Delivery - When a link-layer protocol provides reliable delivery service, it guarantees to
move each network-layer datagram across the link without error but,  many wired link-layer protocols do not provide a reliable delivery service.
4. Error detection and correction - Because there is no need to forward a
datagram that has an error, many link-layer protocols provide a mechanism to detect such bit errors.

