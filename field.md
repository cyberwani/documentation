Field
=====

Themosis framework comes bundled with APIs to build WordPress custom fields. The framework gives you a list of predefined fields to use in order to customize your content.

The framework handles the display of your custom fields in the WordPress administration.

The `Field` class is an helper class in order to build custom fields in WordPress. It's a generic class that you should use to build any type of custom fields.

This class is used for:

* Adding custom fields to a metabox
* Adding custom fields to an option page
* Adding custom fields to a taxonomy
* More to come (Users, ...)

> **Note:** At the moment, all fields are available for metabox. We're still implementing them to the other categories.

Here is the list of custom fields available:

* Text
* Textarea
* Checkbox
* Checkboxes
* Radio
* Select
* Editor
* Media
* Infinite

### Text field

Build a simple text field: `<input type="text"/>`

```php
Field::text($name, $extras = array());
```

* `$name`: _string_. The field/meta name/key.
* `$extras`: _array_. Extra parameters to add to the field.

Possible values for the `$extras` parameter:

```php
$extras = array(

	'title' 	=> 'The field display title. By default it uses the $name.',
	'info'		=> 'Add a helper text/description to the field.',
	'default' 	=> 'You can define a default value for the field.',
	'class'		=> 'Use to filter the value during sanitization before saving the data - In progress',
	'section'	=> 'Specific to option page. Name of a registered section. Attach the field to the section.'

);
```

### Textarea field

Build a textarea field: `<textarea></textarea>`

```php
Field::textarea($name, $extras = array());
```

* `$name`: _string_. The field name.
* `$extras`: _array_. The extras properties. Check the Text field.

### Checkbox field

Build a **single** checkbox field: `<input type="checkbox"/>`

```php
Field::checkbox($name, $extras = array());
```

* `$name`: _string_. The field name.
* `$extras`: _array_. The extra properties. Check the Text field.

### Checkboxes field

Build a **group** of checkbox fields.

```php
Field::checkboxes($name, $options, $extras = array());
```

* `$name`: _string_. The field name.
* `$options`: _array_. An array of values. It doesn't work with associative array. The value is used as a label.
* `$extras`: _array_. The extra properties. Check the Text field.

### Radio field

Build radio fields: `<input type="radio" />`

```php
Field::radio($name, $options, $extras = array());
```

* `$name`: _string_. The field name.
* `$options`: _array_. An array of values. It doesn't work with associative array. The value is used as a label.
* `$extras`: _array_. The extra properties. Check the Text field.

### Select field

Build select field: `<select></select>`

The select field is highly customizable. You can build simple select tag or with subgroups or/and define if you need multiple selections.

You can also define the value of your option tag to be numeric or custom: `<option value="$key">$value</option>`

```php
Field::select($name, $options, $multiple = false, $extras = array());
```

* `$name`: _string_. The field name.
* `$options`: _array_. The select options values.
* `$multiple`: _boolean_. If select tag use single or multiple value. Default to `false`.
* `$extras`: _array_. The extra properties. Check the Text field.

#### Basic select field

Build a simple select field with **numeric** values:

```php
Field::select('my-field', array(
	'None',
	'Belgium',
	'France',
	'United States'
), false, array('title' => 'Choose a country:'));
```

Build a simple select field with **custom** values:

```php
Field::select('my-field', array(
	
	array(
		'none'	=> 'None',
		'bel' 	=> 'Belgium',
		'fra'	=> 'France',
		'usa'	=> 'United States'
	)

), false, array('title' => 'Choose a country:'));
```

#### Select field with subgroups

Build a select field with subgroup of options using **numeric** values:

```php
Field::select('my-field', array(
	
	'europe' 	=> array(
		'Belgium',
		'France'
	),
	'america'	=> array(
		'United States'
	)

));
```

Build a select field with subgroup of options using **custom** values:

```php
Field::select('my-field', array(
	
	'europe' 	=> array(
		'bel'	=> 'Belgium',
		'fra'	=> 'France'
	),
	'america'	=> array(
		'usa'	=> 'United States'
	)

));
```

#### Select multiple values

Simply set the third parameter `$multiple` to `true`.

### Editor field

Build a WordPress Editor TinyMCE field.

**Note:** This field isn't actually working with the `Infinite` custom field.

```php
Field::editor($name, $settings, $extras);
```

* `$name`: _string_. The field name.
* `$settings`: _array_. An array of parameters of the WordPress editor. Use this [codex guide](https://codex.wordpress.org/Function_Reference/wp_editor) to define your editor **settings**.
* `$extras`: _array_. The extra properties. Check the Text field.

### Media field

Build a media field. This field allows to attach any file stored in the Wordpress Media library.

```php
Field::media($name, $extras);
```

* `$name`: _string_. The field name.
* `$extras`: _array_. The extra properties. Check the Text field.

### Infinite field

Build a repeatable field. This allows to define a single field or a group of fields to be repeated.

```php
Field::infinite($name, $fields, $extras);
```

* `$name`: _string_. The field name.
* `$fields`: _array_. An array of fields to repeat. Use any methods of the `Field` class excepts the `editor` field.
* `$extras`: _array_. The extra properties. Check the Text field.

Example of an infinite field:

```php
Field::infinite('books', array(

	Field::text('title'),
	Field::textarea('excerpt'),
	Field::media('cover-image')

));
```

Next
----
Check those guide to implement your custom fields:

* [Metabox guide](https://github.com/themosis/documentation/blob/master/metabox.md)
* [Page guide](https://github.com/themosis/documentation/blob/master/page.md)