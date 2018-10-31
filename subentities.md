# Sub-Entities

Sub-entities can be expressed as either an embedded link or an embedded representation.  In JSON Siren, sub-entities are represented inside an `entities` array.

## Additional Information

> #### Sub-Entities vs. Links
> Another distinction is the difference between Sub-Entities and [Links](links.md).  Sub-entities exist to communicate a relationship between entities, in context.  Links are primarily navigational and communicate ways clients can navigate outside the entity graph.

# Embedded Link
A sub-entity that's an embedded link may contain the following:

## Attributes

`class` [Optional]

Describes the nature of an entity's content based on the current representation.  Possible values are implementation-dependent and should be documented.  MUST be an array of strings.

`rel` [Required]

Defines the relationship of the sub-entity to its parent, per [Web Linking (RFC5988)](http://tools.ietf.org/html/rfc5988) and [Link Relations](http://www.iana.org/assignments/link-relations/link-relations.xhtml).  MUST be a non-empty array of strings.

`href` [Required]

The URI of the linked sub-entity.

`type` [Optional]

Defines media type of the linked sub-entity, per [Web Linking (RFC5988)](http://tools.ietf.org/html/rfc5988).

`title` [Optional]

Descriptive text about the entity.

# Embedded Representation

Embedded Sub-Entity representations retain all the characteristics of a standard [Entity](README.md#entity), but MUST also contain a `rel` attribute describing the relationship of the sub-entity to its parent.

## Attributes

`rel` [Required]

Defines the relationship of the sub-entity to its parent, per [Web Linking (RFC5988)](http://tools.ietf.org/html/rfc5988) and [Link Relations](http://www.iana.org/assignments/link-relations/link-relations.xhtml).  MUST be a non-empty array of strings.

## Additional Information

> #### Classes vs. Relationships
> It's important to note the distinction between link relations and classes.  Link relations define a relationship between two resources.  Classes define a classification of the nature of the element, be it an entity or an action, in its current representation.