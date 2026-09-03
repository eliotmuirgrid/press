# Simplify

One of my core values as a designer is the pursuit of simplicity within systems.

Simpler systems are easier to understand, maintain, and secure. This ongoing commitment to simplicity continues to guide the development of both Iguana 6 and Iguana X.

On September 3rd, I began this process for Iguana X with a straightforward idea: remove many non-core components that are not directly related to HL7 processing. I am documenting these changes on our website so customers interested in those components can find where to access them. The guiding principle is “less is more”—a value that was fundamental in making Iguana a reliable and robust product.

I am confident that Iguana X can achieve this same clarity and reliability as Iguana 6 by moving forward step by step.

You can review the core changes here: [components removed](https://bitbucket.org/interfaceware/interfaceware-core/commits/6841093002e025191e2359ac3a748764f4b183f4).  I followed that with [another scrub of things](https://bitbucket.org/interfaceware/interfaceware-core/commits/9e354cc5012999e1dcd8adaeefddb4770bf7de76) which just are not core to the bread and butter of what
our customers need.  In case people want to access these components then I put them into this repo here on my personal github site:

In addition, I have simplified the To/From LLP components by removing the use of sub-repositories in their implementation. These components are central to an interface engine’s function, and reducing their complexity minimizes the risk of breakages inherent in managing sub-repositories and just makes it easier to browse the code online and check out the entire repository. In this case, simplicity offers clear benefits.

Here are the specific diffs for reference:

- [to-llp-core commit](https://bitbucket.org/interfaceware/to-llp-core/commits/d1ebe41f6269ef11a1596ff53fd7dc4e73178ce4)
- [from-llp-core commit](https://bitbucket.org/interfaceware/from-llp-core/commits/3bbbb39e88e1eee0d257306c504f8a9a337116ae)

I will revisit these ideas as I continue to simplify Iguana X and realize the vision I originally intended:  
a simpler way to manage mission-critical data streams for my customers.

Have a beautiful day.  Bit by bit we get closer to what we all need which is simplicity and security.

Eliot Muir

