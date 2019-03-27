# hello-world-bot
A helloworld webhook nodejs sample for a SAP Conversation AI bot.

## Introduciton
A helloworld webhook sample for a SAP Conversational AI bot with a webhook trigger as action. This simple sample how you reply with text message and a list template message. The nlp result by 
SAP Conversational AI is sent in the request body, in which you can know about the intent and entities etc as a result of your bot training. Usually, the intent indicates a service to be fulfiled by the bot.

For example, the end user is buying something through a conversation with your bot by saying "I want some pizza", once its intent and given contextual information has been understood by the bot, the bot will fulfils the service by invoking a RESTful call to SAP Business One or SAP Business ByDesign to place an order 
etc, and respond to the end user with the order number 
just placed.

To use this sample, please follow the steps below:

## Prequisities
* You have followed this [tutorial](https://recast.ai/blog/build-your-first-bot-with-recast-ai/) to build your first bot with SAP Conversational AI.

## Download the project
```
git clone https://github.com/YatseaLi/hello-world-bot.git
```

## Deploy the webhook project
### Option 1: Local Deployment
Prequisites: You have NodeJS 6.12 or above run-time installed in your local machine.

1. Install the dependent node modules
   ```sh
   npm install
   ```
2. Start the app
    ```
    node hello_world_webhook.js
    ```
3. Publish the webhook url to public internet.
    <br/>If you don’t have a public server, or if you want to test your bot during development, ngrok is a very handy tool: It creates a public URL for you and forwards requests to your computer. Once you installed it, run 
    ```
    ngrok http 5000
    ``` 
    And copy the Forwarding URL in HTTPS (https://XXX.ngrok.io) to your bot Settings (“Bot webhook base URL” field). All requests made to these URL will be forwarded to the port 5000 of your computer.

    As a result, you have obtain the webhook url for your bot.

### Option 2: Deployment on Cloud Foundry, SAP Cloud Platform
Prequisitive: You have followed this [tutorial](https://developers.sap.com/australia/tutorials/hcp-cf-getting-started.html)  to get started with Cloud Foundry

1. To avoid the naming conflict, edit the application name in [manifest.yml](https://github.com/YatseaLi/hello-world-bot/blob/master/hello_world_webhook.js). For example, "xxx-helloworld-bot"(xxx stands for your company namespace)
2. Open terminal and change directory to hello-world-bot
    ```
    cd hello-world-bot
    ```
3. Run the command to login to Cloud Foundry, SAP Cloud Platform,and deploy the app.
    ```
    cf login
    ...
    cf push
    ```

    Once the app is started, as a result, you now obtain the web hook url for your bot. for exmaple: https://xxx-helloworld-bot.<>/

## Apply the webhook url to the skill of your bot
Open your bot on SAP Conversation AI
* Go to tab Build and create a skill for the target intent 
* Setup the trigger as when the target intent is present. 
* For action, use Call Webhook to reply, and fill in the webhook url as step of deployment.

Now test you bot, it will reply two messages 
One as a text message "roger that"
The other as a list of customer with sales amount and gross profit.

## Todo
Complete the service fulfilment in webhook endpoint for your own bot.
```javascript
app.post('/', (req, res) => {
      console.log(req.body)

      //Todo: Please implement your service fulfilment for the intent here
      //And send back the reply message in text or list template.
```

## License
The source code is under MIT license. Please kindly check the LICENSE. Here is to highlight that THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED. Therefore no support available.
