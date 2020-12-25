# Clean Architecture

- [Clean Architecture](#clean-architecture)
  * [Foreword](#foreword)
  * [Preface](#preface)
  * [Introduction](#introduction)
- [Part I: What is design and architecture ?](#part-i--what-is-design-and-architecture--)
  + [The goal](#the-goal)
    * [A tale of two values](#a-tale-of-two-values)
  + [Behavior](#behavior)
  + [Architecture](#architecture)
  + [Eisenhower Matrix:](#eisenhower-matrix-)
- [Part II: Starting from the brick: Programming paradigms](#part-ii--starting-from-the-brick--programming-paradigms)
  * [Paradigm overview](#paradigm-overview)
    + [Structured](#structured)
    + [Object Oriented](#object-oriented)
    + [Functional](#functional)
    + [Food for thought](#food-for-thought)
    + [Conclusion](#conclusion)
  * [Structured Programming](#structured-programming)
    + [Tests](#tests)
    + [Conclusion](#conclusion-1)
  * [Object Oriented Programming](#object-oriented-programming)
    + [Encapsulation](#encapsulation)
    + [Inheritance](#inheritance)
    + [Polymorphism](#polymorphism)
    + [The power of polymorphism](#the-power-of-polymorphism)
    + [Dependency Inversion](#dependency-inversion)
  * [Conclusion](#conclusion-2)
- [Part III: Design Principles](#part-iii--design-principles)
  * [S.O.L.I.D](#solid)
  * [Single responsibility principle (SRP)](#single-responsibility-principle--srp-)
  * [The open-closed principle (OCP)](#the-open-closed-principle--ocp-)
  * [The Liskov substitution principle (LSP)](#the-liskov-substitution-principle--lsp-)
    + [LSP and architecture](#lsp-and-architecture)
  * [The interface segregation principle (ISP)](#the-interface-segregation-principle--isp-)
  * [The  dependency inversion principle (DIP)](#the--dependency-inversion-principle--dip-)
    + [Factories](#factories)
- [Part IV:  Components principles](#part-iv---components-principles)

## Foreword

Describing software through architecture can reveal as much as it hides. It can both promise more than what it can delivers and deliver more than what it promises.

 *Architecture represents the significant design decisions that shape a system, where significant is measured by cost of change.* - *Grady Booch*

Time, money and effort give us a sense of scale to short between the large and the small, to distinguish the architectural stuff from the rest. A good architecture should not only meet the need of its users, developers, and owners at a given point in time, but it also meets them over time.

*If you think good architecture is expensive, try bad architecture.* - *Brian Foote and Joseph Yoder*

The path we are most interested is  the cleanest one, where we recognize the softness of software and preserve it as a first-class property of the system. Recognize that we operate with incomplete knowledge, but also understand that as humans is something we're good at. Play more to our strength than to our weaknesses. 

*Architecture is a hypothesis, that needs to be proven by implementation and measurement.* - *Tom Glib*

To walk this path requires care and attention, thought and observation, practice and principle.  This at first might sound slow, but it's all in the way that you walk.

*Slow and steady wins the race.*

## Preface

Uncle Bob claims to have taken part and tons of different systems from games to multi-threaded, multi processor, GUI and databases apes and all of them follows the same rules.

He concludes "*the rules of software architecture are independent of every other variable.*" He based on the fact that even though technology has improved drastically in term of new hardware more libraries and new languages, the bases are the same. It's made of the same stuff. It's made of `if` statements, assignments statements, and `while` loops. This changeless NESS of the code is the reason that the rules o software architecture are so consistent across system types. Nevertheless, one thing has changed: Back then, they didn't know what the rules were.

## Introduction

Getting something to work --once-- just isn't that hard. Getting it right is another matter entirely. Getting software right is hard and most young programmers don't have what it needs or simply doesn't care about writing clean code.

When you get software right, something magical happens: You don't need hordes of programmers to keep it working. You don't need massive requirements documents and huge issue tracking systems. When software is done right it requires a fraction the human resources to create and maintain.

Unfortunately, It is far more common to fight your way through terrible software designs that it is to enjoy the pleasure of working with a good one.

# Part I: What is design and architecture ?

There has been a lot of confusion about design and architecture over the years and one of the goals of this book is to cu through all that confusion and to define what architecture and design are. For starters, there's no difference at all.

The work *architecture* is often used in the context of something at a high level that is divorced from the lower-level details, whereas *design* more often seems to imply structures and decisions at a lower level. But this usage is nonsensical when you look at what a real architect does. 

### The goal

Both design and architecture can be used to describe a continuum of decisions from the highest to the lowest levels. And what drives that decision ? 

*The goal of software architecture is to minimize the human resources required to build and maintain the required system.*

Once again like in the foreword remark the importance of taking the time to think thing through by stating several quotes and showing a case study on the matter.

*The race is not to the swift, nor the battle to the strong.*

*The more haste, the less speed.*

*Making messes is always slower than staying clean.*

*The only way of going fast, is to go well*

The developers may think that the answer is to start over from scratch and redesign the whole system --  but that's just the hare talking again.

*Their overconfidence will drive the redesign into the same mess as the original project.*

## A tale of two values

Uncle bob says that software mainly provide two values: **Behavior** and **Architecture**. 

### Behavior

**Behavior** , making a machine behave in a way that meets the stakeholders requirements. Functionality. Some programmers think this is their entire job. They think that their job is to implement requirements and fix bugs. They are sadly wrong.

### Architecture

**Architecture**, has to do with the word software. *ware* being product and the word *soft* that is where the second value lies.

Software was invented to be *soft*. It was intended to be a way to easily change the behavior of machines. If we'd wanted the behavior of machines to be hard to  change, we would have called it *hardware*.

Architecture should be agnostics of shape.

### Eisenhower Matrix:

 *The urgent is not important and the important are never urgent.* 

Those things that are urgent are rarely of great importance, and those things that are important are seldom of great urgency.

The first value of software --behavior-- is urgent but not always important.

The second value of software --architecture-- is important but never particularly urgent.

1. Urgent and Important
2. Not urgent and important
3. Urgent and not important
4. Not Urgent and not important

Business managers and developers often place the 3 option to the first place.

# Part II: Starting from the brick: Programming paradigms

 First programming revolution was that of languages. Languages relieved the programmers of the drudgery of translating their programs into binary.

Another revolution, probably more significant, revolution was in programming paradigms. Paradigms area ways of programming, relatively unrelated to languages. ***A paradigm tells you which programming structures to use, and when to use them***. To date, there have been three such paradigms and there are unlikely to be any others. 

## Paradigm overview

The three paradigms included in this overview are **Structured**, **Object oriented** and **Functional.**

### Structured

The first one to be adopted (but no the first to be invented) was structured programming, discovered by Dijkstra. He showed that the use of unrestrained jumps (`goto` statements) is harmful to program structure so he replaced those jumps with the more familiars `if/then/else` and `do/while/until` constructs.

*Structured programming imposes discipline on direct transfer of control*

### Object Oriented

Two years earlier Object oriented programming was discovered by Ole and Kristen. These two programmer noticed that the function call stack frame in the `ALGOL` language could be moved to a heap, thereby allowing local variables declared by a function to exist long after the function returned. The function become a constructors for a class, the local variables became instance variables, and the nested functions became methods. This lead inevitably to the discovery of polymorphism through the disciplined use of function pointers.

*Object-oriented programming imposes discipline on indirect transfer of control*

### Functional

The first to be invented was functional programming. Its  invention predates computer programming itself. Derived from 1-Calculus, its main foundational notions is immutability -- that is, the notion that the values of symbols do not change. 

*Functional programming imposes discipline upon assignment*

### Food for thought

Notice the pattern that I've quite deliberately set up in introducing these three programming paradigms: Each of them removes capabilities from the programmer. None of them adds new capabilities. Each imposes some kind of extra discipline that is negative in its intent. The paradigms tell us what not to do, more than they tell us what to do.

Every paradigm takes aways something. The three paradigms together remove `goto` statements, functions pointers, and assignment. Is there anything left to take away ? These were discovered in the span of 10 years, in the many decades that have followed, no new paradigms have been added.

### Conclusion

What does this has to do with architecture ? We use polymorphism as the mechanism to cross architectural boundaries; we use functional programming to impose discipline on the locations of and access to data; and we use structured programming as the algorithmic foundation of our models. Notice how well those thee align with the three big concerns of architecture function, separation of components, and data management.

## Structured Programming

Dijkstra realized that programming is hard and that programmer don't do it very well. A program of any complexity contains too many details for a human brain to manage without help. 
To solve this issue, Dijkstra tried to apply the mathematical discipline of proof. His vision was the construction of Euclidean hierarchy of postulates, theorems, corollaries, and lemmas.
Programmer would use proven structures, and tie them together with code that they would prove correct themselves.
He discovered that certain uses of `goto` statements prevent modules  from being decomposed recursively into smaller units therefore preventing the use of the divide-and-conquer approach necessary for reasonable proofs.
However, other uses of goto didn't have this problem. He realized that this *good* uses of `goto` corresponds to simple selection and iteration control structures.
All programs can be constructed with three structures: Sequence, Selection and Iteration. This very same structures made a program provable.

The Euclidean hierarchy of theorems was never built. And programmers never saw the benefits of working through the laborious process of formally proving each and every little function correct.
Of course, formal, Euclidean style, mathematical proofs is not the only strategy for proving something correct. Another highly successful strategy is the scientific method. Proving thins incorrect.
That's the nature of scientific theories and laws: They are falsifiable but not provable. Science work by proving statement false, not true. We take as true the statements that, after a long time, we couldn't prove true.

### Tests

Dijkstra once said: *"Testing shows the presence, not the absence, of bugs".* Functions can be proven to be incorrect with a test, but it can't be proven correct.
Software development is not like mathematical endeavor, even though is it seems to manipulate mathematical constructs. Rather, software is like science. We show correctness by failing in proving incorrectness.

### Conclusion

In conclusion, structured programming is this ability to create falsifiable units of programming that makes structured programming valuable today.
At the architecture level, this is why we still consider functional decomposition to be on of our best practices. 

## Object Oriented Programming

The basis of a good architecture is the correct understanding and application of the principles of Object-oriented design (OO)
OO Design is the combination of data and function but is also explain as "A way to model the real world". 
The three magic word to explain OO are encapsulation, inheritance and polymorphism.

### Encapsulation

The encapsulation of data and functions lets us draw a line and bound these together but the idea is certainly not unique to OO. Indeed, we had perfect encapsulation in C. Perfect encapsulation in a non-OO language.
C#, Java and some OO language it's imposible to separate the declaration and definition of a class. Therefore they abolished the header/implementation like pure `C` ,where you would have a `library.h`, weakening encapsulation.
For these reasons it is difficult to accept that OO depends on strong encapsulation. In fact, many OO languages have little or no enforced encapsulation at also.

### Inheritance

Inheritance is simply the redeclaration of a group of variables and functions within an enclosing scope. We could do this with C long time ago or at least we had a trick, but it's not inheritance per se. Moreover, multiple inheritance is considerably more difficult to achieve with such trickery.
It's fair to say that while OO did not give us something completely brand new, it did make the masquerading of data structures significantly more convenient.

### Polymorphism

We did have polymorphism in languages before OO. For example in the `getchard()` and `putchar()` which read and write from the STDIN and STDOUT.
The UNIX operating system requires that every IO devices drivers provide five standard functions: `open`, `close`, `read`, `write` and `seek` and `seek`. The signatures of these functions must be identical for every IO driver
The bottom line is that polymorphism is an application of pointers to functions. Programmers have been using these to achieve polymorphic behavior since 1940s.
In other word, OO has provide nothing new.
The problem with pointers to functions is that they are dangerous. Such use is driven by a set of manual conventions. If any programmer fails to remember these conventions, the resulting bug can be hard to track down and eliminate.
OO languages eliminate these conventions and, therefore, these dangers. Using OO languages, polymorphism is trivial. That fat provides enormous power that old C programmer could only dream of. On this basis, we can conclude that OO imposes discipline on indirect transfer of control.

### The power of polymorphism

The power of polymorphism lays on the fact that by implementing functions in, for example, UNIX IO drivers, then we can assure that the program that use those functions does not depend on the source code of those "not-dependencies" (IO Drivers.)
In short IO drivers have become plugins to out program. The plug-in architecture has been interested to achieve IO devices independence, and has been implemented in almost every operating system since its introduction.
OO allows the plug-in architecture to be used anywhere, for anything.

### Dependency Inversion

Before a safe and convenient mechanism for polymorphism was available, `Flow control` and `Source Code Dependency` followed the same path. In the typical calling tree, main functions called high-level functions, mid-level functions, which called low-level functions.
In this scenario the flow of control was dictated by the behavior of the dependencies and the dependencies were dictated by that flow control.
When polymorphism brought into play, something very different can happen.

![di](./images/dependency_inversion.png)

In `Figure 1` we can see the classical approach where Flow of control goes on the same direction as the dependency. `Figure 2`, shows us how *Object A* a high-level function calls a functions in *Object B* a middle-level function. The fact that it calls this function through the interface is a source code contrivance. At runtime, the interface doesn't exist. *Object A* simply calls the function within *Object B*
Notice that here the flow of control still goes from *Object A* the high-level function to the low-level function *Object B*.
The fact that OO languages provide safe and convenient polymorphism means that any source code dependency, no matter where it is, can be inverted by inserting an interface between them.
That's the power that OO provides. That's what OO is really all about- at least from an architect point of view.

As an example, you can rearrange the source doe dependencies of your system so that the database and the user interface (UI) depend on the business rules rather than the other way around.
This means that the Database and de UI can be plugins to the business rules. This means that the business rules never mentions the UI or the Database.

## Conclusion

OO is the ability, through the use of polymorphism, to gain absolute control over every source code dependency in the system. It allows the architect to create a plug-in architecture, in which modules that contain high-level policies are independent of module that contain los-level details. The low-level details are relegated to plug-in modules that can be deployed and developed independently from the modules that contain high-level policies.

# Part III: Design Principles

The SOLID principles tell us how to arrange our functions and data structures into classes, and how those classes should be interconnected. A class is simply a coupled grouping of functions and data. Every software system has such groupings, Wether they are called classes or not. The SOLID principles apply to those groupings.

## S.O.L.I.D

The goal of the principles is the creation of mid-level software structures that:

* Tolerate change
* Are easy to understand
* Are the basis of components than can be used in many software systems

## Single responsibility principle (SRP)

Of all of the SOLID principles, the SRP might be the least understood and it might be due to its name. It is too easy for programmers to hear the name and then assume that it means that every module should do just one thing.
Make no mistake, there is a principle like that. A **function** should do one, and only one, thing. We use that principle when we are refactoring large functions into smaller functions; we use it at the lowest levels. But it is now one of the SOLID principles-- it is not SRP.

A module should be responsible for one and only one actor (An actor being a group of users or stakeholders that will be likely to request changes to the system).

Now, what do we mean by the word "module" ? The simplest definition is just a source file. Most of the time that definition works fine. Some languages and development environments, though, don't use source files to contain their code. In those cases a module is just a cohesive set of functions and data structures.

[SEE THE EXAMPLE OF THE EMPLOYEE ON THE BOOK]

To conclude, the single responsibility principle is about functions and classes but it appears in a different form at two more levels. At the level of components, it becomes the Common Clausure Principle. At the architectural level, it becomes the Axis of change responsible for the creation of Architectural Boundaries.

## The open-closed principle (OCP)

A software should be open for extension but closed for modification
In other words, the behaviour of a software artifact ought to be extendible, without having to modify that artifact. And this is the most fundamental reason that we study software architecture. A good software architecture would reduce the amount of changed code to the barest minimum. Ideally, zero.
How?  By properly separating the things that change for different reasons (SRP) and then organizing the dependencies between them (DIP).

Bellow we see an image that's fully explained on the book. I suggest reviewing this example in particularly.

![financial ocp](./images/financial_ocp.png)

If component A should be protected from changes in component B, then B depends on A. We wan the *Controller* to be protected from changes in the *Presenters*. We want to protect the *Presenters* from changes in the views. WE wan to protect the *Interactor* from changes in-- well, everything.
Why should the *Interactor* hold such a privilege position ? Because it contains the business rules, it contains the higher level policies of the application.
This is how OCP works at the architectural level. Architects separate functionality based on how, why, and when it changes, and then organize that separated functionality into a hierarchy of components. Higher-level components or protected from changes made to the lower-level components.

OCP is the one driving forces behind the architecture of systems. The goal to make te system easy to extend without incurring a high impact of change. This goal is accomplished by partitioning the system into components, and arranging from changes in lower-level components. 

## The Liskov substitution principle (LSP)

Substitutability is a principle in object-oriented programming stating that, in a computer program, if S is a subtype of T, then objects of type T may be replaced with objects of type S without altering any of the desirable properties of the program.

### LSP and architecture

In the earlier ages of OO we thought LSP as a way to guide the use of inheritance, as shown in the previous sections. However, over the years the LSP has morphed into a broader principle of software design that pertains to interface and implementations. We could have several Ruby clases that implement the same interface or we might have a set of services that all respond to the same REST interface.
In all of these situations, and more, the LSP is applicable because there are users who depend on well-defined interfaces. In conclusion, the LSP can, and should, be extended to the level of architecture. A simple violation of substitutability, can cause a system's architecture to be polluted with significant amount of extra mechanisms.

## The interface segregation principle (ISP)

The interface-segregation principle (ISP) states that no client should be forced to depend on methods it does not use. In general is harmful to depend on modules that contain more than you need. This is obviously true for source code dependencies that can force unnecessary recompilation and redeployment-- but it is also true at a much higher, architectural level.

## The  dependency inversion principle (DIP)

The dependency inversion principle (DIP) tells us that the most flexible systems are those in which source code dependencies refer only to abstractions, not to congregations. 
It is the volatile concrete elements of our system that we want to avoid depending on. Those are the modules  that we are actively developing, and that are undergoing frequent change.
Interfaces are less volatile that implementations. This implications boils down to a set of very specific coding practices:

* Don't refer to volatile concrete classes. Refer to abstract interfaces instead.
* Don't derive from volatile concrete classes.
* Don't override concrete functions. Concrete functions often require source code when you override those functions, you do not eliminate those dependencies-- indeed you inherit them.
* Never mentions the name of anything concrete and volatile.

### Factories

To comply to these rules, the creation of volatile concrete objects requires special handling. The Factory pattern is a creational patter that defines an Interface for creating an object and defers instantiation until runtime. It is commonly used when you don't know how many or what type of objects will be needed until during runtime.

# Part IV:  Components principles

If SOLID principles tell us how to arrange the bricks into walls and rooms, then the component principles tell us how to arrange the rooms into buildings.

## Components
The smallest entities that can be deployed as a single unit. Examples - jar file, DLL, shared library, etc.

They can be combined into single binaries or kept separate as plugins to other binaries.
Whatever the use-case, good components always retain the ability to be independently deployable and, hence, independently developable.

## Component cohesion

There are three principles of component cohesion.

* REP:  The Reuse/Release equivalence principle
* CCP:  The Common Closure Principle
* CRP:  The Common Reuse Principle


### The reuse/release equivalence principle

**The granule of reuse is the granule of release** 

We are now living in the age of software reuse -- a fulfillment of one of the oldest promises of the object-oriented model.
From a software design and architecture point of view, this principle means that the classes and modules that are formed into a component must belong to a cohesive group classes and modules that are grouped together into a component should be releasable together though it is hard to precisely explain the glue that holds these together into a single component. 

The weakness of this principle is more than compensated by the strength of next two principle strongly define this principle in the negative sense.

### The common closure principle

**Gather into component those classes that change for the same reasons and at the same times. Separate into different components those classes that change at different times and for different reasons**

The CCP basically says that a component should not have multiple reasons to change. For most application, maintainability is more important than reusability. If the code in an application must change, you would like all of the changes to occur in one single component. 

#### Similarity with SRP
The CCP is the component form of the SRP. The SRP tells us to separate methods into different classes, if they change for different reasons. The CCP tells us to separate classes into different components, if they change for different reasons.

### The common reuse principle.

**Don't force users of a component to depend on things they don't need.**

The CRP is yet another principle that helps us to decide which classes and modules should be placed into a component. 

We want to make sure that classes that we put together into a component are inseparable--  that it is impossible to depend on some and not on the others. Otherwise, we will be redeploying more components than is necessary, and wasting significant effort.

#### Relation to ISP.

The CRP is the generic version of the ISP. The ISP advises us not to depend on classes that have methods we don't use. The CRP advises us not to depend on components that have classes we don't use. 

### The tension diagram for component cohesion

The REP and CCP are inclusive principles: Both tend to make components larger. The CRP is an exclusive principle, driving components to be smaller. It is the tension between these principles that good architects seek to resolve. 

![Tensions Cohesion Diagram ](./images/CohesionPrinciplesTensionDiagram.jpg)

An architect who focuses on just the REP and CRP will find that too many component are impacted when simple changes are made.. In contrast, and architect who focuses too strongly on the CCP and REP will cause too many unneeded releases to be generated.

Generally projects tend to start on the right hand of the triangle, where the only sacrifice is reuse. As the project matures, and other projects begin to draw from it, the project will slide over to the left.
It has more to do with the way that project is developed and used than with what the project actually does.

Moreover, the balance is almost always dynamic. That is the partitioning that is appropriate today might not be  appropriate next year.

# Component Coupling
