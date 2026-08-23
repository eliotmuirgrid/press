# Function

Having tight conventions for C++ functions is super important in Flow.

## Functions need to have outputs defined with pointers and the return

Here's an example:

```
bool FILEread(const COLstring& FileName, COLstring* pOutput);
```

It's extremely important with declarative testing to rigorously follow
this convention. 

Declarative testing should enforce this furthur.
