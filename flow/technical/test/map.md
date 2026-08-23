# Map

I plan to test C++ functions with the inputs defined in JSON.

The question is how to map native types to JSON strings, numbers, null and
boolean values when C++ supports a much bigger type set?

## Firstly limit C++ types used

This definitely encourages judicious use of C++ types so as to not have
an explosive set of types to support.

## For those we do define mapping functions.

For instance:

```
COLstring JSONCOLstring(const JSONvar& Variable);
int       JSONint      (const JSONvar& Variable);
double    JSONdouble   (const JSONvar& Variable);
COLuint64 JSONCOLuint64(const JSONvar& Variable);
```

This should allow direct mapping of the input types to the conversion functions.

## For reference this is what JSONvar looks like.

```
class JSONvar {
public:
   JSONvar();
   ~JSONvar();
   
   int      Type;  // Corresponds to LUA types

   bool      Boolean;
   double    Number;
   COLstring String;

   // Table entries
   COLarray<JSONvar> Array;
   COLdictSorted<COLstring, JSONvar> Dict;
};
```

The goal is to keep complexity to a minimum and tests to maximum.
