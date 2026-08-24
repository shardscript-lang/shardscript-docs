# ShardScript documentation agent instructions

## About this project

- This is the documentation site for **ShardScript**, built on [Mintlify](https://mintlify.com).
- Pages are MDX files with YAML front matter. Navigation is configured in `docs.json`.
- The source repository for the language and runtime is at `https://github.com/Rikitav/ShardScript`.
- Existing pages were migrated from a custom React/MDX site. New articles should follow the conventions below.

## Documentation framework

Follow the **Diátaxis** framework. Every article must be exactly one of:

- **Tutorial** — learning-oriented, sequential narrative.
- **How-To Guide** — task-oriented, goal-driven steps.
- **Concept** — explanation-oriented, idea-focused.
- **Reference** — information-oriented, scannable API/language details.

Do not mix these paradigms on a single page.

## Article templates

### Reference pages

Use these sections in this order:

1. **Summary** — 1-2 sentence description.
2. **Syntax** — exact signature or grammar.
3. **Parameters / Arguments** — bulleted or tabled inputs.
4. **Returns** — what the feature evaluates to.
5. **Exceptions / Errors** — possible runtime or compile errors.
6. **Remarks** — deep technical details, VM behavior, edge cases, performance.
7. **Examples** — runnable code snippets.
8. **See also** — links to related Reference or Concept articles.
9. **Source** — link to the relevant file in the ShardScript repository (e.g. `ShardScript.Framework/system/<name>.shard.cpp` or `ShardScript/include/shard/<path>.hpp`) when the documented feature is backed by source code.

Reference pages must end with **See also** and **Source**.

### Tutorials

- **Prerequisites**
- **Scenario**
- **Step-by-Step Instructions** (numbered)
- **Expected Output**
- **What's next?** — at least one concrete follow-up action or link.

Tutorials must end with **What's next?**.

### How-To Guides

- **Prerequisites**
- **Goal**
- **Step-by-Step Instructions** (numbered)
- **Verification**
- **Troubleshooting**
- **See also** — link to the Reference pages of every API used.

How-To pages must end with **Troubleshooting** and **See also**.

### Concept pages

- **Summary**
- **What problem it solves**
- **How it works**
- **Key ideas**
- **When to use / When not to use**
- **Related articles**

Concept pages must end with **Related articles**.

## Code formatting rules

All ShardScript and host-integration snippets must follow these rules:

1. **No implicit typing.** Never use `var` or `auto`. Declare every type explicitly.
2. **Explicit scoping and braces.** Never use single-line `if`, `for`, or `while`. Always use `{ }`.
3. **Readable `switch` statements.** Add a blank line between `case` blocks.
4. **No code compression.** Optimize for vertical readability. Avoid single-line logic, tuples, and dynamic/duck typing in host code.
5. **Inline comments explain why, not what.**

## MDX / Mintlify conventions

1. **Front matter** on every page:
   ```yaml
   ---
   title: Article Title
   description: Short summary for SEO and previews.
   ---
   ```
2. **Use standard Markdown headings** (`##`, `###`) instead of custom components.
3. **Use fenced code blocks** for all code examples. Do not use the old `<CodeBlock>` component.
   - `csharp` for ShardScript source (Mintlify maps this to a C#-style grammar).
   - `cpp` for C++ / `.shard.cpp` native library code.
   - `bash` for shell commands.
   - `cmake` for CMake.
4. **Use Mintlify callouts:** `<Info>`, `<Warning>`, `<Tip>`, `<Note>`.
5. **Use `<CardGroup>` and `<Card>` for related-link grids** when appropriate.
6. **Tables** use GitHub-flavored Markdown tables. Escape pipe characters (`\|`) and angle brackets (`&lt;`, `&gt;`) inside table cells when they are not inside backtick code spans.
7. **Link to source files** in Reference pages using stable GitHub URLs when possible.

## Native library conventions

- A ShardScript native library is **any** shared library (`.dll`, `.so`, `.dylib`) that exports `ShardLib_GetMetadata` and `ShardLib_EntryPoint`.
- It can be built from one or many C++ source files, inside `ShardScript.Framework` or in a separate project.
- It links against the ShardScript runtime shared library and uses headers from `ShardScript/include`.
- Do **not** describe a native library as "a single `.shard.cpp` file discovered by the framework CMake glob." That is one convenient build integration, not a requirement.
- Avoid conditional library members (namespaces, classes, or methods registered only when a condition is met, such as the presence of another library, a file, or an environment variable). They are technically possible and allowed, but they create uncertainty in the library surface and gaps in documentation.

## See also / Related articles

Reference, How-To, Tutorial, and Concept pages must end with one of the required closing sections above. Give the reader at least one concrete next step — a related article, an exercise, or a link to the source.
