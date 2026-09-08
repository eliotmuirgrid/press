# OpenSSL

OpenSSL is an essential—and the most complex—dependency in the Iguana build process, particularly on Windows.  It's used by many of the other libraries
that Iguana uses to implement SSL/TLS so there is no other real choice.

However, focusing on it directly makes the challenge manageable.

Building OpenSSL on Windows requires:

- Visual Studio Build Tools (MSVC) command line version
- Perl
- NASM (to generate x86/x64 assembly)
- The OpenSSL source code

The command line C/C++ compiler and essential tools needed to build and link native Windows applications—required to compile OpenSSL source code.

Perl is used to run OpenSSL’s configuration and build scripts using it as cross platform scripting language.  This dependency is difficult to eliminate so the real question is how to minimize it and bootstrap the installation treating it like a make dependency.

Storing the openssl source code as a tarball in the source code repository might not seem purist but it's a very deterministic way to getting the code.  The other approach is is use subrepositories that nails down a particular version of the source.


