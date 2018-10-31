# Links

Links represent navigational transitions.  In JSON Siren, links are represented as an array inside the entity, such as

```json
{
    "links": [
        {"rel": [ "self" ], "href": "http://api.x.io/orders/42"}
    ]
}
```

## Attributes

`rel` [Required]

Defines the relationship of the link to its entity, per [Web Linking (RFC5988)](http://tools.ietf.org/html/rfc5988) and [Link Relations](http://www.iana.org/assignments/link-relations/link-relations.xhtml).  MUST be an array of strings.

`class` [Optional]

Describes aspects of the link based on the current representation.  Possible values are implementation-dependent and should be documented.  MUST be an array of strings.

`href` [Required]

The URI of the linked resource.

`title` [Optional]

Text describing the nature of a link.

`type` [Optional]

Defines media type of the linked resource, per [Web Linking (RFC5988)](http://tools.ietf.org/html/rfc5988).