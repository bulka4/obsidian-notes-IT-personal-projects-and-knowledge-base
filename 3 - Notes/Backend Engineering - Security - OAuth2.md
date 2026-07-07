Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
OAuth 2.0 is an authorization ([[Backend Engineering - Security - Authorization vs authentication|link]]) framework, not an authentication protocol. 

It allows one application to access a user's resources in another application without knowing the user's password in that another application.

For example:
- User uses application X and wants to import files from Google Drive.
- The app redirects user to Google
- User logs in on Google's website
- User approves the requested permissions
- Google gives the app an access token
- The app uses that token to access user's data in Google

Obtained access token is sent by the user together with every request for authentication. This token can be for example JWT ([[Backend Engineering - Security - JWT access token format|link]]).
# Questions
- 