# Abstracton Layer for External Dependencies

## Context and Problem Statement

Working together in a big team or on a big project can be challenging. Especially when it comes to code quality. One of the things that can make it easier to be aligned and have a consistent code quality is to use linters. Linters can help you catch bugs, enforce coding standards, and ensure consistency across the codebase.

Another great use case for linters is to "stop the bleed" of an anti pattern or use of a deprecated API in the codebase. By adding a lint rule that catches the anti pattern or deprecated API you can stop the use of it in the codebase and make sure that it is not used in the future.

## Considered Options

1. **Use a prefab linter** Lint the codebase with a linter that catches common bugs, enforces coding standards, and ensures consistency across the codebase. This can be done with a linter like eslint, stylelint, swiftlint or similar.

2. **Lint the code and add custom rules** Lint the codebase with a linter that catches common bugs, enforces coding standards, and ensures consistency across the codebase. Add custom rules to the linter that catches anti patterns or use of deprecated APIs.

3. **Lint everything** Lint everything. This means that you are not just linting the code but also linting;
- code formatting
- usage of deprecated APIs
- file names
- folder hierarchies
- configuration files
- readme files
- documentation
- commit messages
- PR descriptions


## Decision Outcome

Chosen option: **Lint everything**

While most think of linters as this code formatting warning tool which complains about putting spaces in the wrong place, they can be so much more. Linters can be used to enforce coding standards, catch common bugs, ensure consistency across the codebase, gather insights about the codebase and the team, and stop the bleed of anti patterns or use of deprecated APIs.

### Consistency 

We are all different and we all write code a bit differently but when working together it is important to have a consistent codebase to make it more efficient to work together. If all code in all features or modules are written in the same way it is easier to understand all parts of the code and to move between different parts of the codebase.

### Quality 

If we identify a common bug or quality issue we can write a linter to catch it. This way we can make sure that the bug or quality issue is not introduced in the codebase in the future. This can be a great way to improve the quality of the codebase over time.

### Naming

In our projects we often have contribution guidelines stating how to name things like interfaces vs concrete implementations but instead of just putting it into text you can also write a linter that ensures that the naming conventions are followed.

### Metrics

You could extend your linters to also gather data about the codebase and the team. For example if you track the data over time using a nightly CI workflow you can follow trends in the codebase. You can also track the data over the team and see if there are any developers that are not following the coding standards or are using deprecated APIs to help them.

### Gamification

### Stop the bleed

Working together on a big codebase can be challenging and sometimes we need to deprecate an API or make all code use one implementation ovet another. This is not just about deprecating, it could be about stopping developers from directly using an API that is meant to be accessed through an abstraction layer. 

In the deprecation case you could declare the old API as deprecated which would result in a warning if used. In smaller codebaes it could be easy to migrate all existing usages yourself to the newer API but that is not realistic in all cases. Instead what you could do is to write a linter rule that results in an error (not a warning) and add all existing usages as temporary excludes. This would make sure that no new usages of the deprecated API is added to the codebase and that all existing usages can migrated over time.

In the abstraction layer case you might not be able to do much if you want to stop the use of a system lib or a globally imported 3rd party depencency. In this case you could write a linter that catches the use of the API and throws a warning. This way you can stop the use of the API in the codebase and make sure that it is not used in the future.


## Realworld examples

### Example 1: Deprecating an API in a big codebase

We had this big codebase where multiple teams with multiple developers contributed to different parts that they owned. At various times we ended up in a situation where we needed the whole codebase to move on from an old implementation to a new one.

Before going down the linter approach we used to mark the old API as deprecated resulting in hundreds of warnings throughout the codebase and communicated during chapter meetings about the deprecation. This worked to some extent but was a very slow process and worse, we saw usages of the old API being added to the codebase since people look at existing code and copy bits and pieces. The real problem here was that there were a sea of warnings and adding one more was not a big deal so the problem just kept growing.

After a while we started to look at linters as a good approach for this. We wrote a linter rule that caught the use of the old API and threw an error. We added all existing usages as temporary excludes and made sure that no new usages were added. This way we could stop the use of the old API in the codebase and make sure that it was not used in the future. Thanks to this approach we also got an exhaustive list of all usages of the old API in the linter rule exclude list which made it easier to assign work and migrate all usages to the new API.

### Example 2: Measuring migrations

We had a project where we wanted to migrate from one version of a UI component to another. We had teams working on different parts of the codebase and we wanted to make sure that all projects and teams were migrating to the new version of the UI component.

Instead of just using running linters in CI and posting warnings/errors we implemented a nightly CI workflow that ran the linters and gathered data about the codebase and the team. The linter warning data was split into different categories like;

- Code owner for the warning
- Which module the warning occured in
- Which file the warning occured in
- How many warnings there were per rule

By having all this data over time we could follow migration work from the deprecated UI component to the new one. We could see which teams were lagging behind and which teams were ahead allowing us to pinpoint where to spend efforts embedding with teams to help them migrate. This data was invaluable to us and helped us migrate the whole codebase to the new UI component so much faster than we would have been able to otherwise.

### Example 3: Positive linting

Everyone loves positives reinforcement and we are no different. We had a project where we wanted to make sure that all code was written in the same way. Like mentioned in Example 2, we were tracking migration from one UI component to another and we wanted to make sure that all new code was written in the same way. One way to track the usage of the new component was to implement a positive linter which counted usages of the new UI component in the nightly CI workflow. This gave us the valueable data insight during the migration that we desperately needed and allowed us to see exactly when we hit the threshold of 50% adoption or even 100% adoption.

Another way we used positive linting was to gamify PR feedback. We implemented some linters that looked for really good code patterns and usages of new important APIs. When these linters were finding things in PR diffs they would congratulate the developer in the PR for writing good code. This was a great way to give positive feedback to developers and to make sure that the good code patterns were spread throughout the codebase.
