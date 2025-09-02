# Build efficient teams via strong Team/Code alignment

Getting the organizational side of software right is just as important as any properties of the code. In general,
the modularity of a software design needs to align with the responsibilities of the development teams.
That principle is the core of Conway’s law. The team-code alignment explorer visualizes these properties by
combining measures of Team Coupling and Team Cohesion. The better the team coupling and the more loosely coupled
teams, the less coordination overhead and the fewer merge conflicts.

![The interactive explorer visualizes dependencies between teams and developers in a codebase.](guides/team-code-alignment/team-code-alignment-explorer.png)

## Reverse engineer team dynamics from code

Strong team cohesion means that the team carries a meaning from an architectural perspective; members of a team work in
the same parts of the code. CodeScene reverse engineers this property of team work from the evolution of your code.
We do this by analysing the overlap between the team member’s commits and the files in the codebase.

Following the same principle, we can also discover overlaps in commits to the same parts of the code by members of
different teams. That way, we can detect team coupling – loose or tight.  Loosely coupled teams minimizes coordination
and the risk of conflicting changes to the code, whereas tightly coupled teams become coordination bottlenecks.

## Strive for strong cohesion and loose coupling

Cohesion and coupling are the corner stones of software design. Coincidentally, the same properties are vital to
building efficient teams. The team-code alignment explorer lets you inspect these properties.

There are multiple root causes and remedies for tightly coupled teams:

* **Unclear ownership**: Parts of your architecture might lack team ownership. Frequently, you recognize these packages
  via their names; common, misc, and util are the usual suspects.
* **Lack of team focus**: This happens when members of a team work in parallel on disparate domains or aspects of
  the system. Coordination and communication works best when there’s a shared purpose and clear goals. Streamlining
  the tasks for a team helps.
* **Architectural decay**: Finally, there will never be a fit between the teams and the code if the architecture itself
  suffers strong dependencies or lack of cohesion. Interestingly enough, many team coordination issues can be resolved
  by architectural improvements and code refactoring.

While you cannot deduce the root cause from the team-code alignment explorer itself, other CodeScene analyses let
you drill down and identify areas of improvements:

* **Hotspots and Change Coupling** let you discover complex dependencies and code quality issues in the system
  (see [Hotspots](../technical/hotspots.md)).
* **Coordination and parallel development** analyses highlight \_where_ in the code authors from multiple teams
  need to coordinate their code changes (see [Parallel Development and Code Fragmentation](../social/fragmentation.md)).

## Limitting false positives

CodeScene includes all developers in the analysis. However, to avoid cluttering the overall picture we make sure
to filter out insignificant developer dependencies. These are dependencies weaker than 5%. In other words, if two
developers have committed to the same parts of the code, but those shared commits make up less than 5% of their total
commits, then we will filter out those dependencies from the visualization.
