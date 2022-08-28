# Connections

> This is an entirely distributed system, there isn’t any central control. The only reason it works is because everybody decided to use the same set of protocols. - Vint Cerf inventor of tcp/ip

- 🔗 Link computers to one another to make a network,
- 🌐 Combine networks using the Internet Protocol,
- 📍 Locate a recipient from its Internet address,
- 🧭 Find a route through the Internet to that location,
- 🚚 Transport data between distant applications.

Before the Internet came along, telecommunication between two parties required a direct physical link. In the 1950s, each telephone had a wire leading directly to a central station. For a call to go through, an operator had to physically connect the wires of two telephones. For long distance calls, wires were laid out between distant stations, and several operators in different places had to physically connect the chain of wires linking the two phones.

![Telephone_switchboard](https://upload.wikimedia.org/wikipedia/commons/e/e4/Telephone_switchboard_6_Oct_1907_Salt_Lake_City.jpg)

--

wires are no longer constrained to serve a single connection—many concurrent connections can share the same wire. However, modern networking technology is more intricate than early telephony. It has many successive layers, each building on top of the previous. Let’s explore how connections are made at these different levels, starting with the most basic layer.

## 1.1 Links

A direct connection between two computers is achieved through a transmission medium: a physical channel where signals can flow.

This may be a copper wire carrying electric currents, a fiber-optic cable directing light, or air hosting radio waves

-- recherches

![](https://i0.wp.com/css-tricks.com/wp-content/uploads/2021/09/01-1.png?w=1184&ssl=1)

When a medium exclusively connects two computers, we say they maintain a point-to-point connection, and their link layer relies on the most basic set of rules: the Point-to-Point-Protocol (PPP). It merely ensures the two computers can identify each other and exchange data accurately.

However, connected computers don’t always get to enjoy such an exclusive link. Often, they must share the transmission medium with several other computers.

## Shared Links

One way to link computers in an office is to plug each of them into a hub with a wire. The hub physically connects all the wires that reach it, so a signal sent by one computer will be detected by all the others! This will also happen on your home WiFi, since the same radio frequency is used by all connected devices. Communications can become messy if all of them use the medium at the same time.

![](https://i0.wp.com/css-tricks.com/wp-content/uploads/2021/09/02-1.png?resize=1000%2C589&ssl=1)

The link layer contains a set of rules to define how computers should share their communication medium, fittingly called Medium Access Control (MAC).

***It handle COLLISION and PHYSICAL ADDRESSING***

COLLISIONS — If two computers send a signal through the same medium at the same time, the resulting interference garbles both transmissions.

There are methods to avoid collisions.

First, only start transmitting signals when no other computer is transmitting.

Second, monitor your communications–if a collision occurs, wait for a brief but random amount of time before trying to transmit again.

![RETRY ON COLLISIONS](https://i0.wp.com/css-tricks.com/wp-content/uploads/2021/09/04-1.png?resize=1000%2C588&ssl=1)

These methods have some limitations. If there are too many transmission attempts through a medium, collisions will occur relentlessly. We say the link is saturated when excessive collisions break down communications. Have you ever been frustrated at a large venue because your phone wouldn’t send text messages or make calls? This may happen if too many phones are attempting to communicate concurrently and the cellular link becomes saturated.

PHYSICAL ADDRESSING — Each computer’s network interface has an identifier, known as its physical address or hardware address. (MAC ADDRESS). A transmission in a shared medium must begin with two such addresses: that of the recipient and that of the sender. Upon receiving a transmission, a computer will know if it should be ignored or picked up and to which address it should reply.
This can only work if physical addresses are unique: if two computers use “my_netinterface”, we’re back to square one. **For this reason, virtually all network interfaces follow a naming scheme defined in the rules of Medium Access Control.** These standard physical addresses are called MAC addresses.

## MAC Addressing

Since MAC addresses are simply large random-looking numbers, network interface manufacturers around the world must coordinate to avoid accidentally assigning the same number to two different devices. To this end, they rely on the Institute of Electrical and Electronics Engineers (IEEE), that assigns each of them a different range of MAC addresses.

A MAC address is expressed as six pairs of hexadecimals1 separated by colons. The first half of the address is an identifier assigned by the IEEE to a unique manufacturer. This manufacturer then chooses a unique second half for each network interface.

```

60:8B:0E:C0:62:DE

IEEE to unique manufacturer

60:8B:0E : C0:62:DE

            manufacturer choice
```

![PHYSICAL ADDRESSING](https://i0.wp.com/css-tricks.com/wp-content/uploads/2021/09/06-1.png?resize=1000%2C577&ssl=1)

There’s a special address reserved for transmissions to all computers in a medium. It’s called the broadcast address, and it reads FF:FF:FF:FF:FF. You use it when you try to connect to an unknown device. For instance, when your smartphone’s WiFi card isn’t deactivated, it persistently broadcasts to FF:FF:FF:FF:FF that it’s looking for an access point. Discoverable access points will respond with their own MAC address so you can establish a link.

You can also set your own network interface to promiscuous mode, and it will pick up all transmissions regardless of their intended recipient. Doing so allows you to discover hidden WiFi networks, to list which MAC addresses are in your area, and sometimes even to read the contents of other people’s transmissions. Browsing the Internet through an unsecured WiFi network can therefore be unsafe: your communication is broadcast for anyone in range to hear. This is why encryption4 is important for WiFi’s link layer.

Be careful: a network interface can be configured for its transmissions to start with any MAC address for both the recipient and the sender. Nothing stops a malicious agent from impersonating you by using your MAC address in their transmissions. This type of attack is known as MAC spoofing. When the link layer was invented, security wasn’t a concern. Protocols are evolving to become more secure and neutralize such attacks, but it’s an ongoing process.
