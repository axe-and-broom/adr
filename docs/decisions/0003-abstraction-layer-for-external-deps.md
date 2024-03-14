# Abstracton Layer for External Dependencies

## Context and Problem Statement

In most projects, there comes a point where integration with external dependencies becomes necessary. Whether it's interfacing with a 3rd party service or leveraging existing software for streamlined functionality.

The decision-making process involves determining whether to directly incorporate the external dependency into the codebase or to create an abstraction layer.


## Considered Options

1. **Direct Use of External Dependency:** Incorporating the external dependency directly into the codebase without abstraction. This option involves directly invoking functions or methods provided by the external dependency within the application code. It offers simplicity in implementation but may lead to tight coupling and increased complexity in maintenance.

2. **Abstraction Layer for External Dependency:**
Developing an abstraction layer that acts as an intermediary between the application code and the external dependency. This option introduces an additional layer of abstraction, providing benefits such as decoupling the application from the specifics of the external dependency, facilitating easier testing, and allowing for seamless substitution or updates of the dependency in the future.


## Decision Outcome

Chosen option: **Abstraction Layer for External Dependency**

The decision has been made to implement an abstraction layer for managing external dependencies. This choice is based on several factors:

**Decoupling:** By abstracting the external dependency, we can decouple our application code from the specifics of the dependency's implementation. This reduces the risk of being tightly bound to the external service, making it easier to adapt to changes or switch to alternative solutions in the future.

**Maintainability:** An abstraction layer promotes cleaner code organization and easier maintenance. It allows us to encapsulate the intricacies of interacting with the external dependency, making the codebase more modular and easier to understand.

**Testability:** With an abstraction layer in place, unit testing becomes more straightforward. Faking, mocking or stubbing the external dependency becomes feasible, enabling thorough testing of our application logic in isolation.

**Flexibility:** Introducing an abstraction layer provides flexibility in terms of future enhancements or changes. We can extend or modify the functionality of the external dependency without directly impacting the rest of the application.


## Realworld examples

### Example 1: External dep update brought breaking changes

We had a project that used an external dependency for remote configuration and feature flagging. We early on took the decision to create an abstraction layer for this dependency. Not only for the reasons mentioned in the decision outcome, but also because we wanted an even simpler API for the developers in the project to interact with. In the back of our minds we also thought that if we ever needed to switch to another provider, we could do so without having to change the entire codebase.

Turns out this was a very wise and lucky move on our part. The external dependency we used sometimes brought behaviour breaking changes in their updates. This would have been a nightmare to handle if we had not had the abstraction layer in place. Instead, we could patch the abstraction layer and the rest of the codebase was none the wiser.

### Example 2: External Github Actions in workflows

We had a repo that used Github Actions for CI/CD. The repo was used as a monorepo with shared modules and multiple projects which in turn built multiple targets, the workflows were quite extensive. We started out like anyone else and included external actions from the github marketplace directly into our workflows. This worked fine for a while. However as time went on and we needed to bump the versions of the external actions we used it was a hazzle to search through all places where the action was used and update the version. We decided to create an abstraction layer for the external actions. 

We decided to wrap any action that was used more than once in a custom action that was hosted in the same monorepo. This way we could update the version of the action in one place and all workflows would be updated. This also allowed us to add custom functionality to the actions that we used. 