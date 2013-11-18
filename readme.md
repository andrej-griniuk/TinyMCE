# TinyMCE Plugin for CakePHP #

for cake 2.x

The purpose of placing TinyMCE in a plugin is to keep it separate from a themed view, the regular webroot or the app in general, which makes it easier to update and overall follows the idea of keeping the code clean and modular.

## Installation ##

To use TinyMCE you need to clone git repository:

	git clone git://github.com/CakeDC/TinyMCE.git Plugin/TinyMCE

Or if your CakePHP application is setup as a git repository, you can add it as a submodule:

	git submodule add git://github.com/CakeDC/TinyMCE.git Plugin/TinyMCE

Alternatively, you can download an archive from the [2.0 branch on Github](https://github.com/CakeDC/TinyMCE/zipball/2.0) and extract the contents to `Plugin/TinyMCE`.

### Be aware of short tags ###

If your php.ini has short tags enabled you won't be able to load the asset files from the plugin because the js contains a <? which the asset filter will interpret as php but fail to do so and your TinyMCE asset file will not be loaded.

An alternative is to copy or symlink the editor files to your apps webroot. Which is the best way for performance reasons in any case.

## Usage ##

The TinyMCE helper is basically just a convenience helper that allows you to use php and CakePHP conventions to generate the configuration for TinyMCE and as an extra it allows you to load configs.

There two ways you can use this plugin, simply use the helper or load the editor "by hand" using 

```php
$this->Html->script('/TinyMCE/js/tiny_mce/tiny_mce.js', array('inline' => false);
```

and placing your own script in the head of the page. Please note that the helper will auto add the TinyMCE editor script to the header of the page. No need to to that by hand if you use the helper.

If your app is not set up to work in the top level of your host / but instead in /yourapp/ the automatic inclusion of the script wont work. You'll manually have to add the js file to your app:

```php
$this->Html->script('/yourapp/TinyMCE/js/tiny_mce/tiny_mce.js', array('inline' => false);
```

## How to use the helper ##

Wherever you want to use it, load it in the controller

```php
$this->helpers = array('TinyMCE.TinyMCE');
```

In the view simply use the editor() method and pass config key/value pairs in an array.

```php
$this->TinyMCE->editor(array('theme' => 'advanced', 'mode' => 'textareas'));
```

This will instruct TinyMCE to convert all `textarea` elements on the page to TinyMCE editors. If you require some more precise control, or want to change this behavior, checkout the [TinyMCE configuration options](http://www.tinymce.com/wiki.php/Configuration) on the TinyMCE website.

### Multiple configurations

The helper has a configs property which can be filled with data from database or a config file. How you store, get and pass that data to the helper is up to you. The configs property of the helper takes an array with named keys where the keys are used to load the configs.

Here is a basic example of configuration data:

```php
$configs = array(
	'simple' => array(
		'mode' => 'textareas',
		'theme' => 'simple',
		'editor_selector' => 'mceSimple'
	),
	'advanced' => array(
		'mode' => 'textareas',
		'theme' => 'advanced',
		'editor_selector' => 'mceAdvanced'
	)
);

$this->TinyMCE->configs = $configs;
```

You can also put the configuration in APP/config/bootstap.php or another config file and load it. Inside the config file you have you can write the config as above to the TinyMce configuration:

```php
Configure::write('TinyMCE.configs', array(
	'simple' => ...,
	'advanced' => ...));
```

The different sets of configuration data will be auto loaded by the helper inside its constructor. It is suggested that you use this way of passing different configs to the helper because by this you'll be able to store all of them in one place.

When you passed the configuration to the helper you can simply use it by calling the editor() method of the helper with a string that is equal to the key of the configuration in the array:

```php
$this->TinyMCE->editor('simple'); // This matches the 'simple' config name we passed in earlier.
```

### Application wide default options

If you want a quick way to configure default values for all the TinyMCE Editors of an application, you could use the 'TinyMCE.editorOptions' configuration.

Here is an example of a line you could have in `bootstrap.php`:

```php
Configure::write('TinyMCE.editorOptions', array('height' => '300px'))
```

It will make all editors to have a 300px height. You may want to override this value for a single editor. To do so, just pass the option to the editor() method and it will override the default value.

You can always check the tests to see how to use the helper.

## Requirements ##

* PHP version: PHP 5.2+
* CakePHP version: CakePHP 2.0+

## Support ##

For support and feature request, please visit the [TinyMCE Plugin Support Site](https://github.com/CakeDC/TinyMCE).

For more information about our Professional CakePHP Services please visit the [Cake Development Corporation website](http://cakedc.com).

## License ##

Copyright 2009-2011, [Cake Development Corporation](http://cakedc.com)

Licensed under [The GNU Lesser General Public License](http://www.gnu.org/licenses/lgpl.html)<br/>
Redistributions of files must retain the above copyright notice.

## Branch strategy ##

The master branch holds the STABLE latest version of the plugin. 
Develop branch is UNSTABLE and used to test new features before releasing them. 

Previous maintenance versions are named after the CakePHP compatible version, for example, branch 1.3 is the maintenance version compatible with CakePHP 1.3.
All versions are updated with security patches.

## Contributing to this Plugin ##

Please feel free to contribute to the plugin with new issues, requests, unit tests and code fixes or new features. If you want to contribute some code, create a feature branch from develop, and send us your pull request. Unit tests for new features and issues detected are mandatory to keep quality high. 


## Copyright ###

Copyright 2009-2013<br/>
[Cake Development Corporation](http://cakedc.com)<br/>
1785 E. Sahara Avenue, Suite 490-423<br/>
Las Vegas, Nevada 89104<br/>
http://cakedc.com<br/>
