4: Relationships
================

http://orm.petrprochazka.com/forum/topic/9/vazby-orm/

One to many `1:m`
-----------------

Entity has relation to multiple other entities of same parent. With the `Book` entity we defined in 3-Example-model.md, we could assign multiple authors to each book (author, illustrator, editor, ...).

```php
/**
 * ...
 * @property Orm\OneToMany $authors {1:m AuthorsRepository book}
 */
class Book extends Orm\Entity {}
```

As with all phpdoc property annotations, the first part denotes class (or scalar type) returned, `Orm\OneToMany` in this case. Orm annotations in curly brackets `1:m` _______, `AuthorsRepository` tells Orm which repository _______

Corresponding `m:1`
-------------------

`1:1`
-----

`m:m` (many to many)
--------------------
