
## Access Token update
1. The client is authenticated by sending a login/password pair.
2. If successful, the server creates a new Access Token and Refresh Token. Refresh Token is recorded in the database along with the time of his life.
3. The server sends the response to the client in the form:
```json
{
    "expired_at": ...,
    "access_token": ...,
    "refresh_token": ...
}
```
4. The client saves this data.
5. With each request, the client checks to see if Access Token is expired or not. In case of Access Token has not expired, it simply sends the request using it.
6. For updates, the client sends a Refresh Token to a specially defined endpoint. (for example /v1/account/refresh-token)
7. The server checks the Refresh Token, which is in the database with the sent. Also, check expired or not.
8. In case of Refresh Token is expired, or it is not found in the database, then we return a 401 error to the client, in order to pass authentication.
9. If Refresh Token is found and it is still relevant, then create a new Access Token and update Refresh Token. We send this data as in paragraph 3.
10. Now the client can continue to perform requests with the new Access Token.
