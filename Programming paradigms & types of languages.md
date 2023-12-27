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

### Multiple entry

More rarely, subprograms allow multiple entry. This is most commonly only re-entry into a coroutine (or generator / semi-coroutine), where a subprogram yields control (and possibly a value), but can then be resumed where it left off (Python does this using `yield`). There are a number of common uses of such programming, notably for streams (particularly input/output), state machines, and concurrency. From a code execution point of view, yielding from a coroutine is closer to structured programming than returning from a subroutine, as the subprogram has not actually terminated, and will continue when called again – it is not an early exit. However, coroutines mean that multiple subprograms have execution state – rather than a single call stack of subroutines – and thus introduce a different form of complexity.

From the [Multiple entry](https://en.wikipedia.org/wiki/Structured_programming#Multiple_entry) section, "It is very rare for subprograms to allow entry to an arbitrary position in the subprogram, as in this case the program state (such as variable values) is uninitialized or ambiguous, and this is very similar to a goto".

> **TODO: Find out examples of multiple entry code.** The words "very rare" imply the existence of such code, which I'm curious about.

---

## High level vs Low level

A **high-level programming language** is a language that has a relatively high level of abstraction.

These languages are programmer-friendly and focus on usability over optimal program efficiency. They deal with variables, arrays, objects, complex arithmetic or Boolean expressions, subroutines, functions, loops, threads, locks, and other abstract computer science concepts. High-level languages are easier to understand and maintain, but they may be less memory-efficient compared to low-level languages.

Examples of high-level languages include Java, Python, C#, and even C and C++. The latter two provide more freedom and control over memory, making them more low-level but not low enough to be considered a low-level programming language.

A **low-level programming language** is a language that is closer to machine language and contains commands that are more specific to processor instructions.

These languages are machine-friendly and focus on efficient program execution. They deal with registers, memory addresses, call stacks, and other low-level computer components. Low-level languages are more difficult to understand for humans but are easier for machines to interpret. They are often used when performance and efficiency are crucial, such as in real-time applications or embedded systems.

Examples of low-level languages include assembly languages and machine code.

---

## Compiled vs Interpreted

Compiled and interpreted programming languages differ in how they are processed and executed by the computer.

In a **compiled language**, the source code is translated directly into machine code that the processor can execute, resulting in faster and more efficient execution. Examples of compiled languages include C, C++, and Fortran.

On the other hand, in an **interpreted language**, the source code is not directly translated into machine code. Instead, an interpreter reads and executes the code line by line, allowing for modifications while the program is running. Examples of interpreted languages include Python, JavaScript, and Ruby.

The key differences between compiled and interpreted programming languages:

| Aspect                  | Compiled Language                                      | Interpreted Language                                      |
|-------------------------|--------------------------------------------------------|------------------------------------------------------------|
| Execution               | Directly translated into machine code                  | Read and executed by an interpreter, usually line by line           |
| Steps to Execution      | Only one step from source code to execution | At least two steps from source code to execution |
| Speed                   | Compiled programs run faster than interpreted programs  | Interpreted programs can be modified while running and tend to be slower        |
| Debugging               | Compilation errors prevent the code from compiling     | Debugging occurs at run-time                               |

Most programming languages can have both compiled and interpreted implementations, and the distinction between compiled and interpreted languages refers to the typical implementation rather than the language itself.

---

## Dynamically typed vs statically typed

In programming, a **statically typed language** is one where the data type of a variable is known at compile time, and remains unchanged throughout the execution of the program. Type checking occurs at compile time, and the type associated with each variable must be known before the source code is compiled. Examples of statically typed languages include C, C++, and Java.

On the other hand, a **dynamically typed language** is one where type checking occurs at runtime or execution time. Variables are checked against types only when the program is executing, and the majority of type checking is performed at run-time. Dynamic typing can be more flexible and easier to use, as developers do not need to specify types explicitly. Examples of dynamically typed languages include Python, JavaScript, Ruby, and PHP.

> In a nutshell: Statically typed refers to type checking at compile time, while dynamically typed refers to type checking at runtime.

### Type systems & type safety

There are multiple [type systems](https://en.wikipedia.org/wiki/Type_system) which determine how the types of data is handled by software. A **type system** is a logical system comprising a set of rules that assigns a property called a type (for example, integer, floating point, string) to every term (a word, phrase, or other set of symbols). Usually the terms are various language constructs of a computer program, such as variables, expressions, functions, or modules.

Even a type can become associated with a type. An implementation of a type system could in theory associate identifications called data type (a type of a value), class (a type of an object), and kind (a type of a type, or metatype). These are the abstractions that typing can go through, on a hierarchy of levels contained in a system.

Whether automated by the compiler or specified by a programmer (automatic inference vs manual annotation), a type system makes program behavior illegal if outside the type-system rules. Advantages provided by programmer-specified type systems include abstraction and documentation, while advantages provided by compiler-specified type systems include optimization and safety.

In computer science, **type safety** and type soundness are the extent to which a programming language discourages or prevents type errors. The behaviors classified as type errors by a given programming language are usually those that result from attempts to perform operations on values that are not of the appropriate data type, e.g., adding a string to an integer when there's no definition on how to handle this case. This classification is partly based on opinion.

Type enforcement can be static, catching potential errors at compile time, or dynamic, associating type information with values at run-time and consulting them as needed to detect imminent errors. Type enforcement can also be a combination of both.

A C example that is not memory-safe:

```c
int x = 5;
char y[] = "37";
char* z = x + y;
printf("%c\n", *z);
```

In this example `z` will point to a memory address five characters beyond `y`, equivalent to three characters after the terminating zero character of the string pointed to by `y`. This is memory that the program is not expected to access. In C terms this is simply undefined behavior and the program may do anything; with a simple compiler it might actually print whatever byte is stored after the string "37".

### Strong vs weak typing

One of the many ways that programming languages are colloquially classified is whether the language's type system makes it strongly typed or weakly typed (loosely typed). However, there is no precise technical definition of what the terms mean and different authors disagree about the implied meaning of the terms and the relative rankings of the "strength" of the type systems of mainstream programming languages. For this reason, writers who wish to write unambiguously about type systems often eschew the terms "strong typing" and "weak typing" in favor of specific expressions such as "type safety".

Generally, a strongly typed language has stricter typing rules at compile time, which implies that errors and are more likely to happen during compilation. Most of these rules affect variable assignment, function return values, procedure arguments and function calling. Dynamically typed languages (where type checking happens at run time can also be strongly typed. In dynamically typed languages, values, rather than variables, have types.

A weakly typed language has looser typing rules and may produce unpredictable or even erroneous results or may perform implicit type conversion at runtime. Advocates of dynamically typed (generally "weakly typed") languages find such concerns to be overblown and believe that static typing actually introduces an exponentially larger set of problems and inefficiencies. A different but related concept is [latent typing](https://en.wikipedia.org/wiki/Latent_typing "Latent typing").

> **TODO: Expand on the topic of latent typing**

Strongly typed language examples include Java, C, C++. Some languages considered weakly typed include Python, PHP and JavaScript, which allow for more flexibility in type conversions.

---

## Imperative & Declarative

Programming paradigms classify programming languages based on their features. One language may be classified into multiple paradigms.

**Imperative programming**. In this programming paradigm, we describe the statements that change the program's state. Focus is on how the program operates, step by step; given a sequence of instructions/commands. This is often contrasted to high-level descriptions of its expected results, as observed in Declarative programming.

Imperative languages are often low-level, meaning they are closer to the hardware and have more control over the memory and performance. Some examples of imperative languages are C, Java, and Python.

The programming paradigm used to build programs for almost all computers typically follows an imperative model. Digital computer hardware is designed to execute machine code, which is native to the computer and is usually written in the imperative style, although low-level compilers and interpreters using other paradigms exist for some architectures such as lisp machines. Many imperative programming languages (such as Fortran, BASIC, and C) are abstractions of assembly language.

> Imperative literally means giving authoritative command for a specific needs.

**Declarative programming**. In this programming paradigm logic of computation is expressed without describing its control flow. Many languages that apply this style attempt to minimize or eliminate side effects by describing what the program must accomplish in terms of the problem domain, rather than describing _how_ to accomplish it as a sequence of the programming language primitives; the how being left up to the language's implementation. This is in contrast with imperative programming, which implements algorithms in explicit steps.

In a few words, declarative programming focuses on what to achieve rather than how to achieve it. Declarative languages are often high-level, meaning they are more abstract and expressive and have less control over the details.

Common declarative languages include those of database query languages (e.g., SQL, XQuery), regular expressions, logic programming (e.g. Prolog, Datalog, answer set programming), **functional programming** (Haskell, OCamel), and configuration management systems. Functional and logic programming languages are characterized by a declarative programming style.

**Imperative vs Declarative**. In reality, most programming languages and applications are not purely imperative or declarative, but rather a mix of both (also called hybrid languages). For example, Python is an imperative language that supports some declarative features, such as list comprehensions and generators. SQL is a declarative language that allows some imperative commands, such as loops and variables. Makefiles, specify dependencies in a declarative fashion, but include an imperative list of actions to take as well. Similarly, yacc specifies a context free grammar declaratively, but includes code snippets from a host language, which is usually imperative (such as C). Hybrid approaches can combine the best of both worlds and offer more flexibility and functionality.

---

## Procedural programming

Procedural programming is a programming paradigm, derived from imperative programming, based on the concept of the procedure call. Procedures (a type of routine or subroutine) simply contain a series of computational steps to be carried out. Any given procedure might be called at any point during a program's execution, including by other procedures or itself. The first major procedural programming languages appeared c. 1957–1964, including Fortran, ALGOL, COBOL, PL/I and BASIC. Pascal and C were published c. 1970–1972.

Procedural programming languages are also imperative languages, because they make explicit references to the state of the execution environment. This could be anything from variables (which may correspond to processor registers) to something like the position of the "turtle" in the Logo programming language. Procedural programming could be considered a step toward declarative programming. A programmer can often tell, simply by looking at the names, arguments, and return types of procedures (and related comments), what a particular procedure is supposed to do, without necessarily looking at the details of how it achieves its result. At the same time, a complete program is still imperative since it _fixes_ the statements to be executed and their order of execution to a large extent.

**Distinction from imperative programming**. Often, the terms "procedural programming" and "imperative programming" are used synonymously. However, procedural programming relies heavily on blocks and scope, whereas imperative programming as a whole may or may not have such features. As such, procedural languages generally use reserved words that act on blocks, such as if, while, and for, to implement control flow, whereas non-structured imperative languages use goto statements and branch tables for the same purpose.

**Relation to logic programming**: on [Wikipedia](https://en.wikipedia.org/wiki/Procedural_programming#Logic_programming)

---

## Functional programming

In computer science, **functional programming** is a programming paradigm where programs are constructed by applying and composing functions. It is a declarative programming paradigm in which function definitions are trees of expressions that **map values to other values**, rather than a sequence of imperative statements which update the running state of the program.

In functional programming, functions are treated as first-class citizens, meaning that they can be bound to names (including local identifiers), passed as arguments, and returned from other functions, just as any other data type can. This allows programs to be written in a declarative and composable style, where small functions are combined in a modular manner.

Functional programming (FP) has its roots in academia, evolving from the lambda calculus, a formal system of computation based only on functions. FP has historically been less popular than imperative programming, but many functional languages are seeing use today in industry and education, including Common Lisp, Scheme, Clojure, Wolfram Language, Racket, Erlang, Elixir, OCaml, Haskell, and F#.

Functional programming is also key to some languages that have found success in specific domains, like JavaScript in the Web, R in statistics, J, K and Q in financial analysis, and XQuery/XSLT for XML. Domain-specific declarative languages like SQL and Lex/Yacc use some elements of functional programming, such as not allowing mutable values. In addition, many other programming languages support programming in a functional style or have implemented features from functional programming, such as C++11, C#, Kotlin, Perl, PHP,  Python, Go, Rust, Raku, Scala, and Java (since Java 8).

The principles of modularity and code reuse in practical functional languages are fundamentally the same as in procedural languages, since they both stem from structured programming. So for example:
- Procedures correspond to functions. Both allow the reuse of the same code in various parts of the programs, and at various points of its execution.
- By the same token, procedure calls correspond to function application.
- Functions and their modularly separated from each other in the same manner, by the use of function arguments, return values and variable scopes.
- Functional programming languages support (and heavily use) first-class functions, anonymous functions and closures, although these concepts have also been included in procedural languages at least since Algol 68.

**The main difference between the styles is that functional programming languages remove or at least deemphasize the imperative elements of procedural programming.** The feature set of functional languages is therefore designed to support writing programs as much as possible in terms of pure functions.

### Purely functional programming

Functional programming is sometimes treated as synonymous with **purely functional programming**, a subset of functional programming which treats all functions as deterministic mathematical functions, or pure functions. When a pure function is called with some given arguments, it will always return the same result (deterministic), and cannot be affected by any mutable state or other side effects (pure). It is a style where all computation is treated as the evaluation of mathematical functions.

> Declarative, deterministic, and unchanging (immutability) are terms used to describe purely functional programming.

Purely functional programming consists of ensuring that functions, inside the functional paradigm, will only depend on their arguments, regardless of any global or local state. A pure functional subroutine only has visibility of changes of state represented by state variables included in its scope.

**Randomness and time functions are impure**, because they depend on the state of the system or the environment, which can change at any time. Moreover, they can also affect the state of the system or the environment, which can affect other functions.

> See also: [Pure Function](https://en.wikipedia.org/wiki/Pure_function)

This is in contrast with impure procedures, common in imperative programming, which can have side effects (such as modifying the program's state or taking input from a user). Proponents of purely functional programming claim that by restricting side effects, programs can have fewer bugs, be easier to debug and test, and be more suited to formal verification.

> The exact difference between pure and impure functional programming is a matter of controversy. Sabry, Amr (January 1993). "What is a purely functional language?". Journal of Functional Programming. 8 (1): 1–22 [DOI](https://www.cambridge.org/core/journals/journal-of-functional-programming/article/what-is-a-purely-functional-language/3A39D50DA48F628D17D9A768A1FA39C3)

### Concepts

A number of concepts and paradigms are specific to functional programming, and generally foreign to imperative programming (including object-oriented programming). However, programming languages often cater to several programming paradigms, so programmers using "mostly imperative" languages may have utilized some of these concepts.

**Higher-order functions** are functions that can either take other functions as arguments or return them as results. In calculus, an example of a higher-order function is the differential operator d/dx, which returns the derivative of a function f.

**Pure functions** (or expressions) have no side effects (memory or I/O). This means that pure functions have several useful properties, many of which can be used to optimize the code:
- If the result of a pure expression is not used, it can be removed without affecting other expressions.
- If a pure function is called with arguments that cause no side-effects, the result is constant with respect to that argument list. This can enable caching optimizations such as memoization.
- If there is no data dependency between two pure expressions, their order can be reversed, or they can be performed in parallel and they cannot interfere with one another (in other terms, the evaluation of any pure expression is [thread-safe](https://en.wikipedia.org/wiki/Thread-safe)). (needs more info; using "any" it implies that no two pure expressions have data dependency).
- If the entire language does not allow side-effects, then any evaluation strategy can be used; this gives the compiler freedom to reorder or combine the evaluation of expressions in a program (for example, using [deforestation](https://en.wikipedia.org/wiki/Deforestation_(computer_science) "Deforestation (computer science)")).


