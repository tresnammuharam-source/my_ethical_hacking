# apa itu DNS?


try tools in VM :
user@thm:~$ nslookup --type=CNAME website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

** server can't find .website.thm: NXDOMAIN
user@thm:~$ nslookup 127.0.0.53.website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

** server can't find 127.0.0.53.website.thm: NXDOMAIN
user@thm:~$ nslookup --type=A website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

Non-authoritative answer:
Name: website.thm
Address: 10.10.10.10

user@thm:~$ nslookup website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

** server can't find .website.thm: NXDOMAIN
user@thm:~$ nslookup --type=MX website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

Non-authoritative answer:
website.thm mail exchanger = 30 alt4.aspmx.l.google.com

user@thm:~$ nslookup --type=TXT website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

Non-authoritative answer:
website.thm text = "THM{7012BBA60997F35A9516C2E16D2944FF}"

user@thm:~$ nslookup --type=CNAME shop.website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

Non-authoritative answer:
shop.website.thm canonical name = shops.myshopify.com

user@thm:~$ nslookup website.thm
