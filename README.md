# Alexa Presentation Language (APL) Starter Template

This is an Alexa skill template that can be used as a starting point for building, or learning how to build skills that uses the Alexa Presentation Language (APL). 

This template uses the [Alexa Skills Kit for Node.js](https://github.com/alexa/alexa-skills-kit-sdk-for-nodejs) version 2.0 and is designed to be used with the [Alexa Skills Kit CLI](https://developer.amazon.com/docs/smapi/ask-cli-intro.html).

## Tutorial Video

[![Using the Alexa Presentation Language (APL)](https://i.ytimg.com/vi/pY3XUkvbEIs/sddefault.jpg)](https://youtu.be/pY3XUkvbEIs)

## Introduction

The Alexa Presentation Language or APL is a language that lets you enhance your Alexa skills with full-featured, responsive, and interactive screen displays. Using the APL is works similar creating Web pages and provides similar support for HTML, CSS, and JavaScript.

## Steps to enable APL support in your skill

1. Add the APL interface directive

    Add the following code in the `mainfest` > `apis` > `custom` section of the `skill.json`.

    ```json
      "interfaces": [
        {
          "type": "ALEXA_PRESENTATION_APL"
        }
      ]
    ```

2. Add an APL template named `main.json`

    ```json
    {
        "type": "APL",
        "version": "1.0",
        "import": [
            {
                "name": "alexa-layouts",
                "version": "1.0.0"
            }
        ],
        "mainTemplate": {
            "parameters": [
                "payload"
            ],
            "items": [
                {
                    "type": "Text",
                    "text": "Hello World"
                }
            ]
        }
    }
    ```

3. Require the template in your `index.js` file

    ```javascript
    const main = require('./main.json');
    ```

4. Add the `Alexa.Presentation.APL.RenderDocument` directive to the responseBuilder

    ```javascript
    const LaunchRequestHandler = {
      canHandle(handlerInput) {
        return handlerInput.requestEnvelope.request.type === 'LaunchRequest';
      },
      handle(handlerInput) {
        const speechText = 'Hello there. What is your name?';
        const repromptText = 'Can you tell me your name?';

        return handlerInput.responseBuilder
          .speak(speechText)
          .reprompt(repromptText)
          .withSimpleCard('Example Card Title', "Example card body content.")
          .addDirective({
            type: 'Alexa.Presentation.APL.RenderDocument',
            version: '1.0',
            document: main,
            datasources: {}
          })
          .getResponse();
      },
    };
    ```