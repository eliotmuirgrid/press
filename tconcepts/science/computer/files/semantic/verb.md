# Verbs

**Verbs should be represented independently of tense when performing semantic mapping.**

In Indonesian, verbs do **not** change form to indicate tense. Instead, Indonesian relies on separate time markers, such as _sudah_ ("already"), _akan_ ("will"), and _sedang_ ("currently"), to specify when an action takes place. The verb itself remains unchanged, regardless of whether the meaning is past, present, or future. For example, _Saya makan_ can mean “I eat,” “I ate,” or “I will eat,” depending on context or added time expressions.

When creating **semantic mappings**—such as for natural language processing or in developing lexical databases—it’s important to represent verbs in their base form, **without encoding tense, aspect, or mood**. Tense should be treated as a separate grammatical feature, distinct from the verb’s fundamental meaning. This separation allows for greater clarity and adaptability in linguistic resources and avoids conflating different grammatical categories.

**Key points:**
- **Indonesian verbs** remain in a single, base form regardless of tense.
- **Semantic mapping** should likewise treat a verb’s core meaning as independent of tense, aspect, or mood.

So, just as English has “go,” “going,” “gone”—all sharing the same core meaning but differing in tense and aspect—the semantic representation should focus on the base concept (“go”), while handling tense separately.
