# Your API hacking system

## Burp suite

Burp suite is a tool to scan and fuzz a web API

- Lets you create variables with any parf of a captured request

### Type of attacks
#### Sniper
Attack from a single payload, tries one attack position per request
#### Battering ram
Fuzz all attack positions in a single payload per request
#### Pitch fork
Test multiple payload combinations at once. Doesn't try different combinations of payload
#### Cluster bomb
Cycle through all possible combinations of paylod

### Good for
- BOLA
- Excessive data exposure
- Broken authentication
- BFLA
- Mass assignment
- injection
- Improper assets management
