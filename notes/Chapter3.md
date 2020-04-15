# Chapter3
NodeJS, Express 를 사용하여 REST endpoint 를 구축해보는 것으로 시작.

## --dev flag
Note how we used the --dev flag. It is a good practice to separate between production dependencies and development dependencies. That way when you deploy your server to the real environment, you won't install the unnecessary development dependencies there. 

## Express
Express is a wrapper around the native Node.JS "http" library which is responsible for handling HTTP requests. Yes, it can also be used directly, but Express is much more comfortable and has an amazing ecosystem built around it

## res.json() method
Unlike the previous route, we used the .json()method this time around to send a response. This will simply stringify the given JSON and set the right headers. Similarly to the client, we've defined the db mock in a dedicated file, as this is easier to maintain and look at.

## middleware cors
It's also recommended to connect a middleware called corswhich will enable cross-origin requests. Without it we will only be able to make requests in localhost, something which is likely to limit us in the future because we would probably host our server somewhere separate than the client application. Without it it will also be impossible to call the server from our client app. 
    
    $ yarn add cors
    $ yarn add --dev @types/cors

이런식으로 패키지 설치할 때마다 --dev 로 typescript 타입도 설치해준다. 개발 편의성을 위해 ㅇㅇ

## .env
The .envfile is a file which will automatically be loaded to process.envby the dotenvNPM package. react-scriptsthen filters environment variables which have a REACT_APP_prefix and provides the created JSON to a Webpack plugin called DefinePlugin, which will result in the macro effect.

## React Hooks
With React hooks we can invoke the desired logic in the right life-cycle stage of the target component. This way we can avoid potential memory leaks or extra calculations. 

### React.useState()
which is used to get and set a state of the component - will be used to store the chats fetched from the server.

### React.useMemo()
which is used to run a computation only once certain conditions were met - will be used to run the fetch()function only once the component has mounted.
