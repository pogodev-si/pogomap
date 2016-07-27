# Pokemon Go Map Standarization

Lately, it has been brought up on [/r/pokemongodev](https://www.reddit.com/r/pokemongodev/) several times that we need a "standard way" of doing things within our projects (e.g. dataminers, web maps, databases, etc).
This goes beyond the need of a common database schema to store our data, but also the way we **consume** that data.

Right now, there are many implementations of the same map, using and storing the same information, but with different tools. Although the tools may differ, the composition of the application is always the same:

```
Dataminer/Worker <-> Database (SQL/NoSQL) <-> Web Application(Flask + Google Maps)
```

## What we propose

Instead of just agreeing on a standard way of storing our data (e.g. SQL vs NoSQL), we should also agree on a standard way of **communicating and reading** that data - focus on a **component-based** way of creating our maps, so anyone can fork the existing projects and replace Google Maps for Leaflet, for example.

## Components specification

* Dataminer/Worker: should be easy to replace a worker from a project using `requests` to another using `pycurl` (like [favll/pogom](https://github.com/favll/pogom))
* Database: the database component should provide a common interface to store/get Pokemon, Gyms, PokeStops regardless of the underlying actual RDBMs, for example using RethinkDB (NoSQL) instead of SQLite (like [fourbytes/pogomap](https://github.com/fourbytes/pogomap)). Even further we could work on a distributed effort to point our workers towards a centralized (and beefy) database on a server.
* Web application: The webapp is actually two components into one - the webapp should consume from the DB interface, and provide a standard API for the JS map to consume. Thus way we can migrate from Google Maps to a more libre implementation.
 
## Contributing

As always, PR and issues discussing this points are always welcomed.
