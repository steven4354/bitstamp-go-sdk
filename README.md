bitstamp-go
===========

A client implementation of the Bitstamp API, including websockets, in Golang.

Example Usage
-----

```go
package main

import (
	"fmt"
	"log"
	"time"

	"github.com/steven4354/bitstamp-go"
)

func main() {

	// setup bitstamp api
	b := bitstamp.NewClient("123456", "key", "secret")

	// get balance
	balances, err := b.AccountBalance()
	if err != nil {
		fmt.Printf("Can't get balance using bitstamp API: %s\n", err)
		return
	}
	fmt.Println("\nAvailable Balances:")
	fmt.Printf("USD %f\n", balances.UsdAvailable)
	fmt.Printf("BTC %f\n", balances.BtcAvailable)
	fmt.Printf("FEE %f\n\n", balances.BtcUsdFee)

	// attempt to place a buy order
	// BuyLimitOrder(pair string, amount float64, price float64, amountPrecision, pricePrecision int)
	order, err := b.BuyLimitOrder("btcusd", 0.5, 600.00, 16, 16)
	if err != nil {
		log.Printf("Error placing buy order: %s", err)
		return
	}
	fmt.Printf("Place oder %d", order.Id)
}
```
