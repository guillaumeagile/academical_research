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



### Event Storming as a way to extended interaction & collaboration throughout the design phase


### Using Maps ?



##  Interaction inside the build team 

### Code Reviews and metrics

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

What are the elements that the code can provide to improve collaboration with the Customers?



## Toward an Ubiquitous Language

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

## Architectures enabling changes

## Verifications enabling changes

## Insurances that changes are not breaking




## Evolutions in code
When changes are evolution, how to cope with it?