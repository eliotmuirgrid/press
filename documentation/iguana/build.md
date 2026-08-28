# Build

One piece of maintenance that is high on the agenda is to port backwards some
of the superior testing and build technology that Eliot developed for Iguana X
to Iguana 6.

There is no real reason that products shouldn't benefit from the better technology
that Eliot developed for Iguana X.

Iguana X has a simpler build system which Eliot designed and a better faster multi
threaded testing infra-structure.

What does this matter?  Faster builds and iterations make for better support and
making sure that Iguana 6 is also set up for long term success.

You can see the contrast with the two systems here.  This is Iguana 6's system:

```
    CPP IGCutilsDll.cpp
   MODULE IGCI
        CPP IGCImessageProcessor.cpp
        LIB libIGCI.a
   MODULE FMT
   MODULE DRC
   MODULE DAP
     MODULE openssl_src
        CPP DAPclient.cpp
        CPP DAPerror.cpp
        CPP DAPlabels.cpp
        CPP DAPmessage.cpp
        CPP DAPparser.cpp
        CPP DAPquery.cpp
        CPP DAPqueryResult.cpp
        LIB libDAP.a
   MODULE NTBS
     MODULE openssl_src
   MODULE HTPC
        LIB libHTPC.a
   MODULE HTTP
        CPP HTTPbasicAuthent.cpp
        CPP HTTPbodyParser.cpp
        CPP HTTPcookie.cpp
        CPP HTTPfile.cpp
        CPP HTTPheader.cpp
        CPP HTTPheaderParser.cpp
        CPP HTTPmimeLookup.cpp
        CPP HTTPmultiPart.cpp
        CPP HTTPparser.cpp
        CPP HTTPrequest.cpp
        CPP HTTPrequestParser.cpp
        CPP HTTPresponse.cpp
        CPP HTTPresponseParser.cpp
        CPP HTTPsession.cpp
        CPP HTTPsessionHandler.cpp
        CPP HTTPutils.cpp
        CPP HTTPvariables.cpp
        LIB libHTTP.a
```

This build system goes against one of Eliot's core design values which
is transparency.  Build warnings are swallowed by the system.  It also
requires a lot more effort to add files to the system.

Everytime a file is added, it has to be listed in the makefile system:

```
LIBRARY=HTTP

SRC=\
HTTPbasicAuthent.cpp\
HTTPbodyParser.cpp\
HTTPcookie.cpp\
HTTPfile.cpp\
HTTPheader.cpp\
HTTPheaderParser.cpp\
HTTPmimeLookup.cpp\
HTTPmultiPart.cpp\
HTTPparser.cpp\
HTTPrequest.cpp\
HTTPrequestParser.cpp\
HTTPresponse.cpp\
HTTPresponseParser.cpp\
HTTPsession.cpp\
HTTPsessionHandler.cpp\
HTTPutils.cpp\
HTTPvariables.cpp\

include ../makefiles/library.makefile
```

Compare this Iguana X's build system and it's much simpler with Iguana X, which
scans the directory for code files and automatically compiles and links them.

The same library only requires:

```
include ../make/makefile.library
```

No need to list all of the files like the old system.  This is very aligned
with all of Eliot's design ideas.  The modern build system is much more transparent
which makes it faster to diagnose problems and compiler security warnings visible.

```
EliotHomeServer:~/products/iguanax/HTTP % make
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPbasicAuthent.o HTTPbasicAuthent.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPbodyParser.o HTTPbodyParser.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPcookie.o HTTPcookie.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPfile.o HTTPfile.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPheader.o HTTPheader.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPheaderParser.o HTTPheaderParser.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPmimeLookup.o HTTPmimeLookup.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPmultiPart.o HTTPmultiPart.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPparser.o HTTPparser.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPprecomp.o HTTPprecomp.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPrequest.o HTTPrequest.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPrequestParser.o HTTPrequestParser.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPresponse.o HTTPresponse.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPresponseParser.o HTTPresponseParser.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPsession.o HTTPsession.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPsessionHandler.o HTTPsessionHandler.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPutils.o HTTPutils.cpp
ccache c++ -MMD -I../ -Werror -std=c++11   -Wno-unused-value   -c -o HTTPvariables.o HTTPvariables.cpp
```
