# super-simple-stocks

A Global Beverage Corporation Exchange

### What can it do?
- Create new orders using a Super Simple Order Management System (OMS)
- Execute orders on the GBCE
- Fat Finger checks based on last traded price
- Add new stocks intraday
- Calculate  dividend yield, P/E ratio and ticker prices for all traded stocks
- Obtain the up to date index for the GBCE based on all traded stocks
- Supports two security types
- Execution guaranteed even without liquidity

### How to use it

Build and run unit tests
```
mvn clean install
```

New tests can be quickly added to [CustomComponentTests](src/test/java/com/simplebank/supersimplestocks/component/CustomComponentTests.java)

Sample test:
```java
gbceAdmin.addTickerToMarket(DividendDataFactory.createsNewCommonStock(TEA, 0.0, 100));
gbceAdmin.addTickerToMarket(DividendDataFactory.createsNewCommonStock(POP, 8.0, 100));
		
Order order = orderManagementSystem.enterNewOrderSingle(Side.BUY, TEA, 50, 10.5);
orderManagementSystem.execute(order);
		
Order anotherOrder = orderManagementSystem.enterNewOrderSingle(Side.BUY, POP, 100, 12.0);
Trade trade = orderManagementSystem.execute(anotherOrder);
		
double gbceIndex = orderManagementSystem.gbceIndex();
double teaDividendYield = orderManagementSystem.calculateDividendYield(TEA);
```

### Some notes
- There's no opening price so ticker prices and index are 0 until there are trades or after all trades expire
- Index is calculated with all stocks in the exchange in the trading session including those for which all trades expired (index would be zero)
- New intraday tickers will be included in the index calculation

### Future features
- Market data subscription: multiple clients to consume market data in real time
- Asynchronous ticker price and index calculation on new trades and trade eviction
- Increased precision using BigDecimal
- Trading phases
- NBBO, order types, cancels and amendments
- FIX protocol
- Crossing and settlement of trades
- More beverages and perhaps some snacks!
