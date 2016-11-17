[![Scrutinizer Code Quality](https://img.shields.io/scrutinizer/g/digitickets/phpunit-errorhandler.svg?style=plastic)](https://scrutinizer-ci.com/g/digitickets/phpunit-errorhandler/?branch=master)
[![Scrutinizer Coverage](https://img.shields.io/scrutinizer/coverage/g/digitickets/phpunit-errorhandler.svg?style=plastic)](https://scrutinizer-ci.com/coverage/g/digitickets/phpunit-errorhandler/?branch=master)
[![Scrutinizer Build Status](https://img.shields.io/scrutinizer/build/g/digitickets/phpunit-errorhandler.svg?style=plastic)](https://scrutinizer-ci.com/build/g/digitickets/phpunit-errorhandler/?branch=master)
[![Travid Build Status](https://img.shields.io/travis/digitickets/phpunit-errorhandler.svg?style=plastic)](https://travis-ci.org/digitickets/phpunit-errorhandler)
[![Latest Stable Version](https://img.shields.io/packagist/v/digitickets/phpunit-errorhandler.svg?style=plastic)](https://packagist.org/packages/digitickets/phpunit-errorhandler)
[![Packagist](https://img.shields.io/packagist/dt/digitickets/phpunit-errorhandler.svg?style=plastic)](https://packagist.org/packages/digitickets/phpunit-errorhandler)

Richard Quadling's PHPUnit ErrorHandler
=======================================

An alternative approach to unit testing PHP errors.

Whilst you can use PHPUnit's built-in behaviour of converting all errors, warnings and notices to exceptions,
this package allows you to track all PHP errors, including user generated errors, separately.

The code is supplied as a trait and is based upon [Error Condition Testing with PHPUnit](http://www.sitepoint.com/testing-error-conditions-with-phpunit/)

Here is an example use case:

```php
<?php
use DigiTickets\PHPUnit\ErrorHandler;

class tests extends \PHPUnit_Framework_TestCase
{
    use ErrorHandler;

    protected function setUp()
    {
        // Set the error handler.
        $this->setUpErrorHandler();
    }

    public function testSomething()
    {
        // Run something that will produce an error, warning or notice.
        // For example, a E_USER_NOTICE of 'Incompatible type ignored' can be tested as follows:
        $this->assertError('Incompatible type ignored', E_USER_NOTICE);
    }
}
```
