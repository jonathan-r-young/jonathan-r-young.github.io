---
jupytext:
  cell_metadata_filter: -all
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.16.1
---

# Architecture Diagrams 101

Many IT professionals my find themselves performing the role of Architect by accident, as an evolution of a maturing role in the team or organisation. This guide is intended to help those looking to ensure that their architectures are communicated with maximum impact and clarity.

Communicating an Architecture usually starts with a visual approximation of what is intended to be created - a diagram of sorts. Even a simple sketch is the basis of a "model". The very simplest architecture starts with some sort of _context_ - the system in question and the things it interacts with.

In my experience, as an Open Group Certified Distinguished Architect, I see many IT architects creating diagrams that are lacking in effectiveness due to some common pitfalls.

## Common pitfalls and how to avoid them

### Over simplification

A common representation of an IT architecture might be the following:

```{mermaid}
graph LR
  Person---A(System A)
```

This very simple represention intuitively suggests the following:
- the `Person` entity is probably representing a human that is interacting with ...
- the `System A` entity, which is probably the subject of the project.

However, you are relying on the reader to make the same assumptions as you have when creating this diagram. Let's extend this model to add some complexity:

```{mermaid}
graph LR
  Person---A(System A)
  A---B(System B)
```

The same assumptions are likely to be made about the `Person` element, but now we don't really know what function or roles `System A` and `System B` perform, other than there is some sort of association between them. The names of these entities also do not imply any particular role. 

Let's apply some additional _annotation_ to guide the viewer to the same assumptions as we were thinking when we started, and a short description of each element. Remember we mentioned that this was a _context_ view (e.g. a System Context). 

- `System A` is our system of interest, and is the subject of the design. We can influence its characteristics.
- `System B` is an external system (a _System Actor_). We do not have any influence over its characteristics.
- `Person` is a human actor, an employee in this case, that is interacting with our system, performing the use cases needed to achieve the business goals related to this solution.

```{mermaid}
graph LR
  Person("«person»\nEmployee")-->A(System A)
  A-->B(System B)
```

```{mermaid}
graph LR
  Person("«person»\nEmployee")-->|"«uses»\nhttps"|A(System A)
  A-->|"«uses»\nhttps"|B("«external»\nSystem B")
```

```{mermaid}
C4Context
  title System Context diagram for System A
  Person(person, "Employee", "The user of the system.")
  Boundary(systemA,"System Boundary") {
    System("systemA", "System A", "The system of interest")
  }
  System_Ext("systemB","System B")
  Rel(person, systemA, "uses", "https")
  Rel(systemA, systemB, "uses", "https")
```

You can see that even with a little additional annotation, much more information is conveyed. We can immediately see the scope of the project, and a dependency on an external system. In this example we also add some clue as to the technology used (https).

 ```{mermaid}
 classDiagram
     direction LR
     A ..> B : «uses»
     classA --|> classB : Inheritance
     classC --* classD : Composition
     classE --o classF : Aggregation
     classG --> classH : Association
     classI -- classJ : Link(Solid)
     classK ..> classL : Dependency
     classM ..|> classN : Realization
     classO .. classP : Link(Dashed)
 ```