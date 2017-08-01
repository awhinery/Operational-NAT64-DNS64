This directory holds info on how to filter A responses from DNS

Directory "iptables-regex-2nd-named" is about how to use netfilter to match DNS requests for A records and redirect them to a second named on another port, which has no answers, and therefore responds with NXDOMAIN. 

Soon-to-be-directory "bind9-no-A-patch" is about rewriting BIND9 code to make A record suppression a feature. 


Note: (from https://stackoverflow.com/questions/15862118/aaaa-dns-query-on-ipv4-interface )
The difference between NXDOMAIN and NODATA is described in section 5 of RFC 2308:

A negative answer that resulted from a name error (NXDOMAIN) should be cached such that it can be retrieved and returned in response to another query for the same <QNAME, QCLASS> that resulted in the cached negative response.
So an NXDOMAIN can be cached based on the QNAME (i.e. "blabla.example.com.") and the QCLASS (usually "IN"). So it means that blabla.example.com does not exist at all. The negative cache entry is independent of the QTYPE. A NODATA answer is different:

A negative answer that resulted from a no data error (NODATA) should be cached such that it can be retrieved and returned in response to another query for the same <QNAME, QTYPE, QCLASS> that resulted in the cached negative response.
Here is QTYPE (i.e. "AAAA") is included. A NODATA negative cache entry only means that this specific record type does not exist for this name.

So: If you receive an NXDOMAIN response then you know that the name doesn't exist at all for any record type. If you receive a NODATA response then you know that the requested record type does not exist, but other record types may exist.
