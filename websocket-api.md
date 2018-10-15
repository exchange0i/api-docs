# Websocket-api

Official Documentation for the APIs
 
## Steps   
1）Connect
2）Subscribe
3）Receive

## Subscribe data   

WebSocket server：

	wss://trade.0i.com/ws/

Response： 
  
	{"result": "success", "id": 0, "error": null}

## APIs

### 1)Subscribe depth data
Request raw data: 

	{"method":"depth.subscribe","params":["OMG/ETH", "1x", 10],"id":0} 
 
* Detail:  
OMG/ETH #market   
1x #Consolidation depth(false)   
10 #raw number    

response example： 
	
      {    
          "params": [
              "OMG/ETH",
              [
                  {
                      "bids": [
                          ["0.00001076", "175156"],
                          ["0.00001072", "125499"],
                          ["0.0000107", "7392"],
                          ["0.00001062", "8823"],
                          ["0.0000106", "10000"],
                          ["0.00001051", "32523"],
                          ["0.0000105", "311805"],
                          ["0.00001022", "222222"],
                          ["0.00001011", "42830"],
                          ["0.0000101", "623042"]],
                      "asks": [
                          ["0.0000115", "307646"],
                          ["0.0000119", "30000"],
                          ["0.00001195", "250342"],
                          ["0.000012", "507700"],
                          ["0.00001207", "64161"],
                          ["0.0000121", "30000"],
                          ["0.00001229", "70000"],
                          ["0.00001235", "80483"],
                          ["0.00001237", "1767403"],
                          ["0.00001239", "20000"]],
                      "time": 1526266518.043814
                  }
              ]
          ],
          "method": "depth.update",
          "id": null
      }
      
 
### 2)Subscribe deal tick
Request raw data: 

	{"method":"deals.subscribe","params":["OMG/ETH"],"id":0}  

* Detail:  
OMG/ETH #market   

Response example: 

    {
        "params": [
            "OMG/ETH",
            [
                  [1526261908.24362, "0.0000115", "97045", 2],
                  [1526259958.30595, "0.0000115", "5000", 2],
                  [1526254787.086168, "0.00001149", "849000", 2],
                  [1526254688.183289, "0.00001073", "700000", 1],
                  [1526245846.150899, "0.00001072", "61397", 1],
                  [1526245846.150774, "0.00001073", "76489", 1],
                  [1526245846.15065, "0.00001074", "34256", 1],
                  [1526245846.150516, "0.00001075", "67854", 1],
                  [1526245846.150349, "0.00001077", "34526", 1],
                  [1526245846.150203, "0.00001082", "7000", 1]
            ]
        ],
        "method": "deals.update",
        "id": null
    }
    
### 3)Subscribe order status
Request raw data: 

	{"method":"orders.subscribe","params":["token"],"id":0}

Response example: 
	
      {
            "params": [
                  { "id": 26211,                  #order ID
                    "type": 1,                    #order type   1 limit price  2 market price
                    "market": "OMG/ETH",          #market
                    "side": 2,                    #side   1 sell  2 buy
                    "ctime": 1526205633.6342139,  #order time
                    "mtime": 1526205633.6342139,  #update time
                    "price": "0.00001057",        #order price
                    "deal_money": "0",            #deal money
                    "status": 1,                  #status   0 not deal yet  1 finished  2 canceled
                    "amount": "10000",            #amount
                    "left": "10000",              #left amount
                    "deal_stock": "0"             #deal stock
                    }
            ], 
            "method": "orders.update", 
            "id": null
      }

### 4)Subscribe balance
Request raw data: 
	
	{"method":"balance.subscribe","params":["token"],"id":0} 

Response example: 

      {
            "params": [
                    {"available": "99999980.24173",   #available balance
                    "asset": "ETH",                   #token name
                    "freeze": "23.596"}               #freeze balance
            ], 
            "method": "balance.update", 
            "id": null
      }

