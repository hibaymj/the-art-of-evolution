The general plan for the book is as follows.

Preface: Who is this book for?
* New and experienced API developers
* New and experienced platform architects
* New and experienced platform product owners

* Executives interested in Lean product ownership - APIs: The Executive Summary

Goals:
Understand the nuanced choices to create APIs which gracefully adapt over time.
Understand, measure, and eliminate the root causes of design inertia.
Right-sizing your constraints, picking the architecture for a pattern, and the pattern for an architecture.

A few words before all the REST. - Disecting the Architectural Pattern

SECTION 1 - The groundwork

1. Introduction to APIs
1.1 What IS an API: Cutting through the noise.
1.2 Why build with APIs?
1.3 Why not to build with APIs?
1.4 Why does evolution matter?

2. Design Inertia
2.1 Constraints: Friend or Foe?
2.2 Shaping the unknown
2.3 Separation of Concerns
2.4 Hold the line! aka the information hiding principle
2.5 Authority, state, and messages.

3. Knowing your Audience
3.1 APIs for humans
3.2 APIs for machines
3.3 APIs for both

4. Use the language of the audience
4.1 Ubiquitous Language
4.2 Typed Language
4.3 Bridging the Gap

5. Relationships
5.1 Anonymous
5.2 Contextless
5.3 Standard
5.4 Custom

6. Shedding the bikeshedding
6.1 Measuring the importance
6.2 Measuring the value
6.3 Measuring the impact
6.4 Measuring the use

7. Evolution
7.1 Designing For Change
7.2 Designing For Clarity
7.3 Designing For Death
7.4 Killing your creation.

SECTION 2 - Building, breaking, evolving, repeat.

Preface: In this section we will use an example of an issue tracker, building it over time using traditional patterns, exploring the concentration and causes of design inertia, and presenting multiple possible solutions.

The examples will follow multiple concurrent pathways through to a truly evolvable design to understand both the ways to identify common sources of inertia, as well as the telltale signs of more unique sources of inertia.

8. The initial issue. (Small, only limited functionality centered around created viewing and deleting an issue)
8.1 The first attempts - (RPC, poor resource, deep CRUD)
8.2 A language for our design
8.3 The first revisions


