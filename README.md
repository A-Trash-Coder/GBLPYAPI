# gblapi.py - The official PY API Wrapper for the GBL API

![PyPI](https://img.shields.io/pypi/v/gblpyapi?logoColor=237289DA)

# About
This is the **official** api wrapper for GlennBotList.xyz written in Python, and published to [Pypi](https://pypi.org/project/gblpyapi/)

# Installation
To install **gblapi.py** run this command in a terminal:

> Install gblapi.py:
>
>```
>pip install gblpyapi
>```

## Features
Function  | Action
------------- | -------------
post_server_count(botid, guilds, shards: optional) (note: requires authentication) | POST Server Count 
get_user_info(userid) | GET User Info
get_has_voted(userid) (note: required authentication) | GET If a user has voted
get_bot_votes(botid) (note: requires authentication) | GET Bot Votes
get_bot_stats(botid) | GET Bot Stats
get_vote_count(botid) | GET Bot Votes

# Examples
## Post server count

```python
import discord
import glennbotlist.GBL as GBL
from discord.ext import tasks

gbl = GBL("token") # glenbotlist.xyz API token

@tasks.loop(minutes = 30) # Posts server count every 30 minutes
async def postservers(self):
    await gbl.post_server_count(self.bot.user.id, len(self.bot.guilds))

```
## Get Bot Info

```python
import discord
import glennbotlist.GBL as GBL
from discord.ext import commands

gbl = GBL()

@commands.command()
async def botinfo(self, ctx, bot: discord.Member):
    if not bot.bot:
        await ctx.send("This user is not a bot!")
        return

    info = await gbl.get_bot_stats(bot.id)
    await ctx.send(info['name']) # Name

```
## Get Bot Votes

```python
import discord
import glennbotlist.GBL as GBL
from discord.ext import commands

gbl = GBL("token") # glenbotlist.xyz API token

@commands.command()
async def botvotes(self, ctx):
    votes = await gbl.get_bot_votes(self.bot.user.id)
    await ctx.send(votes['current_votes']['monthly']) # People who have voted this month

```
## Get Bot Vote Count

```python
import discord
import glennbotlist.GBL as GBL
from discord.ext import commands

gbl = GBL("token") # glenbotlist.xyz API token

@commands.command()
async def botvotecount(self, ctx):
    votes = await gbl.get_vote_count(self.bot.user.id)
    await ctx.send(votes['alltime']) # Alltime Votes

```
## Get User Info

```python
import discord
import glennbotlist.GBL as GBL
from discord.ext import commands

gbl = GBL()

@commands.command()
async def userinfo(self, ctx, user: discord.Member):
    info = await gbl.get_user_info(user.id)
    await ctx.send(info['username']) # User Name

```
## Get User Has Voted

```python
import discord
import glennbotlist.GBL as GBL
from discord.ext import commands

gbl = GBL("token") # glenbotlist.xyz API token

@commands.command()
async def voted(self, ctx, userid: int):
    voted = await gbl.get_has_voted(self.bot.id, userid)
    await ctx.send(voted) # Boolean

```

# Authors
> Made by `A Trash Coder#0981`

# Help
> Join our [Discord Server](https://glennbotlist.xyz/discord) for help on this module.