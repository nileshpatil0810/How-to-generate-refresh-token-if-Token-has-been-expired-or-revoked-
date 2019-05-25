# How-to-generate-refresh-token-if-Token-has-been-expired-or-revoked?
How to generate refresh token if Token has been expired or revoked?

#Authorization flow has only two steps.

#1 Is to obtain the authorization code using https://accounts.google.com/o/oauth2/auth? URL.

For that a post request is sent providing following parameters. 'scope=' + SCOPE + '&client_id=' + CLIENTID + '&redirect_uri=' + REDIRECT + '&response_type=' + TYPE + '&access_type=offline' Providing above will receive a authorization code.

Response : code=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX&scope=https://www.googleapis.com/auth/androidpublisher

#2 Retrieving AcessToken and RefreshToken using https://accounts.google.com/o/oauth2/token? URL. For that a post request is sent providing following parameters.

"code" : code, "client_id" : CLIENT_ID, "client_secret" : CLIENT_SECRET, "redirect_uri" : REDIRECT_URI, "grant_type" : "authorization_code",

Here, 

code = Will be get from #1
redirect_uri = Will same of step #1

Response : 

{
    "access_token": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
    "expires_in": 3600,
    "refresh_token": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
    "scope": "https://www.googleapis.com/auth/androidpublisher",
    "token_type": "Bearer"
}

While generate refresh token i found problem which i'm going to share IN first attempt once you authorize the permissions you will be able to get the Refresh token but Subsequent attempts will not provide the refresh token,So If you want the token again the revoke the access in you application and generate token.

# Note : 

- If in Google account any change made like password changed or any other then refresh token will change, so need to take care for this and will get below response while verify on server.

{
  "error": "invalid_grant",
  "error_description": "Token has been expired or revoked."
}
