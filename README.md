# What's the next big thing
- AI
- Crypto
- Quantum computing
- Telegramm Apps
- computational biology/genetics
  
## New era of programming is coming. 

Previously we have several software development revolutions:
* Machine code -> Assembly
* Assembly -> "C"
* People were waiting for "N+1 generation languages" but they do not really ever come. (Do not remember what the N was)
  
At every stage people were afraid of losing control -> so getting less efficiency. The result was that while some efficiency was lost we got way more productivity which compensates for a lost control. Critical areas where using previous generation aproach was indeed still justified were very limited (one do very little ASM programming in the era of C++).  

So, now we can get a totaly new way, which may be that "N+1 generation language" dream finaly come true.

How it can work in future:

1. LLM as program generator: Programm in natural language (prompt) --[LLM]-> Program in Python/C++/... --[Compiler/Interperter]-> Machine code
2. LLM as interpreter: Prompt --[LLM]-> action
3. Hybrid: LLM as program generator + LLM as interpreter
4. LLM as compiler: Programm in natural language (prompt) --[LLM]-> Machine code

### Analyzis option 1: LLM as program generator
Will we get enough productivity boost for option (1) to became mainstream? Currently it seems like LLM require very exact instructions much too often, and using "regular" programming language is a very good way to express ones ideas in precise way. May it be that we do not get any success from "N+1 gen language" because we are actually quite close to be able to explain our orders for computer in precise manner so we can not compress representation much without losing precision to unacceptable level? Human language does carry a degree of uncertanty which can prevent us building 

### Analysis option 2: LLM as interpreter
Will we go to (2) so to LLM as interpreter. Like we build a new "proper" level of virtualization, we command system to do something at natural language and it just do it. Now LLM is our "processor" and programming language is just any human language. Including Python/C++, why not?

I do not think it will be a good idea for all aplications. Humans are not good at doing precise bit operations, and likely AI systems will share this as well.
Where we need precision above all (so, bad for AI interpreter kind of system)
* counting one's money in a bank
* decoding stream of vehicle telemetry from Hostlog messages to HDF5
* Solving LP problems
* Calculating Fourier transformation

Where human-like system can win:
* finding ad_adas decoder executable in an archive provided by Zensact, including, if neccesary, asking Zensact WTF they have done and how to differentiate between different decoders
* parsing large text logs
* recognising santiment of a text
* Generally, not well-defined problems with vague definitions and no clear way to provide exact solution rules

### Analysis option 3: Hybrid
It seems like an mixed system can offer best of both worlds:
* use LLM as program generator to generate code where we want to be precise
* embedd AI agents for ill-defined subtasks

### Analysis option 4: LLM as compiler
Seems like this is exaclty a weakly-sutable for AI problem, as it is exactly an excersise in precise manipluation of bits. But, probably, many steps of compilation/optimization can benefit from AI code analysis. 

## Problems in current approach
- Prompts are lost, but often retried
- I spend a lot of time trying to change prompts, finaly [found a trivial bug | implemented myself much faster]
- can't handle large code:  I've had ChatGPT lose track of the goal with larger endeavours and had to rebuild the same script twice. I've found that combining LLMs for writing with "chunking" techniques (e.g. writing code in small sequential pieces in Zapier) to be an effective technique for getting around this problem. This way, you can build a chunk and test it, before it's gone from the LLM's memory.
- can generate repeated code instead of creating and calling functions
- When an agent starts getting confused and doing really daft things, it's probably best to start a new session with fresh context.
- Make sure your prompts give clear rules about how to work with your project. Best if your rules are codified and enforced.
- When agent is doing changes, human sees low-level changes to codebase, not neccessary in logical order. It is thus can be hard to understand what agent is about to do, and change a direction of his action if human disagree.
### Problems "classical" approach
- One often have a situation when intention of a code is not clear. We have some logic (or some test), but why it is here? What was the reason behind it? Was there any reason at all, or this was some random implementation twist/error. Often this is lost/forgotten. If we will fix intentions in specification this can resolve that problem.  
## Approaches currently used with Vibe coding tools 
### 1
You are right. Some tactics that help - 
1) use either another AI tool to plan out the project structure in advance (Grok/Claude are good for this); then use coding tool to build step by step.
2) in the coding tool, limit each prompt request to a very small change in codebase and after each implementation ask AI to explain the implementation to you and also ask it for any potential bugs.
3) when stuck in a circular loop bug hole, use another coding tool to debug. Load the project in cursor/windsurf and ask for help.
### 2
Take 1: After dense codebases, i find it still works if you chunk up the tasks to tackle into medium or bitesized - which is kind of what it is meant for today on the newer models.

Example: add endpoint, or script, that does Y, in location X. Do/don’t use A, B, C. Or, “get going on this file/folder’s test suites”.

I find it’s still very good at spinning up infrastructure and handling CICD.

Take 2:
If you’re looking for specific outputs requiring high levels of consisten accuracy; i’ve noticed it becomes 2-3x efficient if you essentially re-inforce it yourself and generate samples of good and results for the LLM as files. If you ask it to analyze those final results, and prompt well, i’ve managed to get the LLM to produce a very robust system. This isn’t toil-less, but it’s where we’re at at the moment without training your own fine tuned model
### 3
I now use AI for everything, don't even type any more, but it's like being in constant architect / code reviewer mode. You still have to be very involved with the code, and question the machine constantly.

Small modules, full test coverage, and knowing when to interrupt it with extra context is key.

Don't architect and implement in the same session. when implementing, make sure the agent keeps progress notes so another agent can continue a task with context if necessary. 
### 4
I started by writing a requirements doc with a level of detail similar to what I would have expected to hand off to a junior engineer. These requirements were as detailed as I could make them, including components I wanted it to create, how they should behave and validate, and examples of inputs and expected outcomes.

Then I asked it to break my requirements out into deliverable milestones.

Then I had the Cursor agent write each milestone.
### 5
You cannot. The first thing you need to establish a project structure and establish interaction diagram independently from lovable and keep it perfecting till you feel that functionality is well defined and crisp. 

Once done, pass it to lovable. Then, lovable understands what is required. Please note that it has limited context window, so it cannot fit the context window. So, it will generate some extra file. So, you need to reinforce again and again. The best is to ask to code component by component or page by page. You should have a visual model of project structure and interactions. Your design can change but keep the design updated in document as well as interaction diagrams. 

This will be the model for future coding paradigm where there will be design window and coding window and your job is to keep them in sync as AI generates the code. In future, the context partition will emerge within LLM models which helps to act effectively. It's still work in progress.


## General LLM issues
- LLMs seems to not able to keep focus on target during execution of long run
- LLMs are bad at selecting good/promising solutions from generated options (e.g. invent a novel research direction, understand which theorem can be interesting/good to solve)
  
## Approaches/features for next-gen AI Programming

### New Programming Language vs Specification Management System + Workflow
explain workflow
explain what is needed to support workflow

- **what we need is to keep essential information about project structure, intentions behind this structure, etc - look for context that are lost now. That can give an edge in growing large projects, that is not in place now. We need to make it easier, by saving more information about intentions / requirements behind code.**

- how can we make model to look at description first, not implementation? and in general, how to find good context for a task? can tags help? can we test if model ignores extra context of instructed to do so?

### Multi-level approach
- top level: general system requrements / architecture and diagramms / "pattern level" / class level / function level / loop|operator level
- we should be able to drill down at places where our top-level instructions do not result in correct operation of a system
- UI should allow easy control over level at which we are looking at code (example: test purpose <-> detailed test description <-> test code ), switching between abstraction levels should be as easy as zooming.
  * given that we have many parents and many descendents for documents, it is not clear which branch this zoom in/out should follow, probably selection from a lists (of parents/descendents) is a way to go.
  * if there is a single descendant/parent we can zoom
  * we can zoom up shortest path to top
- abstractions leak. Will we be able to maintain enough flexibility to bend rules when required?
- if we focus on local changes, how do we know when to do large change? How will we understand if need to escalate a change from local to global?

### Linking to requirements
- Can something like Obsidian link system be used to show documents current one depend on (and they form context for LLM generation)
- How do we refence parts of document (both target and source)?
    * Can it be grammar-aware, e.g. if we reference from a function we only affect context when working with this particular function
    * introduce some "scope setting" comments which will allow to establish some scope structure inside documents using programming language comments + special format inside. Won't that be brittle with version control merges?

### Switch between human and programming language on block-to-block level
- Use llm to translate in both directions Prompt -> PL and PL -> Prompt
- we may have more levels then just "Prompt - PL", see example in "Multi-level approach"
- sorta means we do not believe we will have a new full-scale paradigm
Or just allow embedding of traditional programming language in natural language (but how to embedd for a part of function)

### Dynamic dependency updating
Let's say we created a description of a function, and system generated corresponding code. If we see that code is not what we want, it could be good if we then add more requirement to the description and immidiately see how code is changed to reflect this requirement, so we can rapidly adapt requirements on a fly to get to required state fast.
- some light LLM can be used to determine if user input is complete to trigger code regeneration
- could be used with autocompletion feature accepting corrections through voice input (but then we risk loosing some content which was audio only - where should it go?)
- how this could work if we have several levels down current one, or several documents on the same level? How this can be displayed?
- how it works in UP direction?
- should we have a dedicated mode we enter to activate it, and then confirm/reject changes we get?

### Prompt generator/editor
- Prompts are often reused, say one can have prompts for "generate PRD", "generate architecture", "define tests needed", "generate detailed test data", "generate test code", "generate class implementation", etc.
- But exact wording can depend on situation and likely can't be simply addressed by just having a parameter inserted in a prompt.
- A "smart" propmpt generator can be usefull to
    * extract "generic" prompt out of a partucular prompt used by programmer
    * adapt "generic" prompt to particular situation, e.g. adapt test example generation prompt to exactly what should be covered (depending if data should include state of external systems, do we have input parameters, do we have returned output, do we have exceptions generated - we should not confuse our system to generate values for what we do not have) 

### Dependency tracking and updating
- Real situation:
    * Function docstring was updated with new functionality description
    * Tests descriptions for that functionality were generated
    * Examples of test data was generated
    * Now one can see that wording of functionality was misleading and causing some confusion
-  What is needed:
    * we need to change wording of a function description (in docstring) and regenerate test descriptions and examples.
    * we should consider that test file contains not only affected tests, but other tests as well, so only part should be updated
- Possible solutions
    * version control/checkpoint functionality? Just revert and start over -- good if we have automatic generation process we can start one-click
    * automatic "tree-style chat" solution: one change docstring (again) and it creates a new branch of (auto-generated) depenencies, and than one can navigate between branches. Is this the same as rollback solution? Just tree is hidden inside fine grained version control?

### Current issues with prompt programming / vibe programming
- Seems to rely on comments to keep track of what it is going to do -> Let it do in a structured way
- Do more than asked and do wrong things as result
- Ignores styling preferences -> Should we have code style loaded to context
- it is easy to verify if software works (for some extend :) ), so it is easy to train models to generate code which solves done easy to verify task. However, it is not easy to verify that code is off good quality (subjective), so allow for good maintainability. And here we will likely have a place for human expertise.
- A lot of people comment that typed languages improve agent code generation (typescript vs javascript) - this looks like a confirmation that increasing amount of context improves AI code generation.
- requirements are totaly lost (if only provided in prompts) or put in places where they are not accessed any longer (e.g. using BMAD a lot of useful info is put in user stories only). That's like writing program in C++, compile it, throw away source code, test, rewrite C++ from scratch.
- when using AI code completion user can see that it is heading in wrong direction, but do not have a way to correct it otherwise but by continue typing unless there is enough context here for AI to understand user intend. Would be very nice to have "side channel" input to steer in correct direction.
  - voice input is ideal here
  - can work with text as well, if we have done hotkey to switch between entering code and chatting with AI. But probably too slow for productive work. Maybe useful for debugging.
  - can result in very dynamic pair programming experience.
  - **can be implemented as separate product**
- What is general direction of change, which steps were already completed, what we are doing now, and what are the next steps - thats all critical content which allow agent to better control area of changes. This is still often left out today. So, we need planning. And it should be documented and available for the agent.
- **Everybody is just reproducing existing software development system. Reproduce existing best practices of process (like BMAD), introduce planning, reviews, quality control with external tools, make agents more human-like (learn on mistakes), etc... just make the same thing but faster.** What should be done instead - one need to make things which were not done before, because it was impossible/too expensive to do before. Not repeat the same process but with agents, but intorduce new things. What I propose is ortogonal to what is going on now, and those approaches can complement one another - agent using better programming system will do a work better.  

### Future is a group of specialized agents working together?
- one generates code, another checks "what function arguments should be, of what type and in what order". What kind of questions to we ask ourselfs when we do programming?

### RAG for used libraries
- available in e.g. Cursor
- provide better context v.r.t. libraries used in development.
- solve problems with documentation missing/underrepresented in LLM pretrain data

### ... or retain model?
would it be cheaper to train project-specific model with knowledge of used set of libs instead of adding docs to all prompts? 

### Non-linear generation
- when people write books they do not go from start to finish in one pass. I believe they jump from one place to another and fill details in between, change things, etc.
- can this apply to software development? We may consider top-down approach to be a representation of this: we define general structure and than fill it with details. But sometimes we should backtrack and change decisions on higher lever, or move things around.
- It may make sence to start working deeper on areas which are less clear, so that we clarify them first and if neccesary adjust requirements for things around.

### Keep documentation/requirements in sync with code
- If we keep syncing code with documentation (which provides top-level context on what this code should do and how it should be organised) in both directions, than we will have documentation which is allways up-to-date.
- if code (or any other generated document) is changed by the human. Question is, how do we ensure that this change is persistent when/if document is regenerated -> we should understand and fix in upstream document(s) why this was neccessary, so that concern will be addressed next time automatically: 
  - system should track affected documents (both upstream and downstream) that were not revisited yet
  - system can highlight any contradictions with existing requirements
  - system can propose change to requirements (upsteram document, or whatever we depend on) which should lead to no human intervention needed if code is regenerated. System can try to understand which upstream document is most relevant for addressing this change (what we are changing: business logic, formatting preferences, non-functional requirements?).
  - Possibly new upstream document can be added (e.g. before we did not have style guide)
- documentation should enable agent or human to continue development without need to reevaluate what's going on there, solving problem we have now when we cannot easily return to project we do not touch for a few months and be productive from first minute. That should not be the case any longer. On all levels, both for code, high level targets and everywhere in-between. We should keep all project related information in project itself: ideas, architecture, coffee, deployment. Everything should be in there, so we can continue any discussion or devolvement at any moment. Should we not allow unstructured dialog with AI at all?

### Document-centered AI interaction
- Building on previous idea that everything should be in same form, and that form should be a document, could we build and AI interaction which is in form of documents only, no chat?... Like chat is unstructured and information in it would be most likely lost.
- Do not think that will work. I think it is better to have chat around documents, so that ideas can be discussed and iterated, but final results are in form of a document.
- More pragmatic approach seems to be interliving documents and prompts:
  - we start with some document, e.g. project brief or just initial idea documented
  - than human create a prompt, which tells what kind of document we are going to create next
  - LLM generate that document, e.g. PRD
  - human gives another prompt
  - LLM generate next document, e.g. project architecture
  - there should be opportunity to discuss current document with LLM, making changes (which should be reflected in upstream document(s)).
    - How do we adress situation when LLM asks clarifying questions and user provides answers
      - do we treat those answers as next document(s) in our chain (e.g. prompt was "Do X and ask me questions to clarify if needed", list of questions is a document, user answers are next prompt, whatever LLM create out of it is next document which should document those answers?)
      - or do we create a new upstream document(s) for answers, so they become input to original prompt "Do X and ask me questions to clarify if needed", which is than rerun and produce required document X when no new clarification is needed. That can take several iterations.

### Addressing ambiguity of human language
- human language is ambigious and the only way to combat it is checking result of LLM output up untill we reach level of (more or less) unambigious code. Other approaches are just unresponsible.
- if we see misunderstanding we clarify it by changing/expanding requirements, but one can not be sure that all ambigioty is totaly resolved.
  - maybe regenerate downstream document many times and compare to check that they all match expectations in order to locate any imprecision left in upstream documents?
  - That will requie some automatic difference detection and clustering probably?
  - Should check that differences are not due to LLM ignoring requirements, but due to genuine gaps in them.
  - And a lot of money.

### Refactoring
We can use refactoring tools to change e.g. names of classes, but if we have a lot of context in comments/docstrings, how do we ensure they are updated as well? Can IDE renaming tools be extended to it? Can we run a sort of pararllel language server?
 
### have a tool to query requirements of parts of system
should llm have a possibility to query specifications for a parts of code, which code that it is generated now should interoperate?

# Target audience
AI-enabled development of large software projects with good control by software engineers 
Small projects - will not work, already served well by single-short tools (replit, Claude Code)
Damage that can be done by faulty software is unlimited. We should focus on development at areas where potential damage is high.

- think about exact areas where tighter control over code that can be provided with "throw and regenerate" is actually required. 
## Risks
- will not produce an order of magnitude improvement in productivity of SE (already mentioned in analysis option 1)
- single short will work for large projects (but how will specification/prompt look like?)
    : let's find areas where this will now work due to critical quality requirements.
- AI agents will get AGI and will work exactly like we work now

