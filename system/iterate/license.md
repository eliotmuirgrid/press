# License

**Pulling the Plug on `my.interfaceware.com`**

`my.interfaceware.com` was one of the longest-running engineering problems at iNTERFACEWARE.

The original system was built on a framework called TREe. Later, another framework was built on top of it, creating a tightly coupled system that became increasingly difficult to understand, maintain, or replace.

Over the years, I spent a significant amount of money trying to rewrite it.

One developer spent months getting little more than the login screen working. Another rebuilt the front end, but introduced an even more complicated architecture that depended on Nginx working alongside Iguana. Every attempt to delegate the project resulted in a larger, more complex system than the one it was supposed to replace.

The part that frustrated me most was that we kept investing in the old framework. Instead of replacing it, developers learned its increasingly convoluted internals and continued adding new licensing features. From a business perspective, it made no sense. We were spending engineering effort preserving technical debt.

The reality is that the licensing requirements are remarkably simple. Like most enterprise software vendors, we just need a straightforward way to issue licenses and validate customers. Our software runs on our customers' own infrastructure—and that's a feature, not a flaw.

For years, some customers insisted they wanted a hosted version. When we finally built one, almost nobody used it.

That reinforced an important lesson: people are often poor at predicting what they'll actually use. Hypothetical requests are not the same as real demand. Too often, management treats those requests as requirements and spends months or years building features that deliver little value.

Eventually, I pulled the plug on the entire system.

What we have today isn't perfect, but it's good enough. It gets the job done, it's easy to understand, and—most importantly—it no longer consumes months of engineering effort just to make small changes.

From a Theory of Constraints perspective, that's exactly where it should be. The licensing system is no longer the bottleneck. Once something stops being the constraint, the smartest thing you can do is stop polishing it and move your attention to the parts of the business that actually limit growth.

Pulling the plug on the old licensing system was one of the most satisfying engineering decisions I've made. Instead of carrying decades of accumulated complexity, I can now build something radically simpler that reflects the actual needs of the business.

The best rewrite wasn't another rewrite.

It was deciding to stop rewriting the wrong system.

To use the new system go to [License](/license).

