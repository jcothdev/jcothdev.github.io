---
layout: page
---

# Software Manifesto

### Software Development Philosophy and Dialectic

#### What is your main guiding principle for service oriented code development?

You only need at most three objects per service unit. If you think it's unavoidable to use that few an object, split off more service units of three objects each.
1. **Endpoint Handler and Request Normalizer**: At the start of runtime the service opens **object 1** as a live listener to user/client requests. The service-span listener code should be implemented in **object 2**, so **object 1** should initialize these parameters at startup. Upon client interaction the request details are null-checked, and type normalization, ie. many-to-one or one-to-many cases are handled.
2. **Central Shared Resource Instance**: The main connections for **object 3** are established here using configured connection details. Facilities for client normalization are also implemented here. In general, the line count of **object 2** implementable code should far outpace the other two.
3. **Backend/Query Connector**: Use the function space of **object 2** to pass request from **object 1** to query a read connection, or parse into a write connection. The appropriate response is wrapped from code in **object 2**, and returned from the endpoint in **object 1**.

#### How do you organize the chaos of enterprise level code?

- **Dependency inversion** - Knowing what code goes into which object is the art behind acheiving the streamlined pallindromic flow of an efficient call-stack.
- **Robust central libraries** - Developer-friendly abstractions in the **object 2** space of capabilities. Use a rich list of internal service units to bind would-be tramp data where appropriate and shrink your "RAM footprint" as a developer.
- **Polymorphic magic** - When the dependency chain is indeterminant at compile time, callable abstraction and conditionals are absolutely the grease in the wheels of your enterprise system. It is important however to never pre-optimize and use polymorphism out of the gate. This leads to the next point, but a well factored base in **object 2** can make refactoring or optimizing less of a headache.
- **Write extensible code** - From day 0, one of the top goals of an experienced developer should be to write their code in a way that easily allows for extension and, as much as possible for deprecation and sun-setting.

#### What is your take on Object Oriented Programming (OOP)?

The secret to understanding OOP lies in the semantics of "superclasses" and "subclasses". Namely, they are misnomers. Subclasses are algebraically *supersets* and superclasses are algebraically *subsets*. In the Venn-diagram of the set of data a given class can handle, *sub*classes are the actually *larger* circles, and *super*class are *smaller* circles, usually totally nested inside the "subclass" it supposedly "encapsulates". So the better mental picture is that OOP classes are pyramids built pointy side down. While I don't usually care for semantic arguments this case in OOP is too obviously misleading to ignore. The concepts of inheritance and encapsulation in traditional OOP languages are red herrings. Heuristically, scaling an implicitly typed language like Golang would be preferable to implementing a cobweb of polymorphic convolution in Java. I don't say this as a slight to explicit typing, only when coupled with a naive notion of inheritance or encapsulation is it dangerous, to say the least.


#### How do you avoid using code as configuration space?

Easy management of defaults and constants can be achieved by creating a yaml (or similar) resource file in a core directory of the service code. At the initialization of the service the config file is read and the constants can be programmatically tokenized and used where needed.

#### How and when do you interface with file systems?

In general, for live services the answer should be *never*, with certain exceptions for ETL (Extract Transform Load) runs. If it is unavoidable to need file system calls, wrap their use in a well-defined and tightly managed but general-use **object 2** style file system library. This should be a single-source plugin for anything running on (preferably) UNIX, and others for other OSs. File systems are chaotic and unpredictable so make sure to pepper this library with plenty of error handling and prepare for any and all worst-case scenarios on the hard drive.

Outside of the limited ETLs that need file systems, consider alternatives like Mongo or SQL for long-term data stores. In-memory cache and/or messaging queues for short-term data stores.

#### What is your take on Python?

Python is a broadly purposed programming language with rich support in a plethora of paradigms. Most famously, it is the language of choice for data science, machine learning and other related analytical projects. There has been a surge in it's popularity as the most "agile" language to bootstrap just about any burgeoning platform recently. But I genuinely believe this is going to come at a cost in the near future. Service software at considerable scale needs to be implemented in a statically-typed and compiled language, in much the same way that a large enough office building needs a statically numbered and riveted room-numbering scheme. As the scale of a python project grows, the abstraction of the stack grows at a pace that exceeds it's time and space complexity. This means countless hours spent reading and re-reading docs in order to accomplish simple changes because the blueprint of a typing system is not there. My recommendation is always to keep .py files under ~250 lines long and less than 10% of enterprise code base.


#### Contact
jonathan@coth.dev
