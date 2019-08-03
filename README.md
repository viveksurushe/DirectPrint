# DirectPrint
To print a file through api without print perview


## Google Cloud Print

### Add Printer: Goto google chrome browser setting
```
setting --> Advenced --> Printing --> Google Cloud Print --> Manage Cloud Print Devices --> 
add Printer here to google acccount API
```

## Google Cloud Print API

### 1) Get code query parameter to get access & refesh token 


URL -

https://accounts.google.com/o/oauth2/v2/auth?client_id=&response_type=code&scope=&redirect_uri=&access_type=offline 

Put url in browser with your account credentials give access to you google cloud print then you will get code in redirect url

### 2) Get access and refresh token to get access to google api

Note: - The code parameter we get in browser use here.

Remember - store the refresh token to database so as to get new access token to use google api.
If you forget to store it then use same api as 1st with one extra parameter after access_type=offline
&prompt=consent so that you will get refresh token again.

URL - https://www.googleapis.com/oauth2/v4/token 

Headers – 
```
  { 
      Content-Type: application/x-www-form-urlencoded
  }
```

Body - 
```
  {
      client_id,
      client_secret,
      grant_type: authorization_code,
      redirect_uri,
      code
  }
```

Response -
```
  {
      "access_token":"ya29.GltWB56yRRwXWo4PKvcw_bU8HZBprTfYxBEZdGXJ4cUzyVe2r,
      "expires_in": 3600,
      "refresh_token": "1/l3CKTX405t1GRtIiP5e369aFFltNyUfE1FR-cfonweas",
      "scope": "https://www.googleapis.com/auth/cloudprint",
      "token_type": "Bearer"
  }
```

### 3) Get access token with the help of refresh token

URL - https://www.googleapis.com/oauth2/v4/token 

Body - 
```
  {
      grant_type: refresh_token
      client_id: ,
      client_secret: ,
      refresh_token: 
  }
```
Response -
 ```
  {
      "access_token": "ya29.GlxWBygYgO-xSr--1zbBw1KJ0mfrpNLtvK1EElagPQwwjI97Mlr-8nDubM6KljRWhBNBg32T7Obmj25GKXRraHDMTKI",
      "expires_in": 3600,
      "scope": "https://www.googleapis.com/auth/cloudprint",
      "token_type": "Bearer"
  }
```


### 4) Submit print

URL - https://www.google.com/cloudprint/submit 

Headers – 
```
  { 
        Authorization: Bearer (your access token)
  }
```
Body - 
```
  {
        printerid,   // ther printer you want use
        title:         // title of pdf file in gcp job list
        ticket: ,      // object contain printer configration
        content,       // the content you want to print
        contentType    // type of content pdf/string like
  }
```

Response -
```
  {
        "access_token":"ya29.GltWB56yRRwXWo4PKvcw_bU8HZBprTfYxBEZdGXJ4cUzyVe2rGPtb,
        "expires_in": 3600,
        "refresh_token": "1/l3CKTX405t1GRtIiP5e369aFFltNyUfE1FR-cfonwerv",
        "scope": "https://www.googleapis.com/auth/cloudprint",
        "token_type": "Bearer"
  }
```

## Links that may helps -
1. https://developers.google.com/cloud-print/docs/appInterfaces
2. https://medium.com/@pablo127/google-api-authentication-with-oauth-2-on-the-example-of-gmail-a103c897fd98
3. https://developers.google.com/identity/protocols/OAuth2WebServer
4. https://developers.google.com/identity/protocols/OAuth2
