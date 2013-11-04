ORM: Object-relational mapping
==============================

<dl>
	<dt>Entity</dt>
	<dd>Individual "object". For example one Article.</dd>
	<dt>Repository</dt>
	<dd>Main access point for entities. For example you would ask it for collections of Articles (or single article).</dd>
	<dt>Mapper</dt>
	<dd>Moves raw data between objects and storage (e.g. database, array, file, ...) while keeping them independent of each other. For example it could state that Articles map to table "articles" in database.</dd>
</dl>

([ref: SO Pierce Hickey])



[ref: SO Pierce Hickey]: http://stackoverflow.com/a/814479/326257 "What is the difference between the Data Mapper, Table Data Gateway (Gateway), Data Access Object (DAO) and Repository patterns?"
