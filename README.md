# CakePHP Tools Plugin

[![Build Status](https://api.travis-ci.org/dereuromark/cakephp-tools.png?branch=master)](https://travis-ci.org/dereuromark/cakephp-tools)
[![Latest Stable Version](https://poser.pugx.org/dereuromark/cakephp-tools/v/stable.png)](https://packagist.org/packages/dereuromark/cakephp-tools)
[![Coverage Status](https://coveralls.io/repos/dereuromark/cakephp-tools/badge.png)](https://coveralls.io/r/dereuromark/cakephp-tools)
[![License](https://poser.pugx.org/dereuromark/cakephp-tools/license.png)](https://packagist.org/packages/dereuromark/cakephp-tools)
[![Total Downloads](https://poser.pugx.org/dereuromark/cakephp-tools/d/total.png)](https://packagist.org/packages/dereuromark/cakephp-tools)

A CakePHP 2.x Plugin containing several useful tools that can be used in many projects.
This plugin requires PHP5.3+

Please note: New functionality has been tested against 2.x (current master and dev) only. Please upgrade if possible.

## How to include
Installing the Plugin is pretty much as with every other CakePHP Plugin.

* Put the files in `APP/Plugin/Tools`
* Make sure you have `CakePlugin::load('Tools')` or `CakePlugin::loadAll()` in your bootstrap

Tip: You can also use packagist now @ https://packagist.org/packages/dereuromark/cakephp-tools

```
"require": {
	"dereuromark/cakephp-tools": "dev-master"
}
```
or use the tags, e.g. `0.4` directly.

That's it. It should be up and running.

## The basics

In case you want the Tools bootstrap file included (recommended), you can do that in your `APP/Config/bootstrap.php` with

```php
CakePlugin::load('Tools', array('bootstrap' => true));
```

For `CakePlugin::loadAll()` it's

```php
CakePlugin::loadAll(array(
		'Tools' => array('bootstrap' => true)
));
```



MyModel can be extended to use more powerful validation and other improvements:

```php
App::uses('MyModel', 'Tools.Model');

class AppModel extends MyModel {
}
```

MyController can be extended for DRY improvements and to fix some common bugs:

```php
App::uses('MyController', 'Tools.Controller');

class MyController extends MyController {
}
```

MyHelper can be extended and used this way:

```php
App::uses('MyHelper', 'Tools.View/Helper');

class AppHelper extends MyHelper {
}
```

The test suite improvements can be used via:

```php
App::uses('MyCakeTestCase', 'Tools.TestSuite');

class SomeClassTest extends MyCakeTestCase {
}
```

To run any of the console commands (replace [ShellName] and [command]!):

    cake Tools.[ShellName] [command]

The models, behaviors, helpers, libs and other classes are used the same way prefixing them with the plugin name:

```php
App::uses('GooglLib', 'Tools.Lib');
App::uses('TimeLib', 'Tools.Utility');
App::uses('GeocoderBehavior', 'Tools.Model/Behavior');
...
```

Tip: For how to use them, try to find some information in the test cases.
For a quick reference or some larger modules see the [Tools Plugin Wiki](https://github.com/dereuromark/cakephp-tools/wiki)

For including components, helper and behaviors you don't need App::uses() calls.
So for a pretty standard CakePHP app with some Tools plugin enhancements, the AppController could look like this:
```php
public $components = array(
	'Session', 'RequestHandler', 'Tools.Common', 'Auth');

public $helpers = array(
	'Session', 'Html', 'Form' => array('className' => 'Tools.FormExt'),
	'Tools.Common', 'Tools.Format', 'Tools.Datetime', 'Tools.Numeric');
```

## The cool stuff

### Useful fixes

* Auto-trim on POST (to make - not only notEmpty - validation working properly).
* Auto-aliasing for models' "order" properties.
* Disable cache also works for older IE versions.
* Default settings for Paginator, ... can be set using Configure.
* RSS and Ajax Views for better responses (Ajax also comes with an optional component).
* testAction() defaults to GET

A full list of fixes and useful migration tweaks towards the next major version see [here](https://github.com/dereuromark/cakephp-tools/wiki/Included-fixes-and-migration-tweaks).

### Additional classes and features

* Using the Common component's flashMessage() you can have colorful (success, warning, error, ...) flash messages.
  They also can stack up (multiple messages per type). This way no message is lost when redirecting twice etc.
  You will also need `echo $this->Common->flash();` then instead of the default flash code in your layout.ctp template.
  And bear in mind that it will eat all your normal flash messages and outputs it though the same method.
* TinyAuth authorization adapter with single and multi-role support - extremely fast and easy to use.
* The Passwordable behavior allows easy to use functionality for frontend and backend.
* Geocodeable, WhoDidIt, Confirmable and Bitmasked behaviors.
* With MyModel you can build subqueries the Cake way.
* Tokens, Qlogin, TinyUrl, KeyValue functionality included.
* DiffLib, ZipLib, WeatherLib and many more lib functionality.
* The TextExt, Datetime, Numeric helpers etc provide extended functionality if desired.
* FormExt and HtmlExt helpers also provide extended functionality and 3.x shims.
* Tree helper for working with (complex) trees.
* EmailLib as a wrapper for CakeEmail adding some more usefulness and making debugging/testing easier.
* GoogleMapV3, Gravatar, Qrcode, Timeline, Typography, Ical, Hcard provide additional helper functionality.
* NEW: Backported StringTemplate class (from CakePHP3.0) can be used to use template based rendering of HTML tags.
* NEW: Backported password_hash() functionality via Tools.Modern PasswordHasher and Passwordable out of the box.

and much more


## Disclaimer
Use at your own risk. Please provide any fixes or enhancements via issue or better pull request.
Some classes are still from 1.2 (and are merely upgraded to 2.x) and might still need some serious refactoring.
If you are able to help on that one, that would be awesome.

### Branching strategy
The master branch is the currently active and maintained one and works with the current 2.x stable version.
Older versions might be found in their respective branches (1.3, 2.0, 2.3, ...).
Please provide PRs mainly against master branch then.

For details on how to contribute please read the [CONTRIBUTING page](CONTRIBUTING.md).

### TODOs

* Better test coverage (once it's >= 75% I will declare the plugin stable)
* Use [Transifex plugin](https://github.com/dereuromark/cakephp-transifex) and [transifex.com](https://www.transifex.com/projects/p/tools/resources/) (you need to have a login) for translations

### Recent changes (possibly BC breaking)

* 2014-01 Changed Garbige to Garbage in method names.
* 2014-02 Qlogin now uses Token model instead of deprecated CodeKey per default.
* 2014-07 Packagist package name has been renamed to "cakephp-tools".
* 2014-11 All translations now use the `tools` domain; development messages are not translated anymore