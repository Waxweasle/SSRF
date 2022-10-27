# SSRF
Notes on simple SSRF
---

##  Server-Side Request Forgery - vulnerability that allows an attacker to cause webserver to make an additional/edited HTTP request to the resource of the attacker's choosing. 

# Defense 

## Deny List

#### All requests are accepted apart from resources specified in a list or matching a particular pattern. A specific endpoint to restrict access is the localhost(may contain server performance data or further sensitive information) so domain names such as localhost/127.0.0.1 would be on deny list. Can bypass by using alternative localhost references (0, 0.0.0.0, 0000, 127.1, 127.*.*.*, 2130706433, 017700000001) or subdomains that have a DNS record which resolves to the IP Address 127.0.0.1 such as 127.0.0.1.nip.io.
#### Also beneficial to block access to the IP address 169.254.169.254 (in a cloud environment), which contains metadata for the deployed cloud server/ sensitive information. An attacker can bypass this by registering a subdomain on their own domain with a DNS record that points to the IP Address 169.254.169.254.


## Allow List

#### All requests get denied unless they appear on a list or match a particular pattern/ rule that an URL used in a parameter must begin with. Attacker could bypass by creating a subdomain on an attacker's domain name. 


## Open Redirect

#### Endpoint on the server where the website visitor gets automatically redirected to another website address. eg https://website.com/link?url=https://othersite.com. If there was a potential SSRF vulnerability with stringent rules which only allowed URLs beginning with https://website.com/, attacker could  redirect internal HTTP request to a domain of the attacker's choice.
