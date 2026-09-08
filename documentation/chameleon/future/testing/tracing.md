# Tracing

**Tracing** is a technique used to analyze how an interface operates in production. This helps you understand which parts of the interface code are actually used when processing real-world data—such as HL7 messages—so you can identify unused code or rarely-exercised code paths.

## Steps Involved

1. **Take the Interface to the Lab:**
   - Start by copying the interface you want to analyze into a controlled lab environment.

2. **Modify the Interface to Make it Traceable:**
   - Update the code of the interface (for example, both the Chameleon code and any embedded Python scripts) so it logs or records which parts of the code are being executed.
   - This enables the collection of detailed runtime information.

3. **Split the Input Stream:**
   - When running your test, **duplicate** the incoming HL7 messages so that:
     - **Stream 1:** Goes through the original, unmodified interface (the legacy version), ensuring production behavior is preserved.
     - **Stream 2:** Goes through the modified (instrumented) interface, where tracing is enabled.

4. **Analyze Trace Data:**
   - Use the logs from the instrumented interface to determine:
     - Which functions/modules/scripts are being run.
     - How frequently each part of the code is invoked.

**The tracing needs report more on the shape and nature of the data - i.e. numeric, alpha numeric, number of characters in order to avoid disclosing PHI**

## Goals

- **Coverage:** Figure out what percentage of the interface code is actually exercised/used when processing real HL7 data.
- **Dead Code:** Identify code that is never executed under typical workloads—this may be obsolete or redundant.
- **Rare Events:** Detect code that is only executed in unusual scenarios (the "black swan" events)—uncommon message types or edge cases.

## Why Use Tracing?

- To better understand system behavior in production.
- To identify opportunities for code cleanup or refactoring.
- To expose hidden bugs or untested edge cases.

---

**Bottom Line:**  
By tracing interface execution in a lab setting with real-world data, you gain insights into actual code usage, uncover dead or rarely-used code, and improve overall interface quality.  It's about getting control and visibility at scale.
