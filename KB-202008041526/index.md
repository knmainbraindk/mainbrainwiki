---
title: Sender Policy Framework
zid: KB-2008041526
category: kb
tags:
- #spf
- #mail
---

#### source: [web.archive.org](https://web.archive.org/web/20190226105314/http://www.openspf.org/FAQ/Common_mistakes)

SPF records can be quite simple (`v=spf1 a -all`), but they can also be rather complex, to account for the multitude of different outgoing mail server configurations that exist on the Internet. Newcomers to SPF often seem to make similar mistakes when creating their first SPF record. In general you should:

### Begin by making a list of your mail servers

The purpose of SPF is to advertise your domain's mail servers. It often helps to make a list before starting. Consider whether any of the following are used to send mail:

*   web server
*   in-office mail server (e.g., Microsoft Exchange)
*   your ISP's mail server
*   mail server of your end users' home ISP
*   any other mail server

Only the final mail server is relevant. If your company has a more complicated setup where an internal mail server routes mail through an outgoing mail server for delivery to the world, only the outgoing mail server would be listed in SPF.

Note: at one point in time, AOL would capture outgoing SMTP (port 25) traffic from its users and transparently intercept and re-route the message through AOL's outgoing mail servers. Thus any AOL users would end up sending mail through AOL's mail servers whether they wanted to or not. Using an alternate port such as port 587 _may_ work to get around this if your hosting company supports it.

### Create a list of your [domains](/web/20190226105314/http://www.openspf.org/DNS/Domain)

Chances are you have more than just one [domain](/web/20190226105314/http://www.openspf.org/DNS/Domain). Domains that are not used _by you_ could still be abused by spammers! Also see [Publish null SPF records for...](#all-domains)

### List a server only once

Ultimately, SPF lookups resolve to an IP address. It is not necessary to list the same server using multiple host names (e.g., "example.com" and "www.example.com" which both resolve to the same IP). In fact doing so is a bit harder on your DNS servers since a receiving server progressing through your record may be forced to make multiple DNS lookups, when simply referencing the server hostname once would have been sufficient.

If the server's IP rarely changes, consider using the `ip4:x.x.x.x` (or ip6) notation so recipients can avoid DNS lookups entirely. Since there is a limit of 10 DNS lookups per SPF record, specifying an IP address or address range is preferable for long lists of outgoing mail servers.

Often an SPF record can be condensed down to something like `v=spf1 ip4:x.x.x.x -all` if there is only one outgoing mail server.

### Only list outgoing mail servers

SPF's purpose is to publish a list of outgoing mail servers. Any servers that do not deliver mail to the world, such as web servers or incoming-only mail servers, should not be listed.

### Only use "mx" if your MX servers are used for outgoing mail

Sometimes when using configuration aids it is easy to add the mx mechanism. However MX records are used to route incoming mail for your organisation, and the same server(s) may or may not be used for your outgoing mail. If the IP address of your outgoing server is covered by an a, ip4, or other mechanism, it is not necessary to reference that server again using the mx mechanism (see [list a server only once](#only-once) above). If the servers listed in your MX records are only used for incoming mail, it is not necessary to use the mx mechanism.

### Use "mx" with domain names, not mailserver names

Specifying mx:mailserver.example.com is generally incorrect, unless you truly want SPF validation to look up all the hosts that accept mail for the "mailserver.example.com" domain. (Usually, there will not be any such hosts, because "mailserver.example.com" is itself a host, not a domain.) This will not show up as a syntax error, however, it will simply not match anything.

The correct usage for validating against the MX records for "example.com" is mx:example.com, or if you want to specify a particular mail server's hostname or IP, a:mailserver.example.com or ip4:_x.x.x.x_. Finally, note that when your SPF rule is stored as a DNS record associated with "example.com", then "example.com" is the default domain for the rule, so mx on its own (with no explicit domain specified) is sufficient to check the sender IP against all the MX mail hosts listed for "example.com", in that context.

As of 2008 the [SenderID](https://web.archive.org/web/20190226105314/http://www.microsoft.com/mscorp/safety/content/technologies/senderid/wizard/default.aspx) wizard makes it easy to get this wrong. As a simple rule, if the commands _\`dig -tmx mailserver.example.com\`_ or _\`nslookup -q=mx mailserver.example.com\`_ yield nothing, then using mx:mailserver.example.com wastes the bandwidth of receivers checking SPF as well as the bandwidth of your own name servers answering pointless queries.

### Don't assume – especially if you are an ISP

If you host e-mail for others, do not just create an SPF record for a customer without researching what e-mail servers that customer uses. You may find you have blocked or hindered your customer's outgoing mail delivery from their in-office mail server, for example, or from end users who send mail through their home ISP's mail server. See the [hints for ISPs](/web/20190226105314/http://www.openspf.org/FAQ/Hints_for_ISPs) for the safe _include_ magic.

### Only "include" existing SPF records

Let's say you want to include your web hosting company's outgoing mail servers in your SPF record. Let's also say _Network Solutions_ hosts your web site and e-mail. You may be tempted to use something like `include:networksolutions.com` in your SPF record. However there are two potential problems with this. As of this writing, _Network Solutions_ does not publish an SPF record for the networksolutions.com domain. Therefore using `include:networksolutions.com` instantly makes your record invalid.

The other problem is more subtle: `include:networksolutions.com` would include mail servers authorized to send mail from the domain networksolutions.com. This may or may not be the same list of mail servers _Network Solutions_ uses to send mail out using customer domains! Sometimes an ISP will create a special SPF record that customers can include with their record, such as `_spf.example.com`. If you want to use an ISP's mail server(s) you should ask them if they maintain an SPF record for their customers to include, or else you will need to change your record every time your ISP adds, removes, or changes a mail server's name and/or address.

### Publish SPF records for HELO names used by your mail servers

Checking HELO/EHLO names is [recommended](/web/20190226105314/http://www.openspf.org/RFC_4408#helo-ident) by the [SPF RFC](/web/20190226105314/http://www.openspf.org/RFC_4408). Publishing records for these hostnames is an important part of the SPF protocol. HELO or its modern version EHLO is used when Mail from is <> even if a receiver does not do 100% HELO checking.

Publishing a HELO rule involves creating an SPF record linked to the HELO FQDN used by your mailserver (example: "mailserver.example.com"). Normally this should be an entirely separate SPF rule to the one which checks the from addresses in your domain which might be associated with say "example.com". A simple example of two policies might be:

> example.com.             IN  TXT  "v=spf1 mx -all"
> mailserver.example.com.  IN  TXT  "v=spf1 a -all"

The first rule would be activated by any from address ending with "@example.com", and would validate such an email only if it comes from an IP address associated with an MX record for "example.com". The second rule would be activated by a HELO identification of "mailserver.example.com", and would validate the email only if it comes from the IP address associated with that server.

Another reason to take HELO names into account has to do with [Publish null SPF records for your domains that don't send mail](#all-domains). Suppose you follow the advice in that FAQ but don't think about HELO names, you could inadvertently deny servers the right to send email. An example: a cloud of webservers send email forms out, using "[webform@example.com](https://web.archive.org/web/20190226105314/mailto:webform@example.com)" as the sender's address. Each webserver uses (as it should) its own name as the HELO parameter.

> www.example.com.     IN  TXT  "v=spf1 -all"
> web01.example.com.   IN  TXT  "v=spf1 a -all"
> web02.example.com.   IN  TXT  "v=spf1 a -all"
> web03.example.com.   IN  TXT  "v=spf1 a -all"

Eventhough there are no email addresses like "[user@web03.example.com](https://web.archive.org/web/20190226105314/mailto:user@web03.example.com)", the name "web03.example.com" **is** used for email!

If you don't publish an SPF policy for such domains, they are game for spoofers. And if you do publish an SPF policy, you better allow your host to use its own name.

### Publish null SPF records for your domains that don't send mail

Once you've protected your mail sending domains with SPF, if someone is trying to spoof you, then first thing they will try is to spoof your non-mail sending domains. Publishing "v=spf1 -all" says that a domain sends no mail. As an example, you might publish:

> example.com.       IN  TXT  "v=spf1 a:mail.example.com -all"
> mail.example.com.  IN  TXT  "v=spf1 a -all"
> www.example.com.   IN  TXT  "v=spf1 -all"

### Test your new SPF record to make sure it is valid

Use a [testing tool](/web/20190226105314/http://www.openspf.org/Tools) to test any new SPF record.

### Publish your SPF record in the correct DNS server

SPF is based on DNS lookups, so for the world to find your SPF record you need to create it on the correct DNS server. If you do not know which are the "authoritative" (main) DNS servers for your domain, do a "whois" lookup on your domain or ask your web hosting company.

### Allow for DNS caching during testing

Remember that if you are using a testing utility to look up your SPF record in DNS, you need to wait until its TTL (time to live) expires and the change propagates to the world before the utility will see any changes. Often it is easier to paste your SPF record into the utility instead, so that your changes will be seen immediately.

### Tell your users

Don't forget to give instructions to people that need to send mail using the domain you have just protected. They may need to configure SMTP AUTH in their email client, for instance, and you will need to assign them a login and password. If sending from hotel PCs (or whatever) is now forbidden, they need to know about it.

---

Clipped on Tuesday, August 4, 2020, 3:24 PM