# Siren: a hypermedia specification for representing entities

[![DOI](https://zenodo.org/badge/4917422.svg)](https://zenodo.org/badge/latestdoi/4917422)

Your input is appreciated.  Feel free to file a GitHub Issue, a Pull Request, or contact us.  Thank you!

- [Official Siren Google Group](https://groups.google.com/forum/#!forum/siren-hypermedia)
- Kevin on Twitter [@kevinswiber](https://twitter.com/kevinswiber)

## Introduction

Siren is a hypermedia specification for representing entities.  As HTML is used for visually representing documents on a Web site, Siren is a specification for presenting entities via a Web API.  Siren offers structures to communicate information about entities, actions for executing state transitions, and links for client navigation.  

Siren is intended to be a general specification of a generic media type that can be applied to other types that are not inherently hypermedia-powered.  The initial implementation is JSON Siren.  Other implementations, such as XML Siren, may also be implemented using the Siren specification.

All examples in this document are in the JSON Siren format.

## Entity

An Entity is the Siren representation of a URI-addressable resource that has properties and actions associated with it.  It may contain sub-entities and navigational links.  The root element of a Siren response is always an Entity, but all attributes described below such as `properties` or `action` are optional.  This means `{}` is also a perfectly valid (while useless) Siren Entity.

Root Entities and Sub-Entities (Entities within the `entities` array of the root Entity) that are embedded representations SHOULD contain a `links` collection with at least one item contain a `rel` value of `self` and an `href` attribute with a value of the entity's URI.

Sub-entities that are embedded links MUST contain an `href` attribute with a value of its URI. Sub-entities are further explained in [Sub-Entities](subentities.md).

### Example

Below is a JSON Siren example of an order, including sub-entities.  The first sub-entity, a collection of items associated with the order, is an embedded link.  Clients may choose to automatically resolve linked sub-entities.  The second sub-entity is an embedded representation of customer information associated with the order.  The example also includes an action to add items to the order and a set of links to navigate through a list of orders.

The media type for JSON Siren is `application/vnd.siren+json`.

```json
{
  "class": [ "order" ],
  "properties": { 
      "orderNumber": 42, 
      "itemCount": 3,
      "status": "pending"
  },
  "entities": [
    { 
      "class": [ "items", "collection" ], 
      "rel": [ "http://x.io/rels/order-items" ], 
      "href": "http://api.x.io/orders/42/items"
    },
    {
      "class": [ "info", "customer" ],
      "rel": [ "http://x.io/rels/customer" ], 
      "properties": { 
        "customerId": "pj123",
        "name": "Peter Joseph"
      },
      "links": [
        { "rel": [ "self" ], "href": "http://api.x.io/customers/pj123" }
      ]
    }
  ],
  "actions": [
    {
      "name": "add-item",
      "title": "Add Item",
      "method": "POST",
      "href": "http://api.x.io/orders/42/items",
      "type": "application/x-www-form-urlencoded",
      "fields": [
        { "name": "orderNumber", "type": "hidden", "value": "42" },
        { "name": "productCode", "type": "text" },
        { "name": "quantity", "type": "number" }
      ]
    }
  ],
  "links": [
    { "rel": [ "self" ], "href": "http://api.x.io/orders/42" },
    { "rel": [ "previous" ], "href": "http://api.x.io/orders/41" },
    { "rel": [ "next" ], "href": "http://api.x.io/orders/43" }
  ]
}
```

### Attributes

`class` [Optional]

Describes the nature of an entity's content based on the current representation.  Possible values are implementation-dependent and should be documented.  MUST be an array of strings.

`title` [Optional]

Descriptive text about the entity.

`properties` [Optional]

A set of key-value pairs that describe the state of an entity.  In JSON Siren, this is an object such as `{ "name": "Kevin", "age": 30 }`.

`entities` (See [Sub-Entities](subentities.md)) [Optional]

A collection of related sub-entities.  If a sub-entity contains an `href` value, it should be treated as an embedded link.  Clients may choose to optimistically load embedded links.  If no `href` value exists, the sub-entity is an embedded entity representation that contains all the characteristics of a typical entity.  One difference is that a sub-entity MUST contain a `rel` attribute to describe its relationship to the parent entity.

In JSON Siren, this is represented as an array.

`actions` (See [Actions](actions.md)) [Optional]

A collection of action objects, represented in JSON Siren as an array such as `{ "actions": [{ ... }] }`.

`links` (See [Links](links.md)) [Optional]

A collection of items that describe navigational links, distinct from entity relationships.  Link items should contain a `rel` attribute to describe the relationship and an `href` attribute to point to the target URI.  Entities should include a link `rel` to `self`. 
 
## Usage Considerations

Siren supports a resource design style that doesn't have to be primarily CRUD-based.  A root entity may take ownership of facilitating changes to sub-entities via actions.  Using Siren allows you to easily provide a task-based interface through your Web API.

## Feedback

Siren is still a work in progress looking for some real world usage and feedback.  Please contribute!  Feel free to use GitHub Issues to make suggestions or fire up a Pull Request with changes to be reviewed.  Thank you!
