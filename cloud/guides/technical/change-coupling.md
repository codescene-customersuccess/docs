# Change Coupling: Visualize Logical Dependencies

Change Coupling means that two (or more) modules change together over
time. Exploring the change coupling in our codebases often gives us deep and
unexpected insights into how well our designs stand the test of time.

Most users first discover change coupling dynamically when using CodeScene’s Hotspot map.
The specifics of that interface are documented here: [Hotspots](hotspots.md).

Change coupling is also used to evaluate how well a software architecture aligns with the
organizational structure of the teams that build the system.

Note that change coupling is an advanced analysis. As such, it’s usage frequency is lower than the
hotspots and technical debt analyses. We find that a change coupling analysis provides valuable feedback
in a team retrospective or as weekly architectural feedback.

## Understand Change Coupling

CodeScene provides several different metrics for change coupling.
The tool considers two modules coupled in time:

- if they are modified in the same commit, or
- if they are modified by the same programmer within a specific period of time, or
- if they refer to the same Ticket ID in their commit messages.

Change coupling in itself is neither good nor bad; it all depends on *what* modules are coupled and for what reason
they co-evolve. Hence, we recommend using change coupling to visualize the actual, logical dependencies in your codebase and
compare this information to your architectural principles. Any deviations might indicate real problems.

## Visualize System Aspects using Change Coupling

By default, CodeScene shows a hierarchical view of your change coupling. Hover over a label in the graph to
highlight its dependants as illustrated in
[Fig. 46](#change-coupling-hierarchical-view).

![The Change Coupling hierarchical view](../shared/guides/technical/change-coupling-hover.png)

The different colors of the connecting lines illustrates the temporal dimension of the dependency: does it grow stronger (red),
decreases (blue), or remains stable (yellow)? This trend information lets you follow-up on the effect of architectural changes.

CodeScene also lets you capture logical system dependencies that cross team-boundaries:

![Change coupling across components (React)](../shared/guides/technical/change-coupling-by-arch-component.png)

The preceding figure shows you how to uncover dependencies in a monolithic architecture. The cool thing with CodeScene’s
change coupling is that the same analysis works equally well visualize the **change impact** in a microservice or
other distributed architectures.

## Investigate Logical Dependencies across Architectural Boundaries

Now, let’s say that those components are potentially developed and owned by different development teams.
If that’s the case, the coordination costs in the organization might soar as new features and bug fixes require work
by multiple teams before they can be completed.

CodeScene provides a second overlay that lets you visualize the team aspect of change coupling:

![Logical dependencies across team boundaries](../shared/guides/technical/change-coupling-by-team.png)

This visualization presents the same codebase as above, only now it’s grouped based on the main contributing team in
each service.

## Advanced Analyses: X-Ray your Logical Dependencies

When you find an unexpected dependency, you often have to dig
into the code and understand *why*. This is where CodeScene’s X-Ray feature
proves invaluable as it lets you X-Ray a change coupling clusters.
Check out the guide in [X-Ray](xray.md) for more details and examples.

## Sum of Couplings

By summing how many times a module has been coupled to another one in a commit we get a measurement called
**sum of couplings**. This is a way to find modules that are architecturally significant. The higher the number, the
more central the module is in the codebase. The Sum of Couplings view gives you a table of files sorted by this metric.
