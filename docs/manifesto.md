# Software Manifesto

### Software Development Philosophy and Dialectic

#### What is your main guiding principle for service oriented code development?

You only need at most three objects per service unit.
1. **Endpoint Handler and Request Normalizer**: At the start of runtime the service opens **object 1** as a live listener to user/client requests. The service-span listener code should be implemented in **object 2**, so **object 1** should initialize these parameters at startup. Upon client interaction the request details are null-checked, and type normalizations, ie. many-to-one or one-to-many cases are handled.
2. **Central Shared Resource Instance**: The main connections for **object 3** are established here using configured connection details. Facilities for client normalization are also implemented here.
3. **Backend/Query Connector**: Uses functions from **object 2**, to pass request from 1 to query a read connection, or parse into a write connection. The appropriate response is wrapped from code in **object 2**, and returned from the endpoint in **object 1**.

#### How do you organize the chaos of enterprise level code?

- **dependency inversion** - This is the art inherent in the code of **object 2**. The secret lies in understanding that OOP semantics of "superclasses" and "subclasses" are misnomers. Subclasses are algebraically *supersets* and superclasses are algebraically *subsets*, in other words subclasses are the larger circles in the Venn-diagram of your code and a superclass that in OOP can define a subclass is actually a smaller circle that is usually totally nested inside the "subclass" circle. Hence the "inversion" of dependency inversion. This mental heuristic is also useful to keep in mind when scaling up implicitly-typed languages like Golang
- **robust central libraries** - Developer-friendly abstractions in the **object 2** space of capabilities. Bind would-be tramp data where appropriate and shrink your "RAM footprint" as a developer.
- **polymorphic magic** - When the dependency chain is indeterminant at compile time, callable abstraction and conditionals are absolutely the grease in the wheels of your enterprise system. It is important however to never pre-optimize an use polymorphism out of the gate. This leads to the next point but the art of **object 2** can make refactoring to optimize less of a headache.
- **write extensible code** - From day 0, one of the top goals of an experienced developer should be to write their code in a way that easily allows for extension and, as much as possible for deprecation and sun-setting.

#### How do you avoid using code as configuration space?

Easy management of defaults and constants can be achieved by creating a yaml (or similar) resource file in a core directory of the service code. At the initialization of the service the config file is read and the constants can be programmatically tokenized and used where needed.

#### How and when do you interface with file systems?

In general, for live services the answer should be *never*, with a certain exceptions for ETL (Extract Transform Load) runs. If it is unavoidable to need file system calls, wrap their use in a well-defined and tightly managed but general-use **object 2** style file system library. This should be a single-source plugin for anything running on (preferably) UNIX, and others for other OSs. File systems are chaotic and unpredictable so make sure to pepper this library with plenty of error handling and prepare for any and all worst-case scenarios on the hard drive.

Outside of the limited ETLs that need file systems, consider alternatives like Mongo or SQL in the long-term. In-memory cache and/or messaging queues in the short-term.

#### What is your take on Python?

Python is a broadly purposed programming language with rich support in a plethora of paradigms. Most famously, it is the language of choice for data science, machine learning and other related analytical projects. There has been a surge in it's popularity as the most "agile" language to bootstrap just about any burgeoning platform recently. But I genuinely believe this is going to come at a cost in the near future. Service software at considerable scale needs to be implemented in a statically-typed and compiled language, in much the same way that a large enough office building needs a statically numbered and riveted room-numbering scheme. As the scale of a python project grows, the abstraction of the stack grows at a pace that exceeds it's time and space complexity. This means countless hours spent reading and re-reading docs in order to accomplish simple changes because the blueprint of a typing system is not there. My recommendation is always to keep .py files under ~250 lines long and less than 10% of enterprise code base.


#### Contact
jonathan@coth.dev
