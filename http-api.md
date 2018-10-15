# Http-api

Official Documentation for the APIs


## Market API

Post /

URL: https://trade.0i.com/depth/

body:

    {"method": "depth.query", "params": ["OMG/ETH",10], "id": 0}        #query depth data（10：means query for 10 records）

Response：

    {
        "result": [
            {
                "bids": [["0.0000099", "126936"], ["0.00000984", "162179"]...], 
                "asks": [["0.00001088", "282265"], ["0.000011", "1561350"]...], 
                "time": 1529826401.615678
             }
        ], 
        "error": null, 
        "id": 0
     }


## Exchange API

token: please read token-api.md to get details about token

### 1)Query balance

Post /

URL: https://trade.0i.com/

body: 

    {"method":"balance.query","params":["token"],"id":0}                #query all the balance of your tokens
    {"method":"balance.query","params":["token", “ETH”, “OMG”],"id":0}  #query the specified balance of single token

Response：

    {
      "result": [
        {
          "freeze": "0.6",           
          "asset": "ETH",            
          "available": "999.2036012",
          "total": "999.8036012",   
          "btcvalue": "0",           
          "ethvalue": "999.8036012"   
        }, 
        {
          "freeze": "0", 
          "asset": "OMG", 
          "available": "0", 
          "total": "0", 
          "btcvalue": "0", 
          "ethvalue": "0e-8"
        }
      ], 
      "error": null, 
      "id": 0
    }
    
### 2)Your current orders

Post /

URL: https://trade.0i.com/

body: 

    {"method":"order.query", "params":["token", 0, 100],"id":0}     #query your first 100 orders
    {"method":"order.query", "params":["token", 100, 100],"id":0}   #query your 100th - 200th orders

Response：

    {
      "result": {
        "limit": 99, 
        "records": [
          {
            "id": 26211,                  #order ID
            "type": 1,                    #order type 1 limit price  2 market price
            "market": "OMG/ETH",          #market
            "side": 2,                    #side   1 sell  2 buy
            "ctime": 1526205633.6342139,  #make time
            "mtime": 1526205633.6342139,  #update time
            "price": "0.00001057",        #order price
            "deal_money": "0",            #deal money
            "status": 1,                  #order status   1 not deal yet
            "amount": "10000",            #amount
            "left": "10000",              #left number
            "deal_stock": "0"             #deal stock
          }
        ], 
        "total": 1, 
        "offset": 0
      }, 
      "error": null, 
      "id": 0
    }

### 3)Limit price order

Post /

URL: https://trade.0i.com/

body: 

    {
      "method":"order.limit", 
      "params":[
        "token",      #Token
        "OMG/ETH",    #market
        2,            #side 1 sell  2 buy (int)
        "1000",       #number
        "0.00001057", #price
        0             #nothing (number)
      ],
      "id":0
    }

Response:

    {
      "error": null, 
      "result": {
        "id": 26211,                  #order ID
        "type": 1,                    #order type   1 limit price  2 market price
        "market": "OMG/ETH",          #market
        "side": 2,                    #side   1 sell  2 buy
        "ctime": 1526205633.6342139,  #make time
        "mtime": 1526205633.6342139,  #update time
        "price": "0.00001057",        #order price
        "deal_money": "0",            #deal money
        "status": 1,                  #order status 1 not deal yet 2 finished 3 canceled
        "amount": "10000",            #amount
        "left": "10000",              #left
        "deal_stock": "0"             #deal stock
      }, 
      "id": 0
    }

### 4)Market price order

Post /

URL: https://trade.0i.com/

body: 

    {
        "method":"order.market", 
        "params":[
            "token",      #Token
            "OMG/ETH",    #market
            2,            #side 1 sell  2 buy   (int)
            "0.1",        #number buy：ETH number   sell：OMG number
            0             #nothing (number)
        ],
        "id":0
    }

Response:

    {
        "error": null, 
        "result": {
            "id": 26212, 
            "ctime": 1526209901.4186571, 
            "mtime": 1526209901.418669, 
            "left": "0.004", 
            "market": "OMG/ETH", 
            "amount": "0.1", 
            "type": 2, 
            "side": 2, 
            "status": 2, 
            "price": "0", 
            "deal_stock": "16", 
            "deal_money": "0.096"
        }, 
        "id": 97
    }

### 5)Cancel order

Post /

URL: https://trade.0i.com/

body: 

    {"method":"order.cancel", "params":["token", "OMG/ETH", 26211],"id":0}               #cancel order
    {"method":"order.cancel", "params":["token", "OMG/ETH", 26211,262112,26213],"id":0}  #Batch cancel

Response:

    {
        "result": {
            "id": 26316, 
            "type": 1, 
            "market": "OMG/ETH", 
            "side": 2, 
            "ctime": 1526209523.637193, 
            "mtime": 1526209523.637193, 
            "price": "0.0000101", 
            "deal_money": "0", 
            "status": 3, 
            "amount": "10000",
            "left": "10000", 
            "deal_stock": "0"
        }, 
        "error": null, 
        "id": 0
    }
    
### 6)Order history

Post /history/

URL: https://trade.0i.com/history/

body: 

    {
        "method":"order.history", 
        "params":[
            "token",        #Token
            "OMG/ETH",      #market
            1526140800,     #begin time
            1526210312,     #end time
            0,              #offset
            100],           #limit
        "id":0
    }

Response:

    {
        "result": [
            {
                "order_id": 26316,                  #order ID
                "status": 3,                        #order status 1 not deal yet 2 finished 3 canceled         
                "deal_money": "0",                  #deal money
                "create_time": 1526209523.637193,   #make time
                "side": 2,                          #side 1 sell  2 buy
                "finish_time": 1526209523.637193,   #finish time
                "market": "OMG/ETH",                #market
                "t": 1,                             #order type   1 limit price  2 market price
                "price": "0.0000101",               #order price
                "amount": "10000",                  #order number
                "deal_stock": "0"                   #deal stock
            },{
                "order_id": 26211, 
                "status": 3, 
                "deal_money": "0", 
                "create_time": 1526205633.6342139, 
                "side": 2, 
                "finish_time": 1526205633.6342139, 
                "market": "OMG/ETH", 
                "t": 1, 
                "price": "0.00001057", 
                "amount": "10000", 
                "deal_stock": "0"
            }
        ], 
        "error": null, 
        "id": 6
    }

### 7)Trade history

Post /history/

URL: https://trade.0i.com/history/

body: 

    {
        "method":"deals.history", 
        "params":[
            "token",        #Token
            "OMG/ETH",      #market
            1526140800,     #begin time
            1526210312,     #end time
            0,              #offset
            100],           #limit
        "id":0
    }

Response:

    {
        "result": [
            {
                "time": 1526209901.418669,      #time
                "market": "OMG/ETH"             #market
                "deal_id": 47521,               #deal ID
                "side": 2,                      #side 1 sell  2 buy
                "price": "0.00600000",          #deal price
                "amount": "16.00000000",        #deal number
                "deal": "0.0960000000000000",   #deal total
                "fee_asset": "OMG",             #fee asset
                "fee": "0E-16",                 #fee
            }
        ], 
        "id": 0, 
        "error": null
    }
