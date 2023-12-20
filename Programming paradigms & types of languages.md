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




