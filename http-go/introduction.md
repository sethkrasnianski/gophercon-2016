# Introduction to HTTP

- Went over basics of the Hyper Text Transfer Protocol.
- Going over API styles and basics.
- URI - Why it's good and what its limits are.
- URI/REST is the standard, with JSON as the transport.
- Implementations still vary differently.

# REST

- Coined by Roy Fielding in his 2000 PhD dissertation at UC Irvine.
- Resource and Resource collections are identified via URLS.

- `GET` retrieve a resource
- `POST` create new resource
- `PUT` update resource (override)
- `PATCH` partial update
- `DELETE` delete a resource

## Sub-resources

Resources that can only be addressed within the scope of another resource.

## CRUD

- Create, Read, Update, Delete is REST at its purest form.

## Relationships

- Often times the canonical representation of a resource includes a self href.

## Design Considerations

- Join models: should these be represented as a resource? or simple relationships?
- Performance: is there a need for bulk operations? which ones?
- Filtering: no filtering? whitelist of filterable fields? multiple? GraphQL?
- Sorting and pagination: by offset? or absolute?
- Versioning: in the path? header? query string?

Many considerations, involces many parties.

**Do it right** - APIs never go away.

## Join Models

Examples: attached disks

Does the join model need to be addressable? If so use a resource. This can happen if the join model:

- Defines its own fields, e.g. attachment timestamp, attachment status.
- Defines it own actions e.g. DELETE to detach.

Tends to lend itself to a more RESTful API but may be overkill for the simple cases.

## Versioning

If you find yourself releasing versions frequently, timestamps are a great alternative.
