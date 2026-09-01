# Comparison

One idea I am quite keen to put into Iguana 6.2.1 is to see if I could make this bit of code work as intended:

```lua
if MSH[9][1] == "ADT" then
   -- Do something
end
```

That does not work. Instead, you have to do this:

```lua
if MSH[9][1]:S() == "ADT" then
   -- Do something
end
```

This is because the HL7 data structure is a *userdata* type—not a plain string—so we have to explicitly convert it into a string before the comparison works.

To clarify, in Lua, when you access `MSH[9][1]`, what you get is not an ordinary Lua string, but rather a special object (userdata) provided by the Iguana HL7 parsing library. The `:S()` method is used to extract the string representation from that object so it can be compared against a literal value like "ADT". Without this conversion, using `==` will always fail, because Lua does not consider userdata and string types as equal, even if their contents are identical.

It would be nice if this extra step wasn’t necessary. If the comparison worked directly, scripts would be simpler and more intuitive. Achieving this might be possible by modifying the Lua engine or by adding a custom metamethod to allow the HL7 fields to behave more like strings during comparison.  This could improve the developer experience when working with HL7 data in Iguana.

It's a little example of something that would be really high value to the core Iguana experience.
