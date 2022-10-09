# MineflayerDoc
## Docs
### Mineflayer docs
- [mineflayer](https://github.com/PrismarineJS/mineflayer)
- [mineflayer docs](https://github.com/PrismarineJS/mineflayer/blob/master/docs/api.md)
- [javascipt examples](https://github.com/PrismarineJS/mineflayer/tree/master/examples)
- [python tutorial/examples](https://github.com/PrismarineJS/mineflayer/tree/master/examples/python)
### Pathfinding docs
- [pathfinder](https://github.com/PrismarineJS/mineflayer-pathfinder)
## Setup
husk at have downloadet [NodeJs](https://nodejs.org/en/) & [vscode](https://code.visualstudio.com/)
- lav en tom mappe
- open mappen i vscode
- kør følgende commands i terminalen
```shell
npm init -y
npm i mineflayer
```
- herefter bare lav en tom javascript fil (f.eks. index.js)
- nu kan du prøve og lave din første minecraft bot!!
## Hello world example
```js
const mineflayer = require('mineflayer')

//creating the bot
const bot = mineflayer.createBot({
  host: 'pvp.asguho.dk',
  port: '25543',
  username: 'player1',
})

//on the event spawn, sent in chat the message 'helloworld'
bot.on('spawn', () => {
  bot.chat('hello world')
})

// Log errors and kick reasons:
bot.on('kicked', console.error)
bot.on('error', console.error)
```
## Attack example
```js
const mineflayer = require('mineflayer')

//creating the bot
const bot = mineflayer.createBot({
  host: 'pvp.asguho.dk',
  port: '25543',
  username: 'player1',
})

//on the event chat, if the messsage is hit, then it attacks
bot.on('chat', (username, message) => {
if(message == 'hit'){
  bot.attack(bot.nearestEntity())
  }
})

// Log errors and kick reasons:
bot.on('kicked', console.error)
bot.on('error', console.error)
```
## pathfinding example
husk at installere pathfinderen:
```shell
npm i mineflayer-pathfinder
```
for en list af goals her: [goals](https://github.com/PrismarineJS/mineflayer-pathfinder#Goals)
```js
const mineflayer = require('mineflayer')
const { pathfinder, Movements, goals } = require("mineflayer-pathfinder");

//creating the bot
const bot = mineflayer.createBot({
  host: 'pvp.asguho.dk',
  port: '25543',
  username: 'player1',
})

//loading the pathfinder plugin
bot.loadPlugin(pathfinder);

//on the event chat, if the messsage is come, then it pathfinds to the nearest entity
bot.on('chat', (username, message) => {
if(message == 'come'){
  const target = bot.nearestEntity();
  bot.pathfinder.setGoal(new goals.GoalNear(target.x, target.y, target.z, 1))
  }
})

// Log errors and kick reasons:
bot.on('kicked', console.error)
bot.on('error', console.error)
```
## Loop snipet
har du aldrig arbejdet med events så læs her: [Listening for an event](https://github.com/PrismarineJS/mineflayer/blob/master/docs/tutorial.md#listening-for-an-event)
```js
bot.on('physicsTick', () => {
    //alt herinde vil blive kørt hvert tick, aka 20 gange i sekundet.
})
```
events er virkelig pratiske her er alle dem fra mineflayer: [mineflayer events](https://github.com/PrismarineJS/mineflayer/blob/master/docs/api.md#events)

## Collect block example
husk at installere mineflayer-collectblock:
```shell
npm i mineflayer-collectblock
```

```js
bot.loadPlugin(require('mineflayer-blockfinder').plugin);

bot.on('chat', async (username, message) => {
if(message == 'dig'){
    const mcData = require('minecraft-data')(bot.version);

    const dirtblock = bot.findBlock({
      matching: mcData.blocksByName.oak_log.id,
      maxDistance: 64
    })
    
    await bot.collectBlock.collect(dirtblock)
    bot.chat('dirt collected')
  }
})
```
## Crafting function example
har du aldrig prøvet async funtioner så læs her: [promises](https://github.com/PrismarineJS/mineflayer/blob/master/docs/tutorial.md#promises)
```js
bot.on('chat', async (username, message) => {
  if(message == 'craft'){
    await craftItem(oak_planks, 1);
    bot.chat('done crafting!!');
  }
})

async function craftItem (name, amount) {
  amount = parseInt(amount, 10)
  const mcData = require('minecraft-data')(bot.version)

  const item = mcData.itemsByName[name]
  const craftingTableID = mcData.blocksByName.crafting_table.id

  const craftingTable = bot.findBlock({
    matching: craftingTableID
  })

  if (item) {
    const recipe = bot.recipesFor(item.id, null, 1, craftingTable)[0]
    if (recipe) {
      bot.chat(`I can make ${name}`)
      try {
        await bot.craft(recipe, amount, craftingTable)
        bot.chat(`did the recipe for ${name} ${amount} times`)
      } catch (err) {
        bot.chat(`error making ${name}`)
      }
    } else {
      bot.chat(`I cannot make ${name}`)
    }
  } else {
    bot.chat(`unknown item: ${name}`)
  }
}
```

# Example you can make
## [Autoeat](https://github.com/link-discord/mineflayer-auto-eat)
## [perfekt bow](https://github.com/sefirosweb/minecraftHawkEye)
## [Auto equip armor](https://github.com/G07cha/MineflayerArmorManager)
## [view the bot in the browser](https://github.com/PrismarineJS/prismarine-viewer)
## [statemachine](https://github.com/PrismarineJS/mineflayer-statemachine)
## make a schematic builder
[schematic](https://github.com/PrismarineJS/prismarine-schematic) [et forsøg på det](https://github.com/PrismarineJS/mineflayer-builder)

