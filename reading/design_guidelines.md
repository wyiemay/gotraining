## Design Guidelines

These are a set of design guidelines for data, interfaces, composition and packages. Please consider these principles when designing your own software.

#### Bottom Line

The compiler is a tool and it's not all knowing or perfect.  
You need to work with it and help it.

The operating system is doing its best to keep cores busy and leverage the right core at the right time.  
You need to work with it and help it.

The hardware is doing its best to execute as many instructions per clock cycle as possible.  
You need to work with it and help it.

Writing idiomatic code in Go gets you a long way. But you can do so much more when you know how these things work.

#### Integrity, Readability, Simplicity and Performance

You can't make the best decisions without understanding the impact of your decisions. Every decision you make, every line of code you write comes with trade-offs. These trade-offs falls into these four areas. Before you allow a higher numbered trade-off trump a lower numbered trade-off, you must consciously and with great reason be able to explain yourself.

**1) Integrity**  
This is the accuracy and consistency of your code performing every read, write and the execution of every instruction. Nothing trumps integrity - EVER.

**2) Readability**  
This is the ability to easily read code and understand what it is doing. It is also the ability to understand the cost of the code and its impact on your software and the overall ecosystem it exists in.

**3) Simplicity**  
This is algorithm efficiency and not wasting effort. Solving the data transformation problem with the least number of steps. NASA identified that every 10 lines of code produces a bug whether you like it or not. Reduce bugs and simplify code by writing less of it.

**4) Performance**  
This is about micro-optimizing something when it is absolutely necessary. When code is written with this as the priority, it is very difficult to write code that is readable and simple. When readable and simple code is not performing well enough based on real empirical data, then this can be discussed.

#### Data-Oriented Design
[Data-Oriented Design and C++](https://www.youtube.com/watch?v=rX0ItVEVjHc) - Mike Acton  
[Efficiency with Algorithms, Performance with Data Structures](https://www.youtube.com/watch?v=fHNmRkzxHWs) - Chandler Carruth

* If you don't understand the data, you don't understand the problem.

* All problems are unique and specific to the data you are working with.

* Data transformations are at the heart of solving problems. Each function, method and work-flow must focus on implementing the specific data transformations required to solve the problems.

* If your data is changing, your problems are changing. When your problems are changing, the data transformations needs to change with it.

* Uncertainty about the data is not a license to guess but a directive to STOP and learn more.

* Solving problems you don't have, creates more problems you now do.

* If performance matters, you must have mechanical sympathy for how the hardware and operating system work.

* Minimize, simplify and REDUCE the amount of code required to solve each problem. Do less work by not wasting effort.

* Code that can be reasoned about and does not hide execution costs can be better understood, debugged and performance tuned.

* Coupling data together and writing code that produces predictable access patterns to the data will be the most performant.

* Changing data layouts can yield more significant performance improvements than changing just the algorithms.

* Efficiency is obtained through algorithms but performance is obtained through data structures and layouts.

#### Interface and Composition Design

_With help from [Sandi Metz](https://twitter.com/sandimetz)._

* Interfaces provide the highest form of decoupling when the concrete types used to implement them can remain opaque.

* Decoupling means reducing the amount of intimate knowledge code must have about concrete types.

* Interfaces with more than one method has more than one reason to change.

* You must do your best to understand what could change and decouple those aspects of your code.

* Uncertainty about change is not a license to guess but a directive to STOP and learn more.

* Recognizing and minimizing cascading changes across the code is a way to architect adaptability and stability in your software.

* When dependencies are weakened and the coupling loosened, cascading changes are minimized and stability is improved.

* The standardization of interfaces can set clear and consistent expectations.

#### Interface Pollution

_With help from [Sarah Mei](https://twitter.com/sarahmei) and [Burcu Dogan](https://medium.com/@rakyll/interface-pollution-in-go-7d58bccec275)_

* Don't use an interface for the sake of using an interface.

* Don't use an interface to generalize an algorithm.

* Unless the user needs to provide an implementation or you have multiple implementations, question.

* Don’t export any interface unless your user needs it. This includes interfaces for internal testing. Users can declare their own interfaces.

* If it's not clear how an abstraction makes the code better, it probably doesn't.

#### Package-Oriented Design

* Start with a Project that contains all the source code you need to build the products and services the Project owns.

* Maintain each Project in a single repo.

* Only break a Project up when developer productivity is a cost.

* Breaking a Project into multiple projects comes with extra dependency costs.

* In many languages folders are used to organize code, in Go folders are used to organize API's (packages).

* Packages in Go provide API boundaries that should focus on solving one specific problem or a highly focused group of problems.

* You must understand how changes to the API for a particular package affects the other packages that depend on it.

* Recognizing and minimizing cascading changes across different packages is a way to architect adaptability and stability in your software.

* When dependencies between packages are weakened and the coupling loosened, cascading changes are minimized and stability is improved.

#### Code Reviews

I teach a lot about the things I look for in code reviews. I am slowly attempting to document this.

* Try to use functions over methods when it is practical. Functions allow for better readability and reusability because all the input is passed in and the output is returned out. No information is lost or abstracted.

* Eliminate the use of the else statements when it is practical. Do not attempt to push code paths to the end of a function. Keep your positive path code in the first tabbed position and use the if statement to process negative path. Return from the function as part of error handling.

* Don't start off with pointer variables if it can be avoided. It is easier to work with variables that represent a value, even if that value is going to escape to the heap. The use of the & operator can go a long way to maintaining readability in your code.

* Use the keyword var to represent the declaration of a variable that is being set to its zero value. This helps with readability and can provide the basis for developing a consistent set of rules around variable declarations. One of Go's biggest warts is there are too many ways to declare and create variables.


