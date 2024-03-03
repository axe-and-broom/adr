# 0001 - Scout's Honor

Leave the code in a better shape than when you first arrived.

## Context and Problem Statement

In order to keep the code from rotting, we continuously need to maintain it no matter if it's actively developed or considered legacy. This is a general rule that should be followed by all developers. When moving throughout the codebase, we sometimes find old code that doesn't follow the current standards and best practices, it might even have warnings in it. We need to decide if we should update it or leave it as it is.

## Considered Options

* Updating old code to new standards and best practices
* Always rewriting code
* Never touching legacy code

## Decision Outcome

Chosen option: "Updating old code", it's the best way to keep the code in a good shape and to avoid it from rotting. Seeing a problem and leaving it as it is, is not a good practice. If we see something that can be improved, we should do it. This is the only way to keep the code in a good shape. When adding functionality don't just shoehorn it in, but also refactor the existing code to make it better. This is the only way to keep the code from rotting.