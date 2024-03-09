# 0040 - The Danger of Code with Side Effects

Code that has side effects is arguably the most challenging kind of code. It's difficult to test, maintain, and comprehend. Additionally, reasoning about and refactoring such code becomes a Herculean task. In essence, it complicates every aspect of software development, making it an undesirable practice.

## Context and Problem Statement

Unfortunately, in larger organizations, it's common to encounter code riddled with side effects. Sometimes, there's even an implicit "side effect pattern" within the codebase, where developers knowingly write code that anticipates and depends on these side effects. This approach exacerbates the problem, leading to a fragile and confusing codebase.

## Considered Options

- Continue ignoring the issue, maintaining code that relies on side effects.
- Acknowledge the pitfalls of side-effect-laden code and take steps to rectify it.

## Decision Outcome

The chosen path is clear: we must acknowledge the dangers of code with side effects and take steps to minimize and eventually eliminate them.

## Understanding Side Effects

A side effect occurs when a function or operation modifies some state outside its local environment or has an observable interaction with the outside world beyond returning a value. This can include alterations to global variables, static variables, mutable reference arguments, or external resources such as databases or files.

### Example with Side Effects

Consider a scenario where we have a global variable that tracks the number of login attempts in a Swift application. A function modifies this global variable, illustrating a clear side effect.

```swift
var loginAttempts = 0

func incrementLoginAttempts() {
    loginAttempts += 1
}
```

In this example, `incrementLoginAttempts` function has a side effect of modifying the global `loginAttempts` variable. This can lead to several issues, such as difficulty in testing the function independently, challenges in understanding the function's impact without knowing about the global state, and potential race conditions in a multithreaded environment.

### Refactored Example Without Side Effects

To refactor this code into a side-effect-free version, we can return the new number of login attempts from the function instead of modifying a global variable. This approach makes the function's behavior explicit and eliminates the hidden dependency on external state.

```swift
func incrementLoginAttempts(currentAttempts: Int) -> Int {
    return currentAttempts + 1
}
```

Usage of the refactored function could look something like this:

```swift
let initialAttempts = 0
let newAttempts = incrementLoginAttempts(currentAttempts: initialAttempts)
```

This refactored function is a `pure` function now. Its output depends solely on its input, and it has no side effects such as modifying global state or external resources. This makes it much easier to test and reason about, as the function's behavior is predictable and isolated from the rest of the system.

### Further Improvements

To manage state more effectively in a larger application, you might consider using structures or classes that encapsulate the state and its related behavior. For example, a `UserSession` class could manage all session-related information, including login attempts.

```swift
class UserSession {
    private(set) var loginAttempts = 0

    func incrementLoginAttempts() -> Int {
        loginAttempts += 1
        return loginAttempts
    }
}

let session = UserSession()
let newAttempts = session.incrementLoginAttempts()

```

In this improved approach, the state (number of login attempts) is encapsulated within the `UserSession` class. This not only makes it easier to manage the state but also aligns with object-oriented principles, keeping related state and behavior together.

By focusing on minimizing side effects and writing pure functions, your Swift code becomes more modular, testable, and maintainable.

## Why Side Effects are Problematic

- Testing Challenges: Side effects make unit testing more complex since tests must account for the external state or interactions.
- Maintainability: Code with side effects is harder to understand and modify, as changes in one part can have unpredictable impacts elsewhere.
- Concurrent Execution: In multi-threaded or asynchronous environments, side effects can lead to race conditions and other concurrency issues.
- Debugging: Side effects can make it difficult to trace the source of a problem, especially when the codebase is large and complex.

## Strategies for Minimizing Side Effects

- Pure Functions: Strive to write pure functions whenever possible. A pure function's output should only depend on its input, without causing side effects.
- Immutability: Favor immutable data structures that cannot be modified after creation. This approach naturally reduces side effects.
- Encapsulation: Encapsulate side-effect-causing operations within well-defined boundaries, making them easier to manage and predict.
- Functional Programming Paradigms: Adopt functional programming techniques, such as using map, reduce, and filters for data transformations.

## Writing Side-Effect-Free Code: Techniques and Tools

- Dependency Injection: Pass dependencies to functions or modules instead of accessing or modifying global state.
- State Management: Utilize libraries designed for state management to centralize and control state changes in your applications.
- Reactive Programming: Consider reactive programming models that emphasize data streams and the propagation of change, which can help in managing side effects.
- Linters and Static Analysis Tools: Use tools that can identify and flag side-effect-causing code, helping to prevent it from creeping into the codebase.

## Conclusion

Mitigating and avoiding side effects in code is crucial for developing robust, maintainable, and scalable applications. By adopting principles of functional programming, immutability, and careful state management, developers can significantly reduce the complexity and improve the quality of their codebases.
