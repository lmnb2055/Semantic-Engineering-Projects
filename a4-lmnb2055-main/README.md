# RDFS

For this assignment you will take the description and vocabulary that
you started creating for the Data Modeling assignment (A2) and express
them using RDF and RDFS in the Turtle serialization.

Before you start this assignment, be sure to read [your feedback on
A2](https://aeshin.org/teaching/inls-620/2025/fa/grades/).

## Create your description and vocabulary

In `description.ttl`, translate your description diagram into RDF in
Turtle syntax. There should be one resource for each entity in the
diagram, and one statement (triple) for each relation.
**Be sure to fix any problems identified in your feedback on A2!**

In `vocab.ttl`, translate your documentation of your classes and
properties into RDFS in Turtle syntax. Each class and property you
define should have an `rdfs:label` giving it a human-readable label
and an `rdfs:comment` giving it a description. Each property you
define should also have an `rdfs:domain`, and an `rdfs:range` (unless
it takes a literal value; see below).
**Be sure to fix any problems identified in your feedback on A2!**

Remember that:

* Resource names, including class and property names, cannot have
  spaces or other unusual punctuation in them.
* Class and property names should be in "camel case", e.g.:
  `PropertyManager`, `managesProperty`
* Class names should be capitalized.

I have included some example statements in `description.ttl` and
`vocab.ttl`; please remove these statements before you submit.

### Using literal values

You may decide that it makes sense for some values to be literals
rather than resources. For example, a `publicationDate` should
probably just take a literal date value:

```ttl
ex:catch22 rdfs:label "Catch-22" ; ex:publicationDate "1961-10-10"^^xsd:date .
```

 If you choose to do that, do not define a `range` for
 `publicationDate` (or whatever the property is that you think should
 take a literal value). You might be tempted to make the range
 `rdfs:Literal`, but if you do and you have a triple like the one
 above, then it will be inferred that:

```ttl
"1961-10-10"^^xsd:date rdf:type rdfs:Literal .
```

… which is true, but since we cannot have literals in the subject
position, this produces invalid RDF.

## Validate your Turtle files

```text
make validate
```

will check that `vocab.ttl` and `description.ttl` are valid Turtle files.

If either file is invalid, look at it in Visual Studio Code. The
invalid parts should have red squiqqles. If you can't figure out how
to fix it, try asking Copilot for help by highlighting the problematic
part, opening the context menu (right-click or Ctrl/⌘-click) and
choosing Copilot → Explain.

## Infer new triples based on your RDFS vocabulary

```text
make inferred.ttl
```

will create a file `inferred.ttl` containing the triples from
`description.ttl` plus any new triples that could be inferred based on
`vocab.ttl`.

```text
make diff.txt
```

will create a file `diff.txt` showing the differences between
`description.ttl` and `inferred.ttl`.

## Visualize any Turtle file as a graph

```text
make vocab.png
```

will create a file `vocab.png` visualizing `vocab.ttl` as a
graph. This will work for any file ending in `.ttl` (for example,
`description.ttl` or `inferred.ttl`).

## Create all the necessary files for submission

```text
make submit
```

will create:

* `inferred.ttl`
* `description.png`
* `vocab.png`
* `inferred.png`
* `diff.txt`

You can then commit these files along with `description.ttl` and
`vocab.ttl`, and sync everything to submit.
