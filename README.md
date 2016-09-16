
# slackbotify
[![XO code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/sindresorhus/xo)
[![npm](https://img.shields.io/npm/v/slackbotify.svg?maxAge=3600)](https://www.npmjs.com/package/slackbotify)

> Simple slackbot framework

## Installation
```
npm install slackbotify
```

## Usage
Creating a slackbot is as easy require the dependency, load the config and register a handler. Run it. Done. Slackbot is ready!

```
const Bot = require('slackbotify');

let bot = new Bot({
	"bot": {
		"token": "xoxb-XXXXX-XXXXX",
		"name": "butler"
	}
});

bot.registerHandler({
	groups: ['direct'],
	match: /hi/ig,
	handler: function (message, callback) {
		callback('Hi there! :smiley:');
	}
});

bot.registerHandler({
	groups: ['channel', 'direct'],
	match: /:smile:/ig,
	handler: function (message, callback) {
		callback(':slightly_smiling_face:');
	}
});

bot.run();
```

## Configuration
The only thing you have to pass to the constructor is a config object, and this config object should have at least a `bot` object with 2 properties: `token` & `name`. _(example above)_

## Handlers
To register a handler to the bot simple pass an object to the `registerHandler` function. This object needs to contain the following properties: `group`, `match`, `handler`.

### Group
The group defines where the command is available. There are 3 groups. `channel`, `direct`, `admin`. Handlers which are registered to the 'channel' group will fire when a message is send in a channel where the bot is invited to. 'Direct' handlers are private messages to the bot, and the 'admin' group handlers can only be called by an admin user in a private message.

A handler can be registered to multiple groups. In the example above the first handler is listening to direct messages only. The second handler will be called when a :smile: is send in a private message or in a channel where the bot is in.

### Match
The 'match' property is what the message should match in order to get called. This can be a regex or a string.

### Handler
The handler is a function which receives as the first argument the slack message object. The result of the matched message is located at `message.matchResult` this is the parsed result by the `.match()` function. The second argument is the callback. The response you give to that callback is send to the user, so basically what the bot will answer.

## Bots
The current bots are using slackbotify
- [Mr. Potato](https://github.com/RolfKoenders/potato) _Couchpotato slackbot_
- [Butler](https://github.com/RolfKoenders/butler) _Personal butler_

## License
[MIT](https://opensource.org/licenses/MIT)
