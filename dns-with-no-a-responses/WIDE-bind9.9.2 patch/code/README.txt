Files from patch used by WIDE project, written by T. Jinmei while at ISC.

Code and named.conf taken from http://member.wide.ad.jp/tr/wide-tr-live-with-ipv6-wg-ipv6-depolyment-in-japan-01.pdf

Reference in https://www.ietf.org/proceedings/87/slides/slides-87-sunset4-8.pdf

  Of course, A record filtering on DNS64 resolver may work
    • Unfortunately, the current DNS A record filter patch for bind 9.9.2.p1 does not
       work well with DNS64 configuration
    • The patch is simple, just convert AAAA filter parts of bind to A filter
    • However, we met several unexpected segmentation fault errors
    • The patch works well on a simple DNS forwarder
    • If A record filtering does not affect other functions of DNS (cache, glue, etc.), A
      record filtering on DNS64 is reasonable


