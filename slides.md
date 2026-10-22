---
theme: ./theme
colorSchema: light
title: Wiring Up an AI-Native Testing Workflow
author: Filip Hric
transition: none
drawings:
  persist: false
---

# Wiring Up an<br>AI-Native Testing<br>*Workflow*

CypressConf 2026

::image::

![Editorial collage of a hand wiring a computer to task instructions, code, and a tested software package.](/images/cover/testing-workflow.png)

---

# 4 levels of AI engineering

<div class="engineering-levels">
  <figure v-click>
    <img src="/images/ai-engineering/ai-chat.png" alt="Paper collage of a computer with two speech bubbles and a hand at the keyboard" />
    <figcaption>AI chat</figcaption>
  </figure>
  <figure v-click>
    <img src="/images/ai-engineering/ai-enabled-ide.png" alt="Paper collage of a developer typing in an editor with a highlighted AI code suggestion" />
    <figcaption>AI enabled IDE</figcaption>
  </figure>
  <figure v-click>
    <img src="/images/ai-engineering/coding-agents.png" alt="Paper collage of a computer turning task sheets into checked code through a feedback loop" />
    <figcaption>Coding agents</figcaption>
  </figure>
  <figure v-click>
    <img src="/images/ai-engineering/software-factories.png" alt="Paper collage of mechanical arms producing checked software packages on a conveyor belt" />
    <figcaption>Software factories</figcaption>
  </figure>
</div>

<!--
- I want to start off by what I really mean by AI-native testing
- obviously AI has made it to our workflows these days, the question is how much
- I like to think of 4 levels of AI engineering
- there’s a chance you are in the first 3 categories right now - and to be really sucessful in these, we need to talk about some fundamentals
-->

---

# Workshop outline

1. Context engineering
2. Rules
3. Skills
4. MCPs
5. Putting it all together

---
layout: section
---

# Context engineering

---
src: ./pages/context-engineering.md
---

---
class: compaction-settings
---

# Compaction thresholds

<div class="compaction-options">
  <section>
    <h2>Claude Code</h2>
    <div>
      <code>/autocompact 100k</code>
      <p>Set the automatic compaction window for the current model.</p>
    </div>
  </section>
  <section>
    <h2>Codex</h2>
    <div>
      <code>model_auto_compact_token_limit = 100000</code>
      <p>Set at the top level of <code>~/.codex/config.toml</code>.</p>
    </div>
  </section>
  <section>
    <h2>Cursor</h2>
    <div>
      <code>/summarize</code>
      <p>Compact manually. The automatic threshold is not configurable.</p>
    </div>
  </section>
</div>

<p class="compaction-note">100,000 tokens is an example, not a universal recommendation.</p>

<!--
100,000 tokens is an example, not a universal recommendation. Choose a limit for your model and task.

Claude Code: /autocompact saves a model-specific setting and applies it to the current session.
The window is capped at the model's context window. /autocompact auto restores the tuned default.
Older versions can use CLAUDE_AUTOCOMPACT_PCT_OVERRIDE to lower the percentage where applicable.
Source: https://code.claude.com/docs/en/model-config#set-the-auto-compact-window
Source: https://code.claude.com/docs/en/env-vars

Codex: the value is an absolute token count, not a percentage. Unset uses model defaults.
Source: https://learn.chatgpt.com/docs/config-file/config-reference

Cursor: its automatic threshold is controlled server-side, per staff guidance dated July 20, 2026.
Run /summarize while the agent is idle. Current release notes also document /compact as an alias.
Source: https://forum.cursor.com/t/auto-summarization-triggers-too-late-model-quality-degrades-long-before-the-context-limit-context-rot/166182/5
Source: https://cursor.com/docs/release-notes
Verified: 2026-10-21.
-->

---
layout: illustration
class: demo
---

# Demo

::image::

![Editorial collage of a hand placing a red play symbol over a laptop and a rules sheet.](/images/context-engineering/rules-demo.png)

<!--
- show login test with Login component attached
- claude code - write test for creating a new board

https://code.claude.com/docs/en/context-window#what-survives-compaction
-->

---
layout: section
---

# Rules

<!--
Primary source: ../assets/blog/creating-rules-that-stick.md
Supporting source: ../assets/presentations/test-automation-workflows/pages/07-rules-files.md
Presentation followed by a codebase demo; demo steps pending.
-->

---
src: ./pages/rules.md
---

---
layout: schematic
---

# Generation and verification

A coding agent uses Skills, Rules, Ticket, and Docs to write code. A separate code review agent checks that skills were applied, rules followed, the ticket satisfied, and the docs remain consistent. Code flows to review; feedback returns to the coding agent.

::image::

![Editorial paper diagram: a coding agent uses Skills, Rules, Ticket, and Docs. Code flows to a separate code review agent, which checks Skills applied, Rules followed, Ticket satisfied, and Docs consistent. A red feedback arrow returns to the coding agent.](/images/generation-verification/generation-verification.png)

---
layout: section
---

# Skills

---
layout: illustration
---

# Skills in practice

- **Create your own** for repeatable workflows
- **Skills + CLI**: [Cypress TAP](https://docs.cypress.io/app/tooling/cypress-tap)
- **Find existing skills** on [skills.sh](https://skills.sh)

::image::

![Editorial collage of a hand inserting a skill instruction card into a laptop running a CLI, with reusable instruction cards and a checkmark.](/images/skills/skills-in-practice.png)

<!--
Illustration generated with built-in image_gen. Prompt: ./public/images/skills/prompt.json.
- Capture a workflow you repeat as a skill, with the instructions and supporting resources the agent needs.
- A skill can teach the agent how to use a CLI. The cypress-tap skill drives a running Cypress open session to run specs, inspect results, and debug failures.
- Browse skills.sh for existing skills.
Sources:
https://docs.cypress.io/app/tooling/ai-skills
https://docs.cypress.io/app/tooling/cypress-tap
https://skills.sh
-->

---
layout: illustration
class: demo
---

# Demo

::image::

![Editorial collage of a hand placing a red play symbol over a laptop and an instruction sheet.](/images/context-engineering/rules-demo.png)

<!--
- skills.sh + cypress tap installation
- show mailosaur (next slide)
- generate skill
-->

---
layout: schematic
---

# Email testing with Mailosaur

::image::

![Editorial collage: a Cypress test uses test@abc123.mailosaur.net in the app, which sends email to a dedicated Mailosaur inbox with ID abc123. The test retrieves the message with cy.mailosaurGetMessage and asserts its subject, body, links, and codes. SMS testing uses a dedicated number; TOTP testing generates a code from a shared secret.](/images/mailosaur/email-testing-collage.png)

---
class: skills-quote
---

<div class="skills-quote-grid">
  <div>
    <blockquote>“AGENTS.md define intent,<br>RULES.md define boundaries,<br>SKILLS define execution”</blockquote>
    <p class="skills-quote-attribution">Itamar Friedman, Qodo</p>
  </div>
  <img src="/images/skills/itamar-friedman-editorial.png" alt="Editorial photographic portrait based on the supplied photo of Itamar Friedman." />
</div>

<!--
Quote and attribution supplied by the presenter.
Portrait generated with built-in image_gen from /Users/filiphric/Desktop/image (1).png.
Full prompt: ./public/images/skills/portrait-prompt.json.
-->



---
layout: section
---

# MCPs

---
layout: schematic
---

# How MCP adds tools

::image::

![Editorial collage sequence diagram with client on the left, MCP server in the center, and LLM on the right. The client discovers tools, shares definitions with the LLM, executes its tool request, and returns the result.](/images/mcp/client-server-llm-collage.png)

<!--
MCP gives the agent a menu of tools it can call.

1. The MCP server lists each tool’s name, purpose, and inputs.
2. The agent app makes those definitions available to the model.
3. The model picks a tool and supplies the inputs.
4. The app calls the server and returns the result to the model.
-->

---
layout: illustration
---

# Putting it all together

::image::

![Editorial collage of project instructions and external tools wired into a laptop, producing checked software through a feedback loop.](/images/putting-it-together/putting-it-all-together.png)

<!--
Bring context, rules, skills, and MCP tools together in one workflow, then verify the output.
Illustration generated with built-in image_gen. Prompt: ./public/images/putting-it-together/prompts.json.
-->

---
layout: illustration
class: demo
---

# Demo

::image::

![Editorial collage of a hand placing a red play symbol over a laptop and an instruction sheet.](/images/context-engineering/rules-demo.png)

<!--
https://github.com/filiphric/cypressconf-2026/actions/runs/39501121300/job/118898572640
-->

---
layout: schematic
---

# Generation and verification

A coding agent uses Skills, Rules, Ticket, and Docs to write code. A separate code review agent checks that skills were applied, rules followed, the ticket satisfied, and the docs remain consistent. Code flows to review; feedback returns to the coding agent.

::image::

![Editorial paper diagram: a coding agent uses Skills, Rules, Ticket, and Docs. Code flows to a separate code review agent, which checks Skills applied, Rules followed, Ticket satisfied, and Docs consistent. A red feedback arrow returns to the coding agent.](/images/generation-verification/generation-verification.png)


---
layout: schematic
---

# Verification at every step

::image::

![Editorial collage of verification at four stages: Issue, Plan, Uncommitted code, and Pull request. Each stage has its own review question. A left-pointing arrow emphasizes earlier feedback.](/images/putting-it-together/shift-left-verification.png)

<!--
Adapted from /Users/filiphric/tester-2/components/ReviewAtEveryStep.vue
and /Users/filiphric/tester-2/pages/things-to-abandon.md, "Review at every step".

- Waiting for pull request review leaves a wide feedback loop.
- Review uncommitted code locally to catch problems before a commit.
- Review the plan against the issue and the current codebase before implementation.
- Review the issue itself: are the requirements clear and complete?
- These checks bring feedback earlier. Keep testing the application as part of the workflow.
- The source labels the first stage Ticket; this slide uses Issue.

Illustration generated with built-in image_gen. Prompt: ./public/images/putting-it-together/prompts.json.
-->

---
layout: illustration
---

# Thank you!

Filip Hric

[filiphric.com](https://filiphric.com)

::image::

![Filip Hric in the editorial portrait from filiphric.com.](/images/thank-you/filip-hric.png)

<!--
Portrait from https://filiphric.com/about
Original asset: https://res.cloudinary.com/dcnwsgh7c/image/upload/e_background_removal/f_png/q_auto/v1/site/editorial/20261019/about
-->

