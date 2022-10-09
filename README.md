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
- kør følgende commands:
```
npm init -y
npm i mineflayer
```
- herefter bare lav en tom javascript fil (f.eks. index.js)
- nu kan du prøve og lave din første minecraft bot!!
## Hello world example
```
const mineflayer = require('mineflayer')

//creating the bot
const bot = mineflayer.createBot({
  host: 'pvp.asguho.dk',
  port: '25543',
  username: 'player1',
})

//on the event spawn, sent in chat the message 'helloworld'
bot.on('spawn', (username, message) => {
  bot.chat('hello world')
})

// Log errors and kick reasons:
bot.on('kicked', console.error)
bot.on('error', console.error)
```
## Crafting function example
har du aldrig prøvet async funtioner så læs her: [promises](https://github.com/PrismarineJS/mineflayer/blob/master/docs/tutorial.md#promises)
```
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

```
npm i mineflayer-pathfinder
npm i mineflayer-collectblock
```
