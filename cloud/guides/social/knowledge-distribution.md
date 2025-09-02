# Knowledge Distribution

CodeScene measures several aspects of knowledge distribution:
: * *Key personnel risks*: Are there any critical parts of the codebase that are in the head of just one developer?
  * *Low system mastery*: What’s the impact if a developer leaves or moves to a different product line? Can you continue
    to successfully maintain the codebase?
  * *Coordination bottlenecks*: Are there any parts of the code where multiple teams have to coordinate their work?
    Such modules frequently lead to waste via merge conflicts and tend to be defect dense.

This guide shows you how to measure these aspects of your software development.

## How Do We Measure Knowledge?

The knowledge metrics are based on the amount of code each developer has
contributed. CodeScene looks at the deep history of
each file to calculate contributions. This makes sense for two different
reasons:

1. The last snapshot of a source code file wouldn’t be good enough since
   such shallow ownership is sensible to superficial changes (e.g.
   re-formatting issues, automated renaming of variables, etc).
2. Even if one developer completely rewrites a piece of code, its
   original author will still retain some knowledge in that area since
   they’re familiar with the problem domain. The metrics in CodeScene acknowledge that and will retain some knowledge for the
   original developer as well.

CodeScene uses the name of each committer to calculate knowledge
metrics. So please *make sure* you understand the possible biases
discussed in the guide [Know the possible Biases in the Data](bias.md).

## Detect Knowledge Risks

CodeScene’s dashboard presents a high-level summary of the knowledge distribution over time:

![Dashboard summary of the knowledge distribution](../shared/guides/social/knowledge-kpi-trend.png)

This high-level summary consists of two sub-metrics, **Code familiarity** and **Knowledge islands**.
Code familiarity describes how much of the codebase is known by the current team:

![image](../shared/guides/social/knowledge-kpi-code-familiarity.png)

*Knowledge islands* describes how much of the codebase is known only by a single developer:

![Knowledge islands](../shared/guides/social/knowledge-kpi-islands.png)

Using the Knowledge Risk view, you can further drill down and identify the areas where your system is vulnerable:

![Identify risks in the knowledge distribution](../shared/guides/social/key-personnel-knowledge-risks.png)

The Knowledge Risks analysis identifies and highlights the following patterns:

* **Knowledge Island in Complex Hotspot**: A module that’s written mostly by one developer, and that module is a hotspot
  with code health issues. Consider to on-board at least one more person in these areas as these hotspots present a
  significant key personnel risk.
* **Knowledge Island**: A knowledge island is code written mostly by one developer, but the code is of acceptable
  code health. You might still face a key personnel risk, but on-boarding new personnel in this area should be
  lower risk than in complex hotspots. Make sure that *knowledge islands* are supervised using CodeScene’s
  goals (see [Manage Hotspots and Technical Debt with Goals](../technical/augmented-analysis.md)).
* **Complex Code by Former Contributors**: This type represents code with low code health, where the majority of that
  code is written by former contributors. It’s code with low system mastery. Modifying such code is always an
  increased risk, so make sure to schedule additional time for learning.
* **Multiple Active Developers**: This type indicates that the code is actively worked on and that the detailed knowledge
  is shared by at least two developers.

Finally, note that CodeScene also presents warnings for knowledge risks as part of the virtual code review.

## Explore the Individual Knowledge Map

In the interactive knowledge mpas, each color is used to represent the primary author behind a module.

CodeScene allows you to dynamically filter by authors and/or teams:

![Filter the knowledge map visualizations by authors and/or teams.](../shared/guides/social/interactive-social-map-author-filtering.gif)

*Tip*: The knowledge maps are an excellent on-boarding support that helps new team members identify the colleagues that
know that most about a particular piece of code. CodeScene’s knowledge maps go way deeper than a plain git blame and
will present a more accurate picture of the primary authors.

In case of multiple authors, you click on a file – represented as a circle in the visualizations – and explore who the other authors are:

![The details of a file](../shared/guides/social/individual-details.png)

The “Authors” button shows a treemap representation of the proportional contribution of each author, in terms of commits.

### Make sure Pair Programming is configured if needed

CodeScene also supports knowledge maps for pair- and mob programming, where the credits are split between the contributors in
the pair. However, you need to configure your pair programming patterns in CodeScene to activate this feature. Refer to in [Configure Developers and Teams](../../configuration/developers-and-teams.md)
for the configuration options.

## Explore your Team Knowledge Maps

CodeScene also measures knowledge distribution on a team level and this information is usually
even more valuable than the individual metrics.

As soon as you’ve assigned developers to a team, as described in [Configure Developers and Teams](../../configuration/developers-and-teams.md), CodeScene will
accumulate their individual knowledge into their teams. The analysis
results are presented using the same principles as for the Individual
Knowledge Map. Only now, each color represents a team as shown in [Fig. 101](#team-knowledge-map).

![The knowledge distribution on team level](../shared/guides/social/team-knowledge-map.png)

The Team Knowledge Map lets you reason about both the responsibilities
of the different teams. In general, you want to ensure that your team
organization is reflected in the software architecture of your system. For example, the analysis in
[Fig. 101](#team-knowledge-map) has a configuration for three devlopment teams: Net, Unix, and Unicode. The analysis shows
that each time has a clear area of responsibility. However, you get more details by clicking on the *Coordination Needs*
aspect as shown in [Fig. 102](#team-coordination-map).

![The coordination needs on team level](../shared/guides/social/team-coordination-map.png)

The coordination analysis shows you the parts of the code where multiple teams have to coordinate their work. From here
you can explore which teams that are involved. The coordination analysis is also described in more detail in [Parallel Development and Code Fragmentation](fragmentation.md).

Finally, make sure to read the discussions in the guide [Social Networks](social-networks.md) for more information on the organizational
theories and how they correlate to the quality and efficiency of your
organization.

### Measure from the date of the last organizational change

Development organizations aren’t static. People rotate teams, new teams are formed, and old ones abandoned. Each change
introduces a possible bias into the team-level metrics.

The best way to avoid those biases is to select an analysis start date that represents the date of your last organizational
change. For example, let’s say you changed the team structure back in January 2017. In that case you want to start your team
analysis from that date, as illustrated in [Fig. 103](#select-start-date).

![Select a start date from the last organizational change](../shared/guides/social/select-start-date.png)

Note that you typically want to use *a longer* analysis time span for technical analyses. CodeScene resolves this by
letting you configure two separate time spans, as illustrated in [Fig. 103](#select-start-date).

## Visualize Code Ownership Patterns

Many Git hosting platforms (e.g. GitHub, GitLab, BitBucket) support the concept of CODEOWNERS. CODEOWNERS is a file
where your organization can specify code owners for different parts of your codebase. The ownership is specified by
using a set of glob patterns that match different modules, file types, or specific content. Here’s an example:

```shell
# Specify the default owners in case the specific patterns
# given later won't match:
*       @TheArchitect @TheMicroManager

# The last matching pattern gets precedence, so here
# we specify the owners for invidual sub-systems:
/src/frontend    @js-owner
src/backend      @go-owner
docs/*           @TechWriter
```

In this examples, the hypothetical user names @TheArchitect, @js-owner, etc. would match real people in your
organization. You can of course also specify e-mail addresses instead of user handles.

If you have a CODEOWNERS file, CodeScene will include it in the analysis. You just need to specify that path to the
file since it might vary.

![Specify the relative path to the CODEOWNERS file.](../shared/guides/social/code-owners-config.png)

In a multi-repository analysis project you might of course have multiple CODEOWNERS files. That’s OK. Should they be in
different relative locations, then you just specify all options using a semicolon separated list.

CodeScene will now mine and aggregate the code ownership as shown in [Fig. 105](#code-owners-analysis).

![CodeScene visualizes the code owners.](../shared/guides/social/code-owners-analysis.png)

The main use case for this information is to:

1. Ensure that no critical parts of your code lacks ownership.
2. Ensure that your hotspots have a clear and strong ownership. In particular, you want to ensure that there’s a single owner for any hotspots in order to avoid diffusion of responsibility.

### Notify Code Owners on Failed Quality Gates

CodeScene will also include the ownership information in case a CI/CD quality gate fails. You see an example in [Fig. 106](#code-owners-jenkins).

![CodeScene notifies code owners when a quality gate fails.](../shared/guides/social/code-owners-jenkins.png)

## Uncover the Knowledge Loss in your Codebase

Knowledge loss represents code that is written by a developer who is no
longer part of your organization or project. You use this information to
reason about the knowledge distribution in your codebase and as part of
your risk management since it is an increased risk to modify code we no
longer understand. In addition, you can also use the analysis
pro-actively to simulate the consequences, in terms of knowledge loss,
of planned organizational changes.

The *Knowledge Loss* analysis will accumulate the contributions of all
developers that you have marked as Ex-Developers in your configuration (see [Configure Developers and Teams](../../configuration/developers-and-teams.md)).
Those parts of the codebase that are dominated by Ex-Developers are marked as red in the knowledge loss
visualization. [Fig. 107](#knowledge-loss) shows an example from an organization where some core
developers have left.

![An example on a knowledge loss analysis](../shared/guides/social/KnowledgeLossSample.png)

To inspect the knowledge loss you just click on a file, as shown in [Fig. 108](#knowledge-loss-details).

![Inspect detailed knowledge loss](../shared/guides/social/knowledge-loss-details.png)

Note that there’s a special label in the knowledge visualization: *Inconclusive*. Inconclusive means that CodeScene
cannot determine the original author of a piece of code. This is something that happens if you run a knowledge analysis
on a shorter time span than the total lifetime of a codebase. CodeScene tracks moved and renamed content,
but in doing so it depends on the underlaying object model of Git. So in the rare cases where copied content doesn’t
get detected as such, the code may show up as inconclusive.

## Use knowledge loss as a simulation

There are several uses for the knowledge loss information. In retrospect, you use it as part of your planning and
risk management since it is an increased risk to modify code we no longer understand.

However, the knowledge loss analysis is much more powerful when used as a simulation. In this case you use CodeScene to
simulate different scenarios and how they would affect your organization. Used this way, the knowledge loss analysis
becomes a pro-active tool that helps you avoid unpleasant surprises in case a contractor leaves or a developer gets
moved to a different project.

The guide in [Mitigate the Bus Factor via the Off-Boarding Simulation](../simulations/offboarding-simulator.md) describes how to simulate upcoming knowledge loss so
that you can act on time.

## How is the social side of code relevant?

Software development at scale is a social activity. We work in
teams, sometimes distributed, and need to communicate and
coordinate to solve our tasks. Building an organization
responsible for creating and evolving a system is a necessity as soon as
your codebase has grown beyond a certain size.

Moving from individual developers to teams does not come free; No
matter how efficient we, as an organization, are, we’ll always pay a
price. The cost of team work is known as *process loss*. Process loss is
the theory that a team, just like a mechanical machine, cannot operate
at 100 percent efficiency. In the mechanical world we have
inefficiencies like friction and heat loss. Our software equivalents are
coordination and communication. The main challenge in most software
projects is to minimize the process loss. Failures to do so often come
off as technical issues, when in reality those issues have social roots.

The software industry has been aware of these issues. But until now,
we’ve never had a way to measure them. This is one of the key reasons
we developed CodeScene; with these analyses you’re now able to make
organizational decisions based on data from how the teams actually work
with the code.
