A DNS, short for domain name system, is used to **resolve a particular domain name to its IP equivalent**. Domain names (e.g. keycdn.com) are simply used to be more easily read and remembered by humans, however, all domain names are associated with a particular IP address. This can be compared to a phonebook where a person's name would correspond to the domain name (e.g. yourwebsite.com) and their phone number would correspond to the website's IP (e.g. 159.x.x.x).

When you type a website name (like `example.com`) into your browser, **DNS servers** (like internet phone books) look up the correct **IP address** (like `93.184.216.34`) so your computer can connect to the right server.

```shell
dig  https://corporate-dev1.web.app
```
#### How It Works:
1. **Your Device Asks a DNS Server**:
    - _"What’s the IP for `example.com`?"_
2. **DNS Server Checks Its Records**:
    - Both the OS and browser first look at their own DNS caches to see if the information is already stored locally. If not, the resolver must be asked.
    - **Ask resolver**: Once the locally cached DNS records have been checked, the OS asks the resolver. The resolver is usually your ISP (internet service provider). It first checks its own cache to verify if the information is not already stored locally. If it's not, it goes on to ask the root server.
    - **Ask root server**: The next step is to ask the root server. The root server looks at the last section of the request (the .com portion). Although the root server cannot locate the IP address of the website, it tells the resolver where the [top level domain](https://www.keycdn.com/support/top-level-domains) (TLD) servers are for .com. The resolver then stores this information for later use.
    -  **Ask TLD server** - The resolver goes on to ask the TLD servers the IP address of the website in question. Although the TLD servers can't provide us with the required information, they know where to direct our request. The TLD servers provide the resolver with a list of name servers for that website. Again, the resolver stores this information for later use.
    -  **Ask authoritative name servers**:  - Finally, now that the resolver knows what the authoritative name servers are, it can query these name servers and retrieve the required IP information. The authoritative name servers contain all the necessary information regarding a particular domain.
    - **Cache the IP and return it to the browser** - Now that the resolver knows the IP of said domain, it will cache it for later use. At this point, the IP is delivered to your OS where it is locally cached as well. The OS then passes this information on to the browser. Once the browser knows the IP address of the website, it can then begin requesting and receiving information from the website's origin serve
3. **Your Browser Connects to the IP**:
    - Now that it has the IP, your browser loads the website.
#### Key Players:
- **DNS Hosting Provider**: A service (like Cloudflare, Google DNS, or your ISP) that manages the records.
- **Name Servers**: Special servers that store and provide the correct IP when asked.
#### Example:
- **Website**: `example.com`
- **DNS Host**: Cloudflare
- **Name Servers**: `ns1.cloudflare.com`, `ns2.cloudflare.com`
- **IP Lookup**: When you visit `example.com`, Cloudflare’s name servers tell your computer the right IP.
#### DNS Records
DNS servers use DNS records to store information about domain names. There are several types of DNS records, each with a specific purpose.

1. **A (Address) Record**: This type of record maps a domain name to an IP address. For example, the A record for "google.com" might map to the IP address 172.217.1.46.
    
2. **MX (Mail Exchange) Record**: This type of record specifies which mail server is responsible for handling email for a particular domain. For example, the MX record for "example.com" might specify that the mail server for that domain is "mail.example.com".
    
3. **CNAME (Canonical Name) Record**: This type of record maps one domain name to another. For example, a [CNAME](https://www.keycdn.com/support/what-is-a-cname-record) record might map "www.example.com" to "example.com".
    
4. **NS (Name Server) Record**: This type of record specifies which DNS server is authoritative for a particular domain. For example, the NS record for "example.com" might specify that the authoritative DNS server for that domain is "dns1.example.com".
    
5. **TXT (Text) Record**: This type of record is used to store arbitrary text data associated with a domain. It can be used for a variety of purposes, such as domain verification or SPF records for email.


## DNS caching
[DNS caching](https://www.keycdn.com/support/dns-cache) is an important aspect of the DNS system that helps to improve the speed and efficiency of DNS lookups. Caching DNS servers store DNS records in memory for a specified period of time (called the [Time-to-Live](https://www.keycdn.com/support/ttl), or TTL), so that they can respond to queries for that same record without having to query an authoritative DNS server every time.

However, DNS caching can also lead to potential issues such as stale DNS records or DNS poisoning. To mitigate these issues, DNS administrators should monitor their DNS caches regularly, and implement security measures such as DNSSEC (DNS Security Extensions) to prevent DNS spoofing and other attacks.


### Common DNS Server Issues[#](https://www.keycdn.com/support/what-is-a-dns-server#common-dns-server-issues)

There are several common DNS server issues that can occur. Some of these include:

- DNS server downtime: This can occur if the DNS server crashes or goes offline.
- DNS cache poisoning: This is when a hacker alters the DNS cache to redirect users to malicious websites.
- [DNS spoofing](https://www.keycdn.com/support/dns-spoofing): Occurs when a hacker sends false DNS information to a user's computer to redirect them to a malicious website.
- DNS hijacking: This is when a hacker takes control of a user's DNS settings to redirect them to a malicious website.

### Common DNS Issues Solutions
 [DNSSEC](https://www.keycdn.com/support/dnssec) (DNS Security Extensions) is a set of protocols designed to add an additional layer of security to the DNS lookup process. DNSSEC works by adding digital signatures to DNS records, which allows DNS clients to verify that the records they receive are authentic.

Another common DNS security measure is DNS filtering, which is the process of blocking access to certain domains or IP addresses. DNS filtering is often used in corporate environments to prevent employees from accessing malicious websites or other inappropriate content.



