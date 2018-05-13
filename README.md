| Branch                                                                                      | Build                                                                                                                        | Coverage                                                                                                                                                             | Documentation                                                                                                                                   | Project Health                                                                                                                                              |
|---------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `master` (stable)                                                                           | [![Build Status](https://travis-ci.org/Crypto-toolbox/bitex.svg?branch=master)](https://travis-ci.org/Crypto-toolbox/bitex)  | [![Coverage Status](https://coveralls.io/repos/github/Crypto-toolbox/bitex/badge.svg?branch=master)](https://coveralls.io/github/Crypto-toolbox/bitex?branch=master) | [![Documentation Status](https://readthedocs.org/projects/bitex/badge/?version=master)](http://bitex.readthedocs.io/en/latest/?badge=master)    | [![Code Health](https://landscape.io/github/Crypto-toolbox/bitex/master/landscape.svg?style=flat)](https://landscape.io/github/Crypto-toolbox/bitex/master) |
| `dev` [![PyPI version](https://badge.fury.io/py/BitEx.svg)](https://badge.fury.io/py/BitEx) | [![Build Status](https://travis-ci.org/Crypto-toolbox/bitex.svg?branch=dev)](https://travis-ci.org/Crypto-toolbox/bitex)     | [![Coverage Status](https://coveralls.io/repos/github/Crypto-toolbox/bitex/badge.svg?branch=dev)](https://coveralls.io/github/Crypto-toolbox/bitex?branch=dev)       | [![Documentation Status](https://readthedocs.org/projects/bitex/badge/?version=dev)](http://bitex.readthedocs.io/en/dev/?badge=dev)             |  [![Code Health](https://landscape.io/github/Crypto-toolbox/bitex/dev/landscape.svg?style=flat)](https://landscape.io/github/Crypto-toolbox/bitex/dev)      |
| `nightly`                                                                                   | [![Build Status](https://travis-ci.org/Crypto-toolbox/bitex.svg?branch=nightly)](https://travis-ci.org/Crypto-toolbox/bitex) | [![Coverage Status](https://coveralls.io/repos/github/Crypto-toolbox/bitex/badge.svg?branch=dev)](https://coveralls.io/github/Crypto-toolbox/bitex?branch=dev)       | [![Documentation Status](https://readthedocs.org/projects/bitex/badge/?version=nightly)](http://bitex.readthedocs.io/en/nightly/?badge=nightly) |  [![Code Health](https://landscape.io/github/Crypto-toolbox/bitex/dev/landscape.svg?style=flat)](https://landscape.io/github/Crypto-toolbox/bitex/dev)      |

# BitEx
BitEx is a collection of API Clients for Crypto Currency Exchanges.

It comes with two core components - `bitex.api` represents the base level API
interfaces, on top of which the second part - `bitex.interfaces` - builds upon.
`bitex.api` classes can be used without making use of the interface classes.

Donations welcome!
BTC @ 3D4yuyf84eQUauyZLoQKyouPuThoxMMRZa

# BitEx's philosophy

BitEx is a `REST API wrapper`, sprinkled with (partly optional) syntactic sugar. It returns `requests.Response`-like objects and offers parameterized API Methods for interaction between your bots and the exchange servers.

It does not offer rate-limiting or HTTP status handling. From experience, we know how these may interfere with trading strategies in unexpected and unwanted ways.


# State

**RESTAPI** : **Completed**

**Interfaces** : **WIP**



# Supported Exchanges

| Exchange             | REST  API | Authentication | Public Interface<sup>1</sup> | Private Interface<sup>1</sup> | Tests             |
|----------------------|-----------|----------------|------------------|-------------------|-------------------|
| Bitfinex             | DONE      | DONE           | DONE             | DONE              | DONE              |
| Bitstamp             | DONE      | DONE           | DONE             | DONE              | DONE              |
| Bittrex              | DONE      | DONE           | DONE             | DONE              | DONE              |
| Bter                 | DONE      | DONE           | DONE             | DONE              | DONE              |
| C-CEX                | DONE      | DONE           | DONE             | DONE              | DONE              |
| CoinCheck            | DONE      | DONE           | DONE             | DONE              | DONE              |
| Cryptopia            | DONE      | DONE           | DONE             | DONE              | DONE              |
| HitBTC               | DONE      | DONE           | DONE             | DONE              | DONE              |
| Kraken               | DONE      | DONE           | DONE             | DONE              | DONE              |
| OKCoin               | DONE      | DONE           | DONE             | DONE              | DONE              |
| Poloniex             | DONE      | DONE           | DONE             | DONE              | DONE              |
| QuadrigaCX           | DONE      | DONE           | DONE             | DONE              | DONE              |
| The Rock Trading LTD | DONE      | DONE           | DONE             | DONE              | DONE              |
| Vaultoro             | DONE      | DONE           | DONE             | DONE              | DONE              |
| Quoine               | Planned   | Planned        | Planned          | Planned           | DONE              |
| ITBit                | Planned   | Planned        | Planned          | Planned           | DONE              |


Additional clients will be added to (or removed from) this list,
according to their liquidity and market volume.

(<sup>1</sup>): This table considers standardized methods only, when describing the state.
See section `Standardized Methods` for more information on these.


# Standardized Methods

As explained in the previous section, __standardized methods__ refer to the methods of each interface
which have been deemed as part of the set of minimal methods and functions required to trade
at an exchange via its API.

The Methods are:

| Method           | Required Parameters | Requires Authentication? | Function                                                                                        |
|------------------|---------------------|--------------------------|-------------------------------------------------------------------------------------------------|
| ticker()         | pair                | No                       | Returns a specified pair's 'ticker' data from the exchange API.                                 |
| order_book       | pair                | No                       | Returns a specified pair's `order book` data from the exchange API.                             |
| `trades()`       | pair                | No                       | Returns a specified pair's `trades` data from the exchange API                                  |
| `ask()`          | pair, price, size   | Yes                      | Places an `ask` order of type `limit` via the exchange API.                                     |
| `bid()`          | pair, price, size   | Yes                      | Places an `bid` order of type `limit` via the exchange API.                                     |
| `order_status()` | order_id            | Yes                      | Requests the status of the given `order id` via the exchange API.                               |
| `open_orders()`  | -                   | Yes                      | Requests all `open orders` via the exchange API.                                                |
| `cancel_order()` | *order_ids          | Yes                      | Cancels one or more `orders` by their given `order id` via the exchange API.                    |
| `wallet()`       | -                   | Yes                      | Requests the current balances of the account associated with the API keys via the exchange API. |

All standardized methods require also `*args` and `**kwargs` (even if they are not used).


# Standardized Pairs

`Bitex` comes with a `PairFormatter()` class, which formats a given symbol
pair into a format which is recognized by the exchange you're querying;
moreover many common pairs are already available (see below ).

This allows you to specify a pair once, without having to worry about
whether or not you typed it correctly for each individual exchange.

An example:

The Pair `ETH/BTC` is denoted as follows:
 - At Kraken it goes by XETHXXBT
 - At Poloniex it goes by BTC_ETH
 - At Bittrex it goes by BTC-ETH
 - at OKCoin it goes by btc_eth

Instead of passing a string to the standardized methods, then, you may
pass a `PairFormatter()` object instead.
It automatically formats the pair accordingly when a standardized method
is invoked.

You can create a custom `PairFormatter()` easily. Let's consider a common
use case, when we want to query the price for Bitcoin against US Dollar.

```
from bitex.pairs import PairFormatter

class BTCUSD(PairFormatter):
    def __init__(self):
        super(self.__class__, self).__init__(base='BTC', quote='USD')

btcusd = BTCUSD()
```

And that's all you need to do! Whenever you pass this to a standardized
method, the method will call the `PairFormatter()`'s `format_for()` method,
and let it take care of the formatting:

```
>>> btcusd.format_for("Bitstamp")
'btcusd'
>>> btcusd.format_for("Kraken")
'XXBTZUSD'
```

If we now want to query the rate on, e.g., Bitstamp:

```
>>> from bitex import Bitstamp
>>> resp = Bitstamp().ticker(btcusd)
>>> resp.json()
{'high': '19666.00', 'last': '19663.94', 'timestamp': '1513513571', 'bid': '19647.18', 'vwap': '18920.32', 'volume': '9999.47455152', 'low': '17906.01', 'ask': '19663.93', 'open': '19187.78'}
```

## Common standardized pairs

Note that many common pairs (such as the `BTC/USD` pair implemented above) are
already implemented and are available inside the main `bitex` module and can
be passed to any method requiring a pair object, e.g.:

```
>>> from bitex import Bitfinex, ETHUSD
>>> Bitfinex().ticker(ETHUSD)
```

For a complete list of the pairs already implemented, refer to the [relative documentation](http://bitex.readthedocs.io/en/release-2.0.0/reference.html#module-bitex.pairs).

# Installation

Manually, using the supplied `setup.py` file:

`python3 setup.py install`

or via pip

`pip install BitEx`

# Further documentation

Further documentation can be found [here](http://bitex.readthedocs.io/en/release-2.0.0/).

# Disclaimer

Due to technical reasons I cannot test all private methods of each exchange,
since some of them need me to move actual currency - exposing an API Key of an account with
actual value is, as you may imagine, a security risk and thus isn't done.

Therefore, take great care when using the library. I cannot be
held responsible for any losses or damages you suffer while using BitEx.
