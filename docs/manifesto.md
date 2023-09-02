---
layout: page
title: Software Manifesto
---

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

#### How do you solve the two hard problems in computer science?

1. `$ rm -rf ./my_repo/my_cache/`

2. Namespace like a file system, but recursively
   - `project.project_module.project_module_class.project_module_class_operation`

      - tokens in a method from inheritance start point `class_token_a` or with specification as `project_class_token_a`

      - tokens in a function are modular nomers `module_token_a` or with specification as `project_module_token_a`

#### Contact
jonathan@coth.dev
