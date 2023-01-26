
# Sample operations

Sample operations are in [operations.graphql](operations.graphql)

## Basic

### Country

Run the exposed simplified API using `Query.country`.

```
stepzen request -H Authorization: \
   --operation-name=Country \
   "`cat operations.graphql`" \
   --var code=BE
```

> **Note**
> `-H Authorization:` removes the default api key authorization header
>  showing the reshaped api is open.

### Introspection

Shows the exposed fields in `Query` and exposed types for the reshaped API.
Note none of the underlying fields or types from countries are exposed
(they would have a `Countries_` prefix).

```
stepzen request -H Authorization: \
   --operation-name=Introspection \
   "`cat operations.graphql`"
```

### BasicCompare

This shows the same information being returned in its reshaped and original form. 
```
stepzen request \
   --operation-name=BasicCompare \
   "`cat operations.graphql`" \
   --var code=BE
```
