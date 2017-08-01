# Operational-NAT64-DNS64
Details of how to build a network for IPv6-only clients using DNS64/NAT64

"The only Zen you find on the tops of mountains is the Zen you bring up there."
 
 Robert M. Pirsig


THE STORY SO FAR (July 2017- Alan Whinery, co-chair of the Internet2 IPv6 Working Group)

This inquiry arose out an effort to develop some IPv6 tutorials for the Internet2 Technology Exchange in San Francisco, October 2017.

The central question in this inquiry is:

 "Can someone with few or no IPv4 addresses build a network without IPv4, providing access to the entire Internet?"

After some initial work, it seems as if the answer is "yes with conditions". 

Our approach to a v6-only network is using DNS64/NAT64. When one sets up the pieces and starts using it, at first it seems indistinguishable from using an IPv4 or dual-stack network, but eventually one will find issues. As one works on defining a working, shareable DNS64/NAT64 setup, one encounters many and sundry bits of information to record and organize, hence this git. 

SOFTWARE

In the arrangement of a D/N64 network, there are choices to be made for each of the pieces. As of this writing, the following are in use in various deployments:

For NAT64:
            Jool 3.5 (http://jool.mx) for the Linux-based NAT64 (On Debian 8 and Raspbian 8)
            Cisco IOS-XE 3.9S running on an ASR 1001 for the Cisco-based NAT64
                        
For DNS64:
            BIND 9.8 running on Debian 8
            (intention to evaluate InfoBlox DNS)

For 464XLAT CLAT:
            (intention to evaluate Jool 3.5)
            (intention to evaluate Cisco IOS-XE)

For IPv6 ND RAs with RDNSS:
            Cisco IOS-XE 3.9S 
            radvd Version: 1.9.1

For DHCPv6:
     ISC DHCP Server version

INFLUENTIAL DOCUMENTATION: The following resources have been useful in getting started

Incremental Deployment of IPv6-only Wi-Fi for IETF Meetings
  draft-jjmb-v6ops-ietf-ipv6-only-incremental-00
  https://datatracker.ietf.org/doc/draft-jjmb-v6ops-ietf-ipv6-only-incremental/
  
Jool docs
  http://jool.mx/en/documentation.html

