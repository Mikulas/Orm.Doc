5: Working with entities
========================

Explain first!
* persist, flush, attach, ...


Creating new entity
-------------------

* "root", in repository
* related to existing entities (`$entity->{1:m}->add()`)

Loading entity
--------------

* from repository
* from parent entity
* custom repo methods? (`findByEvenId()`, `findAllOrderedByCity()`, ...)

Updating entity
---------------

Removing entity
---------------

* `$entity->delete()`
* `$entity->{1:m}->delete()`, nebo `set([])` nebo jak to je
