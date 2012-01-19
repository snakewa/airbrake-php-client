Airbrake Notifier Client for PHP
---------------------------------------
This client is intended to be a drop-in library for communicating with the
[Airbrake Notifier API](http://help.airbrake.io/kb/api-2/notifier-api-version-22).
[Airbrake](http://airbrake.io/pages/home) is a service that collects errors generated
by other applications, and aggregates the results for review.

This client is maintained by [Jonathan Azoff](https://github.com/azoff), under the
courtesy of [RentJuice Corp.](http://rentjuice.com).

License and Terms
-----------------
This client is freely distributed under the [DBAD License](http://dbad-license.org/license).
If you use this software, you agree to the terms governed by the license and you do so *AT YOUR OWN RISK*.
RentJuice Corp. is not responsible for usage or other concerns with this library. If you have an issue,
please feel free to use [the official bug tracker](https://github.com/rentjuice/airbrake-php-client/issues).

Dependencies
------------
In order to communicate with the Airbrake servers, the PHP client depends on a couple dependencies to
be installed before running. In no particular order, these dependencies are:
 - [cURL](http://www.php.net/manual/en/book.curl.php), to send HTTP requests to Airbrake
 - [SimpleXML](http://us.php.net/manual/en/book.simplexml.php), to validate and parse XML

Getting Started
---------------
To get started, you must first ensure that the aforementioned dependencies are installed. Afterwards, you
may run the [https://github.com/rentjuice/airbreak-php-client/blob/master/example.php](provided example)
to verify that the dependencies are met and that your Airbrake account is set up correctly. In order to
run the example, you will need to provide your API key; I found mine on the project dashboard:

![Project Dashboard](http://f.cl.ly/items/0M0b3I0r092j2B2A3X1d/Screen%20shot%202012-01-18%20at%204.15.12%20PM.png)

If you are looking to jump right into things and reading code isn't your thing, here is the quick and dirty
version:

```php
// load the client
require('/airbrake.notifier.php');

// instantiate the notifier
$notifier = new AirbrakeNotifier($_YOUR_API_KEY);

// catch an error
try {

    // assuming you have an error...
    doSomethingBad();

} catch(Exception $e) {
    
    // track the error, and get back the Airrake ID for the notice
    $noticeId = $notifier->notifyException($e);

    // you can also be explicit...
    $noticeId = $notifier->notify('Something bad happened', $e->getTrace(), array(
        'some_info' => 'both functions take an optional final parameter',
        'more_info' => 'which can be used to add extra information to the notice!',
        'note' => 'you can find this extra information in the session on Airbrake'
    ));

}
```

Special Thanks
--------------
TODO