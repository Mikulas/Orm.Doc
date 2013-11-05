6: Default values
========================

Generally, default values can be set with annotations or `getDefault___()` method.

```php
/**
 * @property $foo {default abc}
 */
class Book extends Orm\Entity {}
```

or equivalently:

```php
/**
 * @property $foo
 */
class Book extends Orm\Entity
{
	protected function getDefaultFoo()
	{
		return 'abc';
	}
}
```

If annotation sets default value and `getDefault` method for the same property also exists, annotation takes priority.

Value can be set to anything that would work as setter argument.
```php
/**
 * @property string $neco {default abc} string
 * @property string $neco {default "abc"} equivalent string
 * @property string $neco {default ""} empty string
 * @property double $neco {default 123.52} number
 * @property bool $neco {default TRUE} constant
 * @property string $neco {default self::FOO} constant
 *
 * @property DateTime $registered {default now}
 */
```

Property can be set back to it's default value by assigning `Orm\IEntity::DEFAULT_VALUE` to it:
```php
$entity->foo = Orm\IEntity::DEFAULT_VALUE;
```

Setting default value to empty array can (for now) only be done with `getDefault` method:
```php
protected function getDefaultFoo()
{
	return array();
}
```

Multiple Orm annotations
------------------------

Default values can also be set for properties with other existing Orm annotations, such as relationships or enumeration. Expected syntax is as follows:
```php
/*
 * @property Region $region {m:1 RegionsRepository $author} {default self::DEFAULT_REGION}
 */
class Person extends Orm\Entity
{
	const DEFAULT_REGION = 1;
}
```

This example sets default region to 1 for `Person` entities.
