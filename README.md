Magento-Packager
================

A simple packaging script for magento connect 2.0 based on a composer.json.

The script relies on a working magento setup. It will not work standalone and it is recommend to install ist with
modman.

The script gather all his information from composer.json file. An example is attached below and in the example folder.

Output will be written in `path to magento/var/connect/modulename.tgz`.

Guide to use this script
========================

1.  install the script with modman `modman clone git@github.com:Flagbit/Magento-Packager.git`
2.  go to <path to magento>/shell
3.  run php packager.php --composer <path to your composer.json file>

Guide to create a composer.json
===============================

Example
-------
    {
        "name":"module_vendor/module_name",
        "type":"magento-module",
        "license":"GPL-3.0",
        "description":"",
        "homepage":"http://example.com",
        "authors":[
            {
                "name":"Author 1",
                "email":"author1@example.de"
            },
            {
                "name":"Author 2",
                "email":"author2@example.de"
            }
        ],
        "extra":{
            "magento_connect":{
                "license_uri":"http://www.gnu.org/licenses/gpl-3.0.html",
                "summary":"",
                "channel":"community",
                "php_min":"5.3.0",
                "php_max":"6.0.0",
                "stability":"beta",
                "content":[
                    {
                        "type":"magecommunity",
                        "structure":"dir",
                        "path":"module_vendor/module_name"
                    },
                    {
                        "type":"mageetc",
                        "structure":"file",
                        "path":"modules/module_config_file_name.xml"
                    },
                    {
                        "type":"mage",
                        "structure":"file",
                        "path":"just a random file path"
                    }
                ]
            }
        }
    }


Elements
--------

### name
The name of the module in magento style notation. Something like `flagbit/packager`. It should be writen
everything in lowser first letter case.

### type
If you would like to install extensions via [composer magento installer](https://github.com/magento-hackathon/magento-composer-installer)
you should use `magento-module`. The packager ignore this property.

### license
The name of the license the package is covered by. Will also be used as a key from [http://www.spdx.org/licenses/], if an explicit URI is not provided in the `magento_connect` options.

### description
A detailed description of you module. It will be used as description and the summary, if an explicit summary is not provided in the `magento_connect` options.

### homepage
Nothing more to say

### authors
Who developed the module

### magento_connect name [optional]
The package name, usually NameSpace_ModuleName. Must be identical to the Module Name. Use this if automatic generation fails because you have uppercase letters in the middle of the Namespace and/or Module Name.

### magento_connect license_uri
URI for a copy of the license text. If no value is provided the URI will default to using the value of `license` as a key from [http://www.spdx.org/licenses/].

### magento_connect summary
A brief summary of your module. If no value is provided then the `description` will be used.

### magento_connect channel
Which channel should be used in magento connect.

### magento_connect php_min
The minimum required version for PHP

### magento_connect php_max
The maximum support version of PHP

### magento_connect stability
Please use some key from [http://getcomposer.org/doc/04-schema.md#minimum-stability]

### magento_connect content
Most complicated part of the config file. You need to tell the packager which files you want to put where in the archive.
It is very similar to modman but you need to tell magento the type, if it is a file or directory and the path of the source.

`type` can be one of the following:

	<targets>
		<target name="magelocal" label="Magento Local module file" uri="./app/code/local" />
		<target name="magecommunity" label="Magento Community module file" uri="./app/code/community" />
		<target name="magecore" label="Magento Core team module file" uri="./app/code/core" />
		<target name="magedesign" label="Magento User Interface (layouts, templates)" uri="./app/design" />
		<target name="mageetc" label="Magento Global Configuration" uri="./app/etc" />
		<target name="magelib" label="Magento PHP Library file" uri="./lib" />
		<target name="magelocale" label="Magento Locale language file" uri="./app/locale" />
		<target name="magemedia" label="Magento Media library" uri="./media" />
		<target name="mageskin" label="Magento Theme Skin (Images, CSS, JS)" uri="./skin" />
		<target name="mageweb" label="Magento Other web accessible file" uri="." />
		<target name="magetest" label="Magento PHPUnit test" uri="./tests" />
		<target name="mage" label="Magento other" uri="." />
	</targets>

`structure` can be file or dir


`path` is the path to your source files.

History
=======
This script was developed first within [https://github.com/Flagbit/Magento-FilterUrls].
