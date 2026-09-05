# FHIR

**Why HL7 Still Matters**

FHIR is often presented as the natural replacement for HL7 v2, but there is a fundamental problem with that idea. FHIR is much more closely coupled to the applications it connects.

HL7 works differently. An application says that something happened: a patient was admitted, an order was placed, a result is available. It packages that event into a relatively simple message. The applications on either side can change substantially without changing that basic contract.

FHIR exposes a much richer model of the application's data through resources, APIs, profiles and extensions. That can be useful, but it also means that when the application changes, the integration is much more likely to be affected. The interface is closer to the internal structure of the application.

FHIR itself is also still evolving. Its resources, profiles and implementation guides continue to change through a large standards process. So you potentially have two moving targets: the application and the standard used to expose it.

HL7 v2 has the opposite advantage. It is mature and, thankfully, has largely stopped evolving. In infrastructure, that is a very good thing. An ADT message doesn't need to be reinvented every few years.

FHIR has useful applications, particularly where interactive API access is genuinely required. But for many everyday healthcare workflows, HL7 solves the problem with a much smaller and more stable contract between systems.

That is why HL7's age should not be seen simply as a weakness. **Its stability is one of its greatest strengths.**

