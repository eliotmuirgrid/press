# First Problem

I want to help Victor Effendi in Singapore by building a small interface that will eliminate the need for him to deal with the complexities of Windows file server permissions and daemon processes.

We can use FlowLua to write a simple program that periodically monitors a folder, then uses HTTPS to send files to Iguana. For the initial version, we'll use CURL since compiling OpenSSL can be challenging, and CURL should suffice for now.

Over time, we'll address all the bottlenecks related to security and usability—since usability is a key part of security.

One advantage is that we already have C++ tracing, and soon we'll have the ability to trace in Lua as well. I used to find the Iguana translator's debugger frustrating; although I could see variable values, I often switched back to C++ because, despite being less sophisticated than the Iguana translator GUI, the C++ tracing felt easier to use.

I think I'll learn from that make a better Lua debugging experience than with classical
Iguana.  This will actually be quite fun!
