# Actions

Actions show available behaviors an entity exposes.

## Attributes

`name` [Required]

A string that identifies the action to be performed.  Action names MUST be unique within the set of actions for an entity. The behaviour of clients when parsing a Siren document that violates this constraint is undefined.

`class` [Optional]

Describes the nature of an action based on the current representation.  Possible values are implementation-dependent and should be documented.  MUST be an array of strings.

`method` [Optional]

An enumerated attribute mapping to a protocol method.  For HTTP, these values may be `GET`, `PUT`, `POST`, `DELETE`, or `PATCH`.  As new methods are introduced, this list can be extended.  If this attribute is omitted, `GET` should be assumed.

`href` [Required]

The URI of the action.

`title` [Optional]

Descriptive text about the action.

`type` [Optional]

The encoding type for the request.  When omitted and the `fields` attribute exists, the default value is `application/x-www-form-urlencoded`.

`fields` [Optional]

A collection of fields, expressed as an array of objects in JSON Siren such as `{ "fields" : [{ ... }] }`.  See [Fields](#fields).

# Fields

Fields represent controls inside of actions.

## Attributes

`name` [Required]

A name describing the control.  Field names MUST be unique within the set of fields for an action. The behaviour of clients when parsing a Siren document that violates this constraint is undefined.

`class` [Optional]

Describes aspects of the field based on the current representation.  Possible values are implementation-dependent and should be documented.  MUST be an array of strings.

`type` [Optional]

The input type of the field. This may include any of the following [input types](http://www.w3.org/TR/html5/single-page.html#the-input-element) specified in HTML5:

> `hidden`, `text`, `search`, `tel`, `url`, `email`, `password`, `datetime`, `date`, `month`, `week`, `time`, `datetime-local`, `number`, `range`, `color`, `checkbox`, `radio`, `file` 

When missing, the default value is `text`.  Serialization of these fields will depend on the value of the action's `type` attribute. See [`type`](#type) under Actions, above.

`value` [Optional]

A value assigned to the field.

`title` [Optional]

Textual annotation of a field.  Clients may use this as a label.