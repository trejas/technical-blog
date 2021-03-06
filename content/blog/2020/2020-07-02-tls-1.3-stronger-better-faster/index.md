---
layout: post
title: "TLS 1.3: Stronger, better, faster"
date: 2020-07-02
comments: true
author: Mustapha Benmbarek
published: true
authorIsRacker: true
authorAvatar: 'https://s.gravatar.com/avatar/0299204313e4fc8d8c722748fa21a6b2?s=80'
bio: "Mustapha works with startups and companies of any size to support their
innovation. In his role as Solutions Architect at Rackspace, he leverages his
experience to help people bring their ideas to life, providing guidance and
technical assistance on cloud-based and AWS architectures."
categories:
    - Architecture
    - Security
metaTitle: "TLS 1.3: Stronger, better, faster"
metaDescription: "."
ogTitle: "TLS 1.3: Stronger, better, faster"
ogDescription: "."
slug: 'tls-1.3-stronger-better-faster'
---

The vast majority of all traffic on the Internet is encrypted. It took almost
20 years to get to about 40 percent encrypted, and then we jumped another 40
percent plus in just the last four years (source:
[Google Transparency Report](https://transparencyreport.google.com/https/overview)).

<!--more-->

### Introduction

Data center and public cloud traffic are a little harder to gauge, but they
could be between 50% and completely encrypted. Across all theaters, we are
undeniably on our way to 100% encryption.

{{<image src="Picture1.png" alt="" title="">}}

While this trend has been growing, the IETF (Internet Engineering Task Force)
released the latest version of TLS in August 2018. Here we are, a few years later,
and encryption is widely supported and deployed. This new version introduces
several changes with a goal to improve the overall security and provide privacy
with the protocol. However, some of these changes have a negative impact on
network-based security solutions. While you might view encryption as a feature,
some real-life use cases are not solved easily without such network-based
security solutions.

### What is TLS?

Before diving into the specificities of TLS 1.3, here's a brief overview of what
TLS is and why it is so important in the world of network security. TLS stands
for Transport Layer Security and is a standard protocol for allowing clients and
servers to communicate securely over the Internet. It provides the security
properties of confidentiality, authenticity, and integrity. Web browsers and web
servers commonly use TLS to secure data sent over the Internet.

The ancestor of TLS is the Secure Sockets Layer (SSL) protocol, which Netscape&reg;
introduced in 1994. SSL 2.0, the first publicly released version of the protocol,
was quickly replaced by SSL 3.0 due to security flaws. Because the SSL protocol
was proprietary to Netscape, the IETF formed an effort to standardize the protocol,
resulting in TLS 1.0 ([RFC 2246](https://tools.ietf.org/html/rfc2246)), which
they published in January 1999. Since then, the IETF has updated the protocol to
address security flaws and extend its capabilities, providing the following
releases:

- **TLS 1.1**: 2006, [RFC 4346](https://tools.ietf.org/html/rfc4346)
- **TLS 1.2**: 2008, [RFC 5246](https://tools.ietf.org/html/rfc5246)
- **TLS 1.3**: 2018, [RFC 8446](https://tools.ietf.org/html/rfc8446)

It is worth mentioning that many use the terms TLS and SSL interchangeably, even
though they are completely different technologies.

### Why do we need TLS 1.3?

To understand why the IETF and the security community have been working so hard
to release a new version of TLS, let's consider the issues that these protocols
have had over the years:

- SSL v3.0 had multiple vulnerabilities. It's formally deprecated, so you should
  no longer use it ([RFC 7568](https://tools.ietf.org/html/rfc7568)).

- The TLS protocol has been subject to serious attacks over the last 20 years,
  including attacks on its most commonly used ciphers and modes of operation.
  [RFC 7457](https://tools.ietf.org/html/rfc7457) summarizes all of these attacks
  if you are interested.

- TLS versions 1.0 and 1.1 are both quite old and are rapidly being phased
  out.

- TLS version 1.2 is currently the best choice, but it is also fairly
  old&mdash;about 12 years old. The consensus was that it needed to be updated
  with more modern cryptography advancements.

### What are the key features of TLS 1.3?

TLS 1.3 is a major overhaul of the TLS protocol with two primary benefits:
enhanced security and improved speed. Let's take a look at each of those
improvements in more detail.

#### Enhanced security

The protocol embraces the "less is safer" approach. It removes support for
outdated cryptography, which improves the security and makes it less likely that
someone can break a session because of an insecure cipher suite or some other
form of weak cryptography.

The removed legacy and obsolete cryptography protocols include:

- Static RSA and Diffie-Hellman key exchange
- CBC mode ciphers
- MD5 and SHA-1 hash functions
- 3DES and RC4 ciphers
- Arbitrary Diffie-Hellman groups

TLS 1.3 also removes unsafe built-in features such as compression and
renegotiation, which were vulnerable to some attacks like Compression Ratio
Info-leak Made Easy (CRIME) attacks. Check out the exhaustive list published in
[RFC 7457](https://tools.ietf.org/html/rfc7457). In general, TLS 1.3 supports
fewer modern cryptographic algorithms that are more efficient and more secure
such as:

- RSASSA - PSS signature algorithm
- ChaCha 20 and Poly1305 stream ciphers
- X25519 and X448 elliptic curve Diffie-Hellman key agreement mechanisms
- Edwards curve digital signature algorithm

#### Improved speed

TLS 1.3 is also faster than previous versions of the TLS protocol. It has an
entirely new handshake module, which requires fewer round trips (RTT). TLS 1.2
requires two round trips for a complete handshake. TLS 1.3 uses one round trip
by default, and optionally, with pre-shared keys, can use zero round trips. It's
worth mentioning here that this 0-RTT mode came initially from the
[QUIC protocol](https://www.developer.rackspace.com/blog/quic-a-game-changer/).

### What are the challenges encountered with TLS 1.3?

While encryption is great for privacy and security, it limits network visibility.
The challenge is that these advanced features of the protocol make the enterprise
security model much harder. Enterprises will likely need to replace the
middleboxes in enterprises such as your firewall, Intrusion Prevention System
(IPS), and Data loss prevention (DLP) to handle this new protocol.

Here are some examples that we think will have a negative impact on enterprise
security:

- Due to server certificate encryption during the handshake, you can't whitelist
sites anymore. Therefore, your network security appliance won't be able to figure
out whether you're communicating with a legitimate website (your bank, for example),
or a malicious site, without breaking the connection.

- Due to perfect forward secrecy and the removal of static keys, these man
(or monster) in the middle (MITM) middleboxes can't use your internal server
private key to break the client-server session or inspect the traffic later on.

### Conclusion

No doubt, this latest version of TLS is way more secure than previous ones. It
brings privacy to the heart of the protocol, making TLS implementation very
difficult within enterprises.

Some market leaders, like Cisco&reg; and others, have already come up with new
network security solutions that tackle these challenges with the help of artificial
intelligence.

There is still a long road ahead, and the debate within the NetSec community has
just started. The IETF is currently working on another
[internet draft document](https://tools.ietf.org/html/draft-camwinget-tls-use-cases-05)
that addresses these issues and especially lists all the use case scenarios that
TLS 1.3 impacts negatively.

Use the Feedback tab to make any comments or ask questions.
