# MineflayerDoc
## docs
### mineflayer docs
- [mineflayer](https://github.com/PrismarineJS/mineflayer)
- [mineflayer docs](https://github.com/PrismarineJS/mineflayer/blob/master/docs/api.md)
- [javascipt examples](https://github.com/PrismarineJS/mineflayer/tree/master/examples)
- [python tutorial/examples](https://github.com/PrismarineJS/mineflayer/tree/master/examples/python)
### pathfinding docs
- [pathfinder](https://github.com/PrismarineJS/mineflayer-pathfinder)
## setup
husk at have downloadet [NodeJs](https://nodejs.org/en/), [vscode](https://code.visualstudio.com/)
- lav en tom mappe
- open i vscode
- kør følgende commands:
```
npm init -y
npm i mineflayer
npm i mineflayer-pathfinder
npm i mineflayer-collectblock
```
## hello world example
```
const mineflayer = require('mineflayer')

const bot = mineflayer.createBot({
  host: 'pvp.asguho.dk',
  port: '25543',
  username: 'player1',
})
bot.on('spawn', (username, message) => {
  bot.chat('hello world')
})

// Log errors and kick reasons:
bot.on('kicked', console.log)
bot.on('error', console.log)
```
## crafting function example
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
