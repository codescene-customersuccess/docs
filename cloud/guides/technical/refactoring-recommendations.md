# Refactoring Recommendations

### How do we actually solve code health issues?

## What are refactoring recommendations?

There’s no shortage of books or websites with compilations of refactoring examples.
They are typically short and concise, but at the same time they don’t have a strong
relationship to your own code. What if they instead could point to patterns and abstractions
introduced into your project by your own colleagues?

Just as CodeScene monitors your codebase for code health degradations, it can also detect
changes in the opposite direction. How did your colleagues tackle issues like
*Deep Nested Complexity*, *Bumpy Road* or *Complex Method* in the past? CodeScene tries to find
the best solutions, and compiles them into your project’s own collection of recipes for refactoring.

![A simple example found by CodeScene that improves code health.](guides/technical/refactoring-recommendations-example2.png)

## Virtual Code Review

When performing a virtual code review on a file, CodeScene lists all the code issues found.
If CodeScene has found any solutions to a code issue in the past, it lists
them alongside the description of the issue.

CodeScene ranks the examples by general readability and how much they improve code health.
Further, to make the examples as relevant as possible, CodeScene prefers
examples from related files (based on e.g. team composition). That way, the recommended
refactorings reflect your team’s domain and preferred style.

## Past refactorings

It’s also possible to view all past refactorings CodeScene has found, for each issue category.
In the project sidebar, under the “Code” header, you will find a link to “Past Refactorings”. CodeScene looks for
solutions to issues each time it analyzes your code and, as it finds them, adds them to this page.

![A complete listing of the refactorings found within a project.](guides/technical/refactoring-recommendations-performed-refactorings.png)
