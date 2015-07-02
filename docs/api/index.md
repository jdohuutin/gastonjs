GastonJS HTTP API
==================
Lets start by saying that the API is **not REST**, is a simple HTTP interface where you can send POST requests with the command you want the browser to execute and the parameters to execute such commands.

This statement can change in the future but that will require all clients to upgrade to the REST implementation.

##Start the Browser and the API
```bash
phantomjs --ssl-protocol=any --ignore-ssl-errors=true vendor/jcalderonzumba/gastonjs/src/Client/main.js 8510 1024 768 2>&1 >> /tmp/gastonjs.log &
```
This will start a phantomjs process and the API listening on the 8510 port, the 1024x768 parameters are the width and height you want the browser to use. You can start the API on the port you want 8510 is just an example.

##API endpoint
Your client can start making HTTP POST requests to `http://localhost:8510/v1/api`

##API command request
Every POST request to the API needs a command name and the arguments that the commands needs to run.

This command is a JSON body that has the following schema:
```json
{
  "name": "COMMAND_NAME",
  "args" : [
    "COMMAND_ARG_1",
    "COMMAND_ARG_2",
    ...
  ]
}
```

##API request example
The following example will teach you how to visit a page and save the rendered page:

1. Visit the page:
```bash
curl -X POST -H "Content-Type: application/json" -d '{"name":"visit","args":["https://www.google.es"]}' 'http://127.0.0.1:8510/v1/api'
```

2. Save the rendered page to a PNG file:
```bash
curl -X POST -H "Content-Type: application/json" -d '{"name":"render","args":["/tmp/google.png", true]}' 'http://127.0.0.1:8510/v1/api'
```