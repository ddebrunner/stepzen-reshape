
# Sample operations

Sample operations are in [operations.graphql](operations.graphql)

## Basic

### Country

Run the exposed simplified API using `Query.country`.
```
stepzen request -H Authorization: \
   -f operations.graphql \
   --operation-name=Country \
   --var code=BE
```
> **Note**
> `-H Authorization:` removes the default api key authorization header
>  showing the reshaped api is open.

### Introspection

Shows the exposed fields in `Query` and exposed types for the reshaped API.
```
stepzen request -H Authorization: \
   -f operations.graphql \
   --operation-name=Introspection
```
> **Note**
> None of the underlying `Query` fields or types from countries are exposed
> (they would have a `Countries_` prefix).

### BasicCompare

This shows the same information being returned in its reshaped and original form. 
```
stepzen request \
   -f operations.graphql \
   --operation-name=BasicCompare \
   --var code=BE
```
