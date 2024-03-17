- [1. What is DDD](#1-what-is-ddd)
  - [1.1 Key definitions](#11-key-definitions)
    - [1.1.1 Domain](#111-domain)
    - [1.1.2 Subdomain](#112-subdomain)
      - [1.1.2.1 Core Domain](#1121-core-domain)
      - [1.1.2.2 Supporting subdomain](#1122-supporting-subdomain)
      - [1.1.2.3 Generic Subdomain](#1123-generic-subdomain)
    - [1.1.3 Domain Expert](#113-domain-expert)
  - [1.2 Focus of DDD](#12-focus-of-ddd)
  - [1.3 Building blocks of DDD](#13-building-blocks-of-ddd)
- [2. How to begin](#2-how-to-begin)
  - [2.1 Have Event Storming Sessions](#21-have-event-storming-sessions)
    - [2.1.1 Event storming roles](#211-event-storming-roles)
    - [2.1.2 Required elements](#212-required-elements)
    - [2.1.3 Steps](#213-steps)
  - [2.2 Identify Bounded Context](#22-identify-bounded-context)
  - [2.3 Create and Update Ubiquitus Language](#23-create-and-update-ubiquitus-language)
    - [2.3.1 How to tackle communication challenges](#231-how-to-tackle-communication-challenges)
  - [2.4 Create Context Maps](#24-create-context-maps)
    - [2.4.1 Types of relationships](#241-types-of-relationships)
  - [2.5 Anti Corruption Layer](#25-anti-corruption-layer)
  - [2.6 Define Shared Kernels](#26-define-shared-kernels)

# 1. What is DDD

Useful articles

Business materials:

https://www.lucidchart.com/blog/domain-driven-design-introduction

https://www.linkedin.com/pulse/entry-domain-driven-design-fundamentals-mohamed-hassan?trk=article-ssr-frontend-pulse_little-text-block

Technical implementation materials:

https://learn.microsoft.com/en-us/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/ddd-oriented-microservice

https://learn.microsoft.com/en-us/dotnet/architecture/cloud-native/introduce-eshoponcontainers-reference-app

* Dev hint: Tricks with entity framework code first can be used to implement reaction/policies in Entities from CommandHandlers before DomainEvents are created and handled, and using unit of work to transact them after domain event is generated. Can be seen in eShop example.

## 1.1 Key definitions

### 1.1.1 Domain
Field or industry a business operates in. Contains many activities.
Example: Amazon e commerce contains Sales, Shipment, Fulfillment, Web Portal, AWS Hosting, Payment.

### 1.1.2 Subdomain
A domain can be broken down into several activities called subdomains. A subdomain can become a domain when focused on during the modeling process. 

Types of sub domain
#### 1.1.2.1 Core Domain
Main business flows and models. This is where core activities of the business is. eg. Discovering new medicine
#### 1.1.2.2 Supporting subdomain
All activities that need to exist to support the core business function. eg. pharmacy medicine stock management
#### 1.1.2.3 Generic Subdomain
Common across many domains, but not part of specific core subdomain. eg. payroll

### 1.1.3 Domain Expert
Goal is to understand the subdomains, and once identified, analyze them separately. It's difficult to master all domains, so people specialize and be domain expert in one domain while learning about others.

## 1.2 Focus of DDD
Use DDD only for complex domains, 

Domain Modeling

Break domain into smaller pieces

Works well with agile scrum mvp. Create a basic model that everyone understands, yet can be evolved sprint by sprint until complete product is done.

## 1.3 Building blocks of DDD
Entity

Value Object

Aggregate

Domain Event

Command

Query

Service

Repository

Factory

# 2. How to begin

## 2.1 Have Event Storming Sessions

Events are baked into domains, and they are used as communications between domains / subdomains to be consumed.

Event storming allow domain experts to share their complex business process with developers.

### 2.1.1 Event storming roles
Facilitator: Organizes the sessions and ensure the rules of the event storming are followed.

Domain Experts: Experts from subdomains whose processes and features that are set to be modeled.

Technical Experts: Responsible for the design and development of the software.

https://www.linkedin.com/pulse/how-use-event-storming-domain-driven-design-mohamed-hassan

### 2.1.2 Required elements

The individual colors of the sticky notes each represent something:

Orange (Events) are actions that happen in a domain, written in the past tense in domain experts’ language.

Blue (Commands) represent the intent of an actor, basically what the actor wants to do. They trigger / cause events

Purple (Policies) are Reactions combined with events. These reactions are necessary prerequisites to the execution of a command. If this prerequisite is not met, the reactions may even replace a command. They can be understood with the phrase: “whenever this event happens, then carry out this command or action.”

Yellow (Actors) represent the people or systems that execute a command.

Pink (third-party or internal systems) can emit or receive events.

Red (Questions or issues) reference something that is scheduled to be considered later on in the session. They should be explored in more detail.

Green (The read model) highlights the specific data that allows one to make a decision or carry out an action. They come from a SQL query, a specific part of the UI, or any data source. This sticky note can be placed below the command/event pair.

Pale yellow sticky (Aggregates) represent a specific business logic, with a particular responsibility. Aggregates let us discover bounded contexts.

### 2.1.3 Steps

Map all events that occur in the process

Map all commands that caused those events

Map policies as reactions to events

Map external services, questions, actors

Map aggregates and read models

Group aggregates together to find boundries among functionalities. Draw lines around them to form bounded context.

## 2.2 Identify Bounded Context

A bounded context is a strategic pattern used to maintain consistency between subdomains and their models. There must be a clear definition of limits between all of the bounded contexts that exist in a domain. These limits can be set during event storming.

* Subdomains are the problem space

* Bounded Contexts are the solution space

* Every bounded context is translated into one or more modules or microservices in the future.

When bounded contexts are defined, a team should take the following characteristics into account to confirm that they are designing bounded context well:

Each bounded context should possess its own domain model. Each subdomain represents its structure and the way that every part interacts with another.

Each bounded context uses its own ubiquitous language. Just because wording are the same doesn't mean they should be grouped in same bounding context if the meaning of the words are different in each domain.

There is a clear separation of vocabulary that exists inside each subdomain in a large organization. It guarantees a clear definition of responsibilities and concerns that an actor may encounter.

A domain model built for a bounded context is only suitable within its boundaries.

## 2.3 Create and Update Ubiquitus Language

When a domain is modeled during an event storming session, business experts may use business jargon and technical experts may use technical jargon. This will require both sides to translate the terms between each other, and may cause mistranslations and misinterpretations.

In DDD, both domain and technical experts must speak the same language to guarantee that the software evolves quickly over time, and to solve this DDD offers a strategic pattern called ubiquitous language. 

Ubiquitous language aims to avoid translations between the business and technical world to create a better understanding of the domain. 

Software that is built on top of ubiquitous language is easy to understand, because it reflects business terminology in its code. Such software needs access to the exact names and terms that are defined in a model.

### 2.3.1 How to tackle communication challenges
Ubiquitous language solves this problem. In each business context, ubiquitous language is used by all of the participants in the model-definition process.

The model has common terms and acronyms, which are all used within a defined context. If someone works in a specific context, it is implied that there is a context of particular and understandable terms. Different domains would have their own ubiquitous language.

Ubiquitous language should evolve over time. It should be well-documented in a repository, such as in a Confluence, for a team to manage their common terminology. 

This language consists of terms that are commonly used by business and technical experts. In other words, ubiquitous language is made up of a mixture of terminologies from both the business and the technical worlds.

Ubiquitous language must be used across source code, testing code, daily conversations between domain and technical experts, and documentation to guarantee correct understanding of the domain and avoids the need for translations.

## 2.4 Create Context Maps

Bounded contexts are independent, but they do not work in isolation. 

Context maps are mappings of the relationships between bounded contexts to understand the dependencies between them and how they communicate with each other.

They are a visual representation of the relationships that are present between different bounded contexts and show the interactions and the types of connections that bounded contexts share.

Context maps help to maintain clear communication between bounded contexts clearly showing what types of interactions occur during a business process. 

### 2.4.1 Types of relationships
Four types of relationships among bounded contexts

* Separate ways: No need to connect two bounded contexts, because that interaction will not give significant payoffs to a team. These bounded contexts implement their own logic and operate in a separate way.

* Symmetric relationship: Communication between two bounded contexts in both directions. This scenario is common in orchestrations where there is a component A that invokes component B. After an execution of something, component B invokes component A to convey the result (API)

* Asymmetric relationship: Communication between two bounded contexts in only one direction. Commonly connected by queues, where component A sends a message to component B through a queue and does not wait for a response.

* One-to-many relationship: Communication between two or more bounded contexts. Bounded context can connect and send messages to one or more bounded contexts. Commonly seen in publish-subscribe pattern, where component A sends a message to a broker, and the broker fan out that message to all of the subscribers.

## 2.5 Anti Corruption Layer
A strategic pattern in DDD. It's basically a translator. Helps with microservice communication, but avoids business logic. Some ACL patterns are Facade and Adapters.

## 2.6 Define Shared Kernels
External libraries ontains functionalities that are common across two or more bounded contexts. It avoids the repetition of code in several places and helps the projects evolve quickly over time.

Pros:

Reusability, because library can be included in many components.

Streamlining the development process, because a lot of common functionalities are developed when a team wants to develop a new component.

Government over components, because everyone controls changes.

Cons:

Require regular communication among all of the teams to evolve the shared kernel. Sometimes, this communication is difficult.

Need to be should be as small as possible, because it could slow down the development process if it becomes too big.

Must guarantee backward compatibility because it can cause failures in microservices.