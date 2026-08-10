# Execute

**Executing processes arbitrarily is one of the most significant security holes that every modern (ish) engine has.**

It's incredibly convenient to do this - since it can be used to solve many practical problems.

However, this approach makes every single interface engine vulnerable, including Rhapsody, Qvera, Mirth, Iguana, Cloverleaf, and any other obscure engines I haven't yet heard of.

## Why is that?

All sorts of attacks can be enabled through executing commands. There the
obvious:

```
# Delete all files from a the current location!
rm -rf *
```

An attacker can:

 - Manipulate files 
 - Install more software 
 - Launch login sessions into other computers

It's a bad thing to leave this [door open if you don't need to](area).

## How we stop it.

Our Flow technology means that when a production interface is produced, the compiled binary actually removes everything that isn't needed for production. 

See [Flow Integrate](/flow/aiguana).

This is true innovation in security using innovation to provide an unheard of level of security using solid engineering to push the boundaries of what is possible.

