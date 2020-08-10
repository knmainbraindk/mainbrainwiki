---
title: Explaining the SPF record
zid: KB-2008041135
tags:
- spf
- mail
- spam
---


#### by Nick Canzoneri, [postmarkapp.com](https://postmarkapp.com/blog/explaining-spf)

SPF isn’t just for sunscreen. In the world of email, [Sender Policy Framework](http://www.openspf.org/) or SPF is a method to validate that an email came from an authorized domain. In other words, it is a way to say that Postmark is allowed to send emails for your domain.

[Learn more about using SPF to protect your domain from email spoofing.](https://postmarkapp.com/guides/spf)

How SPF protects you? [#](#how-spf-protects-you)
------------------------------------------------

The [SMTP protocol](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol), the literal definition of email, has no protections on the From field in an email. As long as it’s a valid email address, there is no further validation. A malevolent actor can impersonate your bank, your employer, or anyone at all. This problem led to the creation of SPF.

SPF is a relatively recent solution. Different variations of the idea were proposed in the early 2000s, and these coalesced into the SPF specification as [RFC 4408](https://tools.ietf.org/html/rfc4408) in April 2006. SPF describes a DNS record in a special format to list all the domains allowed to send mail from the domain. This allows spam filters to easily check if the origin of an email is from an authorized domain.

Personally, I think it’s a rather elegant solution in that it uses existing architecture pieces, but it’s definitely not perfect. Using a special format for the TXT DNS record (which I’ll describe below) is non-standard but certainly is an easy way to gain adoption for a specification. The use of DNS for authentication [isn’t without issues either](https://www.zdnet.com/article/google-free-public-dns-services-were-briefly-corrupted/). Despite the flaws of SPF, at Postmark we _highly_ recommend users set up SPF in addition to [DKIM](https://postmarkapp.com/guides/dkim). To paraphrase, we use the spam fighting tools we have, not the spam fighting tools we wish we had. From the [Google Online Security Blog in December 2013](https://security.googleblog.com/2013/12/internet-wide-efforts-to-fight-email.html), 89.1% of the non-spam email that Gmail received was authenticated by SPF and 74.7% was authenticated by both SPF and DKIM.

How SPF records work? [#](#how-spf-records-work)
------------------------------------------------

At a high level, here is the workflow of how a mail server checks SPF:

*   the Postmark server with IP address of 1.2.3.4 sends a message FROM joe@foo.com TO jill@bar.com
*   the bar.com mail server gets the DNS records of type TXT for foo.com, looking for the SPF record
*   the bar.com mail server compares the 1.2.3.4 IP address against the parts of the foo.com SPF record (described below)
*   the message is accepted or rejected based on which part of the SPF record it matches

What SPF records mean? [#](#what-spf-records-mean)
--------------------------------------------------

When you set up a sender signature in Postmark, we recommend you use the following SPF record:

    v=spf1 a mx include:spf.mtasv.net ~all

Let’s break down what that means.

First thing to note is the syntax of the SPF record. It’s broken down into the version prefix and one or more mechanisms:

![Version: (v=spf1) Mechanisms: (a mx include:spf.mtasv.net ~all)](https://public-assets.postmarkapp.com/blog/spf_version_mechanisms.png?mtime=20180411071613&focal=none 2x)

SPF version mechanisms

The version prefix is pretty simple. Since there can be multiple TXT records for a domain, this is the way to let parsers know that this is the record to be used for SPF checking. The mechanisms that follow are checked **left** to **right** and these specify different rules on how SPF is checked for the domain. The record that Postmark gives you has four mechanisms: `a`, `mx`, `include:spf.mtasv.net` and `~all`. Before we go deeper into mechanisms, I need to explain qualifiers.

What are SPF qualifiers? [#](#what-are-spf-qualifiers)
------------------------------------------------------

The mechanisms can also be prefixed with a qualifier which describes the action to take when a sending IP matches the qualifier. The default qualifier is `+`. So the Postmark SPF record is the same as:

!["v=spf1 a mx include:spf.mtasv.net ~all" is equivalent to "v=spf1 +a +mx +include:spf.mtasv.net ~all"](https://public-assets.postmarkapp.com/blog/spf_modifier_equivalence.png?mtime=20180411071611&focal=none 2x)

SPF qualifier equivalence

Let’s go over what qualifiers are available.

*   `+` **Pass**, an IP that matches a mechanism with this qualifier will pass SPF.
*   `-` **Fail**, an IP that matches a mechanism with this qualifier will fail SPF.
*   `~` **SoftFail**, an IP that matches a mechanism with this qualifier will soft fail SPF, which means that the host should accept the mail, but mark it as an SPF failure.
*   `?` **Neutral**, an IP that matches a mechanism with this qualifier will neither pass or fail SPF.

What are SPF mechanisms? [#](#what-are-spf-mechanisms)
------------------------------------------------------

### The “a” mechanism [#](#the-a-mechanism)

![SPF A mechanism](https://public-assets.postmarkapp.com/blog/spf_a_mechanism.png?mtime=20180411071609&focal=none 2x)

Let’s say that I send mail from IP 1.2.3.4 for the domain “example.com”. If “example.com” has an A record that returns 1.2.3.4 then this mechanism will pass.

### The “mx” mechanism [#](#the-mx-mechanism)

![SPF MX mechanism](https://public-assets.postmarkapp.com/blog/spf_mx_mechanism.png?mtime=20180411071612&focal=none 2x)

Any domain that hosts email has one or more MX records. These records define which email servers should be used when relaying email. For instance, when using Google Apps you insert several MX records into DNS. By including the “mx” mechanism, it automatically approves these servers and avoids you having to list them individually. This also avoids maintaining the list if they change later.

### The “include” mechanism [#](#the-include-mechanism)

![SPF Include mechanism](https://public-assets.postmarkapp.com/blog/spf_include_mechanism.png?mtime=20180411071610&focal=none 2x)

Let’s say that I send mail from IP 1.2.3.4 for the domain “example.com”. If the SPF record for “example.com” includes spf.mtasv.net and 1.2.3.4 passes against the SPF record for spf.mtasv.net then this mechanism will pass.

### The “all” mechanism [#](#the-all-mechanism)

![SPF All mechanism](https://public-assets.postmarkapp.com/blog/spf_all_mechanism.png?mtime=20180411071610&focal=none 2x)

The all mechanism will match against everything, and in this case, the result will be a SoftFail for everything that gets to this point.

Further reading [#](#further-reading)
-------------------------------------

There are other mechanisms as well, but hopefully this post is enough to teach you the basics about SPF. [The SPF project](http://www.openspf.org/) is a great resource and the [section on record syntax](http://www.openspf.org/SPF_Record_Syntax) goes into much more detail about the different parts of the SPF record.

Keep an eye on the blog for more topics like this. I’ll have posts about [DKIM](https://postmarkapp.com/guides/dkim) and [DMARC](https://postmarkapp.com/guides/dmarc) coming up. DMARC in particular has become much greater in relevance lately and SPF and DKIM are the building blocks that DMARC uses.

---

Clipped on Tuesday, August 4, 2020, 11:34 AM