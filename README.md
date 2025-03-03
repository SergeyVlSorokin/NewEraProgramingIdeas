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
  
## Approaches for next-gen AI Programming

### Multi-level approach
- top level: general system requrements / architecture and diagramms / "pattern level" / class level / function level / loop|operator level
- we should be able to drill down at places where our top-level instructions do not result in correct operation of a system

### Switch between human and programming language on block-to-block level
- Use llm to translate in both directions Prompt -> PL and PL -> Prompt
- sorta means we do not believe we will have a new full-scale paradigm
Or just allow embedding of traditional programming language in natural language (but how to embedd for a part of function)

### Current issues with prompt programming / vibe programming
- Seems to rely on comments to keep track of what it is going to do -> Let it do in a structured way
- Do more than asked and do wrong things as result
- Ignores styling preferences -> Should we have code style loaded to context

### Future is a group of specialized agents working together?
- one generates code, another checks "what function arguments should be, of what type and in what order". What kind of questions to we ask ourselfs when we do programming?

### RAG for used libraries
- provide better context v.r.t. libraries used in development.
- solve problems with documentation missing/underrepresented in LLM pretrain data 
