# Utils Plugin for CakePHP #

for cake 2.x

The utils plugin contain a lot of reusable components, behaviors and helpers. Here we will list and detail 
each component.

## Behaviors 

* Btree          - 
* CsvImport      - adds the ability to import csv data to the model.
* Inheritable    - 
* Keyvalue       - allows to get and save group of settings in key/value representation.
* List           - provide a way to make collection ordered
* Lookupable     - looks up associated records up based on a given field and its value
* Pingbackable   - 
* Publishable    - 
* Serializable   - allows serialize/deserialize array data into large text field.
* Sluggable      - implement slugs for model.
* StateMachine - implements simple state machine no top of model with flexible configuration.
* SoftDelete     - soft deleting for model.
* TinySluggable  - creates tiny slugs similar to known url shorteners like bit.ly
* Toggleable     - toggle field values

## Libraries

* Languages      - List of languages that can be used in selects

## Components

* Archive        - Creates the data for "archive" date ranges that can be used to generated links like "May 2010", "March 2010",...
* FormPreserver  - Allow to keep form data between login redirect and returning back after login.
* Pingbacks      - 
* Referer        - Allow to keep referer url inside the add/edit form to reuse it for redirect on success POST or submit.
* Utils          - 

## Helpers

* Cleaner        - Allow to strip tags from input markup
* Gravatar       - Gravatar Helper
* Tree           - 

### CsvImport Behavior

You can configure the Importable behavior using these options:

* delimiter      - The delimiter for the values, default is ;
* enclosure      - The enclosure, default is "
* hasHeader      - Parse the header of the CSV file if it has one, default is true

The main method of this behavior is

	$this->Model->importCSV('myFile.csv');

It will read the csv file and try to save the records to the model. In the case of errors you'll get them by calling

	$this->Model->getImportErrors();

### Keyvalue Behavior

You can configure the Importable behavior using these options:

* foreignKey     - The foreign key field, default is user_id
* scope          - Find condition like array to define a scope

### List Behavior 

The list behavior allows you to have records act like a list, for example a tracklist and to move records in this list.

* positionColumn - The column in the table used to store the positiot, default is 'position'.
* scope          - Find condition like array to define a scope, default is empty string ''.
* validate       - validate the data when the behavior is saving the changes, default is false.
* callbacks      - use callbacks when the behavior saves the data, default is false.

### StateMachine

#### Behavior Configuration
	
* initial - string literal, declare initial state
* column - string literal, describe column name storing current state
* states - array, describing list of states, with action to trigger on diferent events.
	Keys of this array are event names, and values is array with methods to trigger on three operation:
	 * exit - called when we leave state 
	 * enter - called before we entering new state 
	 * after - called after we enter new state 

		'states' => array(
			'in' => array('exit' => 'exitTest'),
			'ready' => array('after'=>'afterTest', 'enter'=>'enterTest'),
			'out' => array()),
	 
	 
* events - array, list of transitions between states.
	Keys of this array are event names. Transition has inside 'from' and 'to' keys, that contain set of states allowed for this transition.
	

			'events' => array(
				'prepare' => array(
					'transitions' => array(
						'to'=>'ready',
						'from'=>array('in', 'out'))),
				'close' => array(
					'transitions' => array (
  						'to'=>'out',
						'from'=>array('ready', 'in'))),
	
	
To trigger transition behavior provide two ways. First is calling Model::fire with event name. Second call magic method Model::setState{$CamelizedEventName}. Both methods change event state only if this transition is allowed.

	
## Languages Lib

The languages lib is basically just a helper lib that extends I10n to get a three character language code => country name array.

	App::import('Lib', 'Utils.Languages');
	$Languages = new Languages();
	$languageList = $Languages->lists();

`$languageList` will contain the three character code mapped to a country. This list can be used in language selects for example.

## Archive Component

## Referer Component

Allow to keep referer url inside the add/edit form to reuse it for redirect on success POST or submit.

## Requirements ##

* PHP version: PHP 5.2+
* CakePHP version: 1.3 Stable

## Support ##

For support and feature request, please visit the [Utils Plugin Support Site](http://cakedc.lighthouseapp.com/projects/59607-utils-plugin/).

For more information about our Professional CakePHP Services please visit the [Cake Development Corporation website](http://cakedc.com).

## Branch strategy ##

The master branch holds the STABLE latest version of the plugin. 
Develop branch is UNSTABLE and used to test new features before releasing them. 

Previous maintenance versions are named after the CakePHP compatible version, for example, branch 1.3 is the maintenance version compatible with CakePHP 1.3.
All versions are updated with security patches.

## Contributing to this Plugin ##

Please feel free to contribute to the plugin with new issues, requests, unit tests and code fixes or new features. If you want to contribute some code, create a feature branch from develop, and send us your pull request. Unit tests for new features and issues detected are mandatory to keep quality high. 

## License ##

Copyright 2009-2012, [Cake Development Corporation](http://cakedc.com)

Licensed under [The MIT License](http://www.opensource.org/licenses/mit-license.php)<br/>
Redistributions of files must retain the above copyright notice.

## Copyright ###

Copyright 2009-2012<br/>
[Cake Development Corporation](http://cakedc.com)<br/>
1785 E. Sahara Avenue, Suite 490-423<br/>
Las Vegas, Nevada 89104<br/>
http://cakedc.com<br/>
