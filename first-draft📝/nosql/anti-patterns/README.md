Schema design anti pattern

Massive Array

Massive number of collections

Unnecessary index

Bloated document

Case insensitive queries without case insensitive index

Separating data that is access together

—
Massive Array 

16mb document (record) size limit 

Index perf decrease on array as they grow

Dollar lookup

Extended reference pattern -> Mix of normalisation, ie put info that is unlikely to change and needed to view, but have another schema for update

—

Massive num of collections (table)

Every collection have indexes on the _id field, so if you make a lot of collection you have a lot of indexes

In general limit replicat set(see course on mongo) to 10 000 collections

—