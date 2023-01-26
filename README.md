# stepzen-reshape

Snippets showing how a GraphQL api can be reshaped to expose subsets of the information or with a different structure.

In this case the open countries GraphQL API is reshaped, though any GraphQL schema within StepZen can be reshaped.
That is if the root operation fields and types are in the StepZen schema, then they can be reshaped, regardless
of how they are produced.

## Countries API

`stepzen import graphql` was used to import the open countries API (https://countries.trevorblades.com/graphql)
with a prefix of `Countries_`. The prefix provides clarity on which are the types and fields that we do not
want to expose, and allows a natural name space for the types we do want to expose, for example we want to
expose a field `Query.country` returning `Country` that is a reshaping of the `Countries_Country`

## Reshaping

### Basic

`reshape/basic.graphql` demonstrates some basic reshaping.

Field `Query.country` invokes `Query.Countries_country` and reshapes the result into type `Country` instead of
returning the underlying `Countries_Country`.

The reshapes are:

 - The field returns `Country` type with fields `code` and `capital` taken directly from `Countries_Country`.
 - `Country.name` is a rename of `Countries_Country.native` so that the name of the country is returned in its native language.
 - `Country.landmass` pulls a value from a child object type field and renames it, a rename of `Countries_Country.continent.name`
 - `Country.languages` pulls a field from an list of child object types and converts it to a simple list of `String` values,
    a rename of `Countries_Country.languages.native`.

## Introspection

StepZen field based access rules are used to only expose the reshaped top-level fields (when not using an admin or api key).

This means an authenticated client (in this case open access, typically with a JWT) will only see the fields and types
of the resphaped API. These clients have no visibility into the underlying countries `Query` fields and types.

