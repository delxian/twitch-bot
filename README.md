# Twitch Bot
Twitch chat bot with extensibility support.
## Features
- Connection to multiple channels (cross-channel communication possible)
- Configuration, user ranks and blacklist
- Chat history tracking and User ID recording (name change recognition)
- Console colors (chat messages, bot logging, IRC messages)
- Timers (scheduled recurring events)
- Commands
  - Aliases, prefixes, role restriction, cooldowns, toggling, and hiding
  - Canonical parameter structure/generation with argument parsing system
## Configuration
The bot is configured via environment variables. The following variables are required:
|Variable|Type|Description|Default Value|
|-|-|-|-|
|USERNAME|str|Twitch username of the bot account|''|
|ONLINE_CHANNELS|list[str]|channels to act in while live|[]|
|OFFLINE_CHANNELS|list[str]|channels to act in while not live|[]|
|USERNAMES_FOLDER|str|path to folder storing username and ID data|''|
|RICH_IRC|bool|whether to show more IRC data in the console|True|
|SHOW_ERRORS|bool|whether to log errors to chat|True|
|HISTORY_LIMIT|int|maximum messages in message history|1000|
|TIMESTAMP_FORMAT|str|todo|"12h"|
|URI|str|Twitch IRC Websocket URI|"ws://irc-ws.chat.twitch.tv:80"|
|CLIENT_ID|str|application ID from Developer Console|''|
|CLIENT_SECRET|str|application secret from Developer Console|''|
|OAUTH|str|OAuth token obtained via grant flow|''|
|CAPABILITY|list[str]|capabilities to request from Twitch|["commands", "membership", "tags"]
## Extending Functionality
The bot is written to be extensible mostly via class inheritance and decorators.

- To add bot features, subclass the `BaseBot` class and override relevant methods.
- To add channel features, subclass the `BaseChannel` class and override relevant methods.
- To add config entries, subclass the `BaseConfig` dataclass. If a value needs to be converted from a string, add such logic to the `from_env` method.
- To add a timer, decorate a function that takes a `Bot` argument with the `@Timer.timer` decorator.
- To add a command, decorate a function that takes a `Context` argument with the `@Command.timer` decorator.

`main.py` provides basic templates for such extensions, and `default.py` demonstrates how timers and functions should look in practice.
## Requirements
- Python 3.11 or higher
- [requests](https://pypi.org/project/requests/), [websockets](https://pypi.org/project/websockets/), [dotenv](https://pypi.org/project/python-dotenv/)
## License
- [MIT](LICENSE)