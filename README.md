# Coinbase API Recurring Purchases
A crypto DCA server coded in kotlin & OkHttp3
## What is Dollar-Cost-Averaging (DCA)?
DCA is a way of minimizing risk by spreading your investments.

The server allows you to make small crypto orders on a daily schedule (24-hours apart) 

Bonus: while saving a lot on swap fees.
### API Saves over 97.9% on fees (August 2024)
Typically, Coinbase retail fees for recurring investments will range you anywhere from 50% (on the large end) to 14.2% (on the medium range) of your orders.

Making trades through the API, reduces that to 0.6% instead.

Uses your USD balance (free to top up via bank transfers).
Once USD runs out it will switch to using USDC instead (coming soon).

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
