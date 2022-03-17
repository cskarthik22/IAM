
# Azure Active Directory Pass-through Authentication: Technical deep dive

![image](https://user-images.githubusercontent.com/38231831/158726939-2f53ab63-5196-4fa5-a72f-6bbe85c34d33.png)

When a user tries to sign in to an application secured by Azure AD, and if Pass-through Authentication is enabled on the tenant, 
the following steps occur:

- The user tries to access an application, for example, Outlook Web App.
- If the user is not already signed in, the user is redirected to the Azure AD User Sign-in page.
- The user enters their username into the Azure AD sign in page, and then selects the Next button.
- The user enters their password into the Azure AD sign in page, and then selects the Sign in button.
- Azure AD, on receiving the request to sign in, places the username and password (encrypted by using the public key of the Authentication Agents) in a queue.
- An on-premises Authentication Agent retrieves the username and encrypted password from the queue. Note that the Agent doesn't frequently poll for requests from the queue, but retrieves requests over a pre-established persistent connection.
- The agent decrypts the password by using its private key.
- The agent validates the username and password against Active Directory by using standard Windows APIs, which is a similar mechanism to what Active Directory Federation Services (AD FS) uses. The username can be either the on-premises default username, usually userPrincipalName, or another attribute configured in Azure AD Connect (known as Alternate ID).
- The on-premises Active Directory domain controller (DC) evaluates the request and returns the appropriate response (success, failure, password expired, or user locked out) to the agent.
- The Authentication Agent, in turn, returns this response back to Azure AD.
- Azure AD evaluates the response and responds to the user as appropriate. For example, Azure AD either signs the user in immediately or requests for Azure AD Multi-Factor Authentication.

If the user sign-in is successful, the user can access the application.
