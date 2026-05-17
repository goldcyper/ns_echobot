![Echo Bot image](https://raw.githubusercontent.com/goldcyper/ns_echobot/refs/heads/main/bot.png)
# NationStates Echo Bot

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)

**What is Echo Bot?:** Nationstates Echo Bot is a Discord bot designed for the management of NationStates regions, which includes tracking of nations, wa proposals and resoluttions, nation and delegate monitoring, region history of nations, and a lot more...

[Screenshot or GIF demo here]

## Why This Project?

- ✅ **Region management tools:** Designed to give regions the tools to easily manage their regions through discord
- ✅ **WA proposals and resolutions tracking:** Tracks World Assembly proposals and resolutions, and posts them to discord and/or region forum
- ✅ **Regional security tools:** GDPR compliant regional security tools that keep user privacy intact
- ✅ **Nation and Region history:** Region history of nations going back to 2012, which is important since the end of NS Dossier
- ✅ **NationStates Maps Management:** Allows for maps you have created for RPs or Nationtates to be uploaded, edited, and live viewed
- ✅ **Forum integration:** Intergrates with XenForo, Discourse, vBulletin, and IPB forum APIs for citizenship checks and wa posts
- ✅ **Discord Linking:** Adds linking of discord accounts to nations, and to forum accounts in case of residents
- ✅ **IP Proxy checking:** Supports checking for IP Proxies and such, which is a limitation for non-forum owners

## Quick Start Guide
This is a quick start guide to running the bot, which is recommended to run in python or a virtual environment if on a local system

Collect your Discord Developer credentials for the bot, such as the bot token and invite your bot to the server:
[Discord Developer Guide](https://designbeep.com/2026/05/14/discord-developer-portal/)

```bash
# Install python dependencies for project
pip install -r requirements.txt

# [Optional] Edit config.json file in config folder with bot token (if no console access)
{
    "bot_token": "your_bot_token_here",
    "bot_name": "Echo Bot",
    "command_prefix": "?",
    "log_file": "bot.log",
    "log_messages": true,
    "log_commands": true,
    "database_file": "echo.db",
    "echo_api_database": "echo_api.db"
    ,
    "auto_restart_on_disconnect": true,
    "auto_restart_delay_seconds": 5
}

# Run the bot using bot.py
python bot.py
```
Most discord bot hosts ask for a start file, which is the simply named bot.py:
```text
bot.py
```
When bot.py runs it will ask for a bot token, if hasn't already been added to the config.json file in config folder, the config.json file will be reset to show your_bot_token_here, so this is never left exposed. 

## Installation
This is more in depth installation if needed, windows systems require cairosvg to be installed specially, as it is not included by default on windows

### Prerequisites
- Python 3.11+
- `pip`
- Python `venv` for windows if running locally
- CairoSVG is required for the image generation features, if on windows you will need to install this specially
- `lxml` if no wheels, but wheels is reccomended as lxml really racks up memory and cpu usage 
- [Optional] `certbot` for HTTPS support. If unavailable, some deployments can fall back to HTTP

### Option 1: Python
Python is highly recommended because this is the environment the bot is designed to run in, and has been tested to work in.

Most discord bot hosting will ask for a start file, as they use [Pterodactyl](https://pterodactyl.io/) often: 
```text
bot.py
```
For a manual python command in console just use:
```bash
python bot.py
```
If it won't start then install the requirements using pip:
```bash
pip install -r requirements.txt
```
Create a virtual environment (really only required if you are using the hosting for other things):
```bash
python -m venv .venv
```
Windows installation requires a virtual environment:
```bash
.venv\Scripts\activate
pip install -r requirements.txt
python bot.py
```
Linux installation if you require a virtual enviromnent (such as a non console set up):
```bash
source .venv/bin/activate
pip install -r requirements.txt
python bot.py
```

### First-Time Bot Token Setup

When bot.py runs it will ask for a bot token, if hasn't already been added to the config.json file in config folder, the config.json file will be reset to show your_bot_token_here, so this is never left exposed. 

The normal start up option for python is to just start the bot.py which then starts up the first install: 
```bash
python bot.py
```
Alternatively the config.json file in config folder can be edited before startup to include the bot token:
```bash
{
    "bot_token": "your_bot_token_here",
    "bot_name": "Echo Bot",
    "command_prefix": "?",
    "log_file": "bot.log",
    "log_messages": true,
    "log_commands": true,
    "database_file": "echo.db",
    "echo_api_database": "echo_api.db"
    ,
    "auto_restart_on_disconnect": true,
    "auto_restart_delay_seconds": 5
}
```
You can also use the cli_setup.py to run the token directly, but it is probably easier to just edit the config.json than do that before runnning the bot.py:
```bash
python cli/cli_setup.py token
```

### Option 2: NPM
NPM is not really reccomended as it is python bot, and the depencies are really meant for python

Here is the command for this if you need it:
```bash
npm run setup
npm run run:bot
```
This will install a python 3.11+ environment for the bot and the required dependencies

### Option 3: Clone the Repo to where you want it
```bash
git clone https://github.com/goldcyper/ns_echobot.git
cd ns_echo_bot
python -m venv .venv
pip install -r requirements.txt
python bot.py
```

## Usage
This bot should not be used for any implementation against the terms and conditions of Discord, Nationstates and the forum hosts this was designed for.

## Bot Configuration

| Option | Type | Default value | Description |
|--------|------|---------|-------------|
| `bot token` | string | none | Discord bot token that is essential for operation |
| `guild regions` | list | empty | Discord guilds enabled on the bot, and one region per guild usually |
| `NationStates credentials` | string/object | none | Nationstates password key that is encrypted and stored |
| `forum settings` | object | optional | The setings for the forum implementation, which includes the forum API key |
| `proxy verification settings` | object | optional | This is for if you want to run the proxy server and map features |

### Environment Variables
You could potentially need python buffered or a cairo path variable in the case of windows.

Python buffered enable:
```bash
PYTHONUNBUFFERED=1
```
.env file for windows to provide a CAIRO path:
```bash
# Environment configuration for NS Echo Bot
# Cairo library path for Windows (required for cairosvg)
CAIRO_PATH=C:\msys64\ucrt64\bin
```
Basically CAIRO needs to be given a clear path on windows.

## API References
- This bot can't function without the [Nationstates API](https://www.nationstates.net/pages/api.html), Discord API, and other APIs related to your implementation of the bot. You need to assign a NationStates nation to the bot to comply with API rules and API keys for use of APIs. 

### Main Bot and Installation Bot
This installs dependencies, starts the bot, and runs the scheduling tasks:
**Entry file:**
- `bot.py`

### Echo API Service
This processes the archvival data of daily dumps and provides an database for the main bot to use:
**Startup file:**
- `run_echo_api.py`

### Proxy Verification Service
This runs the proxy server, which helps to identity IP addresses and check if they are proxies:
**Startup file:**
- `start_proxy_server.py`

## Performance
This project is focused for now on peformance of running its operations over effiency, though this might change as more edits are made to the project.

The key issues being faced are the following:
- the size of the databases
- the API limits on performing certain actions
- size of the historical and current daily dump data stored in `echo_api.db`
- avaliablity of `lxml` and wheel for faster parsing of XML data from the daily dumps
- how many servers the bot is in and how many action requests are made on the bot

## Roadmap achievements thus far
- [x] Core functions are working for the bot
- [x] Nation and WA monitoring is working well
- [x] Resident and Verification tools functioning
- [x] Most map operations are functioning
- [ ] Map includes full NS Map export functions for NS color limitations
- [ ] Menu is clean and without minor bugs
- [ ] Depreciatied code has been removed
- [ ] Dedicated CPU and Memory throttler for 500 MB, 1 GB, and 1.5 GB systems
- [ ] Documentation complete and deployed to repo

See the repo notes and planning docs for ongoing cleanup direction.

## Contributions
If you want to contribute fork this repo, or get in touch with me if you have some ideas.

## Troubleshooting 
This is for some errors you might encounter with installation

### Error: bot won't start due to missing dependencies
You need to have most of these installed, though some are fallback depedencies: 
```bash
pip install -r requirements.txt
```
Usually this down to a few things:
- Python version isn't correct, must be python 3.11+
- Highly reccommend you install wheels for `lxml` due to memory issues
- CairoSVG must be installed as otherwise the image generation features won't work

### Error: problems with your configuration or bot token
You can use the cli setup tools for this:
- `config/config.json`
- This tells you whether the token was installed in the database
- It allows setup through `python cli/cli_setup.py token`
- It will tell you whether your host allows console or not
- This isn't likely to happen as the bot token setup has the config.json file failsafe you can use

### Error: help my bot crashed due to memory or cpu 
This is common unfortunately, as the daily dumps are so large to process on first load
- If you have these problems you need to sure your hosting can support the bot
- Despite my best efforts to make this as low memory and cpu intensive as possible, it is likely that you will require 1 GB+ to run the bot.
- Daily dump processing is just huge on CPU usage, as is the first start processing of the echo_api.db
- Often a restart will fix this, but if not there aren't a lot of options, as the bot needs the daily dump to be processed

### Still stuck?
- Check the bot documentation here (as I planned it to be pretty extensive)
- Check the live console log (if you have console access)
- Check the bot logs for issues (same as above output)
- Restarting the bot solves most memory and CPU usage issues (should be done at least once a week anyway)
- Send me a message or ask me for help on the Lazarus discord server. I really don't bite...much (not a vampire)

## License
MIT License for this project, as this was done for fun and non-commerical purposes

## Acknowledgments
- Nationstates API developers that made this all possible. Thanks to Violet and the whole team! :heartpulse:
- Developers of the `discord.py` and the Discord API that made this all possible as well! :purple_heart:
- [Spyglass](https://github.com/Derpseh/Spyglass) developers that gave me the idea for region update implementation in python
- [FluffyCogs(RedBot Cog)](https://github.com/zephyrkul/FluffyCogs) developers who gave me the idea for various nation and region lookups
- To Visual Studio Code, Github, and Codex for their awesome devlopment tools that made this way less stressfull 
- To the Lazarus region who bore the brunt of bot development woes and bug testing :green_heart:
