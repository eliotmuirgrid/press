# Flow

![](i.png)

## Flow is the logical successor to Iguana

The idea is to take the best of Iguana 6 technology and some of the better ideas from Iguana X, and build a platform that is more dependable than Iguana 6.

## Flow is open source

Flow code is being developed as an open source technology. It's actually a lot more
versatile what what Iguana itself could do.

## Flow is based on the same core technologies as Iguana

C++, Lua, and Git combined together to make a robust platform. Customers are actually
able to see the C++ code and the Lua code and the platform will encourage them to learn
both meaning there are no limits to what can be done with this technology.

## What is the migration path?

Flow needs to mature first, but the technology is essentially delivered as small cross-platform binaries which can be monitored and controlled by Iguana 6.

It addresses a huge problem with Iguana 6 upgrades: upgrading was always massively risky. An upgrade would consist of changing every interface at once, which was absolute lunacy in an enterprise environment.

No sane customer would ever want to do it, and it's not surprising given the risk involved.

## Flow technology eliminates that risk

Each interface ceases to be part of the same process. Instead, Flow applications are always delivered as a single binary that works on any operating system. That binary will expose a standards-based HTTPS interface to Iguana 6, allowing the Flow binary to be seamlessly controlled and logged via the same mechanisms as other Iguana channels—but it means interfaces can be upgraded one by one, rather than putting the entire set of interfaces at risk in a single upgrade.

## The ultimate solution

Once a customer has fully migrated to Flow-based interfaces, we'll have a replacement dashboard and logging technology with which the Flow binaries can integrate.

It all makes for a much more robust and resilient architecture.

## It solves many problems caused by bad technology

Oracle drivers, for instance, are notorious for crashing the applications that use them. This way, the overall interface engine is never exposed to an Oracle driver. Instead, only the Flow binary is exposed.

The same goes for dangerously insecure technologies like HTTP2, which we jokingly refer to as the "Spyware" edition of HTTP because it's so complicated and has a lot of security vulnerabilities. In this way, clients who have no choice but to deal with these legacy technologies can at least contain their exposure—preferably on machines which run these technologies in a contained way, thus insulating the overall environment from these risks.

