# Coinbase API Recurring Purchases
A crypto DCA server coded in kotlin & OkHttp3
## What is Dollar-Cost-Averaging (DCA)?
DCA is a way of minimizing risk by spreading your investments.

This server allows you to make small crypto orders on a daily schedule (24-hours apart) 

**Bonus:** *while saving a lot on swap fees.*
### API Saves over 97.9% on fees (August 2024)
**Normal Retail Fee**

Coinbase retail fees for recurring investments will range you anywhere from 50% (on the large end) to 14.2% (on the medium range) of your orders.
![coinbase retail fee for $1 of litecoin](https://i.gyazo.com/bd8d1ca03a6dcb6b3ce53911517dbe80.png)

Making trades through the API reduces that to 0.6% instead.

**Fee with API**

Server response:

![Coinbase Server Response](https://i.gyazo.com/d4714a091da4a8020bee8bd4d600c1ec.png)

**Actual fee paid:**
# 2¢

![Final fee paid using the developer api](https://i.gyazo.com/f3a4e97656536f673552b0905cd62c93.png)

# How *'Kotlin Coinbase Recurring Purchases'* works
It uses your quote asset balance i.e USD (which is free to top up via bank transfers).

And once USD (or quote asset) runs out it will switch quote asset to using USDC instead (coming soon).

### Uses CDP API
This application uses CDP API credentials (Coinbase Developer Platform) to make trades on your behalf. Credentials should be placed as a .json file  in the same directory as the .jar file.

Alternatively, Environment variables (.env) can be used. COINBASE_NAME & COINBASE_PRIVATE_KEY
## Endpoints

### GET: /
Confirms if the kotlin server is running.

### POST: /start/{jobId}
Start a recurring buy order (job).

{jobId} can be anything you want to name this order (in case you want to stop it later too).

Order configuration options (request body)
```
{
  productId:String, //(i.e BTC-USD)
  quoteSize:String //(amount of btc to buy in USD terms [uses right-hand currency])
}
```

 OR

```
{
  productId:String (i.e BTC-USD),
  baseSize:String (amount of btc to buy [uses left-hand currency])
}
```

### GET: /stop/{jobId}
Stops a recurring buy order job.

### GET: /status
Lists currently running jobs, their jobId and the order configuration
