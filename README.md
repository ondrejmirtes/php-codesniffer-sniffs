Moxio PHP_CodeSniffer sniffs
=============================
This is a collection of our custom PHP_Codesniffer (3.x) sniffs for detecting potential bugs 
and unexpected behavior in PHP code. It may be used as a ruleset on its own, but it is mainly
intended as a set of separate sniffs that can be integrated into other standards.

We described the motivation behind some of these sniffs [on our blog](https://www.moxio.com/blog/10/detecting-hidden-bugs-in-php-code-using-php-codesniffer).

Installation and usage
----------------------
Install as a development dependency using composer:
```
$ composer require --dev moxio/php-codesniffer-sniffs
```
Check your files against this set of sniffs:
```
$ ./vendor/bin/phpcs --standard=vendor/moxio/php-codesniffer-sniffs/Moxio path/to/your/files
```

Description of sniffs
---------------------
_More sniffs will be added soon._

**Moxio.PHP.DisallowBareContinueInSwitch**: Disallows the `continue` statement without a numeric
argument when used directly within a `switch`-`case`. This prevents silent bugs caused by PHP 
considering `switch` [to be a looping structure](http://php.net/manual/en/control-structures.switch.php).

**Moxio.PHP.DisallowImplicitLooseComparison**: Disallows implicit non-strict comparisons by functions
like `in_array` and `array_search`. Requires that the `$strict`-parameter to these functions is
explicitly set. This prevents hidden bugs due to [counter-intuitive behavior of non-strict 
comparison](https://twitter.com/fabpot/status/460707769990266880).

**Moxio.PHP.DisallowUniqidWithoutMoreEntropy**: Disallows calls to `uniqid()` without `$more_entropy = 
true`.  When `$more_entropy` is `false` (which is the default), `uniqid()` calls `usleep()` to avoid 
collisions, which [can be a substantial performance hit](http://blog.kevingomez.fr/til/2015/07/26/why-is-uniqid-slow/).
Always calling `uniqid()` with `$more_entropy = true` avoids these problems.

License
-------
These sniffs are released under the MIT license.
