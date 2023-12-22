# Programming paradigms & types of languages

Programming paradigms are a way to classify programming languages based on their features. One programming language can be classified into multiple paradigms.

Some paradigms are concerned mainly with implications for the execution model of the language, such as allowing side effects, or whether the sequence of operations is defined by the execution model. Other paradigms are concerned mainly with the way that code is organized, such as grouping a code into units along with the state that is modified by the code. Yet others are concerned mainly with the style of syntax and grammar.

According to the criticism section on Wikipedia, some programming language researchers criticize the notion of paradigms as a classification of programming languages, e.g. Harper, and Krishnamurthi. They argue that many programming languages, in reality, include features from several paradigms.

**Degree of coupling and cohesion**

In software engineering, coupling is the degree of interdependence between software modules; a measure of how closely connected two routines or modules are; the strength of the relationships between modules. Coupling is usually contrasted with cohesion. Low coupling often correlates with high cohesion, and vice versa. Low coupling is often thought to be a sign of a well-structured computer system and a good design, and when combined with high cohesion, supports the general goals of high readability and maintainability.

The software quality metrics of coupling and cohesion were invented by Larry Constantine in the late 1960s as part of a structured design, based on characteristics of “good” programming practices that reduced maintenance and modification costs. Structured design, including cohesion and coupling, were published in the article Stevens, Myers & Constantine (1974) and the book Yourdon & Constantine (1979).

> In a nutshell: Tight coupling = more interdependency, coordination and information flow while low coupling = higher organization and modularity.

Among the types of cohesion mentioned on Wikipedia, functional cohesion is considered superior. See also 'perfect cohesion' under [High Cohesion](https://en.wikipedia.org/wiki/Cohesion_(computer_science)#High_cohesion).

Peter Van Roy created a [map](https://upload.wikimedia.org/wikipedia/commons/f/f7/Programming_paradigms.svg) with various programming paradigms. Cited sources are: [Programming Paradigms for Dummies: What Every Programmer Should Know](https://www.info.ucl.ac.be/~pvr/VanRoyChapter.pdf) and the book [Concepts, Techniques, and Models of Computer Programming](https://books.google.gr/books?id=_bmyEnUnfTsC&redir_esc=y)

> **TODO: Read the 2 above sources and update this document.**

As stated previously, just as software engineering (as a process) is defined by differing methodologies, so the programming languages (as models of computation) are defined by differing paradigms. 

"Programming paradigms can also be compared with programming models, which allows invoking an execution model by using only an API. Programming models can also be classified into paradigms based on features of the execution model."

> **TODO: Learn what exactly programming models are and how they relate to paradigms.** Context: Using APIs, parallel computing and the below paragraph. Not much is listed on the [Wikipedia article](https://en.wikipedia.org/wiki/Programming_model)

For parallel computing, using a programming model instead of a language is common. The reason is that details of the parallel hardware leak into the abstractions used to program the hardware. This causes the programmer to have to map patterns in the algorithm onto patterns in the execution model (which have been inserted due to leakage of hardware into the abstraction). **As a consequence, no one parallel programming language maps well to all computation problems**. Thus, it is more convenient to use a base sequential language and insert API calls to parallel execution models via a programming model. Such parallel programming models can be classified according to abstractions that reflect the hardware, such as [shared memory](https://en.wikipedia.org/wiki/Shared_memory "Shared memory"), [distributed memory](https://en.wikipedia.org/wiki/Distributed_memory "Distributed memory") with [message passing](https://en.wikipedia.org/wiki/Message_passing "Message passing"), notions of _place_ visible in the code, and so forth. These can be considered flavors of programming paradigm that apply to only parallel languages and programming models.

---

## Unstructured vs Structured

**Non-structured programming** is the historically earliest programming paradigm capable of creating Turing-complete algorithms (citation needed). It is often contrasted with the structured programming paradigm, in particular with the use of **goto statements** or equivalent. The distinction was particularly stressed by the publication of the influential "Go To Statement Considered Harmful" open letter in 1968 by Dutch computer scientist Edsger W. Dijkstra, who coined the term "structured programming".

There are both high- and low-level programming languages that use non-structured programming. Some include JOSS, FOCAL, TELCOMP, assembly languages, MS-DOS batch files, and early versions of BASIC, Fortran, COBOL, and MUMPS.

**Structured programming** (aka modular programming) is a programming paradigm aimed at improving the clarity, quality and development time of a computer program by making extensive use of the structured control flow constructs of selection (if/then/else) and repetition (while and for), block structures, and subroutines. Code becomes more efficient and easy to understand. It is possible to do structured programming in any programming language.

### Early exit

The most common deviation, found in many languages, is the use of a return statement for early exit from a subroutine. This results in multiple exit points, instead of the single exit point required by structured programming. At the level of functions, this is a return statement. At the level of loops, this is a break statement (terminate the loop) or continue statement (terminate the current iteration, proceed with next iteration). Break and continue can be replicated by adding additional branches or tests, but returns from nested code can add significant complexity, and especially as seen in some languages that have "labeled breaks", which allow breaking out of more than just the innermost loop.

The most common problem in early exit is that cleanup or final statements are not executed – for example, allocated memory is not deallocated, or open files are not closed, causing memory leaks or resource leaks. These must be done at each return site, which is brittle and can easily result in bugs. For instance, in later development, a return statement could be overlooked by a developer, and an action that should be performed at the end of a subroutine (e.g., a trace statement) might not be performed in all cases. Languages without a return statement, such as standard Pascal and Seed7, do not have this problem.

Kent Beck, Martin Fowler and co-authors have argued in their refactoring books that nested conditionals may be harder to understand than a certain type of flatter structure using multiple exits predicated by guard clauses. **Their 2009 book flatly states that "one exit point is really not a useful rule. Clarity is the key principle: If the method is clearer with one exit point, use one exit point; otherwise don’t"**.

In his 2004 textbook, David Watt writes that "single-entry multi-exit control flows are often desirable". Using Tennent's framework notion of sequencer, Watt uniformly describes the control flow constructs found in contemporary programming languages and attempts to explain why certain types of sequencers are preferable to others in the context of multi-exit control flows. ... Watt also examines how exception sequencers differ from escape and jump sequencers; this is explained in the next section of [this Wikipedia article](https://en.wikipedia.org/wiki/Structured_programming#CITEREFWattFindlay2004).

### Exception handling

Based on the coding error from the Ariane 501 disaster, software developer Jim Bonang argues that any exceptions thrown from a function violate the single-exit paradigm, and proposes that all inter-procedural exceptions should be forbidden. Bonang proposes that all single-exit conforming C++ should be written along the lines of:

```C
bool MyCheck1() throw() {
  bool success = false;
  try {
    // Do something that may throw exceptions.
    if (!MyCheck2()) {
      throw SomeInternalException();
    }
    // Other code similar to the above.
    success = true;
  } catch (...) {
    // All exceptions caught and logged.
  }
  return success;
}
```

Peter Ritchie also notes that, in principle, even a single throw right before the return in a function constitutes a violation of the single-exit principle, but argues that Dijkstra's rules were written in a time before exception handling became a paradigm in programming languages, so he proposes to allow any number of throw points in addition to a single return point. He notes that solutions that wrap exceptions for the sake of creating a single-exit have higher nesting depth and thus are more difficult to comprehend, and even accuses those who propose to apply such solutions to programming languages that support exceptions of engaging in cargo cult thinking.

David Watt also analyzes exception handling in the framework of sequencers (introduced in the aforementioned article). Watt notes that an abnormal situation (generally exemplified with arithmetic overflows or input/output failures like file not found) is a kind of error that "is detected in some low-level program unit, but (for which) a handler is located in a high-level program unit". For example, a program might contain several calls to read files, but the action to perform when a file is not found depends on the meaning / purpose of the file in question to the program and thus a handling routine for this abnormal situation cannot be located in low-level system code. Watts further notes that introducing status flag testing in the caller, as single-exit structured programming or even (multi-exit) return sequencers would entail, results in a situation where "the application code tends to get cluttered by tests of status flags" and that "the programmer might forgetfully or lazily omit to test a status flag. In fact, abnormal situations represented by status flags are by default ignored!" He notes that in contrast to status flags testing, exceptions have the opposite default behavior, causing the program to terminate unless the programmer explicitly deals with the exception in some way, possibly by adding code to willfully ignore it. Based on these arguments, Watt concludes that jump sequencers or escape sequencers are not as suitable as a dedicated exception sequencer with the semantics discussed above.

In addition, the necessity to limit code to single-exit points appears in some contemporary programming environments focused on parallel computing, such as OpenMP. The various parallel constructs from OpenMP, like parallel do, do not allow early exits from inside to the outside of the parallel construct; this restriction includes all manner of exits, from break to C++ exceptions, but all of these are permitted inside the parallel construct if the jump target is also inside it.
