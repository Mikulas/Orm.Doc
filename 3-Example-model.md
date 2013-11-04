3: Example model
================

In this example, we will be creating a simple library. Let's start with model of one Book.

Entity
------

Instances of entity class will be individual books. Each book has multiple scalar properties: text value (abstract), date published and isbn code. In Orm, Entity properties are most ofen specified with `@property` [phpdoc] annotations:

Conventionally, entities are named in singular (because one instance is *one entity*).

```php
/**
 * @property string $abstract
 * @property string $isbn
 * @property DateTime $datePublished
 */
class Book extends Orm\Entity
{

}
```

We don't need to specify property `$id` as it's already defined in `Orm\Entity` ([source: Entity]). (Also note it's not defined with `@property` annotation but rather `@property-read` which although being self-explanatory will be fully covered later on in this documentation.)
)

Repository
----------

Delegates loading, saving, updating and deleting entities to mapper, independently of the specific storage. Each entity definition (or group of related entities) is expected to have it's own repository.

Because repository wraps all entities, it's conventionally named as plural of the entity name (as it's *group of entities*).

```php
class BooksRepository extends Orm\Repository
{

}
```

Mapper
------
Most commonly, you will presumably persist entities into database. For that, Orm has fully featured `Orm\DibiMapper` ([api: DibiMapper]), built upon [dibi], which supports MySQL, PostgreSQL, SQLite, MS SQL, Oracle, Access and generic PDO and ODBC.

By default, this mapper uses conventional naming ([api: SqlConventional]). It expects primary key on column `id` and converts camelCase properties into underscore notation (i.e. `datePublished` to `date_published`). Besides other things, it also specifies table names, which default to repository name (`books` in this case). Note that you might modify any or all parts of this convention to suit your coding style.

As with repository, mapper is also named as plural of the entity name.

```php
class BooksMapper extends Orm\DibiMapper
{

}
```

or if we don't plan on extending the mapper, we could specify mapper on the `BooksRepository`, without creating the `BooksMapper` class explicitly:
```
/**
 * @mapper Orm\DibiMapper
 */
 class BooksRepository extends Orm\Repository
```

With the `Book` entity specified above, conventional mapper would expect table such as:
```sql
CREATE TABLE `books` (
	`id` bigint unsigned NOT NULL AUTO_INCREMENT PRIMARY KEY,
	`abstract` text NOT NULL,
	`isbn` varchar(80) NOT NULL,
	`date_published` date NOT NULL
);
```
Note that these exact column types are not enforced.

There two more implementations of `Orm\IMapper`:
* `Orm\ArrayMapper` stores all values in memory (fast, but not persistent between requests), and
* `Orm\FileMapper` serializes all entities into single file.

More end points could easily be added by implementing the `Orm\IMapper` interface. For example: LDAP, restful 3rd party api, read only map from remote json...

[phpdoc]: http://www.phpdoc.org/docs/latest/for-users/introduction/definitions.html "Example phpdoc definitions"
[source: Entity]: http://orm.petrprochazka.com/api/v0.4.0-RC7/php53/source-class-Orm.Entity.html#15 "source of class Orm\Entity"
[api: DibiMapper]: http://orm.petrprochazka.com/api/v0.4.0-RC7/php53/class-Orm.DibiMapper.html "api of class Orm\DibiMapper"
[api: SqlConventional]: http://orm.petrprochazka.com/api/v0.4.0-RC7/php53/class-Orm.SqlConventional.html "api of class Orm\SqlConventional"
[dibi]: http://dibiphp.com/ "Dibi is Database Abstraction Library for PHP 5."
