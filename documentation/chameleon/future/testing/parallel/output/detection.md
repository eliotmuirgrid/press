# Detection

**How do you determine the true outputs of an existing HL7 interface?**

There are three complementary techniques, each providing a different level of confidence.

## 1. Institutional knowledge — fastest, least reliable

Ask the engineers who know the interfaces what they do and where their outputs go.

This is the quickest starting point, but interfaces may have evolved over decades, people have moved on, and documentation and memories may be incomplete.

## 2. Static code analysis — more reliable

Analyze the interface configurations and code directly.

For Chameleon, VMD files can be represented as XML and the embedded Python extracted. This makes it possible to automate analysis across hundreds or thousands of interfaces, looking for outputs such as stored procedures, database access, files, messages or other side effects.

This provides much stronger evidence, but code analysis alone still cannot prove what actually happens at runtime.

## 3. Runtime tracing — most reliable

Ultimately, the strongest evidence comes from observing what the interface actually does.

Tracing can initially be developed and validated in test environments, but the most meaningful evidence will eventually come from carefully tracing the interface **in parallel in production**, without changing or interfering with its existing behaviour.

The progression is therefore:

**institutional knowledge → static analysis → runtime tracing**

Each technique increases confidence while helping us understand what actually needs to be measured before an interface can be safely modernized.

