# URL shortening system

## Requirement and goals of the system

[Reference](https://www.educative.io/collection/page/5668639101419520/5649050225344512/5668600916475904?affiliate_id=5082902844932096&gclid=CjwKCAjwpeXeBRA6EiwAyoJPKhOf_cbEXY5ogUOgfAI9nV5RvArGPSAuWIYaqpN-OHgfab-LWrjiqhoCNPkQAvD_BwE#utm_source=google&utm_medium=cpc&utm_campaign=grokking-manual)

**Functional Requirements:**

- Given a URL, our service should generate a shorter and unique alias of it. This is called a short link. (Write)
- When users access a short link, our service should redirect them to the original link. (Read)
- Users should optionally be able to pick a custom short link for their URL. (Hash options)
- Links will expire after a standard default timespan. Users should also be able to specify the expiration time. (Expiration)

**Non-Functional Requirements:**

- **Availability**
    - The system should be highly available. This is required because, if our service is down, all the URL redirections will start failing.
- **Low Latency**
    - URL redirection should happen in real-time with minimal latency.
- **Non-predictable Hash Algorithm**
    - Shortened links should not be guessable (not predictable).

## Capacity Estimation and Constraints

- **Read and Write ratio**
    - assume 99:1
- **Traffic estimates**
    - assume 500M new urls
        - 500 million / (30 days * 8 hours * 3600 seconds) = 600 URL/second
    - assume 100 redirections per URL
        - 59400 read query / second, 600 write query / second
- **Storage estimates**
    - assume we store urls for 5 years
        - 500 million * 5 years * 12 months = 30 billions URLs
    - assume 500 bytes per url for storage
        - 30 billion * 500 bytes = 15 TB
- **Network Bandwidth estimates**
    - assume 500 bytes per query
        - 60000 query / second * 500 bytes = 30 MB/s
- **Memory estimates** - use as memory cache
    - assume 80/20 rule - 20% URLs use 80% traffic
    - cache 20% of possible urls of one duration
        - if cache 20% of all URLs
            - 15 TB * 0.2 = 5TB (of all URLs)
        - if cache 20% of one day URLs
            - 500 million URLs / 30 days * 100 query per URL * 500 bytes per query * 0.2 = 167 GB
- **Computation estimates**
    - depends on what algorithm the system uses.
    
## Basic System Design and Algorithms

a. Encoding actual URL

1. Hashing
- Hashing Methods
    - MD5 (generate 128-bit hash)
    - SHA256
- Hash Code encoding
    - base 32 [a-z,0-9]
    - base 64 [A-Z,a-z,0-9,-,.]
    - How many bits should we use when encoding?
        - Using base64 encoding, a k-bit key can represent 64^k possible strings.
        - take first k bits of hash code as key
- Collision of hash code
    - we need to map each key to only one url
    - so we change part of the key and make sure that it is unused before. For example, we add 1 to the key.
    - Way to avoid collision
        - use 100 times value space
    - Way to check collision
        - use bloomfilter to check collision
- Issues with multiple users?
    - Multiple users have one same URL, but we want to get different urls for each user
    
2. Use a key generator
        
We generate random keys in advance and stores them in a database.





