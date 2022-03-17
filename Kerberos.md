

![image](https://user-images.githubusercontent.com/38231831/158721798-361eeac2-d48c-4c9c-bd78-95b88d09a4ca.png)

# Kerberos
'''
Kerberos itself is a network protocol that enables authentication for users of client/server applications through the use of symmetric-key cryptography.
Kerberos is usually used for authenticating desktop users on networks, but through the use of some additional tools, it can be used to authenticate users to web applications and to provide SSO for a set of web applications. This essentially allows users who have already authenticated on their desktop network to seamlessly access secured resources in web applications without having to re-authenticate. This concept is known as Desktop-Based SSO since the user is being authenticated via a desktop-based authentication mechanism, and their authentication token (or ticket) is being used by the web application as well. This differes from other SSO mechanisms such as Browser-Based SSO, which authenticates users and issues tokens all via the browser.

The Kerberos protocol defines several components that it uses in authentication and authorization:

- Tickets : A Ticket is a form of a security token that Kerberos uses for issuing and making authentication and authorization decisions about principals.
- The Authentication Service (AS) challenges principals to log in when they first log into the network. The authentication service is responsible for issuing a Ticket Granting Ticket (TGT), which is needed for authenticating against the Ticket Granting Service and subsequent access to secured services and resources.
- The Ticket Granting Service (TGS) is responsible for issuing Service Tickets and specific session information to principals and the target server they are attempting to access. This is based on the TGT and destination information provided by the principal. This service ticket and session information is then used to establish a connection to the destination and access the desired secured service or resource.
- The Key Distribution Center (KDC) is the component that houses both the TGS and AS. The KDC, along with the client (principal) and server (secured service), are the three pieces required to perform Kerberos authentication.
- A Ticket Granting Ticket (TGT) is a type of ticket issued to a principal by the AS. The TGT is granted once a principal successfully authenticates against the AS using their username and password. The TGT is cached locally by the client (principal), but is encrypted such that only the KDC can read it (i.e. it is unreadable by the client). This allows the AS to securely store authorization data and other information in the TGT for use by the TGS and enabling the TGS to make authorization decisions using this data.
- A Service Ticket (ST) is a type of ticket issued to a principal by the TGS based on their TGT and the intended destination. The principal provides the TGS with their TGT and the intended destination, and the TGS verifies the principal has access to the destination based on the authorization data in the TGT. If successful, the TGS issues an ST to the client (principal) for both the client as well as the destination server (server containing secured service/resource), which grants the client access to the destination server. The ST, which is cached by the client and readable by both the client and server, also contains session information that allows the client and server to communicate securely.
'''

## Identity Provider
```
An identity provider (IDP) is the authoritative entity responsible for authenticating an end user.
```

## Identity Store
```
An identity provider needs an identity store to retrieve users' information to use during the authentication and authorization process. Identity stores can be any type of repository: 
- Database 
- Lightweight Directory Access Protocol (LDAP), 
- properties file, and so on.
```
