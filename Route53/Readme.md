# Route 53 
  * name derived from: first interstate road, that went from one corner to another
  * dns is on port 53
  
## DNS 
  * is used to convert domain names into IP address
  * like a phone book

## IP 4:
  * 32 bit field, and has 4 billion different addresses

## IP 6:
  * 340 undecillion address

## Top Level Domains:
  * .com.au : top level is au, .com is second level
  * .com,.gov etc are top level domains
  
## ICANN:
  * enforces uniqueness of each domain

## Who is database:
  * Central database for domains
 
## domain registrars:
  * amazon, godaddy, 123-reg.co.uk
  
## NS: Name Server Records
  Used by top level domain server to direct traffic to content DNS which contains the authoratative DNS records
  
## TTL:
 * Time To Live
   * Lower the TTL, the faster changes to DNS records take to propogate through the internet
   * Default TTL is 48 hours

## A Record
 * fundamental type of DNS.
 * A stands for Address
 * used by computer to translate name of domain to IP address

## CNAME:
* Canonical Name used to resolve domain name to another.
* e.g. `m.jawadxiv.com` , you also want users to route from `mobile.jawadxiv.com`

## Alias Records:
* are used to map resource records in your hosted zone to ELB, Cloud Front Distribution or S3 Bucket that are configures as ***websites***

* CNAME cant be used for naked domain (zone apex record). cant have cname for http://jawadxiv.com it must be either an A record or alias


# Understanding DNS:
 
1. A user opens a web browser, enters www.example.com in the address bar, and presses Enter.
2. The request for www.example.com is routed to a DNS resolver, which is typically managed by the user's Internet service provider (ISP), such as a cable Internet provider, a DSL broadband provider, or a corporate network.
3. The DNS resolver for the ISP forwards the request for www.example.com to a DNS root name server.
4. The DNS resolver for the ISP forwards the request for www.example.com again, this time to one of the TLD name servers for .com domains. The name server for .com domains responds to the request with the names of the four Amazon Route 53 name servers that are associated with the example.com domain.
5. The DNS resolver for the ISP chooses an Amazon Route 53 name server and forwards the request for www.example.com to that name server.
6. The Amazon Route 53 name server looks in the example.com hosted zone for the www.example.com record, gets the associated value, such as the IP address for a web server, 192.0.2.44, and returns the IP address to the DNS resolver.
7. The DNS resolver for the ISP finally has the IP address that the user needs. The resolver returns that value to the web browser. The DNS resolver also caches (stores) the IP address for example.com for an amount of time that you specify so that it can respond more quickly the next time someone browses to example.com. For more information, see time to live (TTL).
8. The web browser sends a request for www.example.com to the IP address that it got from the DNS resolver. This is where your content is, for example, a web server running on an Amazon EC2 instance or an Amazon S3 bucket that's configured as a website endpoint.
9. The web server or other resource at 192.0.2.44 returns the web page for www.example.com to the web browser, and the web browser displays the page.

![dns](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/0%20-DNS.PNG)

![dns](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/1-%20DNS.PNG)

![dns](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/1%20-%20b%20DNS.PNG)

![dns](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/2%20-%20DNS.PNG)

![dns](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/3%20-%20DNS.png)



  
  