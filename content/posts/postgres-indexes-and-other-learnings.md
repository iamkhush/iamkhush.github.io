---
title: "Postgres Indexes, PL/pgSQL and other learnings"
date: 2016-02-02T01:30:01+05:30
tags: [Postgres, Database, PLSQL]
type: "post"
summary: 'Learn about different types of indexes present in Postgres. Trigram / Bigram Indexes, Partial Indexes'
---

Recently I had to do a bit of reading on building Indexes in Postgres. Intrestingly I found some striking features about indexing types in Postgres

## Extensions

Postgres has a collection of extensions/modules. These are basically set of functions. One such module is `pg_trgm`. Quoting from the documentation- "pg_trgm provides functions and operators for determining the similarity of ASCII alphanumeric text based on trigram matching, as well as index operator classes that support fast searching for similar strings" [Documentation](http://www.postgresql.org/docs/9.1/static/pgtrgm.html)

To use extensions one has to enable / create extensions. Extensions like pg_trgm are built in, meaning they dont have any other depenedencies, you can build them whenever you need to use them.

{{< highlight plpgsql >}}
CREATE EXTENSION pg_trgm;
{{< / highlight >}}

One interesting function that I would like to experiment on is *similarity* which basically returns a number ( between 0 and 1 ) indicating how similar the two arguments are, 1 for when comparing identical strings

## The Trigram Indexes

Now apart from this just plug n play functionality, pg_trgm also provides us GIN and GiST indexes. They allow very fast similarity searches ( using the method above) and also support LIKE and ILIKE queries.

As stated in the documentation, GIN is generally faster than GiST index, but GIN is much more suited for static data.

For my use case , I needed to implement a full text search, from 5 million rows. Using the index , search got completed in couple of 8ms, whereas it took about 17 secs. I am quite happy with the results.

{{< highlight plpgsql "title='Command to create gin index'">}}
CREATE INDEX trgm_idx ON test_trgm USING gin (t gin_trgm_ops);
{{< / highlight >}}

Check this [page](http://blog.2ndquadrant.com/text-search-strategies-in-postgresql/) for indexing strategies.

Official documentation about text search [www.postgresql.org](http://www.postgresql.org/docs/9.5/static/textsearch.html)


## Cons of the Trigram Indexes

Even though using GIN solved the issues, there were two issues that came to me

- Firstly, the size of GIN Index was around 2GBs for a table having size of 700MBs only
- Secondly, since this is a trigram index, search for words with less than 3 letters couldnt use the index.

For the second problem, we used a simple hack. Since the use of index was giving much better performance, we decided to search for words less than 3 letters, in memory/code.


## Partial Indexes

Partial indexes, as the name suggests, builds indexes for only rows that fall under the condition( called predicate ) we mention while creating the index.

{{< highlight plpgsql >}}
CREATE INDEX orders_unbilled_index ON orders (order_nr)
    WHERE billed is not true;
{{< / highlight >}}

They save space and are also easier to update as compared to full table indexes.


## PL/pgSQL - SQL Procedural Language

One last thing I learnt was PL/pgSQL. Its a procedural language in Postgres. I wanted to build partial indexes and wanted to iterate over loops. So I wrote a procedural script and ran it. One example below

{{< highlight plpgsql >}}
do $$
begin
for i in 1..97 loop
execute format('drop index table_%s',i);
end loop;
end;
$$ LANGUAGE plpgsql;
{{< /highlight >}}

Helpful documentation and examples can be seen [here](http://www.postgresql.org/docs/current/static/plpgsql.html).


## Bigram Indexes

Now, similar to Trigram Indexes, Postgres also supports Bigram Indexes. The module name is called `pg_bigm`. Now this module is not available on the fly in postgres.

The module can be accessed here. This module needs to be fetched and compiled before you can use it.

Unlike Trigram, it used 2 letters grams or tokens. Also it supports on GIN Index. More elaborate comparision is available on the link above.


