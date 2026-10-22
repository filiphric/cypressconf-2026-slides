---
layout: schematic
---

# The context window

A finite working space for the model.

::image::

![An empty rectangular context window with a fixed boundary.](/images/context-engineering/finite-window-collage.png)

<!--
- we are going to start with the context window
- this context window has a limit, you can almost think about this as a RAM on your computer and you’ll see why
-->

---
layout: schematic
---

# The first exchange

Your prompt and the reply both occupy context.

::image::

![User message and agent message paper blocks occupy the top of a colored context rectangle.](/images/context-engineering/first-exchange-collage.png)

<!-- 
- you start off by sending a message to your agent, and then agent responds back
- so far, nothing unexpected
-->

---
layout: schematic
---

# Conversation history

Each turn carries the history forward, along with the new message.

::image::

![Six alternating user and agent message blocks fill the context window, bracketed as conversation history.](/images/context-engineering/conversation-history-collage.png)

<!-- 
- however, as the conversation continues, what you are sending to the LLM is not just your next message, but the whole conversation
- LLM is stateless, so it doesn’t store your conversation, instead it tries to complete the conversation based on what came before - you send it the available history, and it calculates the rest
- so as the conversation gets longer, the amount of data that you are sending is getting longer too
- however, this is not really a data problem, it’s the context window problem
- i said that the context window is sort of like a RAM - there is a limit on how much data can LLMs operate on at once, just as your computer has it’s limit
- but this is as if the your computer starting making more random mistakes when you have too many chrome tabs open
-->

---
layout: schematic
---

# Capacity and recall

Fitting more context does not guarantee reliable recall.

::image::

![GPT-5.4 MRCR v2 8-needle accuracy line graph: 97.5, 93, 95, 90, 86, 79.5, 57.5, and 36 percent across eight context ranges from 4–8K to 512K–1M tokens.](/images/context-engineering/capacity-and-recall-collage.png)

<!-- 
- and this is a problem that’s there by design
- some LLMs claim that they have context window as big as 1 million tokens, but I’m skeptical
- just because the LLM is able to take in many tokens, it doesn’t automatically mean they are able to operate well with them
- there are different benchmarks for this, and a popular one is "needle in a haystack"
- when Anthropic and OpenAI update their models to take in more tokens, they usually use these benchmarks to show how they perform
- however, some critics say that even performing well in this benchmark doesn’t mean that the model is better at finding the needle, it’s just a bigger haystack they operate on
- this graph reproduces the data shown in the original LongContext.webm: GPT-5.4 MRCR v2, 8-needle benchmark, dated March 5, 2026
- accuracy by context range: 4–8K 97.5%; 8–16K 93%; 16–32K 95%; 32–64K 90%; 64–128K 86%; 128–256K 79.5%; 256–512K 57.5%; 512K–1M 36%
- source attribution in the original: OpenAI GPT-5.4 eval table, MRCR v2 8-needle; this is a reproduction of the supplied chart, not a fresh benchmark verification
-->

---
layout: schematic
---

# Focused context

Start a fresh session with the task and the relevant context.

::image::

![A context rectangle divided into a teal smart zone and a red dumb zone; conceptual zones with no fixed threshold.](/images/context-engineering/focused-context-collage.png)

<!-- 
- if you’re hoping to get most out of your AI agent, you need to stay in a so-called smart zone
- this is an area where your conversation is failry short, LLM has no trouble making connections, understanding your tasks, it has a good idea about which files you’re working with and so on
- basically, when you start interacting with your agent, whether this is Cursor, Claude Code or chatGPT, you keep track of how long the conversation is, how much data the LLM has to deal with
- with shorter conversations you can expect less errors, better performance
- open a new chat, launch sub agents, split your work into smaller tasks and use a separate context window for each, you can use spec driven development, where each spec works in it’s own context window, heck you can even use a ralph loop if you want
- but of course, there’s another problem space we need to deal with - how to teach our agent about the specifics of our project, we cannot start totally fresh everytime we want to write code, can we?
- well of course not (this is where project rules, AGENTS.md, and SKILL.md files come into play)
-->

<!--
Illustrations generated with the built-in image_gen tool. Full revised prompts: ../public/images/context-engineering/collage-prompts.json.
-->
