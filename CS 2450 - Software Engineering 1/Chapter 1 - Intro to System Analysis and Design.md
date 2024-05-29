## System Development Life Cycle (SDLC)
---
==The *system development life cycle* is the process of understanding how an information system (IS) can support business needs by designing a system, building it, and delivering it to users.==

Major phases in the SDLC:
- Planning 
- Analysis
- Design 
- Implementation

#### Planning:
The planning phase is understanding ==WHY== an information system should be built and go about ==HOW== to go about building it.

Two Steps:
- ==*Project Initiation*==, figuring out how this information system will be valuable for the business and getting it approved.
- *==Project management==*, the project manager creates a workplace, staffs the project, and uses techniques to help the project go though the SDLC.

#### Analysis:
The analysis phase answers the questions of ==WHO== will use the system, ==WHAT== the system will do, and ==WHERE== and ==WHEN== it will be used. The project team researches any current system, looks at where to improve, and develops concepts.

Three Steps:
- *==Analysis strategy==*, a way to guide the project team's efforts. Looks at the ==current system (as-is system)== and its problems and then ways to design a ==new system (to-be system)==.
- *==Requirement gathering==*, usually done through interviews or questionnaires.
- *==System proposal==*, is the analyses, system concept, and models which are presented.

#### Design:
The design phase decides how the system will operate, in terms of the hardware, software, and network infrastructures; the user interface, forms, and reports; and the specific programs, databases, and files that will be needed.

Four Steps:
- ==*Design Strategy*==, the first to develop. This clarifies whether the system will be developed in-house or outsourced to another company or if the company will buy existing software.
- ==*Architecture Design*==, describes the hardware, software, and network infrastructure needed for the new system.
- ==*Database and File Specifications*==, this defines exactly what data is to be stored and where. 
- ==*Program Design*==, determines what programs need to be written and what each program will do.

#### Implementation:
The final phase in the SDLC is the Implementation phase, during which the system is ==actually== built (or purchased).

This phase has Three steps:
- ==*System Construction*==, The system is built and tested to ensure it performs as designed.
- ==*Installation*==, the process of installing the new system and turning off the old.
- ==*Support Plan*==, includes formal or informal post-implementation review and support for future patches.

What are the roles of a project sponsor and the approval committee?
- The project sponsor is the person or department that generated the request to create the system. The approval committee decide if the project should be undertaken.

What does _gradual refinement_ mean in the context of SDLC?
- Gradual refinement means that over each step in the SDLC (Planning, Analysis, Design, and Implementation) the system goes from vague to defined. Each phase refines and elaborates on the work from previous phases.

## System Development Methodologies:
---
Structured Design, Rapid Application Development, and Agile Development.
### Structured Design:
A formal ==Step-by-step== approach to the SDLC phases which moves from one phase to another.

##### Waterfall Development:
the original structured design methodology.
Hard to go back up the waterfall (going back to previous phases).
![[Pasted image 20230830120429.png]]
Advantages:
- identifies system requirement log before programming begins 
- minimized changes to requirements

Disadvantages:
- design must be completely specified before programming begins.

##### Parallel Development:
Addresses the problem of long delays between the analysis phase and the delivery of the system. 
![[Pasted image 20230830120501.png]]
Advantages:
- reduce the time to deliver a system.

Disadvantages:
- subprojects are not completely independent.
- need to integrate after subprojects.

### Rapid Application Development (RAD):
emerged in 1990's

##### Phased Development: 
Breaks an overall system into a series of ==version== that are developed sequentially.
The most important features are baked into version 1.
![[Pasted image 20230830120527.png]]
Advantages:
- quickly gets a useful system into the hands of the users.

Disadvantages:
- begin to work with systems that are intentionally incomplete.

##### Prototyping:
Preformed the analysis, design, and implementation phases concurrently, and all three phases are preformed repeatedly in a cycle until the system is completed.
![[Pasted image 20230830120611.png]]
Advantages:
- quickly provides a system with which the users can interact

Disadvantages:
- fast-paced system releases challenge attempts to conduct careful, methodical analysis. Often the prototype undergoes such significant changes that many initial design decisions become poor ones

##### Throwaway Prototyping:
similar to prototyping-based methodologies however, throwaway prototypes are done at a different point in the SDLC.

a *design prototype* is the idea without it actually working

"Each of the prototypes is used to minimize the risk associated with the system by confirming that important issues are understood before the real system is built"
![[Pasted image 20230830121534.png]]
==balance the benefits of well-thought-out analysis and design phases with the advantages of using prototypes to refine key issues before a system is built==
A design prototype is not a working system.
uses mockup screens to assess what needs to be fixed.
Takes longer than normal prototyping but delivers more stable product.

### Agile Development:
Based on the agile manifesto and a set of twelve principles:
1. Software is delivered early and continuously through the development process, satisfying the customer.
2. Changing requirements are embraced regardless of when they occur in the development process. 
3. Working software is delivered frequently to the customer. 
4. Customers and developers work together to solve the business problem. 
5. Motivated individuals create solutions; provide them the tools and environment they need, and trust them to deliver. 
6. Face-to-face communication within the development team is the most efficient and effective method of gathering requirements.
7. The primary measure of progress is working, executing software.
8. Both customers and developers should work at a pace that is sustainable. That is, the level of work could be maintained indefinitely without any worker burnout.
9. Agility is heightened through attention to both technical excellence and good design.
10. Simplicity, the avoidance of unnecessary work, is essential. 
11. Self-organizing teams develop the best architectures, requirements, and designs.
12. Development teams regularly reflect on how to improve their development processes.
Much of the modeling and documentation overhead and the time spent on those tasks are eliminated. Projects emphasize simple, iterative application development.
![[Pasted image 20230830131821.png]]
Downsides:
- Because today's businesses outsources different development, agile will be less effective because agile requires co-location of the development team.

##### Extreme Programming (XP):
Four core values: 
- communication
- simplicity
- feedback
- courage

First, the developers must provide rapid feedback to the end users on a continuous basis.
Second, XP requires developers to follow the KISS principle. (Keep It Simple Stupid)
Third, developers must make incremental changes to grow the system, and they must not only accept change, they must embrace change.
Fourth, developers must have a quality-first mentality

Testing and efficient coding practices are the core of XP.
Standards are very important to minimize confusion

XP projects deliver results sooner than even the RAD approaches

##### Scrum:
Scrum is a methodology that “embraces chaos” meaning that the only thing to do is just try to control the chaos that ensues when development starts.

Teams are self-organized and self-directed.
Scrum teams do not have a designated team leader
==iteration== is the term for each "Sprint" of the ball.

flow:
- teams organize themselves in a symbiotic manner and set their own goals for each sprint (iteration)
- Any new requirements that are uncovered are placed on a backlog of requirements that still need to be addressed
- At the end of each sprint, the team demonstrates the soft ware to the client.
- Based on the results of the sprint, a new plan is begun for the next sprint

Drawbacks:
- Scrum might not scale up to develop very large, mission-critical systems.
- only has 7 people per scrum

## Selecting the Appropriate Development Methodology:
---
![[Pasted image 20230831091034.png]]

Key Factors:
- ==Clarity of User Requirements==, Users normally need to interact with technology to really understand what a new system can do and how to best apply it to their needs. 
- ==Familiarity with Technology==, When the system will use new technology with which the analysts and programmers are not familiar, early application of the new technology in the methodology will improve the chance of success.
- ==System Complexity==, Complex systems require careful and detailed analysis and design.
- ==System Reliability==, For some applications, reliability is truly critical (e.g., medical equipment, missile-control systems), whereas for other applications (e.g., games, Internet video) it is merely important.
- ==Short Time Schedules==, RAD-based and agile methodologies are excellent choices when timelines are short because they best enable the project team to adjust the functionality in the system based on a specific delivery date.
- ==Schedule Visibility==, One of the greatest challenges in systems development is determining whether a project is on schedule.

## OBJECT-ORIENTED SYSTEMS ANALYSIS AND DESIGN (OOSAD):
---
any modern object-oriented approach to developing information systems must be ==use-case driven==, ==architecture-centric==, and ==iterative and incremental==.

#### Use-Case Driven:
Use-case driven means that *use cases* are the primary modeling tools defining the behavior of the system.
A use case describes how the user interacts with the system to perform some activity, such as placing an order, making a reservation, or searching for information.

#### Architecture-Centric:
Architecture-centric means that the underlying software architecture of the evolving system specification drives the specification, construction, and documentation of the system.

support three architectural views of a system:
- functional, the behavior of the system from the perspective of the user. 
- static, the system in terms of attributes, methods, classes, and relationships.
- dynamic, messages passed among objects and state changes within an object.

#### Iterative and Incremental:
the systems analysts develop their understanding of a user’s problem by building up the three architectural views little by little.
![[Pasted image 20230831111333.png]]

#### The Benefits of OOSAD:
Concepts in the object-oriented approach enable analysts to break a complex system into smaller, more-manageable modules, work on the modules individually, and easily piece the modules back together to form an information system.

## THE UNIFIED PROCESS:
---
The Unified Process is a specific methodology that maps out when and how to use the various Unified Modeling Language (UML) techniques for object-oriented analysis and design.

