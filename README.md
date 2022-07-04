# DisWebhooker
this libray for webhooks. to have fun bots and to create discord applications.

diswebhooks more fun and more contrell. a tool to use webhooks like discord bots
this tool doesn't really use wehbooks its just copy them and use their info anywhere

if you want only the webhook api,

you can use [DisWebhook github](https://github.com/programminglaboratorys/DisWebhook)/[DisWebhook PyPi](https://pypi.org/project/DisWebhook) libray. its easy and simple to use


# installation

Run the following to install:
```cmd
pip install DisWebhooker
```
### or
```cmd
python -m pip install DisWebhooker
```
if that didn't work, try replacing `pip` with `pip3`.
need help? my discord: [lab](https://discord.gg/vzEZnC7CM8)


# simple bot
```py
########################## imports #########################
from DisWebhooker.bot import Bot               # the webhook Bot
from DisWebhooker.bot import hibot             # hibot this to run our bot. works as commands.bot
from DisWebhooker.func import CreateTree as CW # CW = Create webhook Tree
import discord                                 # importing discord for Intents
#########################  exec  ###########################

TOKEN   = "the bot token here"
intents = discord.Intents.all() # to get the massages.content

# setuped=True means the webhook will be an webhookIO (unreal webhook)
webhookerBot = Bot(command_prefix="#",setuped=True,username="beepboop")
# this can be a list object or a Tree object -c "import mkrTree; mkrTree.Tree(childern=[webhook1,webhook2])" \
# CW is a func to create a Tree object
webhooks = [CW(webhookerBot)] #;print(CW(Bot)) # output: <Tree(data(name="webhook",obj=<class 'Bot'>),children=[])>

# hibot = high-level-bot. this object will handle the webhooks process_command
client = hibot(webhooks=webhooks,command_prefix = "!",intents=intents, guild_subscriptions=True) 

@webhookerBot.event
async def on_raw_message_delete(bot,message):
	print("message been deleted",repr(message),sep=": ")

@webhookerBot.command(name="say",description="make the bot say anything :) 'Hello World'")
async def test_webhook(self,ctx,*arg):
	# self is the bot and ctx is the main bot
	await self.send(*arg)

@webhookerBot.command(name="hi",description="say 'Hello, World!'")
async def Hello_World(self,ctx):
	await self.send("Hello, World!")

# the main bot
@client.command(name="ping")
async def ping(ctx):
		await ctx.send(f'Pong! {round(client.latency * 1000)}')

# webhookerBot is already setup no need to setup the bot
client.run(TOKEN)

```


# the test bot
```py
########################## imports #########################
from DisWebhooker.bot import Bot               # the webhook Bot
from DisWebhooker.bot import hibot             # hibot this to run our bot. works as commands.bot
from DisWebhooker.func import CreateTree as CW # CW = Create webhook Tree
from DisWebhooker.func import GetToken         # going to use it, to get the webhook token and id
import discord                                 # importing discord for Intents
#########################  exec  ###########################

WEBHOOK_TOKEN = "a webhook token"
TOKEN         = "the bot token here"
intents       = discord.Intents.all() # to get the massages.content

webhookerBot = Bot(command_prefix="?")#,setuped=True)
# setuped=True means the webhook will be an webhookIO (unreal webhook)
webhookerBot2= Bot(command_prefix="#",setuped=True,username="beepboop")
# this can be a list object or a Tree object -c "import mkrTree; mkrTree.Tree(childern=[webhook1,webhook2])" \
# CW is a func to create a Tree object
webhooks = [CW(webhookerBot),CW(webhookerBot2)] #;print(CW(Bot)) # output: <Tree(data(name="webhook",obj=<class 'Bot'>),children=[])>

# hibot = high-level-bot. this object will handle the webhooks process_command
client = hibot(webhooks=webhooks,command_prefix = "!",intents=intents, guild_subscriptions=True) 

# bot 1
# a new features event can be added now
@webhookerBot.event
async def on_raw_message_delete(bot,message):
	print(message)
	print(bot)
# listen can be use too. note this events are for the bot himself not the webhook
@webhookerBot.listen(name="on_message")
async def on_something(bot,message):
	pass

# bot 1 commands
@webhookerBot.command(name="say",description="make the bot say anything :) 'Hello World'")
async def test_webhook(self,ctx,*arg):
	# self is the bot and ctx is the main bot
	await self.send(*arg)

@webhookerBot.command(name="hi",description="say 'Hello, World!'")
async def Hello_World(self,ctx):
	await self.send("Hello, World!")

# bot 2
@webhookerBot2.command(name="hi",description="say 'Hello, World!'")
async def Hello(self,ctx):
	await self.send("Hello, World!")


@webhookerBot2.command(name="time",description="give you the date time")
async def Hello_World(self,ctx):
	import time
	await self.send(f"the time right now is {time.strftime('%I:%M:%S %Y/%m/%d (%z)')}")

# the main bot
@client.command(name="test")
async def ping(ctx):
		await ctx.send(f'Pong! {round(client.latency * 1000)}')

@client.command()
async def pong(ctx):
    await ctx.send('**ping**')



# this setup the webhook object its like run but its for the webhook. can be put in the start of the code or the end of the code recommand to put at the end before the bot runs
webhookerBot.setup(*GetToken(WEBHOOK_TOKEN))
client.run(TOKEN)
```
## any ideas?
### places
- [github](https://github.com/programminglaboratorys/DisWebhooker)
- [discord](https://discord.gg/vzEZnC7CM8)


Change Log
==========

0.1.0 (2022/7/4)
-------------------
- First Release

