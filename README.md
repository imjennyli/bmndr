bmndr
=====

Simple python CLI to [Beeminder](https://www.beeminder.com/) which uses the [Beeminder API](https://www.beeminder.com/api).

Requirements
============

* A [Beeminder](https://www.beeminder.com/users/sign_up) account. Get one, they are free and you won't regret it.

Usage
=====

Usage is simple. First, log into Beeminder, [get an auth token](https://www.beeminder.com/api/v1/auth_token.json), then create a ~/.bmndrrc file with the following contents:

    [account]
    auth_token: <auth_token>

Running the command with no arguments will show you all of your goals in order of how close you are to derailing. Here's an example for [my Beeminder goal](https://www.beeminder.com/bkam/oto) of watching the films in the book [_1001 Films You Must See Before You Die_](http://msls.net/films/):

    $ bmndr
    ...
    oto        14 safe days   Way above the yellow brick road with 14 days of safety buffer
    ...

Get more data on a specific goal by using the slug as an argument. It gives you the headline summary as well as a summary of the graph, plus the URL to the graph, and the last ten datapoints entered.

    $ bmndr oto
    ::: Progress on 1001 Films :::

     Way above the yellow brick road with 14 days of safety buffer 
     618 on 2013.07.17 (3 datapoints in 2 days) targeting 1001 on
    2020.12.01 (2694 more days). Yellow Brick Rd = +1 / week. 

    http://brain.beeminder.com/nonce/bkam+oto+51e59450cc1931715100000c.png

    16 616 "initial datapoint of 616 on the 16th"
    16 1 "Nanook of the North"
    17 1 "Onibaba"

Enter a datapoint by adding further arguments after the slug. The format is the same as beeminder the Beeminder emails except that quotes aren't necessary. The script prints the server's response, pretty-printed.

    $ bmndr oto 1 Out of Africa
    {'canonical': '17 1 "Out of Africa"',
     'comment': 'Out of Africa',
     'id': '51e685eecc193104d800008c',
     'requestid': None,
     'timestamp': 1374076800,
     'updated_at': 1374062062,
     'value': 1.0}

You can also tell Beeminder to refresh a goal by using the following syntax:

    $ bmndr refresh <slug>

Configuration
=============

Currently there are only a few options. `auth_token` is required as described above.

Todo
====

* More configuration.
  * Make the number of goals displayed by default configurable.
* Nicer formatting of the JSON that comes back when you submit data.
* Silent switch for scripts when posting data.
* Verbose switch for summary.
