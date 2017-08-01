In order to make an un-patched BIND9 return a NXDOMAIN for any A record request, whether there really is an answer or not, so that resolvers in client cannot choose to prefer A over AAAA. This is for use in a DNS64/NAT64 network, where all questions for existing hosts have AAAA answers, whether they are "real" or "synthesized". 

Using ngrep to develop a regexp to match A requests on the wire:

ngrep -d eth0 -q -F filter -O dns-requests.cap  "\x00\x00\x00\x01\x00\x00\x00\x00\x00\x01.(([a-zA-Z0-9]|[a-zA-Z0-9][a-zA-Z0-9\-]*[a-zA-Z0-9])[^A-z0-9\-])*([A-Za-z0-9]|[A-Za-z0-9][A-Za-z0-9\-]*[A-Za-z0-9]\x00)\x00\x01\x00\x01"

with file "filter" consisting of:

  udp and dst port 53

seems to work.

Using the REGEX match from:
  https://github.com/xnsystems/kpcre/wiki/iptables-string-regex

(I haven't checked whether it works with ip6tables, which is what it needs to do)

Which has a decent DKMS install process, one can write something like:

iptables -A INPUT -p udp -m udp --dport 53 -j dnsnoa

iptables -A dnsnoa -p udp -m string --string "/\x00\x00\x00\x01\x00\x00\x00\x00\x00\x01.(([a-zA-Z0-9]|[a-zA-Z0-9][a-zA-Z0-9\-]*[a-zA-Z0-9])[^A-z0-9\-])*([A-Za-z0-9]|[A-Za-z0-9][A-Za-z0-9\-]*[A-Za-z0-9]\x00)\x00\x01\x00\x01/" --algo regex -j dns2

<redirect to named2 > 

And:
-A OUTPUT <rewrite so that it comes from src port 53>



