# Serialization 

**Seeing the Difference in the Serialized Models**

The difference between the original Chameleon HL7 model and the Iguana X model becomes very obvious when we look at how the same ideas are serialized.

This is not really a comparison of XML versus JSON. Either model could have been written in either format.

What we are seeing is the **shape of the object model underneath the serialization**.

## Chameleon: each concept has its own structure

In the original Chameleon VMD, different parts of HL7 are represented by different kinds of objects.

For example, date/time has its own specialized representation:

```xml
<date_time name="DateTime">
   <description>DTM DateTime</description>
   <fields_required>False</fields_required>
   <mask>YYYY</mask>
   <mask>MM</mask>
   <mask>DD</mask>
   <mask>HH</mask>
   <mask>mm</mask>
   <mask>SS</mask>
   <mask>.SSSS</mask>
   <mask>+/-ZZZZ</mask>
</date_time>
```

The VMD actually defines separate `date_time` structures with their own masks and properties.

A composite is represented differently:

```xml
<composite name="MSG">
   <description>Message Type</description>

   <field>
      <name>Message Code</name>
      <max_length>-1</max_length>
      <is_required>True</is_required>
      <is_length_restricted>False</is_length_restricted>
      <data_type>Composite</data_type>
      <composite_ref>ID</composite_ref>
   </field>

   <field>
      <name>Trigger Event</name>
      <max_length>-1</max_length>
      <is_required>True</is_required>
      <is_length_restricted>False</is_length_restricted>
      <data_type>Composite</data_type>
      <composite_ref>ID</composite_ref>
   </field>
</composite>
```

Here a child is a `field`, and that field contains another set of concepts such as `data_type` and `composite_ref`.

A simple datatype such as `ID` is represented through that same composite machinery, but with another special form for its field:

```xml
<composite name="ID">
   <description>Coded Values For Hl7 Tables</description>

   <field>
      <name>Value</name>
      <max_length>-1</max_length>
      <is_required>False</is_required>
      <is_length_restricted>False</is_length_restricted>
      <data_type>String</data_type>
   </field>
</composite>
```

As the datatype becomes richer, this representation becomes increasingly verbose. A composite such as `XON` repeats the same machinery for every component:

```xml
<field>
   <name>Organization Name</name>
   <max_length>50</max_length>
   <is_required>False</is_required>
   <is_length_restricted>False</is_length_restricted>
   <data_type>Composite</data_type>
   <composite_ref>ST</composite_ref>
</field>

<field>
   <name>Organization Name Type Code</name>
   <max_length>-1</max_length>
   <is_required>False</is_required>
   <is_length_restricted>False</is_length_restricted>
   <data_type>Composite</data_type>
   <composite_ref>CWE</composite_ref>
</field>
```

The same pattern continues for every component in the composite.

The important point is not merely that this takes more characters.

The serialization is exposing the underlying design:

```text
date_time
composite
field
data_type
composite_ref
message
table_grammar
...
```

Each concept has its own representation and therefore requires code which understands that representation.

## Iguana X: one structural idea

Now compare that with the Iguana X grammar.

A message looks like this:

```json
"ADTA02": {
   "desc": "Transfer a patient",
   "type": "message",
   "children": [
      {"type":"MSH", "desc":"Message Header", "req":true},
      {"type":"SFT", "desc":"Software Segment", "repeats":true},
      {"type":"UAC", "desc":"User Authentication Credential Segment"},
      {"type":"EVN", "desc":"Event Type", "req":true},
      {"type":"PID", "desc":"Patient Identification", "req":true}
   ]
}
```

That is directly visible in the serialized grammar.

Now look at a segment:

```json
"AL1": {
   "desc": "Patient Allergy Information",
   "type": "segment",
   "children": [
      {"type":"SI",  "desc":"Set ID - AL1", "req":true},
      {"type":"CWE", "desc":"Allergen Type Code"},
      {"type":"CWE", "desc":"Allergen Code/Mnemonic/Description", "req":true},
      {"type":"CWE", "desc":"Allergy Severity Code"},
      {"type":"ST",  "desc":"Allergy Reaction Code", "repeats":true},
      {"type":"ST",  "desc":"Identification Date"}
   ]
}
```

The structure is essentially identical.

Now look at a composite:

```json
"AUI": {
   "desc": "Authorization Information",
   "type": "composite",
   "children": [
      {"type":"ST", "desc":"Authorization Number"},
      {"type":"DT", "desc":"Date"},
      {"type":"ST", "desc":"Source"}
   ]
}
```

Again, the same structure.

Even a much larger composite such as `CNE` is represented by exactly the same mechanism:

```json
"CNE": {
   "desc": "Coded with No Exceptions",
   "type": "composite",
   "children": [
      {"type":"ST",  "desc":"Identifier", "req":true},
      {"type":"ST",  "desc":"Text"},
      {"type":"ID",  "desc":"Name of Coding System"},
      {"type":"ST",  "desc":"Alternate Identifier"},
      {"type":"ST",  "desc":"Alternate Text"},
      ...
   ]
}
```

That is the entire architectural idea made visible.

## The new model keeps saying the same thing

The Iguana X grammar repeatedly says:

```text
I am a node.
I have a type.
I may have children.
```

The meaning changes:

```text
type = message
type = segment_group
type = segment
type = composite
```

but the structural model does not.

A message can therefore be thought of as:

```json
{
   "type": "message",
   "children": [...]
}
```

A segment is:

```json
{
   "type": "segment",
   "children": [...]
}
```

A composite is:

```json
{
   "type": "composite",
   "children": [...]
}
```

The child itself is also described using the same vocabulary:

```json
{
   "type": "CWE",
   "desc": "Allergen Type Code"
}
```

Optional behaviour is added only where needed:

```json
{"type":"MSH", "req":true}
```

or:

```json
{"type":"ROL", "repeats":true}
```

The grammar does not need a different structural language just because something happens to be a message instead of a segment.

## Compare the conceptual models

The older model is approximately:

```text
Message
    TableGrammar

Segment
    Field
        DataType
        CompositeReference

Composite
    Field
        DataType
        CompositeReference

DateTime
    Mask
    Mask
    Mask
```

The newer model is approximately:

```text
Node
    type
    children[]
```

That is a profound difference.

In Chameleon, moving from one level of HL7 to another often means moving into another object model.

In Iguana X, moving down one level generally means following another `children` relationship.

## The serialization is telling us something about the code

Serialized data frequently reveals the architecture of the program which created it.

When a serialized model contains many different structural concepts, it is a strong indication that the implementation also needs many pieces of code to understand those concepts.

For example, an older implementation naturally tends towards operations such as:

```cpp
ParseMessageGrammar(...);
ParseSegment(...);
ParseField(...);
ParseComposite(...);
ParseDateTime(...);
```

Each implementation then develops its own rules.

How do we iterate it?

How do we validate it?

Can it repeat?

Can it be required?

How do we find its children?

How do we report errors?

What kind of object does it contain?

What does it reference?

Even where the answers are similar, the software has different places in which those answers must be implemented.

The newer model permits something conceptually much closer to:

```cpp
ParseNode(Node* Node) {
   Validate(Node);

   for (auto Child : Node->Children) {
      ParseNode(Child);
   }
}
```

The real parser will obviously contain more logic than this, but the important thing is that the **recursive structure is centralized**.

The algorithm follows the same shape as the data.

## Compare one HL7 relationship

Take a simple relationship:

> A composite contains another datatype.

In the Chameleon representation, that relationship is expressed indirectly:

```xml
<field>
   <name>Message Code</name>
   <data_type>Composite</data_type>
   <composite_ref>ID</composite_ref>
</field>
```

There are several pieces involved:

```text
field
data_type
Composite
composite_ref
ID
```

In Iguana X, essentially the same relationship becomes:

```json
{"type":"ID", "desc":"Name of Coding System"}
```

or:

```json
{"type":"CWE", "desc":"Allergen Type Code"}
```

The child simply says what type of node it is. Examples of these direct child references appear throughout the segment and composite definitions.
There is much less translation between what the grammar means and how the grammar expresses it.

## Required and repeating are properties, not new structures

The newer representation also handles variation cleanly.

A mandatory child is simply:

```json
{"type":"PID", "req":true}
```

A repeating child is:

```json
{"type":"ROL", "repeats":true}
```

And something which is neither required nor repeating needs neither property.

You can see these variations next to each other in the ADT message definition.

This matters because these are genuinely properties of the relationship between parent and child.

They do not require a new family of object types.

That keeps the essential structure small.

## The difference is much larger than XML versus JSON

It would be easy to look at these files and conclude:

> JSON is cleaner than XML.

That misses the point.

We could serialize the Iguana X model in XML:

```xml
<node type="segment" name="AL1">
   <child type="SI" required="true"/>
   <child type="CWE"/>
   <child type="CWE" required="true"/>
   <child type="CWE"/>
   <child type="ST" repeats="true"/>
   <child type="ST"/>
</node>
```

It would still be the simpler model.

Likewise, we could serialize the original Chameleon model in JSON and still retain all of its different object types, references and special cases.

The improvement is not syntax.

**The improvement is abstraction.**

## Why this matters

The Iguana X representation is easier to understand because a programmer only has to learn a small number of structural rules.

It is easier to traverse because everything participates in the same recursive hierarchy.

It is easier to extend because new HL7 structures can often be expressed as another flavour of the same node rather than requiring another subsystem.

It is easier to test because much more behaviour passes through the same implementation.

And it is easier to secure because there are fewer independent code paths processing externally supplied data.

The serialized files make this unusually concrete.

The original Chameleon VMD is approximately 180 KB, while the Iguana X grammar supplied here is approximately 71 KB.
File size alone is not a fair measure of architectural quality—the Chameleon file also contains configuration information that the newer grammar does not—but the contrast is still illustrative.

More importantly, when we inspect the files, the source of the difference is visible.

Chameleon repeatedly describes **different kinds of things in different ways**.

Iguana X repeatedly describes **the same kind of thing with different flavours**.

That is why the newer implementation can be so much smaller.

It did not simplify HL7 by throwing information away.

It simplified HL7 by finding a model which more closely matches what HL7 actually is:

**a recursive structure.**

