# Abstract

# Keywords

# Introduction

# Obervation: the Agile Manifesto

The manifesto exposes 4 values written in the same form:
&lt;X&gt; over &lt;Y&gt;
where X is a value (or set of values) that comes other Y.

We will focus on X and have no discussion on Y in this paper. 

# First value : Individuals and interactions

 In a development team, how can the code be a medium between individuals and ease interactions?
In an agile perspective (or an agile ideal), the developement team, often mentionned as 'the team', should include: testers, ergonomists, front end developpers, back end devs, data specialists, devOps engineers, technical leaders, architects and so on.

The aspect of sharing informations with the end users (aka customers) is exposed in the third value.

##  Interaction between the build team and the stakeholders
Modelisation: what model is easy to share and interact with?  Which consequences for the code?

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


### the importance of Ubiquitous Languge

While a lot of practices, tools, recipes exists to emphase communication between people in an agile IT environment, one major drawback is still human language.
The need of an Ubiquitous, shared langugage is absolutly vital between end users, business experts and people involved in the production of the software deliveries.
Because what is delivered is what the software engineers did have understood.
And most of all, what is delivered is the result of code source, being compiled and distributed, even on premises or on a cloud infrastructure.

Classical Agile methodologies often end on the side of project management and requirement gathering (with the final aim of writing user stories). But there's a lack of considerations about the code, which still remains an obscure face of the long process of building software.

One must look for guidelines and practices beyond the Agile Manifesto, hence use mostly common sense, or less known guidances such as Domain Driven Development, coined and developped by Eric Evans

Ubiquitous Language is modeled within a Limited context (so called bounded), where the terms and concepts of the business domain are identified, and there should be no ambiguity.


##  Interaction inside the build team 

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

### Code Reviews and metrics

Individuals (the coders) havre also they own channel to discuss.
We're not going to talk about tools. As they still are many and other studies exist to discuss their usage.

The coders are in perpetual interaction each other when they write, read and fix code.
Source code, as I said, is a vector.
A vector of shared knowledge, but also intentions.
That's why code review is an important interaction whithin the members of the team around the code.
It's a time where people should discuss is the problem has properly been understood and if the solution is viable and 


### Sprint Review and metrics


### Decision Records


## Interactions in code: it's all about dependencies


---------------------
# Second value : Working software 

How can we ensure that the software is working?

## Difference between V&V and tests

## Validations and Verifications

### The tests pyramid

### Unit tests 

## Tests: a human factor

## On the feedback loop

---------------
# Third value : Customer collaboration 

What are the elements that the code and the developement team can reveal to improve collaboration with the Customers?


## Based on an Ubiquitous Language

As mentionned in the 1st principle of collaboration over processes, people will understand each other in a better way if they speak the same language.
More than the native tongue, it is also important to agree on the meaning behind terms and acronyms.
In that sense, and to avoid a lot of unproductive meeetings, it is interesting to involve end users and domain experts into the process of co-creation.
For that, they need to build a common glossary and progress on disambiguate any term or concept coming from the business/end user side.
The aim is to discuss, research, conceptualize, develop and speak the Ubiquitous Language of the Domain Model.

### Event Storming as a way to extended interaction & collaboration throughout the design phase

One very efficient way is the Event Storming (or more recently moved in Event Modeling) meeting.
It brings togethers those who have the knowledge of the business concerns, the needs of the customers, but also the imperative of regulations or law inforcements with the ones in charge of the development and the integration of the product with other systems (the technical parts). In that mutual exercise they simply discuss and share higly valuable knowledge while producing artefacts that will become the angular stone of the code.

Those ertefacts are: Aggregates of information, views of the model, views of the future HMI, policies, events in a timeline, commands and systems. 
They are not complete, just a sketch, but enough to start coding and most important an ongoing conversation between stakeholders.

## ATDD and BDD
Another form of collaboration is to involve the End Users and the Domain Experts in the inception of verification.

"What comes out in production is what the developers have understood"

## Domain Modeling

As seen in chapter of "Event Storming", what comes right next after a Workshop where ideas emerge, is to catpure the shared knowledge into a tangible and applicable model.
On can be attached to UML modeling while others prefer putting it down directly to code.
There's many tools that handle reverse direction mapping between code and a model like UML
In fact, there's is no reason that code and model should be seperated. They hold the same information.
As duplicating information is an absolute anti pattern, one should choose wich should master and be the reference for the design: either the UML representation, or the code.

Benefit of the code: it is compiled easily and quickly, thus verified again 


## Human Readable Verification

## Human Readable code

--------------
# Fourth value : Responding to change

How can the code help us to facilitate any responses to change?

Quote: "Make the change easy, the make the easy change" (Kent Beck).

## Nature of changes

## Why code is difficult to change

Explain here the connanscence problema.
https://www.maibornwolff.de/en/blog/connascence-rules-good-software-design

In the common sense, connascence is the act of growing together.
In the code, it is the relationship between two or more elements (packages, components, classes or functions) in which changing one necessitates changing the others in order to maintain overall correctness.

+ illustration


## Agile Code as a way to allow and minimize impact of change

### Agile code must be SOLID

## Architectures enabling changes

## Verifications enabling changes

## Insurances that changes are not breaking




## Evolutions in software
When changes are evolution, how to cope with it?



#References

[^1]: https://cucumber.io/docs/tools/related-tools/
[^2]: https://www.nilslesieur.fr/2020/12/impact-mapping/
