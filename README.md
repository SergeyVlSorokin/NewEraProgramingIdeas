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
- abstractions leak. Will we be able to maintain enough flexibility to bend rules when required?
- if we focus on local changes, how do we know when to do large change? How will we understand if need to escalate a change from local to global?

### Switch between human and programming language on block-to-block level
- Use llm to translate in both directions Prompt -> PL and PL -> Prompt
- we may have more levels then just "Prompt - PL", see example in "Multi-level approach"
- sorta means we do not believe we will have a new full-scale paradigm
Or just allow embedding of traditional programming language in natural language (but how to embedd for a part of function)

### Current issues with prompt programming / vibe programming
- Seems to rely on comments to keep track of what it is going to do -> Let it do in a structured way
- Do more than asked and do wrong things as result
- Ignores styling preferences -> Should we have code style loaded to context
- it is easy to verify if software works (for some extend :) ), so it is easy to train models to generate code which solves done easy to verify task. However, it is not easy to verify that code is off good quality (subjective), so allow for good maintainability. And here we will likely have a place for human expertise.

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

### Keep documentation in sync with code
- If we keep syncing code with documentation (which provides top-level context on what this code should do and how it should be organised) in both directions, than we will have documentation which is allways up-to-date.

#### Refactoring
We can use refactoring tools to change e.g. names of classes, but if we have a lot of context in comments/docstrings, how do we ensure they are updated as well? Can IDE renaming tools be extended to it? Can we run a sort of pararllel language server?
 
### have a tool to query requirements of parts of system
should llm have a possibility to query specifications for a parts of code, which code that it is generated now should interoperate?

# Target audience
AI-enabled development of large software projects with good control by software engineers 
Small projects - will not work, already served well by single-short tools (replit, Claude Code)

- think about exact areas where tighter control over code that can be provided with "throw and regenerate" is actually required. 
## Risks
- will not produce an order of magnitude improvement in productivity of SE (already mentioned in analysis option 1)
- single short will work for large projects (but how will specification/prompt look like?)
    : let's find areas where this will now work due to critical quality requirements.
- AI agents will get AGI and will work exactly like we work now

