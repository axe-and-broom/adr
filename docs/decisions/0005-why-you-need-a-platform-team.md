# Why you need a platform team

Having a platform team is a great investment that will pay dividends in the long run. It will make the other teams more efficient and it will make the project more stable. It will make it easier to refactor, maintain and migrate to new technologies. It will make it easier to onboard new developers and it will make it easier to work together as a team.

## Context and Problem Statement

App projects are often built by a team of developers that are responsible for the whole project. This means that the team is responsible for everything from the codebase to the infrastructure. This can be a good approach for small projects but as the project grows it can be hard to keep up with everything. 

When the project grows the team often needs to split up into smaller teams that are responsible for different parts of the project. While this is good to increase focus and depth of features. The teams need to work together and they need to be aligned. They need to have a common understanding of the project and they need to have a common way of working.

As part of teams splitting up and working on different parts of the project they some times end up with different ways of working. They might have different coding standards, different ways of deploying, different ways of monitoring, different ways of testing, different ways of documenting, different ways of communicating, different ways of working with the infrastructure and so on. This can be a big problem when the teams need to work together and when they need to work on the same codebase.

## Platform Team - The missing piece

We have been in projects before where the stability of the platform and foundation that the developers write code ontop as a whole has not been keeping up with the changes to the structure of the project. 

### Anyone heard of "release master" and "feature teams"?

In order to keep releasing the product without having a dedicated team to do it most companies opt for a rotating "release master" role. While this in theory means that everyone owns the release process it often means that no one does. A platform team can step in here and focus on the release process and make sure that it is as smooth as possible. Ideally a release should be fully automated and happen without any manual intervention at a fixed interval.

### Hard to deal with refactoring and migrations

If no team owns the platform you also don't have a team that focuses on making it easy to build and maintain the product. You want someone to build and push for having abstractions for common things like storage, networking, logging, monitoring, testing etc. If those abstractions are there it becomes easier to refactor, maintain and migrate to new technologies throughout the codebase.

### A team that solely focuses on quality and efficiency

Ideally a platform team should be making you money by making the other teams more efficient. They should be the team that makes sure that the other teams can focus on building features and not having to worry about the infrastructure. They should be the team that makes sure that the other teams can focus on writing code and not having to worry about basic things like storage, networking etc. They should be the team that makes sure that the other teams can focus on features.


## Real world examples

### Long term assignment at a client

We had been at a long time assignment at a client who grew a lot during our stay. The app project was a number of years old already and the client had bought some competitors and we separately maintained multiple different apps in different teams in different countries with little to no conversation.

The team size at the time was only around 12-15 but we saw a need for a couple of different things in order for the product to become easier to maintain and develop. Releaseing the app was done through a rotating "release master" role with written instructions on what commands and bitrise workflows to run and in what order. The instructions were rusty and most of the time we relied on the previous release master for guidance.

Over the time we spent at the client we pushed for forming a Design System team to deal with the visual appearance, accessibility and providing easy to use composable components. We also pushed for a Platform team to deal with the release process, base libraries, best practices, project structure, infrastructure, and monitoring.

As a result of this we managed to introduce a monorepo for all the apps, make releases almost a non-event for all apps, increase quality, implement modularization so apps could share modules and code could be written and tested in isolation, implement fantastic developer and employee tooling for debugging and testing new features behind feature flags and many more things.

For this client having a platform team that could focus on making the other teams more efficient paid itself back many times over.