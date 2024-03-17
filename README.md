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
  - [2.1 Event storming](#21-event-storming)
    - [2.1.1 Event storming roles](#211-event-storming-roles)
    - [2.1.2 Required elements](#212-required-elements)
    - [2.1.3](#213)

# 1. What is DDD

Useful articles

Business:

https://www.lucidchart.com/blog/domain-driven-design-introduction

https://www.linkedin.com/pulse/entry-domain-driven-design-fundamentals-mohamed-hassan?trk=article-ssr-frontend-pulse_little-text-block

Technical implementation:

https://learn.microsoft.com/en-us/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/ddd-oriented-microservice

https://learn.microsoft.com/en-us/dotnet/architecture/cloud-native/introduce-eshoponcontainers-reference-app

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

## 2.1 Event storming

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

### 2.1.3

Map all events that occur in the process

Map all commands that caused those events

Map policies as reactions to events

Map external services, questions, actors

Map aggregates and read models

Group aggregates together to find boundries among functionalities. Draw lines around bounded context