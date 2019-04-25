# An authentication project using JWT Tokens, Vue.js(frontend) and Django-Rest(backend).

## Flow: 
 - Users enter their credentials at the client side(Vue.js). The info is forwarded to the backend API. If the info is valid generate an access and refresh token, send it back to the client.
 - The tokens are stored on Vue.js store(Vuex). 
 - '/mods/' is a path on the backend which is an example protected view. It can handle only GET requests. The client has to send the access token with the GET request to proof the user is authenticated to view this path.
 - '/downloads/' route on the client side display's the data which is fetched from '/mods/' path on the backend. This is accomplished using axios. If the server returns a 401(meaning the access token has expired), axios response interceptor is used to refresh the access token, re-send a GET request to '/mods/' and save the received data to APIData**.
 - Logout is initialized by informing the backend to blacklist the access token(prevents possible misuse if the token is stolen), the access and refresh tokens are destroyed at the client side.
 
**Note: The Vuex store state defines 'APIData' to save the received data from the backendAPI.

## Features: 

 - Autologout if no activity(using vue-idle)
 - Automatically refresh access token on expiration(using axios interceptors)
 - CORS in backend
