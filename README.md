[![Travis Build Status](https://img.shields.io/travis/digitickets/phpunit-errorhandler.svg?style=for-the-badge&logo=travis)](https://travis-ci.org/digitickets/phpunit-errorhandler)
[![Scrutinizer Build Status](https://img.shields.io/scrutinizer/build/g/digitickets/phpunit-errorhandler.svg?style=for-the-badge&logo=scrutinizer)](https://scrutinizer-ci.com/g/digitickets/phpunit-errorhandler/)
[![Scrutinizer Code Coverage](https://img.shields.io/scrutinizer/coverage/g/digitickets/phpunit-errorhandler.svg?style=for-the-badge&logo=scrutinizer)](https://scrutinizer-ci.com/g/digitickets/phpunit-errorhandler/)
[![GitHub issues](https://img.shields.io/github/issues/digitickets/phpunit-errorhandler.svg?style=for-the-badge&logo=github)](https://github.com/digitickets/phpunit-errorhandler/issues)

[![PHP Version](https://img.shields.io/packagist/php-v/digitickets/phpunit-errorhandler.svg?style=for-the-badge)](https://github.com/digitickets/phpunit-errorhandler)
[![Stable Version](https://img.shields.io/packagist/v/digitickets/phpunit-errorhandler.svg?style=for-the-badge&label=Latest)](https://packagist.org/packages/digitickets/phpunit-errorhandler)

[![Total Packagist Downloads](https://img.shields.io/packagist/dt/digitickets/phpunit-errorhandler.svg?style=for-the-badge&label=Total+downloads)](https://packagist.org/packages/digitickets/phpunit-errorhandler)
[![Monthly Packagist Downloads](https://img.shields.io/packagist/dm/digitickets/phpunit-errorhandler.svg?style=for-the-badge&label=Monthly+downloads)](https://packagist.org/packages/digitickets/phpunit-errorhandler)
[![Daily Packagist Downloads](https://img.shields.io/packagist/dd/digitickets/phpunit-errorhandler.svg?style=for-the-badge&label=Daily+downloads)](https://packagist.org/packages/digitickets/phpunit-errorhandler)


PHPUnit ErrorHandler
====================

An alternative approach to unit testing PHP errors.

Whilst you can use PHPUnit's built-in behaviour of converting all errors, warnings and notices to exceptions,
this package allows you to track all PHP errors, including user generated errors, separately.

The code is supplied as a trait and is based upon [Error Condition Testing with PHPUnit](http://www.sitepoint.com/testing-error-conditions-with-phpunit/)

Here is an example use case:

```php
<?php
use DigiTickets\PHPUnit\ErrorHandler;

class TestErrorHandling extends \PHPUnit\Framework\TestCase
{
    use ErrorHandler;

    public function testSomethingGeneratedAnError()
    {
        // Run something that will produce an error, warning or notice.
        // For example, a E_USER_NOTICE of 'Incompatible type ignored' can be tested as follows:
        $this->assertError('Incompatible type ignored', E_USER_NOTICE);
    }

    public function testSomethingDidNotGenerateAnError()
    {
        // Run something that should not produce an error, warning or notice.
        $this->assertNoErrors();
    }
}
```

Upgrading from V3.0.0 to V4.0.0
===============================

Thanks to [imbrish](https://github.com/digitickets/phpunit-errorhandler/issues/1), the upgrade is extremely simple.

In previous versions, you were required to have the following setup logic. 

    protected function setUp()
    {
        // Set the error handler.
        $this->setUpErrorHandler();
    }

Now you don't. You can remove the `$this->setUpErrorHandler();` call. If you now have an empty `setup()` function,
you can remove that also!

