# MineflayerDoc

```
npm init -y
npm i mineflayer
npm i mineflayer-pathfinder
```
```
const mineflayer = require('mineflayer')

const bot = mineflayer.createBot({
  host: 'pvp.asguho.dk',
  port: '25575',
  username: 'player1',
})

bot.on('chat', chatBack(username, message));

function chatBack(username, message){
  if (username === bot.username) {return}
  bot.chat(message)
}

// Log errors and kick reasons:
bot.on('kicked', console.log)
bot.on('error', console.log)
```
