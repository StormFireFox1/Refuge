+++
title = "Around The World in 80 (VPN) hops"
date = 2019-02-07T11:30:12+02:00
publishDate = 2019-02-20T12:00:00+02:00
draft = false
weight = 0
tags = ["networking", "vpn", "privacy"]
categories = ["Privacy"]
+++

*This is a verbatim copy of the article written for Stempathy, a STEM-oriented teen magazine, with the exact*
*same title. Anything that might seem out of context is most likely explained by reading this article directly*
*from the magazine itself.*

---

Hello everyone! I'm Matei Gardus, a programmer with a knack for side-projects and insane complications
and min-maxing over every aspect of my life. I hope you enjoy this first issue of Stempathy.
Today I'm going to be telling you about one of my ongoing adventures in the world of networking, and it
starts around three years ago.

There was once a time when Netflix wasn't available in Romania, along with all the other streaming services
we've all come to know and love, such as Spotify. However as you can imagine, for a guy like me who knew of
their benefits, I couldn't idly stay being complacent; I wanted to find a way to get all those services in
Romania legally and in an efficient way.
Luckily for me, I had a lead on how to do just that.

---

## A friend

Whenever we get the chance, my family and I go to the United States to not only see new landmarks and get
new experiences, but also to visit my Mon's childhood friend who moved there. Her husband and her are very
nice people and we all enjoy the time when we're there. They welcome us into their home every time we visit,
almost like a home away from the home across the world. Whenever we go there, my father and I also fix whatever
problems they may have with computers, phones and the like, so it makes for a interesting time in that domain
as well (my most interesting tech support stories come from there, you can e-mail me anytime about them).
However, last year, they were also in need of a new Internet configuration, so we helped with that as well.
When we asked what limitations do we have, they said:

> "Go wild! We just want it to work well and fast!"

It was at that moment that my father and I exchanged some knowing glances and asked our friends if they
would be so kind as to allow us to use their Internet connection ourselves from anywhere in the world.
They allowed us, and so the lead was ready to be followed.

We have an US-based IP available to us, so we could theoretically access all the available streaming
services using it. But how could we do that from Romania? Well, that took a *lot* of work and quite
a bit of tinkering.

---

## VPNs everywhere

Obviously, firstly, we would need a **VPN** to access the local network from our friend's house from Romania.
You've probably heard of VPNs as a way to access geo-locked websites from anywhere in the world (what you've
probably used some VPNs for already, although I do not recommend using free ones) but that's not what they
were originally intended for, really.

VPN stands for "**V**irtual **P**rivate **N**etwork and they were initially designed to be used in order
to access a local network through an encrypted tunnel and act like a member of said local network. That
way, you could establish a tunnel to a VPN server that might be installed at, let's say, your workplace,
and once you connected to it, your computer would act as a legitimate device connected to that network,
without any third party being able to extract confidential information from this very public connection.
There is also the option to connect two separate local networks together, and have them act as one
cohesive network (this is called a **site-to-site** VPN, as opposed to the **remote-access** VPN previously
discussed). I used this type to link two separate networks together, one in my house and one at my
friends' house.

![A graphical representation of a VPN.](/public/img/vpn-representation.jpg)

To set up a VPN server anywhere is not inherently complicated, most routers actually do come with the option
to connect to a VPN server. Unfortunately for me, however, my friend's router could not host a VPN server
normally, so we decided to ship our own solution there, an EdgeRouter 4 from Ubiquiti, which looks something
like this:

![Picture of the EdgeRouter 4.](/public/img/edgerouter-4.jpg)

After getting it in there, I configured the VPN server, along with a few clients configured for my iPad, my PC,
my dad's PC, etc. We had two Wi-Fi networks in our home, "Rares" and "Rares_us", one that was a simple access point
to our normal Internet, the other being an access point attached to a switch which kept the VPN tunnel running.
We finally solved our problem elegantly, and now we could watch Netflix using a VPN tunnel to the US that always
worked...

Except when it didn't.

---

## Meet The Problems

As is always the case in the world of computer science, nothing *ever* works on the first try, but that is because
we delude ourselves with the idea that what we are working on is as simple or complicated as we think it is,
when in reality, it never is. And the problems started showing up very soon.

For starters, our VPN tunnel would frequently drop due to unnatural circumstances (i.e. power outages, random person
tripping over a plug, as is often the case in my house), so I had to find a way to automatically restart the VPN
tunnel whenever I needed to. I did so by essentially adding **cron jobs** (scheduled tasks in Linux) that would run
periodically to check whether our VPN tunnel was still up and running, and if not, to re-enable it and send my father
an e-mail telling him of the outage so we know if something went wrong.

```bash
#!/bin/bash
# Ping tunnel, make sure it's open
/bin/ping -c 5 -i 3 -W 3 172.16.100.1 1>/dev/null 2>&1
if [ $? -ne 0 ];
   then
      echo "Failed ping tunnel! First try"
      # We'll give the tunnel the benefit of the doubt, let's try again
      sleep 2
      /bin/ping -c 5 -i 3 -W 3 172.16.100.1 1>/dev/null 2>&1
      if [ $? -ne 0 ];
         then
             echo "Failed ping tunnel ! Second try"
             # Restart the VPN
             /bin/vbash -ic 'restart vpn'
             # Send e-mail to make sure everyone knows
             /bin/vbash -ic 'echo -e "Tunnel down\nRestarted IPSEC VPN\nTimestamp: $(date)" | /config/scripts/notifyemail'
         else
             # The VPN works after the second try
             echo "Ping tunnel success!"
      fi
   else
      echo "Ping tunnel success!"
fi
```

In addition, my home is a bit more special than your average household. We have two internet lines linked to my
house, provided by two different ISPs, both of which were in Romania. This meant we had to use one of the networks
in order to establish a VPN tunnel to the US, but it wouldn't be incredibly stable, since we could have our Internet
connection randomly cut as well. In addition, it would also mean that not all the devices had access to the US network.
In the end, I decided to have *two* VPN tunnels open on two different networks, with both on separate Wi-Fi networks. But now the
question is *"Which network do I use to connect to the US or to Romania?"* I mean, don't get me wrong, I love the
freedom of choice, but having 7 Wi-Fi networks is not fun for me or for any potential guest to our home. So, in the end,
I decided to reduce the number of networks by implementing a **load balancer** between the two separate VPN networks.
Now we only have two Wi-Fi networks: "Rares RO" and "Rares US", and both handle all requests quite nicely.

A load balancer is, essentially, a piece of software that takes requests of a specific internet protocol and redirects
them to whichever server is less overloaded with requests, or even using a specific set of rules that you apply to its
configuration. It is commonly used at all the major websites, like Google, to distribute requests in a region to
multiple servers, not just one, since one server will never be capable of handling everything. Imagine having one PC
handling billions of searches a second. That's not gonna happen.

This becomes even more complicated as we find out a relatively crucial issue with our VPN: as much as it is currently
working on two separate networks, load balanced and all, nothing in our house is stable, and not even at our friend's
house either. Network packets were randomly dropped for no reason and some packets just straight up disappeared, as if
lost through the tunnel. Something was wrong with my tunnel and I didn't know what. After a bit of debugging, though,
I finally figured out the problem: NAT.

---

## NAT: The Final Boss

To explain what NAT really is, one must understand a bit about IP addresses as well, those nifty four numbers with 
dots between them you may have found on the Internet (They look like this: xxx.xxx.xxx.xxx). IP addresses are a way
to know where to address a specific packet so that whoever is supposed to receive it can get it correctly. There are
different types of IP addresses:

- Class A, generally assigned to all the external servers of the world (1.1.1.1, for instance, is a DNS server for everyone to use.
If you don't know what a DNS is, that's a story for another time)
- Class B, reserved for medium-sized networks (i.e. huge corporation departments)
- Class C, most commonly found in homes (192.168.1.1, 172.16.0.61)

*(Tech rant: Technically, the reason why there are multiple classes is due to the way that computers handle transforming*
*an IPv4 address to a physical address, since they require specific limitations to the IPs in order to be converted*
*correctly, but this is beyond the scope of this article.)*

There is, however, one problem. Due to the world having way too many computers, and IP addresses being restricted to
very limited amounts (or rather, IPv4 addresses, the ones I'm talking about here, IPv6 addresses could account for
more computers than there are atoms in the observable universe), people have decided to reuse some IP addresses
by having closed networks with the same IP addresses in them (non-routable addresses, of type C) and switching between
network using a method called NAT.

NAT, short for **N**etwork **A**dress **T**ranslation, is a method used to switch the IP addresses I've been talking about
by "modifying network address information in the IP header of packets while they are in transit across a traffic routing device."
(Thanks, Wikipedia!) This way, you can have your phone communicate with any other website as if it were on the same network.
*However*, in a VPN, NAT can be a pain, since it can't really change those encrypted packets that the VPN sends over.
Essentially, you have to find a way to manually change the IP header before it his encryption so that you can redirect
the packet at the right address on the other side of the tunnel (oh, this has to be done on both sides of the tunnel as well,
so you can't shortcut your way out of this). In the end, I managed to fix the problem by configuring the switches on both
sides of the VPN tunnel to modify the IP header on both sides using predefined rules which, while very hard coded, work well
for our case.

Finally, everything seems fine...right?

---

## Room for improvement

Of course, work is never over, and my father's dream is to reduce those two Wi-Fi networks to one, "Rares", and have the network
automatically figure out through which network you'd actually want to go through when visiting a website by using a DNS whitelist
to route requests through the different networks (netflix.com goes through the US tunnel, for instance), but that is a project for
the future. In the end, if there is one thing that you should really learn from this article is that you should never be daunted
by obstacles that might appear in whatever project you may be working on, since you can definitely get past them and achieve
exactly what you envisioned, provided you put in the effort. And yes, even if your computer might be against you, you will definitely
be able to solve the problem. After all, we made them, we can fix them.
I have plenty of stories I have left to share, and I'm sure you'll all enjoy hearing all about them. I'll give you a hint for next
issue's article here: "tiny PC".
