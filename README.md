# Demo Stoploss implementation on Serum DEX

Hi, thanks for reading this. First, what am I ?

Well this is a targetted demo of a stoploss implementation for [Serum DEX](https://github.com/project-serum).

## What is a stoploss ?

A stoploss is an ordertype available on lots of centralised trading platforms. Its aim is to limit a trading positions losses. So for example imagine you are long and the price is going down, or vice versa short and price is rising. The stoploss is used as a risk management tool to close positions before losses get too big. Example:

* user is long 1000 units current price is 10.00 and price is falling. User sets a SellStop order to trigger when price reaches 8.00. The SellStop sells 1000 units to close the position when the price falls to 8.00

### Why is it useful ? 

if in the above example the user set the order to sell at a price of 8 then in normal limit order book this would try to match immediately if the market is at 10 (price 8 below 10 so match would be attempted). 

The stoploss order is conditionally executed to allow more complex trading strategies.

It also allows the user to forget about positions and allow automated components help with risk management (ie leave it overnight etc).


## Why on Serum DEX ?

Serum DEX is a Decentralised Limit Order Book built on [Solana](https://solana.com/). Decentralised orderbooks have many advantages, however one area thats harder to maanage is conditional execution, due to on chain compute resources.

The stoploss is part of Serum roadmap and has been open for interested thirdparties to implement.


## This Demo's contents
This demo will show the architecture of on chain/off chain components, a sequence diagram of the flow, and a video of the stoploss in action.

### ARCHITECTURE

![alt text](https://github.com/teddytomas/stoploss/blob/master/Architecture.png?raw=true)

The **STOPLOSS** program is an onchain component. It communicates with the SRM DEX program. 

The **ALGOSERVER** and Gui Server are off chain components responsible for continually scanning for new Stoploss orders and for executing when conditions are met

The **ALGO UI** is a component for managing stoplosses (and potentially other more complex order types)

The **STORE** is a Time Series database that captures market data and order details.

The **MKT DATA** is a listener for market data updates responsible for sending orderbook updates.

green components are the ones developed independantly. 
blue components are existing project Serum components.

### Sequence Diagram


![alt text](https://github.com/teddytomas/stoploss/blob/master/stoploss-sequence.png?raw=true)



