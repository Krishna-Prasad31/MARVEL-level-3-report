# MARVEL-level-3-report

# Task1: AWS Lambda:
AWS Lambda is one of many services provided by Amazon Web Services. Using Lambda developers can execute code without needing to provision or manage servers. It follows and event driven architechure, where fucntions(Lambda function) are triggered in response to specific events such as HTTP request, file upload , database updates, etc...AWS Lambda is a Function-as-a-Service (FaaS) platform.

For this task i created a chat application using AWS Lambda and API gateway services. The following Lambda functions were developed to handle different stages of communication in the chat application:

1. websocket-connect
- Triggered when a client connects to the WebSocket API
- Establishes a connection between client and server
- Stores connection details if required
3. websocket-disconnect
- Triggered when a client disconnects
- Removes or cleans up connection data
- Ensures efficient resource management
4. chat-handler
- Core logic of the chat application
- Processes incoming messages from users
- Generates appropriate responses
- Implemented using Node.js runtime
5. websocket-send
- Responsible for sending messages back to clients
- Handles outgoing communication
- Ensures real-time message delivery

## How this works
- the user sends a request to the API gateway whilst interacting with the frontend
- API gateway receives the request and forwards it to the lambda function which is intended to be used
- Lambda function sends response to the user through API gateway.

![website](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(665).png?raw=true)
![website](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(740).png?raw=true)
![website](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(741).png?raw=true)
![website](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(739).png?raw=true)
  
