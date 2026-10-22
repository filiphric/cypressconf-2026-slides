# Rules files

- General project instructions: `AGENTS.md` and `CLAUDE.md`
- Scoped rules: instructions for a particular part of the project
- Cursor: `.cursor/rules/*.mdc`
- Claude Code: `.claude/rules/*.md`

<!--
Source: ../../assets/blog/creating-rules-that-stick.md, "What I mean by rules" and "Every tool handles them a little differently".
Supporting source: ../../assets/presentations/test-automation-workflows/pages/07-rules-files.md (section title only).

- rules give the agent project instructions we would otherwise repeat in chat
- some apply across the project, others only matter for a particular task or set of files
- different tools have different locations, metadata and triggers
- sharing the same repository does not guarantee that every tool loads the same instructions
- these are instructions to the model, so we still need to check what it does with them
-->

---

# What belongs in a rule

What does the agent need to know that it **can't easily find in the project**?

- Team decisions and the reasons behind them
- A particular way to seed the database
- Conventions that differ from the obvious approach

<!--
Source: ../../assets/blog/creating-rules-that-stick.md, "What you put in the file matters".

- the useful question is what the agent cannot easily discover for itself
- telling it that the project uses React adds little when package.json already tells it that
- a database might have five ways to seed it, but our team chose one for a reason
- that reason may not be traceable from the code, and that is useful context to write down
- the article discusses mixed research results, so avoid claiming that more rules always improve performance
-->

---
layout: illustration
class: demo
---

# Demo

::image::

![Editorial collage of a hand placing a red play symbol over a laptop and a rules sheet.](/images/context-engineering/rules-demo.png)

<!--
```
# Cypress test conventions

- Use `data-cy` or the app's existing `data-test-id` attributes to interact with elements. Avoid CSS classes, positional selectors, and DOM structure selectors.
- Wait for the relevant network request with `cy.intercept()` and an alias instead of using fixed delays such as `cy.wait(1000)`. Register the intercept before the action that triggers the request. Use retryable Cypress assertions to wait for UI state.
- Keep tests independent: each test creates the data it needs and cleans up the data it creates. Prefer API calls for setup and cleanup when those steps are not the behavior under test. Never depend on data left by another test or delete unrelated data.
```
-->

---

# Loaded does not mean followed

- Rules compete with conversation history and tool results
- Conflicting instructions leave the agent to resolve the ambiguity
- Compaction changes the context available to the agent
- Outdated rules make each of these problems worse

<!--
- I used to assume that getting a rule into the context window was enough
- but the file can be loaded and still have no effect on the task
- think back to the context window: rules compete with code, old plans and tool output
- if two rules pull in different directions, the agent may make a choice without asking us
- after compaction, do not assume every scoped instruction is still available
- a markdown instruction is guidance, not a guarantee
-->
