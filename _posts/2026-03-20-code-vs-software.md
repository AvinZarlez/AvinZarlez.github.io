---
title: "Code vs. Software: The Vocabulary I Rely On When Talking About AI‑Assisted Development"
categories:
  - Blog
tags:
  - Code
  - Software
---

I spend a lot of my time explaining technology to people who have fundamentally different ideas of software and code. From engineers deep in the implementation details, to leaders trying to understand the development workflow, and everyone in-between.

We often use the words **“code”** and **“software”** as if they are interchangeable. In casual conversation, that usually works. In technical planning and when talking about AI-assisted development, it creates subtle misunderstandings that turn into very practical problems. Mismatched expectations, unclear “done” definitions, and teams talking past each other about what to deliver, or worse, what has or has not already been delivered.

A single Python file is unambiguously **code**. When code becomes **software** depends on something much larger than the file itself. When it expected to be used, how does it behave when pushed to its boundaries, how it’s packaged and run, how it’s tested, how it’s documented, and—most importantly—how it will be maintained when requirements and environments inevitably change.

I’ve written both code and software professionally for dozens of different industries over my career. When I say professional, I explicitly mean something that had to survive outside of my controlled development environment, used by people when I am not around, expected to be used long into the future. My experiences have made me increasingly strict about vocabulary—not just because I enjoy pedantry—but because precise language prevents confusing and expensive ambiguity.

The AI era has made this distinction even more important. AI can generate a lot of code quickly. But the real engineering question is often: **did we generate code, or did we build software?** The difference determines how we test, ship, secure, operate, and maintain what we create.


## **Code is an artifact. Software is a capability.**

I want to anchor this discussion in something other than my intuition. Not because standards are perfect, but because they are _deliberately written_ to reduce ambiguity.

IEEE’s software engineering glossary defines **code** narrowly, as a representation of instructions and data:

> “**Computer instructions and data definitions expressed in a programming language or in a form output by an assembler, compiler, or other translator.**”
> — ISO/IEC/IEEE 24765:2010 ([PDF](https://cse.msu.edu/~cse435/Handouts/Standards/IEEE24765.pdf))

That is exactly how most engineers use the word “code” when they are being precise: source files, compiled forms, scripts, and the literal text or artifacts that drive computation. Code is concrete. It can be copied, diffed, refactored, and compiled.

But when we move to definitions of **software**, the scope expands. In ISO/IEC/IEEE vocabulary, software includes more than programs:

> “**All or part of the programs, procedures, rules, and associated documentation of an information processing system.**”
> — ISO/IEC/IEEE 24765:2010 ([PDF](https://cse.msu.edu/~cse435/Handouts/Standards/IEEE24765.pdf))

I like these definitions because they make two points explicit.

First, software is not “code only.” It includes procedures, rules, and documentation—things that are essential if the capability is meant to exist outside one person’s head.

Second, software is framed “of an information processing system.” That phrase quietly implies environment and context. Not just what instructions the computer executes, but how it is run, what it depends on, and what it means for it to behave correctly.

This is the key conceptual split I use in practice:
- **Code** is the artifact I can point to.
- **Software** is the capability I can deliver and sustain.


## **The moment code becomes “software”: the product test**

This topic feels philosophical because the boundary between “code” and “software” is not a single line, it’s a gradient. Prototypes become tools, tools become products, products become systems, and systems become platforms.

Frederick Brooks captured the core of this transition in _The Mythical Man‑Month_. When he distinguishes a program from a “programming product,” he describes a program that has been made robust for other people:

> “**This is a program that can be run, tested, repaired, and extended by anybody.**”
> — Brooks, _The Mythical Man‑Month_ (“The Tar Pit” excerpt) ([PDF](https://www.tup.tsinghua.edu.cn/upload/books/yz/102352-01.pdf))

If “anybody” needs to be able to run it, the code must be packaged, dependencies must be controlled, and execution must be repeatable. If “anybody” needs to test it, you need a test strategy that is not purely institutional knowledge. If “anybody” needs to repair it, the system must be diagnosable—logs, error messages, reproducible failures, and enough structure that debugging is tractable. If “anybody” needs to extend it, the design must be understandable and the interfaces stable enough to build on.

This is not to say "code" can't be useful but carries different expectations.


## **Time is the real interface**

In the day-to-day rhythm of building systems, the “act of writing” is often a smaller fraction of the work than people expect—especially who think *vibe coding* will replace the need for most developers. Software must evolve, be supported, and remain correct under changing constraints.

Google’s _Software Engineering at Google_ expresses this distinction almost perfectly:

> “**Software engineering is programming integrated over time.**”
> — _Software Engineering at Google_ ([Chapter 1](https://abseil.io/resources/swe-book/html/ch01.html))

And in the same chapter:

> “**Programming is the immediate act of producing code. Software engineering is the set of policies, practices, and tools that are necessary to make that code useful for as long as it needs to be used and allowing collaboration across a team.**”
> — _Software Engineering at Google_ ([Chapter 1](https://abseil.io/resources/swe-book/html/ch01.html))

If you’ve ever returned to code you wrote six months ago and felt like it was written by a stranger, you already understand why time changes everything. Now scale that effect across a team, across multiple releases, across customers, and across platforms—and you have a very practical reason why not all "code" is “software."


## **The hardest part is not the syntax**

At this point, I may sound repetitive saying software is “code plus documentation and operations.” That is true but also understates the more fundamental point: If you use code when what you need is software, you may not realize what is missing until after negative consequences.

This is why this distinction is important in AI discussions. Code generation is accelerating the act of typing. We can celebrate that, but we should not pretend the conceptual work disappears. If I am trying to construct a process, a repeatable system used in business, that can't just be built upon a piece of *code*.

Whether that code was handwritten by a human or an AI. If it is going to be part of your normal flow of business, a human needs to understand what exactly is happening. How the system could behave under edge cases. Know what should happen if it fails. We need to be careful not to confuse “more code” with “more software.”

There is a reason "Works on my machine" is a saying. I have seen so many times someone in a project meeting or standup claim something is "Done", only for it to come out that it wasn't. Not by the professional standards of software I have explained here. It is easy for someone without experience to think that because the code exists, runs, and maybe even accomplishes the required task, that the task is "done." Teams need to be clear and up front with what their shared definition of done entails, and what is required to make code robust and stable enough to become part of **software**.


## **What AI changes: the bottleneck shifts from writing to verifying**

When I explain AI-assisted development to teams, I try to avoid a simplistic “AI helps you write code faster” narrative. That can be true, but it is also incomplete. AI shifts the bottleneck. When code is produced quickly, the cost of _verification_ becomes more visible. You can generate ten variations of a function in seconds, but you cannot responsibly ship ten variations without understanding what they do, how they fail, how they interact with the rest of the system, and whether they introduce new security or reliability risk.

I can tolerate a different level of rigor when I am writing code myself. I can understand a goal in my head without having each metric of quality thoroughly documented and described in the project management tool. I would be embarrassed to make a pull request with code that only works on the "happy path" and breaks if something unexpected comes up. AI doesn't have this kind of rigor. Even if you write out strict agent guidance explaining everything that needs to be accounted for, you quickly get to the point where the context of the AI gets overloaded and things might get missed.

It's much more effective to send out an agent with narrow and specific context and instructions than to try and teach it everything a mid-level or senior engineer would naturally understand and think about. Treat it as a junior developer that needs constant supervision. Junior engineers are valuable! It's a good thing for your team to have senior engineers spend most of their time supervising junior ones. They often come up with solutions a senior engineer may not have even considered. That doesn't mean you'd ever trust a junior engineer to ship something that will be used by someone else without that supervision and guidance.

AI doesn't change the need for junior engineers. It makes it more important than ever to train humans to step into that senior role. To understand the strengths and weaknesses of systems. To not just focus on finding a solution as quickly as possible but determining exactly what questions they need to be asking in the first place.

Where AI code generation can greatly enhance a pipeline is helping developers ensure they are following **software** engineering best practices in their work. Not just automated checks to ensure unit tests exist, but tasking agents to implement robust unit tests for all the edge cases the developer can think of. A developer can use AI to thoroughly ensure all functions have in-code documentation comments, helping future developers understand what was implemented and why.

These are processes that should always be practiced, but the reality of the real world is that often we don't have the time to check all these boxes while trying to remain agile and move at a fast pace. Agents can flesh out and run tests while a developer's attention can shift towards breaking down the next few tasks. The inflexibility of AI can be leveraged as a strength when given the right kinds of narrow well-defined tasks.


## **A clearer way to describe what AI is actually doing**

One reason teams talk past each other is that “AI-assisted development” can mean several different things. I’ve found that clarity improves immediately when I name _which layer_ is being accelerated.

Sometimes AI is accelerating the creation of code artifacts: a function, a snippet, a script, a refactor. That can be a real value, especially for individual workflows and prototypes.

Other times, AI are set to integration or productization tasks: identify API usage patterns, proposing changes required by dependency upgrades, creating scaffolding for packaging, generating documentation or example usage. The artifacts produced here could still generally be considered “code" taken in isolation, but it begins to touch the boundaries of producing software as things come together. Again, there can be value that AI can help here, but it doesn't happen automatically.

If you leave the AI to make up what it thinks it needs, it won't architect proper software. If you take a junior engineer and put them "in charge" of an even more junior AI agent, quality code can be produced. However, the guidance of a senior developer will be needed to guide exactly what and how the AI is prompted.

Instead of saying something was *vibe coded*, be precise with your language. For example:

- “AI produced a prototype implementation.”
- “AI drafted documentation and tests, and then humans verified them.”
- “AI helped structure the design, now we need to validate behavior under real inputs.”

Those statements are not just more honest, they are more actionable. They tell you what work is complete and what work remains.

If we’re clear about the boundary between code and software, we can make better decisions on where and what AI can safely be incorporated into our work, what must be validated by human, and what “done” truly means in terms of production ready deliverables.


## References Used
    
- ISO/IEC/IEEE 24765:2010, _Systems and software engineering — Vocabulary_ ("code" and “software”) — [PDF](https://cse.msu.edu/~cse435/Handouts/Standards/IEEE24765.pdf)
- Frederick P. Brooks, _The Mythical Man‑Month_ excerpt (“The Tar Pit”) — [PDF](https://www.tup.tsinghua.edu.cn/upload/books/yz/102352-01.pdf)
- _Software Engineering at Google_ (Abseil web edition), Chapter 1 — [Link](https://abseil.io/resources/swe-book/html/ch01.html)
