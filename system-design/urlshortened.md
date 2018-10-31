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







