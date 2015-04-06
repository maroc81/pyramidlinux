## Configuring Pyramid Mesh ##

Some OLSR references

  * [olsr.org homepage](http://olsr.org/)
  * [The OLSR Story/history](https://www.open-mesh.net/optimized-link-state-routing-deamon/olsr-story.txt/view)
  * [O'reillynet article](http://www.oreillynet.com/pub/a/etel/2006/02/10/free-mesh-networking-with-metrix-pebble.html) on Metrix-Pebble and OLSR
  * [Wireless Networking in the Developing World](http://wndw.net/)
  * [Linux OLSR IPv6 How To](http://www.tldp.org/HOWTO/html_single/OLSR-IPv6-HOWTO/)

### OLSR ###

OLSR is a dynamic link state mesh routing protocol.

Currently the web interface only supports a few options, but it should be enough to get a basic mesh going.

If you are going to mesh any pre-existing networks or do anything more complex than an OLSR only network, you should edit /etc/olsrd.conf by hand.

### OLSR Configuration ###

![http://farm3.static.flickr.com/2354/2247886683_9fb9df3256.jpg](http://farm3.static.flickr.com/2354/2247886683_9fb9df3256.jpg)

> Enable OLSR::
> > Obvious enough. Check this box to turn on mesh. Note that the httpinfo plugin doesn't do anything either until this is enabled.


> ath0, eth0, wlan0::
> > Your list may differ, but you should see one choice for each interface (wired or wireless) in your device. You guessed it, check the box that corresponds to the interface you wish to run OLSR on. Generally this will be the 'backbone' or 'backhaul' of your network. For example, you might run 802.11b locally on the wlan0 interface and run 802.11a on the ath0 card to mesh your nodes.


> httpinfo::
> > Enable this to get [nice status](http://www.olsr.org/files/httpinfo/config.html) about the current state of the mesh network from this box. Set the port as desired.


> dyn\_gw::
> > If the box you are configuring will be connected to the internet, enable dyn\_gw and provide an address that it can ping to confirm that it is connected (the default 72.1.140.203 is the metrix webserver http://metrix.net). You could leave this always enabled if the internet connection comes and goes and it should do the right thing.

### Advanced ###

![http://farm3.static.flickr.com/2284/2247886781_cdce12fe0d.jpg](http://farm3.static.flickr.com/2284/2247886781_cdce12fe0d.jpg)


Announcing non OLSR routes.


> OLSR only propagates routes that it knows about.   To announce additional routes, add HNA4 rules to /etc/olsrd.conf. By default OLSR only advertises single hosts, not full subnets, which you want if your nodes are going to act as routers. Example, advertise a node as the default gateway & 1 subnet (probably the internal interface).
```
Hna4
{
0.0.0.0 0.0.0.0
192.168.145.0 255.255.255.0
}
```

Nameservices

By combining OLSR's nameserver plugin (to create /var/run/hosts\_olsr and DNSMasq's name services, you can do some very interesting DNS tricks.

> see http://seattlewireless.net/DnsMasqSetup for automagic dns.

## Verify its Working ##

![http://farm3.static.flickr.com/2358/2248680938_ca684a7d76.jpg](http://farm3.static.flickr.com/2358/2248680938_ca684a7d76.jpg)

After saving the above settings, OLSR will start up and find routes.

Route Visualizations are available on the Route Info page.


## Encryption ##

See ConfiguringEncryption for a quick guide on configuring WPA for a Pyramid box at either end of a link.