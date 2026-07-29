# VMD Format in Iguana X

This was one of the better ideas in Iguana X that Eliot was (is) quite proud of. 

He figured out how to greatly simplify the design from Chameleon.  Instead of having
objects for:

 - Messages
 - Segment Groups
 - Segments
 - Composites
 - Datetime formats

He said, screw all that!  Let's just have one object for everything and represent and
change the'type' based on all of the above bollocks.

As usual he thought he built the best thing since sliced bread with his clever way of
representing JSON in a sweet way.

But it still kind of sucked when he tried to edit it over the internet - turns out that
even nice JSON isn't simple enough!

So he'll revisit the idea with [Flow](/flow) in time.  Good ideas come back to you!
