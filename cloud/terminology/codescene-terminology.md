# CodeScene Terminology

CodeScene is the world’s first behavioral code analysis platform. As such, there are some new concepts that you
might not be familiar with from other tools. The purpose of this document is to explain the terminology.

## Domain: Building maintainable Software Systems and efficient Teams

CodeScene’s mission is to turn code analysis data into actionable information for the whole organization. We see the
largest value add in working as a communication bridge between the engineering organization and management. As such,
there are some general terms that we want to cover in the context of the CodeScene platform.

### Behavioral Code Analysis

The main difference between CodeScene’s behavioral code analysis and traditional code scanning techniques is that
static analysis works on a snapshot of the codebase while CodeScene considers the temporal dimension and evolution of
the whole system in the context of the development work. That is, while the code is important, it’s even more important
to uncover how it evolves and where it’s heading.

Another key distinction between behavioral code analysis and traditional techniques, is that a behavioral code analysis
focuses on the development organization. This enables powerful organizational and social analyses.

*Read More*: [How it works](https://codescene.com/how-it-works/).

### Technical Debt

Technical debt is a metaphor where – just like in finance– debt incurs interest payments. This means
that technical debt makes code more expensive to maintain than it has to be. This has a direct impact on business.
The typical development organization can increase their feature delivery efficiency by at least 25% by managing
technical debt.

*Read More*: Technical debt knowledge bank [at codescene.com](https://codescene.com/technical-debt/).

### System Mastery

While the technical solution is important, managing the people side of software is vital too.
System Mastery means that everyone involved with the system maintains knowledge of how the system works. An organization
loses System Mastery when there’s a high turn around on staff or due to increasing complexity of the system.

### Code Complexity

Code complexity refers to how challenging the code is for a human to understand. As humans, we
can only keep a finite amount of information in our head and reason effectively about it. Once a piece of code grows in
size (many lines of code) or conditions (logic like if-else chains), our working memory can no longer keep up and
we start to make mistakes. Code Complexity is addressed via refactoring.

*Read More*: [Code complexity patterns](https://codescene.com/blog/bumpy-road-code-complexity-in-context/).

### Refactoring

Refactoring is the process of improving existing code without changing its behavior. Refactorings are
typically small and done in increments; we start with some overly complex code and simplify it.

The most common refactorings are to extract a method, encapsulate a complex conditional, or renaming a variable.
Many refactorings are automated via IDEs. An effective refactoring process requires good test automation as a
safety-net to ensure we’re not changing the external behavior of the code.

## General: Projects and Analyses

### Project

A CodeScene project refers to one or more Git repositories together with their analysis configuration.
The project is an organizatory construct used to trigger analyses. We recommend to define one CodeScene project per
product line, no matter how many Git repositories you use to represent the codebase.

### Analysis

A CodeScene analysis of a specific project at a point in time. We recommend to schedule a daily CodeScene
analysis so that your dashboards are always up to date.

### Delta Analysis

A quick analysis of work in progress.
A Delta Analysis analyses the changed code with reference to the target branch (e.g. develop, main).

CodeScene supports out-of-the-box integrations with
GitHub, BitBucket, Azure DevOps or GitLab via our PR Integration.

*Read More*: [PR Integration with CodeScene’s Delta Analysis](../guides/pr-integration/integrate-codescene-with-pull-requests.md).

### PR Integration

CodeScene automates a Delta Analysis via webhooks to Pull Requests. This integration is used as
input to code reviews and/or as a quality gate (e.g. fix the code health degradations before merge).

*Read More*: [Integrate CodeScene with Pull Requests](../guides/pr-integration/integrate-into-ci-cd.md).

### Recommended Review Level

As part of a Delta Analysis, CodeScene recommends a review level.
The recommended review level is relative to the risk profile for your codebase. The review level is intended to
let your team prioritize code reviews that have an increased delivery risks.

Under the hood, CodeScene calculates a unique risk profile for your codebase based on how the system has evolved and
what a typical change set looks like. This risk profile is a combination of technical and social metrics.
The technical metrics relate to the depth and diffusion of the change – the more changes and the more widespread, the higher the risk.

*Read More*: [PR Integration with CodeScene’s Delta Analysis](../guides/pr-integration/integrate-codescene-with-pull-requests.md).

## Technical Analyses: Hotspots, Code Health, and Change Coupling

### Hotspots

Hotspots identify the code with the highest development activity. As such, hotspots point to modules that
are likely to have a high business impact and affect maintenance costs and the effort to implement new features.
Hotspots are calculated on three levels:

1. file level hotspots,
2. architectural hotspots as defined by the configured architectual components, and
3. function/method level hotspots via CodeScene’s X-Ray analysis.

Note that hotspots don’t imply a quality problem on their own; hotspots are about \_relevance_ to be able to reason
about code quality and impact within a context. This means that hotspots need to be combined with the code health
measure.

Read more: [Hotspots](../guides/technical/hotspots.md).

### Code Health

The Code Health metrics is based on patterns known to correlate with increased maintenance costs.
Patterns that make the code harder to understand and, hence, increase the risk of change and make the module more
expensive to evolve.

The Code Health score goes from 10 (healthy code that relatively easy to understand and evolve) down to 1, which
indicates code with severe quality issues. The score is calculated from a combination of both properties of the code
as well as organizational factors. In total, CodeScene calculates 25-30 factors depending on programming language.

Read more: [Code Health – How easy is your code to maintain and evolve?](../guides/technical/code-health.md).

### X-Ray

X-Ray is an analysis that calculates *Hotstpots* on the function/method level. The resulting function-level
hotspots serve as a prioritized list on where to pay down any identified technical debt.

Read more: [X-Ray](../guides/technical/xray.md).

### Change Coupling

Change Coupling means that two (or more) modules change together over time. CodeScene provides
several different metrics for change coupling. The tool considers two modules coupled in time:

* if they are modified in the same commit, or
* if they are modified by the same programmer within a specific period of time, or
* if they refer to the same Ticket ID in their commit messages.

Change Coupling is calculated at three levels: architectural, file, and function level.

Read more: [Change Coupling: Visualize Logical Dependencies](../guides/technical/change-coupling.md).

## Organizational and Social Analyses: Teams, Knowledge Distribution, and the Bus Factor

### Teams

All organizational and social metrics can be aggregated at the level of development teams. This requires that
you configure your development teams inside CodeScene by assigning each developer to an organizational unit.
CodeScene is flexible, and a team can be anything that makes sense for your organization: Scrum team, feature team,
component team, departments, external vs internal staff, etc.

*Read More*: [Configure Developers and Teams](../configuration/developers-and-teams.md).

### Bus Factor

The Bus Factor tells how many developers that can leave before the code becomes unmaintainable. The lower the
Bus Factor, the higher the key person risk. In many codebases, the Bus Factor is as low as just 2-3 developers.

The metric is calculated from the amount of code each developer has contributed. CodeScene looks at the deep history of
each file to calculate contributions. The main purpose is to identify risks: when a core developer leaves, the system
mastery decreases which makes it more challenging to maintain the system.

*Read More*: [Knowledge Distribution](../guides/social/knowledge-distribution.md).

### Former Contributors

These are people who are no longer part of the current development team. Could be due to
off-boarding or because the person moved to a different team or role. Former Contributors is configurable and used
to calculate Knowledge Loss.

Note that there’s a special case: “Inconclusive”. This simply means that CodeScene cannot determine the original
author of a piece of code. The most common reasons are:

1. the complete history isn’t included in the analysis,
2. an author has been excluded from the analysis, or
3. one or more commits have been excluded from the analysis.

### Knowledge Loss

Knowledge Loss indicates a lack of system mastery due to off-boardings.
The metric is calculated from the amount of code written by former contributors. The metrics is calculated from the
historic lines of code contributed by each person. Any module that has at least 50% of its code written by former
contributors is indicated as having Knowledge Loss.

### Main Author

Presents the contributor who has written most lines of code in the specific file/component historically.
The metric is calculated for both individual contributors as well as aggregated per development team.

### Knowledge Risks

Presents the knowledge distribution in terms of author contributions. Modules where 95% or more of the
code is written by an individual contributor are considered *Knowledge* *Islands*. If that module is also a development
hotspot (relevance) and has low code health (expensive hand-over), then the module is indicated as a
*Knowledge* *Island* *in* *Complex* *Hotspot*.

### Coordination Needs

Calculates the overlap in code changes to the same file/component from different contributors.
The Coordination Needs are calculated using a fragmentation value. A high fragmentation value means that the development
effort is shared between multiple programmers. This is a risk factor for both defects as well as lower system mastery.
The metric is calculated for both individual contributors as well as aggregated per development team.

*Read More*: [Parallel Development and Code Fragmentation](../guides/social/fragmentation.md).
