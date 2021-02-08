# Abstract

# Keywords

# Introduction


The purpose of this paper is to scan the Agile Manifesto through the lens of software developpers, the people that produce code.

As a reminder, these four values of the Manifesto are:

1.     Individuals and interactions over processes and tools
2.     Working software over comprehensive documentation
3.     Customer collaboration over contract negotiation
4.     Responding to change over following a plan 

We will focus on X and any discussion on Y are out of the scope in this paper.
We did not work on agile principles. Even if some of the twelve principles can be considered as refinements of agile values, others are just consequences of scrupulous application of a value, and the remaining are expected benefits on the functioning of the team (collaborations runned, transparency builded, and motivation improved). 

What are the best practices promoted by agile methods to help the team to efficiency work with these four values? How recognize that these values have applied considering the final product: software and code. In this work, we try to respond to these two questions.


Code is the only tangible, executable, verifiable and valuable asset that is produced when a software is build.

Whatever are the amount (and valuable) of work done by Scrum Masters, Product Owners, Release Train Engineers; the one and only asset that goes into production is what the software developpers have undestood.

It is then usefull to research what are the different impacts of code source in the four first values of the Agile Manifesto.



# First value : Individuals and interactions

 In a development team, how can the code be a medium between individuals and ease interactions?
In an agile perspective (or an agile ideal), the developement team, often mentionned as 'the team', should include: testers, ergonomists, front end developpers, back end devs, data specialists, devOps engineers, technical leaders, architects and so on.

The aspect of sharing informations with the end users (and customers) is discussed in the third value.


### The importance of Shared Language among developpers

While a lot of practices, tools, recipes exists to emphase communication between people in an agile IT environment, one major drawback is still human language.
The need of an ubiquitous, shared langugage is absolutly vital between end users, business experts and people involved in the production of the software deliveries.
Because what is delivered is what the software engineers did have understood.
And most of all, what is delivered is the result of code source, being compiled and distributed, even on premises or on a cloud infrastructure.

Classical Agile methodologies often end on the side of project management and requirement gathering (with the final aim of writing user stories). But there's a lack of considerations about the code, which still remains an obscure face of the long process of building software.

One must look for guidelines and practices beyond the Agile Manifesto, hence use mostly common sense, or less known guidances such as Domain Driven Development, coined and developped by Eric Evans

One of the great advantages of the Ubiquitous Language is to bring together the domain experts, the technical team, and the others involved in the project. 
 The Language used between individuals should never be a set of terms and technical jargons imposed by developpers;
 on the contrary, it should be developed in agreement of the whole team. The Ubiquitous Language must be spoken at all times between the team members and expressed in the software model.

Shared Language is modeled within a Limited context (so called bounded), where the terms and concepts of the business domain are identified, and there should be no ambiguity.

It eliminates inaccuracies and contradictions from domain experts. And of course misunderstanding from the technical team. It shall avoid the issue of "translations", whether it could be technical translations or countries/dialects translations.
It has a trend to evolve throughout the lifetime of the project or the product lifecycle.

A first good practice is to create a glossary of all terms with definitions and disambiguations.

This leads the technical team to write the code and its specifications with the same words, whithin the same context, always. Thus it makes the interactions inside the technical team far more easy.

##  Interactions inside the technical team 

Individuals and interactions are of course adressed in the Third value : Customer collaboration.
But what remains to explore are interactions whithin the development team.
Agility comes with a lot of innovations in terms of having people working together more seamlessly and fluently.
How can this translate when it comes to code?

Code (source code) is not only what will be compiled and produces an executable asset;
Code has became more and more expressive, fluent. Through the evolution of programing language (think about how an assembly code looks like, it's barely unreadable for a human being) in one hand, and the rise of better libraries, framework and practices.
Let's dive into more details:

### Code Readabilty
The ability of reading fluently a source code come from multiple factors:
- speak the Ubiquitous Language of the bussiness and the clients : as said before it's a consequence of empowering interactions between stakeholders.
- follow a design/conception that is close to the business needs: applying the recommandations of DDD, and name everything upon the Ubiquitous Language.


### Test understandably is at least as important as code
On the way to share knowledge, code is an interesting vector, but it has to be verified and behind code is another code: the code needed to verify its behavior.
In that sense, a better way to interact with and priorly understand code is to read tests.
Good Tests, written in the TDD cycle of working, must express a clear intention (through exposing clear ARRANGE and ACT steps) and also even more clear expectation (using well expressed ASSERTIONS).
We're talking about unit tests of course, those close to the code.
It is the exact location where we can verify that the Ubiquituous appears in the naming of classes, properties and method.
It is where we can judge of the quality of code, the way it has to be used;it reveals any flaws in the object design and the domain rules and their cohesion.

As tests act as the first real user of the code, they prove a concrete, verifiable interaction whith it.
And they are error prone. Because on one hand they compile (static type verification), then they pass! (they have to).

Although those tests are code themselves, they are written by a human being.
One can think that tests are only written by developpers, but not only.
With the now acclaimed use of Agile practices such as User Stories, Story Mapping [^2], Impact Mapping and so on, non technicians are able to write acceptance tests, or behavior expectations.
Those expectations can lead directly to code through Excecutable Specifications.
They are to be written in a human readable language, in a specific form using these keywords at the beginning of each sentences (in English, but translatable to any dialect): Given / When / Then.
Then we associate (map) some code behind the natural language, through the use of Regular Expressions.
Many test libraries allow to do that and target unit test code written in Java, C#, TypeScript, Java Script, PHP, Ruby, etc.
The top library acheiving this is Cucumber and there are many tools and test runtimes to make it work in any CI/CD pipeline [^1]. One can also use the Fitness framework.

The observable result is that tests are now reflecting code, or at least the Domain Model in the same form that it is expressed in code: events, aggregates, even class names or abstraction names are trully and durably in the code.
And they are covariants. Always synchronised; otherwise the code cannot compile and the tests cannot pass.

Further more, when we mention unit testing, or technical tests, it expresses what developpers have understood about the domain and its subtleness.

With those processes (tests and code together written as a base to interact between stakeholders), we are acheiving one most precious thing in the art of software development: a *Single Source of Trust*.

And a way to talk between technicians and non technicians about the expected behavior of what is to be delivered.

### Pair Programming & Mob Programming

The agile manifesto didn't say much about how to drive interactions within the technical teams.
However, throughout time, some practices have emerged among  agile developpers; Pair Programming and more recently Mob Programming.
Pair programming is an Agile technique originating from Extreme programming (XP) in which two developers team together and work on one computer. The two people work together, at the same desktop and in front of only one computer to design, code and test user stories.
It encourages the use of emergent design.
In a pair, we have a driver and a navigator. Like in driving a rally. The driver is hands on the wheel, and in control of paying attention to the immediate task at hand. For the driver checking the map would be a distraction. That is where the navigator is needed to Keep track of goals on a larger scale, paying attention to other level of details they can help significantly in getting to better results.
 Navigator takes care of directions and instructions, and feeding them to the driver as needed.
 Navigator thinks and driver only type code on screen. 
 Most important thing is that they actively talk to each other. They're having a permanent discussion.

But this practice is not enough when it comes to share problems and solutions to the rest of the team.

That's why Mob Programming is an interesting agile complement. 
2014 Woody Zuill originally described Mob Programming in an Experience Report at Agile2014 [^3].
The principle is extending the Pair Programming to the whole group of technicians, but also can open to non technician people involved in the building of the software solution.
There is still the role of the Driver and the Navigator, but it shifts at fixed time intervalls accross the whole group. The navigator only collect the ideas of the rest of the group. The driver says nothing, just acting as mecanical type writer.



### Code Repository (sharing)

l'outil de repository , et les outils de code review
voir outil Themis 
...... . . . . . .


### Code Reviews and metrics

Individuals (the coders) havre also they own channel to discuss.
We're not going to talk about tools. As they still are many on the market and other studies exist to discuss their usage and benefits.

The coders are in perpetual interaction each other when they write, read and fix code.
Source code, as said, is a vector.
A vector of shared knowledge, but also intentions.

That's why code reviews (CRs) is an important interaction whithin the members of the team around the code.

It's a time where people should discuss if the problem has properly been understood and if the proposed solution is viable .
They exchange ideas about how it is coded and can improve (refactor) for clearer reading or for revealing intentions.
It as also very important to ensure during that phase, the future of the interactions with code, namely: maintenance.

Maintenance is an expensive phase, often cause by error in programming (and so a lack of CRs, or poor CRs) or undestanding (low quality interaction with POs and PPOs, or PMs).

Code review is also the time for evaluating the level of shared knowledge that comes to the engineering team.

{trouver des papiers sur les codes reviews}
https://queue-it.com/blog/agile-code-review-best-practices/
  https://www.amazon.com/Code-Complete-Practical-Handbook-Construction/dp/0735619670



### Architecture Decision Records
Although we are going to discuss a form of documentation, it is important to remember that Architecture and code are conversations in first place.
Then, those conversations needs to be recorded.

> cf Quick Design Session: Xtreme Programming

> caser les C4 et UML ici

The Architecture Decision Records (ADR) are actually not really about documenting the current, or future, state of an application architecture, but instead the reasons that led to it. They are specially important because they intend to tell others, and our future selves, why the architecture, therefore the code, is as it is.

An ADR is a log entry about the architecture decisions that have been made and that lead to the state of the architecture as it is now or as it is intended to be in the future. They contain the why behind the the diagrams that describe the architecture.

ADR are written in a simple MarkDown (MD) language.

To start, there are a few artefacts that we need to know:

Architecturally-Significant Requirement (ASR): a requirement that has a measurable effect on a software system’s architecture;
Architecture Decision (AD): a software design choice that addresses a significant requirement;
Architecture Decision Record (ADR): a document that captures an important architectural decision made along with its context and consequences;
Architecture Decision Log (ADL): the collection of all ADRs created and maintained for a particular project (or organisation);
Architecture Knowledge Management (AKM): the higher sphere of all previous concepts.


---------------------
# Second value : Working software 

The second value is to be understood as: delevering a software that whithout bugs has higher value than (just) producing a extensive documentation of it.

In the common sense, we could say: more code, less unused papers.

With all the years and practices of developing software guided by the Manifesto, and also bearing in mind the principles of Xtreme Programming, it appears that the best documentation one can made for a software is the code itself.

That momentum has been coined under the name of Living Documentation by Cyrille Martaire (ISBN-13: 978-0134689326), based on the widely used concept of "Living Documents" 
 Shanahan, Daniel R (11 April 2015). "A living document: reincarnating the research article". Trials. 16 (1): 151. doi:10.1186/s13063-015-0666-5. PMC 4403711. PMID 25873052. 

A code that works has great value for the end users; rather than a code with bugs.
A code that is tested and that easy to read and maintain has a great value for developpers.

We shall define a working software as this: it shall be delivered from a code that works and that is of the greatest intrinsic quality, as defined above.


> Clean Code that Works (Kent Beck)





> Not only working software but also well crafted software ()




## a Working Software must have Verifications and Validations

Verification checks whether the software confirms a specification whereas Validation checks whether the software meets the requirements and expectations. 
Verification finds the bugs early in the development cycle whereas Validation finds the bugs that verification can not catch.

The most effective, error prone, robust, long lasting Verification a developper can made is when a test is written first.
It is the principle of TDD  (refs)

The consequences of praticing TDD continuously are:
 - one line of code has at least a mandatory test that covers it
 - one test that is written shall stay green forever when the code change (refactor) but the expected behaviour shall remain unchanged
 - a test has to follow the single responsibility principe: one test must only verify one behavior and one unit of code at the same time. It is the principle of "Testing in isolation" (refs)
- test must be stable, reproducible, independent running order, independant in degrees of parallelism
- test must verify expected behaviors, not implementation details.

https://www.researchgate.net/publication/236893390_Quality_of_Testing_in_Test_Driven_Development



## The need for automation in test

There are many ways to enforce verification and validation. But in a fist glance it falls into two categories: manual and automated testing.

We're looking at the 2nd principle of the Agile Manifesto through the lens of code.
Verification and validation can (and should) by made by code. Hence, they are also code.


 ## What is working ?

 Software is an assembly of many pieces.
 The difficulty is to have an efficient verification.
The process of verification is tightly coupled to the architectural choices of the software.

## Coupling and dependencies : how to verify it is working



 ## Verifications are feedback loops


## Heuristic for verifications

speed

robusteness

accuracy





Conclusion: automated verification are code! They shall obey the same rules.





---------------
# Third value : Customer collaboration 

> Right Product

What are the elements that the code and the developement team can reveal to improve collaboration with the Customers?




## Behaviour Driven : let's start verification: executable specification

Here is the boundaries between the 2nd and the 3rd principle of the manifesto: when the working software meets the collaboration with the customer.

We already asked ourselves: what is a working software?  A software whithout bugs.
But what are bugs? When the observable behavior is not what the customer has expected.

To verify that the people who wrote code need to have a clear explanation of what is expected.
Agile principles let emerge a various set of practices to express specification and expectation

Impact Mapping


Example Mapping

Use Cases

Acceptance TDD (ATDD).
 With ATDD you write a single acceptance test, or behavioral specification depending on your preferred terminology, and then just enough production functionality/code to fulfill that test. The goal of ATDD is to specify detailed, executable requirements for the project . ATDD comes along with Behavior Driven Development (BDD).

Behavior Driven Development (BDD).


> Based on an Ubiquitous Language

As mentionned in the 1st principle of collaboration over processes, people will understand each other in a better way if they speak the same language.
More than the native tongue, it is also important to agree on the meaning behind terms and acronyms.
In that sense, and to avoid a lot of unproductive meeetings, it is interesting to involve end users and domain experts into the process of co-creation.
For that, they need to build a common glossary and progress on disambiguate any term or concept coming from the business/end user side.
The aim is to discuss, research, conceptualize, develop and speak the Ubiquitous Language of the Domain Model.

> Fowler


### Event Storming as a way to extended interaction & collaboration throughout the design phase

One very efficient way is the Event Storming (or more recently moved in Event Modeling) meeting.
It brings togethers those who have the knowledge of the business concerns, the needs of the customers, but also the imperative of regulations or law inforcements with the ones in charge of the development and the integration of the product with other systems (the technical parts). In that mutual exercise they simply discuss and share higly valuable knowledge while producing artefacts that will become the angular stone of the code.

Those artefacts are: Aggregates of information, views of the model, views of the future HMI, policies, events in a timeline, commands and systems. 
They are not complete, just a sketch, but enough to start coding and most important an ongoing conversation between stakeholders.



## Domain Modeling

As seen in chapter of "Event Storming", what comes right next after a Workshop where ideas emerge, is to catpure the shared knowledge into a tangible and applicable model.
On can be attached to UML modeling while others prefer putting it down directly to code.
There's many tools that handle reverse direction mapping between code and a model like UML
In fact, there's is no reason that code and model should be seperated. They hold the same information.
As duplicating information is an absolute anti pattern, one should choose wich should master and be the reference for the design: either the UML representation, or the code.

Benefit of the code: it is compiled easily and quickly, thus verified again 


##  Partial Conclusion:  DDD is a valuable approach 



--------------
# Fourth value : Responding to change

How can the code help us to facilitate any responses to change?

>  "Make the change easy, the make the easy change" (Kent Beck).

Responding to change is -in pratice- a technical activity.

The software is the result of build and assembly pieces of code together. 
Delivering it  as a working result is challenging. Changing it can be difficult.

If the code of the software hasn't been engineered to accept changes along time, then responding to change will probably fail.

## Why code is difficult to change

Explain here the connascence problema.
https://www.maibornwolff.de/en/blog/connascence-rules-good-software-design

In the common sense, connascence is the act of growing together.
In the code, it is the relationship between two or more elements (packages, components, classes or functions) in which changing one necessitates changing the others in order to maintain overall correctness.

+ illustration


### Mutations, side effects and stateness make changes complicated


## SOLID heuristics are vitals

Open Close principle is the main element a coder should think of when he/she wants to respond to a need for change.


### Pattern are usefull to enforce SOLID




## Accept changes that won't break with Feedback Loops

TDD is the key for safe refactoring but also safely change or evolve the behavior of the software.


### Decoupling for easing the change




## Architectures enabling changes



### N-tiers

### Hexagonal / Onion Architecture

### CQRS
    
    pro / cons



## (??) a side note : on fucnctionnal programming and proof based languages



# Conclusion




------------------------
#(à déplacer qq part) Motivation 
### Breaking the monolith of design & conception phase
Traditional software project management guidelines (Waterfall, RUP) tend to avoid live interactions between the various actors of a project: from user to late end validators and receiptors, only a heavy and cheesy documentation was allowed. And all things must be expressed as a whole, a monolith; rarely in terms of increment.
Agile methodologies arrived to change this. But how the design and conception phased is durably impacted?

While going to discover the product backlog and its refinement through user stories, the need of design & conception process was still on the urge.

While some XP (eXtreme Programming) supporters said that one has just to code the solution (which is quite acceptable if you have the end user or the skateholders fully involved in the whole construction of the software), the vast majority still needs to express intermediates between User Stories and the code.

Thus, Agile practices encourage more human readable, and interactions prone, artefacts such as:
 - Express User Stories in a form using BDD / Gherkin / Cucumber 
 - Acceptance (Tests) Driven Development
 - Executable Specification

But also C4 Models (to move accross high level use case, architectural views, and code implementations) and traditionnal UML diagramms are still good candidates to encourage intense discussion with the stakeholders and the builder of the project/product.




#References

[^1]: https://cucumber.io/docs/tools/related-tools/
[^2]: https://www.nilslesieur.fr/2020/12/impact-mapping/
[^3]: https://www.agilealliance.org/glossary/mob-programming


