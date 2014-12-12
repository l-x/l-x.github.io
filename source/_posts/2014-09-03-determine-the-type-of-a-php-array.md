---
layout: post
title: "Determine the type of a PHP array"
description: "How to find out, if an array is a list or a dictionary"
comments: true
sharing: true
category: 
    - php
    - snippets
tags: [php,Array]
---

PHP’s arrays are a mix of dictionaries and lists (i. e. in Python). 

Sometimes you have to determine if an array is a [list](http://en.wikipedia.org/wiki/List_%28abstract_data_type%29): 

```php
array('foo', 'bar', 'baz');
```
or a [dictionary](http://en.wikipedia.org/wiki/Associative_array):

```php
array(
	'foo' 	=> 'bar', 
	'herp' 	=> 'derp'
);
```

Unfortunately PHP has no built-in method to do so. One of the good solutions I’ve ran across is to use the  `array_filter()` on the array’s keys to determine if they’re all integers:
<!--more-->

{% codeblock lang:php %}

function is_array_indexed($array) { 
	return count(array_filter(array_keys($array), 'is_int') == count($array); 
}

{% endcodeblock %}

This function simply compares the number of items which keys are integers to the number of all items in the array. If both are equal the array is indexed.

As a variation one could use `is_string()` instead of `is_int()`:

{% codeblock lang:php %}

function is_array_indexed($array) { 
	return count(array_filter(array_keys($array), 'is_string') == 0;
}

{% endcodeblock %}

The advantage of this variant is that no additional count($array) is required, so it should be slightly faster than the first variant.

Both examples can easily be modified to return the type of the array:

{% gist 7765283 %}
