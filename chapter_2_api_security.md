# How Web API security work

## OWASP top 10 vulnerabilities

### Information disclosure
Sharing sensitive data to unprivileged user in API responses, code respo, search results, social medias, etc. Might come from code whose messages
are too verbose and provide information about the inner workings.

### Broken Object-level Authorization (BOLA)
Happens when API gives access to a user for resources it is not authorized to access.
Complexe object IDs makes BOLA hard to find by trying to figure out sequential IDs

django-rest-framework permission classes do not enforce object-level permissions. It also makes listAPIView slower since it checks every object so
`get_queryset` override is a good solution.

### Broken User Authentication
Any weaknesses related to user authentication. Since APIs are stateless, clients have to send authentication proof in each interactions.

### Excessive Data Exposure
When the API response contains too much information and/or sensitive data. A good example would be to have an endpoint that returns objects to
display as options in a dropdown. If the endpoint returns more than the display information and the object ID, it might leak sensitive information.

### Lack of resource or rate limiting
If rate limits are not in place, an attacker can incure hight costs or DoS the service.

To verify if an API is vulnerable to this, first test with lots of requests. If an `http 429` is returned, check how rate limiting is enforced and it's
possible to reset it by changing a variable i.e.: add/remove a parameter, use a different client, change your IP address, etc.

### Mass Assignment
If you can specifiy an extra parameter and this value is not checked and it update a variable to give it unwantes effects.

Check documentation for user related parameters or capture the packets to inspect or fuzz them in the API requests.

### Security Misconfiguration
Anythin misconfigured by developers that opens a security hole such as:
- give too much information
- allow automatic parsing without sanitization
- XSS injection
- Default credentials
- Unnecessary HTTP methods

Useful scanning tools for these holes:
- Nessus
- Qualy
- OWAPzap
- Nikto

### Injections
Unsanitized inputs sent directly to database for execution

```
{
  "param1": "' OR 1=0--"
}
```

If an error is returned, it is a clear indication about an injection weakness

### Improper Assets Management
When an old vulnerable or an under developped vulnerable API is exposed. Inspect requests and responses, inspect packets, fuzz urls.

### Busine Logic Vulnerabilities
Business Logic Flaws or `BLF` 

Using features outside their intended use. Red flag is the business relies on trust as a security mechanism. This vulnerability is hard to scan because
you need to understand the business logic which is unique to all businesses.
