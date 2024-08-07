---
layout: cheatsheet
tags: dns dig dog nslookup reverse lookup
section:
  - name: DNS lookup
    commands:
      Get IP for domain name: dig google.com
      Get domain name for IP (reverse lookup): dig -x 157.240.210.35
      Shorten output: dig -x 157.240.210.35 +short
      Get A records: dig +noall +answer -t A google.com
      Get AAAA records: dig +noall +answer -t AAAA google.com
      Get MX (e-mail, smtp) records: dig google.com MX
      Specify DNS server: dig @8.8.8.8 google.com
      Trace: dig +trace google.com
      DNSSEC (flags must include ad and response RRSIG): dig cyberciti.biz +dnssec +multi
      DNS over TLS (DoT): dig +tls google.com
      DNS over TLS (DoT) via dog: dog google.com --tls @dns.google
---

# dig ns nslookup

> dig uses the OS resolver libraries. nslookup uses is own internal ones.
> That is why Internet Systems Consortium (ISC) has been trying to get people to stop using nslookup for some time now. It causes confusion.

[Source](https://unix.stackexchange.com/questions/93808/dig-vs-nslookup)

# dig vs dog

I recommend using [dog](https://github.com/ogham/dog), a command-line DNS client written in Rust.

The only downsides vs. dig are

1. the missing support for DNSSEC yet:
[DNSSEC support : query and validation #65](https://github.com/ogham/dog/issues/65)
2. and reverse lookups are not supported AFAIK
