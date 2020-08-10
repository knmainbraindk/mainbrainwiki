---
title: How to Check an SMTP Connection with a Manual Telnet Session
zid: KB-202008051417
category: kb
tags:
- #telnet
- #smtp
- #cli
---



#### [www.sparkpost.com](https://www.sparkpost.com/blog/how-to-check-an-smtp-connection-with-a-manual-telnet-session/)

In the world of email, there are many facets to testing, but one of the most basic tests you can do is to simply telnet into a given SMTP server.  This test is useful in determining if the most basic of problems do or do not exist.

*   Is the server up?
*   Is there a firewall blocking communication?
*   Does the mail server allow for relaying of a particular domain/email address?
*   What SMTP commands does the mail server support?
*   Does the server respond with the correct hostname?
*   Does the connection work outside any third party software or APIs?

All these questions and more can be answered with a simple telnet test.

As a note, the commands used in the following examples (as well as additional commands) are covered in section 4.1 of [RFC 2821](http://www.ietf.org/rfc/rfc2821.txt).

Most computers come pre-installed with a telnet client.  For those Windows versions that do not, one can be installed by opening the “Programs and Features” section of the control panel and selecting “Turn Windows features on or off”.  With this window open, select “telnet client” and then click OK.

Once a telnet client has been verified to be installed on the server we first need to find a mail server to log into.  For this, we will need the DNS MX record for a given domain. This can be found with the following command (for these examples port25.com will be used, but any domain can be substituted):

Windows:  

nslookup -type=mx port25.com

  
Non-authoritative answer:  

port25.com  MX preference = 100, mail exchanger = mail.port25.com

  
Linux:  

nslookup -type=mx port25.com

  
Non-authoritative answer:  

port25.com  mail exchanger = 100 mail.port25.com.

  
Next we need the DNS PTR for the IP we are going to use.  First we need to know what IP address the internet sees us as having.  To find that we can use a website like:

[http://whatismyipaddress.com/](http://whatismyipaddress.com/)

With the IP address run the following command, where A.B.C.D is the IP address.

Windows:  

nslookup -type=ptr A.B.C.D

  
Non-authoritative answer:   

D.C.B.A.in-addr.arpa name = server.example.com

  
Linux:  

nslookup -type=ptr A.B.C.D

  
Non-authoritative answer:   

D.C.B.A.in-addr.arpa name = server.example.com

  
server.example.com is just an example, and your results will be different.

So now that we have the MX record for port25.com and the PTR for the IP we are going to use, it is time to login to the SMTP server.  To do so, use the following command:  

telnet mail.port25.com 25

  
Something similar to the following should now be displayed:  

Trying 69.63.149.30...

Connected to mail.port25.com (69.63.149.30).

Escape character is '^\]'.

220 mail.port25.com (PowerMTA(TM) v4.0) ESMTP service ready

  
The first command we need to issue to the mail server is the EHLO  or HELO.  This is a basic greeting that starts the communication between the telnet client and the SMTP server.  Also passed is the DNS PTR for the IP address from which we are connecting as determined previously.  

EHLO server.example.com

  
Something similar to the following should be returned:  

250-mail.port25.com says hello

250-STARTTLS

250-ENHANCEDSTATUSCODES

250-PIPELINING

250-CHUNKING

250-8BITMIME

250-XACK

250-XMRG

250-SIZE 54525952

250-VERP

250 DSN

  
This shows the SMTP commands that the SMTP server accepts.  Not all SMTP servers support the same sets of commands. For example, yahoo only shows the following:  

250-8BITMIME

250-SIZE 41943040

250 PIPELINING

  
And aol shows only one with:  

250 DSN

  
The next command we need to issue is the MAIL FROM command.  This determines the address to which bounces are sent. This is not the same as the from header, which is the email address shown in an email client.  

MAIL FROM: <support@port25.com>

250 2.1.0 MAIL ok

  
Now that the MAIL FROM  command has been sent we can send the RCPT TO  command.  This command tells the SMTP mail server to who the message should be sent. This can be the same or different than the to header, which is the email address shown in the email client.  

RCPT TO: <support@port25.com>

250 2.1.5 <support@port25.com> ok

  
The last command to run before starting the body of the message is the DATA  command.  This command lets the SMTP mail server know that everything else about to be sent is the body of the message (which also contains the headers).  

DATA

354 send message

  
It is important to note that if a mail server supports PIPELINING, as mail.port25.com does, the SMTP mail server may wait until the DATA command is issued before responding to any other commands after the EHLO/HELO.  In this case, enter the MAIL FROM, RCPT TO, and DATA  commands before waiting for a response.

Now that the DATA command has been sent we can start sending the message contents.  This starts with the various headers. At minimum a message should contain a to, from, subject, and date header. The headers entered here will be shown to the user in their email client.  

From: "John Smith" <jsmith@port25.com>

To: "Jane Doe" <jdoe@port25.com>

Subject: test message sent from manual telnet session

Date: Wed, 11 May 2011 16:19:57 -0400

  
With the headers set, we now add one blank line with a carriage return/line feed (just press enter twice) and then we start the actual body of the message.  

Hello World,

This is a test message sent from a manual telnet session.

 

Yours truly,

SMTP administrator

  
With the message complete, we need to tell the SMTP server that we are done with the message and want the SMTP mail server to accept it.  This is done with a period on a line by itself. If during the writing of a message a period on a line by itself is needed, you must put 2 periods, the first escaping the second.  

.

 

250 2.6.0 message received

  
Lastly the QUIT  command is sent to close the connection:  

QUIT

221 2.0.0 mail.port25.com says goodbye

  
With that the mail server has now accepted the message for delivery, and it should be sitting in the inbox of the RCPT TO address!!!

Here are all the commands without interruption:  

telnet mail.port25.com 25

Trying 69.63.149.30...

Connected to mail.port25.com (69.63.149.30).

Escape character is '^\]'.

220 mail.port25.com (PowerMTA(TM) v4.0) ESMTP service ready

EHLO server.example.com

250-mail.port25.com says hello

250-STARTTLS

250-ENHANCEDSTATUSCODES

250-PIPELINING

250-CHUNKING

250-8BITMIME

250-XACK

250-XMRG

250-SIZE 54525952

250-VERP

250 DSN

MAIL FROM: <support@port25.com>

250 2.1.0 MAIL ok

RCPT TO: <support@port25.com>

250 2.1.5 <support@port25.com> ok

DATA

354 send message

From: "John Smith" <jsmith@port25.com>

To: "Jane Doe" <jdoe@port25.com>

Subject: test message sent from manual telnet session

Date: Wed, 11 May 2011 16:19:57 -0400

Hello World,

This is a test message sent from a manual telnet session.

Yours truly,

SMTP administrator

 

 

.

250 2.6.0 message received

QUIT

221 2.0.0 mail.port25.com says goodbye

  
~ Scott

[![](https://www.sparkpost.com/wp-content/uploads/2020/02/PMTA_bottombanner.png?is-pending-load=1)](https://www.sparkpost.com/powermta/free-trial/)

---

Clipped on Wednesday, August 5, 2020, 2:16 PM