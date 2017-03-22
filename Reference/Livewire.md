Livewire's Layers of Abstraction
--------------------------------

Livewire is an Audio over IP standard. Basically it allows any device on the network to access any stream, regardless of the location (so a router selector node can pull up the microphone in Studio A from Ballou and listen to it).

For clarity, there are three types of audio transmission methods:

1. Analog (usually balanced) audio, for instance XLR
2. AES Digital, transferred over XLR connectors - the professional method for transferring fully digital audio in stereo up to 192 KHz at 24 bit.
3. Livewire Audio-over-IP, a software-defined audio transmission method

To make this a little more confusing, we use CAT cables and RJ45 connectors for all three, but you can't interchange them. The term digital can be confusing becuase Livewire is technically "digital" but you cannot directly plug the network into a standard digital AES source.

In general, all Livewire interface happens through proprietary dedicated devices. These perform one of two functions:

1.  A node performs a bridge between a standard protocol (analog balanced audio, digital AES audio, or PCM digital audio inside our computer in the case of the ASI card) and the Livewire network. Basically, this bridges standard non-Livewire audio with a fully routable Livewire stream.
2.  Several devices do processing on solely Livestream audio, so both input and output are Livewire streams. Examples of these are the Studio Engine and the Omnia audio processors (though the Omnia has support for digital audio output directly).

Problems with IP Audio
----------------------

One of the critical issues with IP-based audio has to do with latency. Packetized data transmission enables very flexible routing and delivery, but is a "best effort" system. If the amount of data to be sent exceeds the capacity of the channel or the buffer, data will be dropped indiscriminantly. To account for this, protocols exist which guarantee delivery of data (TCP) over unreliable channels. However, this can increase the latency of the channel.

Livewire requires Quality of Service (QoS) configuration to prioritize its traffic. In essence, equipment can "tag" its data with a priority flag (0-7) that allows networking equipment to forward some data with higher priority than others. In such a fashion, the switch will drop standard data packets (like your browser HTTP connection to Facebook) before it drops Livewire packets, thus prioritizing reliability of the Livewire stream over standard traffic.

This is not a perfect system: it is still possible for interference to garble packets, but in practice in a small and well-constructted network like ours (read: actual CAT6 cables and not chinese garbage --thanks Max), the effect of this will be minimal and it is accounted for by the protocol. As with any digital system, Livewire incurs a delay; however, the real delay of a stream configured in "livestream" mode is impressively low: about 2 ms, well below the minimum acceptable delay before people will notice. The liveware manual details a bit more about this delay and comparisons.

In addition, Livewire provides a very efficient way of getting around the network. Multicast is a capability of Ethernet and IP networks to forward data to multiple hosts from one source. What this means in practice is that every node on the network can send its data to the core switch; the switch is able to transmit this data to every receiving node that requests it and *only* the receiving nodes that requested it. The protocol used to control this behavior is called IGMP, which contains messages like "I want to subscribe to stream #10420" and "I'm done with stream #10420, thanks boo." Essentially the switch acts as an IGMP "querier," which will ask each node which streams it wants and then distribute them to only the nodes that need it. For this reason, it is very important that switches connected to the network that also have Livewire nodes attached have IGMP Snooping set up properly -- snooping simply listens to the IGMP messages flowing across and then uses that to ensure the right nodes get the right streams (only one querier can exist on the network).

If Livewire behaved like a standard (unicast) service, the network would quickly become flooded. If I am sending audio data from a microphone and 12 people on the network want that data, I would have to send 12 copies of that. Imagine adding 100s of sources and you'll see that we'll run out of bandwidth. Just for example, a standard webstream like the one that serves listeners the WMFO webstream operates in this fashion; the number of listeners is limited by available bandwidth.

There are two types of livewire streams: standard streams incur a relatively high amount of a delay because of the nature of packeting - if we wait for a standard payload on a 1500 byte packet to fill, there's a certain amount of latency incurred. By contrast, Live streams keep the packet size very small to minimize latency, but this also increases network load so they should only be used on critical sources like microphones and airfeeds. CD players can easily get by with more latency so they should use standard streams.

Livewire is the protcol that all Axia/Telos equipment uses. For more information see the WMFO Operations Mandatory Reading *Introduction to Livewire* and other [manuals](https://www.telosalliance.com/downloads?search=product-manuals#downloadListing "https://www.telosalliance.com/downloads?search=product-manuals#downloadListing") published by the Telos Alliance.

### Entering and Leaving the Livewire Network

All audio devices on the network operate using the Livewire protocol to get data in between them. However, we need to be able to connect standard audio sources to the network:

*Inputs* and *Outputs* on the Nodes and PowerStations are RJ45, the same connector used for Ethernet cables. While this seems a little weird, it's because of the fact that the cables are actually very well-suited to both Analog and Digital audio and it's very easy to crimp cables to length. For the audio data, we use a shielded cable (abbreviated STP for shielded twisted pair as opposed to network cables which are generally UTP or unshielded). Each standard node has 8 inputs and 8 outputs, each present as an RJ45 jack on the rear. Adapters are available to connect to all sorts of peripherals, generally under the StudioHub name.

### Organization of the Audio on the Network

Viewed from the perspective of the Livewire network, a "Source" is any audio that is fed to the network. These usually come from standard audio devices like microphones, line inputs, or CD Players but may also be generated internally (the Studio Engine that mixes the audio for Studio A produces several sources, like Program 1 which carries the main board sound output). 

Audio in the network is in the form of a *stream*. Streams are identified by both a name and a channel number. Streams must have exactly one source but may be routed to any number of destinations. The name and channel number are assigned at the source, the latter by [WMFO convention](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/LW_Address_Space "LW Address Space"). Streams are global to the WMFO LAN.

## Device Types

### Nodes

There are Analog and Digital nodes positioned throughout the network. These are simple bridges between Livewire and conventional audio devices.

### Router Selector

These are devices that can be used as a troubleshooting tool. Using the screen, you can tune to any source available on the network and listen with headphones. They also have every possible connector (XLR stereo, AES, RJ45 AES and Analog) as well as one source which can be either AES or Analog. There are three on our network, one in each of Studio B, Control, and the tower.

### ASI Card

These devices are very clever: they incorporate a standard soundcard on one end and a Livewire node on the other. This allows Linux devices that are completely agnostic of the Livewire protocol to send and receive 8 channels of audio. There is one of these present in our hypervisor that handles Rivendell, as well as an old PCI version that doesn't have a use yet.

### Zephyrs

These are two units that support webstream transmission of audio between the two units. They can behave as standard SIP phones but also support running through a third-party service through Telos. Getting them to work is always fun, though it appears that they have run into trouble with Tufts' new TCP firewall setup. Best to test these things in advance, as they may require a firewall exception to run properly. They should also run off an LTE modem, but that behavior is yet to be confirmed.

### Omnia

The Omnia is a broadcast compressor with a variety of uses. We employ 2 of them, one for the webstream and one for the transmitter. It was sortof decided that we wanted to be able to tune compression settings individually for both, for which I agree. Each are controllable with an abysmal web interface through a Java Applet which often refuses to work because of Java security shenanigans. Good luck.

Conomnia1 runs the "Multicast" firmware. We use it as a multiband compressor but also to LOUDify the audio before it pipes into the webstream. 

The towomnia1 runs an FM firmware. Currently this feeds the transmitter over an AES connection and gets its audio over Livewire. We have also configured a backup audio source (namely the towrs1 router selector) to output AES, and the towrs1 is attached to one of the Fibox lines thus it runs independently of the tows1 switch.

### StudioEngine (conse1) and Element GPIO Controller (egpio1)

The most finnicky pieces of hardware in the station is this lively crew. The studio engine resides in control and handles mixing duties; the Element GPIO unit lives in Studio A and runs the Element as well as GPIO sources. We had a great deal of frustration with these units prior to the installation of an Online (double conversion) UPS which literally converts the power to DC and back to AC before delivering it to the studio; thus Studio A gets the cleanest feasible power source and since that point we have had no problems. Occasionally it would previously crash, necessitating reboot (there's a separate wiki page on that). It's now attached to a PDU allowing us to remotely pull the plug.

### Powerstation main and aux

Axia's solution to the disaster above was this duo, running in studio C. Combines EGPIO, Studio engine, a switch, and several nodes worth of I/O. Works quite well and features a redundant PSU setup between the two.

We have had this go offline a few times, and as a result I moved the PDU such that it plugs directly into the Control switch. You can use it to pull the plug remotely and give it some time to chill before rebooting.
