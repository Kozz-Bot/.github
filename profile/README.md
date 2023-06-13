# Kozz Bot

Kozz Bot is a platform-neutral chatbot creating tool focused on a distributed system with high independence of the modules and easy multiplatform integration.

_Warning:_ This tool is still in it's pre-alpha release. There will be many bugs and I'm expecting to reach a beta stage until December/2023.

## Architecture

The chatbots are supposed to work in a distributed environment. Multiple instances of different API's working together. They all talk to each other via websocket, using socket.io. There is no such thing as a single repo (yet) for all your bot needs because it requires different pieces being connected depending on what you want to build.

You may think this is a very convoluted way to create a simple chatbot, and I agree. This is a tool focused on a professional use and requires a little bit more infrastructure than simply running a node instance.

I'm still planning on creating docker images and buildscripts of preset environments for more simple usages.

## Gateway

The gateway is the main orchestrator of all the other entities. It's the Gateway's responsability to receive connections of all the others API's of the chatbot, receive the events and forward to the appropriate handlers.

[Here](https://github.com/Kozz-Bot/Kozz-Gateway) you can find the repository for the gateway with instructions on how to

## Boundary

A boundary is the entity that carries the chat instance. It's the Boundary's responsability to listen to chat events, like receiving messages, changing online status, group invites, and forwarding to the Gateway. The boundary also needs to be listen to the Gateway sending events, like reply message, react to message, send media, and so on.

In short, the Boundary is the entity that has direct connection to the platform the chatbot is talking to.

[Here](https://github.com/Kozz-Bot/kozz-wa) is a boundary for whatsapp using [Whatsapp.Web.js](https://github.com/pedroslopez/whatsapp-web.js) as it's automator.

## Modules

Modules are entities that receive events from the gateway and may or may not send events to the gateway. They are the main brains of the chatbot as its their job to deceide what happens when a user sends a message, how they respond, when they respond and so on.

[Here](https://github.com/Kozz-Bot/kozz-module-maker) is a library to help you to create new handlers for kozz-bot

### Proxy Module

The Proxy is an entity that can listen to every single message that is proxied to it. When a message is forward to a Proxy, the Proxy can reply the message, just log it to a database or simply do nothing. Proxies can listen to messages from a given chat of a given Boundary or all the messages from a given boundary

### Basic Module

The Basic Module has simple controls. It can't listen to messages, but it can send. Useful when you want to create marketing campaings or trigger the sending of a message from another source other than another message from the chat.

### Command Handler

The Command Handler deals with commands. Kozz-bot has a cool CLI-ish command parser that enable users to create commands directly in the chat. It's useful to create debug statements or evoke functions of another entity directly.

## Asking resources

The entities can talk to each other not only through events but also asking resources directly. You can set resources when instanciating the entities.
