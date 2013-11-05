5: Working with entities
========================

We will expect following model:
```php
/**
 * @property string $summary
 * @property string $isbn
 * @property DateTime $datePublished {default now}
 */
class Book extends Orm\Entity {}

/**
 * @mapper Orm\DibiMapper
 */
class BooksRepository extends Orm\Repository {}
```

Creating new entity
-------------------

```php
$book = new Book;
$book->summary = 'Ender Wiggin, the third in a family of...';
$book->isbn = '0812550706';
```

The entity is not yet registered anywhere and is not persisted. First, we need to "put it in" the repository, *attach* it.
```php
$repository = $orm->getRepository('BooksRepository');
$repository->attach($book);
```
Now, the entity is tracked in repository but is not yet persisted, meaning it only lives in the current request, until we persist it. We will cover different aspects of persistence in the next chapter. For now, we can persist the entity with calling `flush`:
```
$orm->flush();
```

There is also another way to create an entity. Let's assume the following definitions:
```php
/**
 * @property Orm\ManyToMany $genres {m:n GenresRepository books}
 */
class Book extends Orm\Entity {}

/**
 * @property name
 * @property Orm\ManyToMany $books {m:n BooksRepository genres map}
 */
class Genre extends Orm\Entity {}
```

`Orm\OneToMany` and `Orm\ManyToMany` classes can create new entities directly by values. The following snippet creates two new entities of class `Genre`: one with name 'Sci-Fi' and the other one named 'Fantasy'.
```php
$book->genres->add(array('name' => 'Sci-Fi'));
$book->genres->set(array(
	array('name' => 'Fantasy')
));
```

Loading entity
--------------

* from repository
* from parent entity
* limit, order, offset, pagination (?), ...
* custom repo methods? (`findByEvenId()`, `findAllOrderedByCity()`, ...)

Updating entity
---------------

Removing entity
---------------

* `$entity->delete()`
* `$entity->{1:m}->delete()`, nebo `set([])` nebo jak to je
