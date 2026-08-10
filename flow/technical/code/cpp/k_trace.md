# Tracing C++

Once you learn how to program with tracing you'll never go back.

It dazzles me how smart all the people who program without it.  But
then may be it's not that dazzling because it also dazzles me how
buggy most software is - like why is [the page for this](f_header.md)
has F Header in the left menu instead of the title of the page.

Most rapid development environments of the modern error give swift
initial results and then reward you with a never ending long tail of
bugs.

I prefer to write more boring code.  To use tracing you use the trace
command line setting, it takes a wild card expression to show what C++
file names to match on:

```
EliotHomeServer:~/flowlua/flowlua % ./flowlua.com --install --trace "APP*"   
### Tracing files matching: APP*
  Timestamp       Thread ID File
  03:02:41.931618     96189 APPinstall         >APPinstall Line:11
  03:02:41.931805     96189 APPinstall         . .
  03:02:41.931812     96189 APPinstall         . ..
  03:02:41.931817     96189 APPinstall         . dir
  03:02:41.931823     96189 APPinstall         . git
  03:02:41.931830     96189 APPinstall         <APPinstall
EliotHomeServer:~/flowlua/flowlua % 

```
