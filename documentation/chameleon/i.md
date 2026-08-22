# Chameleon

**Chameleon is now only supported when combined with Iguana.**

While we won’t mention any specific customers, we want to take this opportunity to highlight an important topic that some long-time Chameleon users may need to revisit.

Over the years, we’ve introduced a variety of advanced dashboards and innovative features. However, there has been a persistent, fundamental challenge that deserves more attention:

**Many legacy Chameleon deployments are not encrypting TCP/IP traffic.**

This means data is being transmitted without the security benefits provided by encryption. From both a security and compliance perspective, this falls short of best practices — and may raise questions regarding SOC2 compliance (although, to be fair, you would probably just have to document that you completely disregard client security with SOC2) and, in some cases, HIPAA.

Therefore, we strongly encourage everyone managing legacy Chameleon systems to implement encryption for network traffic as soon as possible.

**The good news is that there’s a straightforward solution.** By setting up a local socket connection from your legacy Chameleon source into Iguana, you can leverage Iguana’s TLS/SSL capabilities to encrypt your traffic — without needing to significantly redesign your existing applications.

This simple adjustment can provide significant improvements in both security and regulatory compliance.

Ultimately, our primary concern is the protection of sensitive information for the individuals whose data traverses these systems. They deserve the highest standard of care when it comes to data privacy.

Thank you for your attention to this important matter. If you need guidance setting up encrypted LLP channels, please let us know. We’ll also be updating documentation shortly to further assist with this process.

Migration is designed to be simple and focuses primarily on [regression testing](../../system/test/regression.md).

