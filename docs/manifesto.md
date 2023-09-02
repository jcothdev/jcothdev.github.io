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

   - functional namespace:
      - Class methods
         - `project.project_module.project_module_class.project_module_class_$operation`
      - Module functions:
         -  `project.project_module.project_module_$operation`
      - some examples of $operation:
         - query
         - parse
         - initiate
         - obtain
         - create
         - complete
         - connect
         - append
         - delete
         - push
         - contains
   - field namespace:
      -   `project.project_module.project_module_class.class_token_a`
      -  disambiguated as  `project.project_module.project_module_class.project_class_token_a` OR `project.project_module.project_module_class.module_class_token_a`
   - module token namespace:
      -   `project.project_module.project_module_token_a`
    
#### Light mode, or dark mode?

Light mode. This is actually a very interesting debate coming from a biology background. The reason I use light mode is because the cone and rod cells in your retina use less energy when exposed to more light. The retina cells are essentially modified neurons equipped with an action potential that feeds into the optic nerve. There are specialized proteins on the visual surface the retina cells that change it's shape when exposed to certain wavelengths of light. Counterintuitively, when light is *not* hitting a retina cell, this protein is configured such that it opens the sodium/potassium channels of the optic synapses and causes rapid action potential firing. The exposure to light causes less neural activity in the optical nerve, meaning that less energy is being expended when your eyes are exposed to light. [source 1](https://www.ncbi.nlm.nih.gov/books/NBK10806), [source 2](https://en.wikipedia.org/wiki/Hyperpolarization_(biology))

This relates to the light mode vs dark mode debate because when developers are sitting at a screen, after many hours fatigue frequently sets in. A few months ago I remembered this fact about the retina and switched from dark to light mode. Since, I have experienced less fatigue overall even after a full day of work simply by saving my nervous system from expending the extra energy it uses on dark mode! **Disclaimer**: This is anecdotal, and I am not a physician. This should not be taken as medical advice.


#### Contact
jonathan@coth.dev
