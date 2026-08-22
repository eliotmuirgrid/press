# Signing

**What are Signing Certificates and Signed Binaries?**

**Signing certificates** are digital credentials issued by trusted Certificate Authorities (CAs) that let software publishers prove their identity. When an application or executable file (“binary”) is signed with one of these certificates, it embeds a digital signature into the file. This signature ensures **integrity** (the binary hasn’t been tampered with) and **authenticity** (it genuinely comes from the claimed publisher). Both Microsoft and Apple increasingly require software to be signed before it will run on their operating systems.

For **Microsoft Windows**, unsigned executables and drivers trigger warnings or are outright blocked, especially with features like SmartScreen and strict driver signing requirements. **Apple** goes even further with macOS and iOS: unsigned or unnotarized apps are typically blocked or cannot be installed at all, thanks to Gatekeeper and mandatory code signing. These mechanisms help prevent malware, increase accountability, and build user trust.

However, this approach comes with a **central authority trust paradox**. Large software organizations, like Microsoft and Apple, rely on external Certificate Authorities to verify the identity and trustworthiness of software publishers. But it’s increasingly difficult for these organizations or the CAs themselves to comprehensively vet every company or developer requesting a certificate. As a result, some malicious actors can obtain valid certificates by disguising their identity, undermining the whole trust model. Thus, while digital signing strengthens security in principle, it ultimately shifts the system’s trust to a relatively small group of central authorities—whose effectiveness and diligence is not always transparent or guaranteed.

In summary, while signing requirements are essential for modern software security, they inherit the limitations of central trust: if a bad actor can obtain a certificate, their software seems just as trustworthy as anyone else’s, despite the best efforts of large platform owners
