# Article.EikonAPI.RDP.Python.OptionStrategyBacktesting

## Overview

This article explores how short iron condor strategies can be backtested. The important part of this article is the reconstruction of expired options, which used to be a challenge reported many times in the Developer community Q&A forum. The challenge is that one cannot directly access expired options through a single API call. To get historical data on options, one will need to reconstruct options Refinitiv Identification Codes (RIC) following the logic of RIC construction rules and the rules specified by the exchange where the option is traded. Further, in this article, RIC reconstruction and validation functions are presented; they can be used for options on OPRA exchange-traded indices and stocks. Functions reconstruct and validate AM settlement options expiring on the 3rd Friday of each month.

In this article, we test and visualize the profit/loss of the short Iron Condor strategy with 10% and 20% Out of Money (OTM) sizes for NDX; however one can use the functions and codes of this article to backtest other OPRA exchange-traded indices (such as SPX) and equities (such as IBM, TWTR) at the same time specifying OTM sizes other than 10/20%. It should be noted that options with different underlying assets have different liquidity, and one may not get data for specific OTM ranges for some underlying assets. The current backtesting model is not at the production level and is not tested on a wide range of underlying assets. Except for NDX, we tested the functions on SPX, IBM, TWTR and AAPL, which produced the required results to be used for backtesting of options on these assets. Additionally, we considered also the impact of stock split event on the underlying price and strike price, and adjusted the prices accordingly. The impact of other corporate events, such as stock dividends, right offering, M&A is not considerd and tested in the scope of this article.

The article follows the following structure. In Section 1, we build and present a function for expired option RIC reconstruction and validation. Section 2 introduces functions to conduct option transactions to build iron condor legs and report the strategy outcome. Also, we use a function to offset the transactions before expiration based on VIX movements. Finally, Section 3 implements a short iron condor strategy on NDX and visualizes the backtesting results.
