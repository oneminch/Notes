---
id: dns
title: "Computer Networks: DNS Basics"
description: "What is the Domain Name System?"
tags:
  - dns
  - http
  - https
  - networking
image: "/content/cover/dns.png"
cover_image: https://raw.githubusercontent.com/oneminch/portfolio/main/public/content/cover/dns.png
canonical_url: https://minch.dev/blog/dns
series: Computer Networks
navOrder: 1
published_on: "2022-02-21"
---

## Introduction

When a user makes any form of request on a network such as a website by typing the URL, all the user is asking is the files associated with that URL. To fetch these files, the client needs to know which computer (server) on the Internet they are being hosted on and open a secure connection to that computer. On a network, computers and different network devices can't identify and locate one another using names. Instead, they communicate with each other using what is known as IP addresses. Therefore, the client needs to know what the IP address of the server is. Since users can't memorize the IP address of each website they're using, the client needs a way of figuring out what IP address is associated with the given URL. This system of mapping or translating domain names to corresponding IP addresses is known as the **Domain Name System** or **DNS**.

The Domain Name System is a distributed database of hostname to IP address mappings. It is updated whenever someone purchases and register a new domain. You can imagine this being as the phone book of the Internet. Its primary function is to provide translation or resolution of hostnames to IP addresses.

It is much easier for you to memorize the domain name of a service (e.g. https://duckduckgo.com) than one of its corresponding IP addresses (e.g. 23.21.193.169). Typing the IP address in the URL bar and submitting would still take you to the site, but doing that for every website you are using is not very convenient. Instead, your computer relies on DNS servers to automatically do the mapping for you. To make requests even faster, it uses caching to store mappings for easier future reference.

The role of DNS is more predominant in distributed computing for the reason that it maps domain names to the IP address of the server that is closest to the client requesting it. This means the same domain name can be mapped to different IP addresses at the same time, which is a key feature in providing a faster and more reliable response to users.

## How DNS Works

DNS servers can be any of these 4 categories:

1. Recursive nameserver (DNS Resolver)
2. Root nameserver
3. Top-level Domain (TLD) nameservers
4. Authoritative nameservers

Let's assume a user wants to visit https://mozilla.org and types the URL in the bar.

1. The computer searches for the associated IP address in the local DNS cache to see if this site has been recently retrieved. If it is found, the process ends here and the IP address gets returned.

2. If not found in the local cache, the computer continues to ask the DNS resolver from the Internet Service Provider (ISP) which has its own cache. Many customers of the ISP are likely using the same resolver, so popular services and domains will probably be cached. It looks for the mappings in the resolver's cache as well. If it's found, the process ends here and the IP address gets returned. Otherwise, it continues to the next stage.

3. The DNS resolver queries the root nameservers, which don't know the IP address but help direct the queries to the servers that know where to find it. These are responsible for knowing the IP addresses of the servers for each top-level domain (TLD). They look at the TLD of the domain name, which in our case is the .org in mozilla.org. Each TLD has its own set of nameservers. Then, it forwards our query to the TLD nameserver responsible for .org domain names.

4. The TLD nameserver looks at the next part of the domain name, the second-level domain (Mozilla in this example), and it directs the query to the authoritative nameserver which is responsible for this particular domain. This is the final stop of the DNS servers, and it is responsible for all the details about a particular domain. It contains many types of records, which are sets of different kinds of information about the domain. In this example, we are only looking for the IP address of the web server, so we request the authoritative nameserver for that information.

5. The DNS resolver receives the info and stores in its local cache for future reference. Another customer wanting to navigate to https://mozilla.org is spared this lookup process because of caching. But, cached records have expiration dates and need to be replaced with new copies by the resolver to ensure up-to-date information.

6. The record is returned to the client by the resolver. The client stores the record in its own cache. It then retrieves the IP address from the record and passes it to the browser, so the browser can open a connection and make the request to the web server with the site information.

> **Note**: In occasions where the query contains a subdomain (e.g. https://developer.mozilla.org), there will be an extra nameserver that gets added to the end of the sequence which is responsible for that subdomain (`developer`).

![DNS Resolution Flowchart](/content/dns.resolution.png)

All this process is performed whenever someone wants to visit a website, and it is completed in a matter of milliseconds.

It is important to know that caching may cause some problems. If a certain website changes its IP address and the local cache is not updated, that site may not be accessible since its address has changed and the cached address is now outdated. Security issues may also arise due to caching. If a malware has infected a user's device and poisoned the local cache, it may change the entries of hostname to IP mappings. It may change the IP address of a certain site, so it points to the server of a malicious site instead of the actual server. Therefore, clearing DNS cache regularly and using some anti-malware software is necessary.

## DNS over HTTPS (DoH)

As you saw from the above text on how DNS works, DNS queries pass through the DNS resolver, which is basically an ISP. The information being passed around is in plain text, which means anyone including the ISP and a potential attacker can view DNS queries and therefore where you want to navigate to. This can be used for surveillance, eavesdropping, or to manipulate actual data to make users visit malicious sites. This raises big security and privacy concerns.

In recent years, there is a movement to implement encrypted DNS with a protocol known as DNS over HTTPS (DoH). DoH protocol takes advantage of the HTTPS protocol to encrypt DNS queries. It is the similar concept behind encrypting HTTP requests. It provides more security and privacy to users as it encrypts DNS data between the client and the resolver. Widely used browsers like Firefox Browser have already added these features in their settings, and it's being implemented by more and more browsers.

---

_Originally Posted on [OpenGenus IQ](https://iq.opengenus.org/domain-name-system-explained/)_
