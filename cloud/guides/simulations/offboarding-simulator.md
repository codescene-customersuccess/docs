# Mitigate the Bus Factor via the Off-Boarding Simulation

Every developer which leaves an organization takes a piece of the collective knowledge with them. Such off-boardings can
become an existential risk for many codebases: with enough knowledge loss, a development project grinds to a halt since the
remaining developers don’t know how the code works. This phenomenon is known as the Bus Factor.

The Bus Factor refers to how many developers that can leave before the code becomes unmaintainable. Often, the bus factor is
as low as a couple of long-term contributors; few organizations have resilience to the sudden loss of key personnel.

To shine a light on this critical factor, CodeScene comes with a simulation module that lets you explore the effects of a potential off-boarding.
The simulation lets you identify off-boarding risks as pro-actively discover unhealthy areas of the code with a low Bus Factor. These are
likely to be the highest key-person risks.

## Access the Off-Boarding Simulation

The off-boarding simulation is accessible from each analysis view in a separate module, as shown in [Fig. 109](#simulation-module-view).

![Access the off-boarding simulator in the SIMULATIONS module](guides/simulations/simulation-module-view.png)

The former contributors in your codebase, the ones configured as ex-developers in your project, are visualized using the black color.
The simulation also lists all known developers. To simulate the impact of an off-boarding, select one or more developers from that list as
shown in [Fig. 110](#simulation-select-developers). The areas of the code affected by the off-boarding are then highlighted in red. Note that you can search and filter in the developer list, a
feature that’s useful in projects with many contributors.

![Simulate off-boarding effects](guides/simulations/simulation-select-developers.png)

### Detect Off-Boarding risks

CodeScene auto-detects high risk areas in the off-boarding simulation. That is, if a major hotspot is in the head of a developer who might leave,
we consider that an increased off-boarding risk. The off-boarding risks are highlighted as illustrated in [Fig. 111](#off-boarding-risks).

![Detect off-boarding risks](guides/simulations/off-boarding-risks.png)

## Act on the Off-Boarding Information

The off-boarding simulation lets you identify the areas of the system where most code has been written by
developers who might become former contributors in the future. This might happen for several reasons: a developer or contractor could
leave the organization, or maybe a team of developers are re-assigned to a different project.

In both situations you typically have a period of time when the soon to be former contributors are still around to
support the on-boarding of new people. Using the simulation, you can:

* *Guide on-boarding*: If you identify a high-risk area where you will lose system mastery, then use this information to on-board a new developer in that part of the code.
* *Mitigate risks by refactoring unhealthy code with a low Bus Factor*: Organizational risks like key-person dependencies and knowledge silos can be mitigated
  by improving the Code Health. That way, the code becomes easier for new developers to understand. Also, do the refactoring by pairing up the key-person with
  another member of the team so that you distribute the knowledge in the process.
* *Support planning and priorities*: If the simulation shows that the organization will lose active knowledge of entire components or
  sub-systems, then you might have to re-prioritize or re-plan features that require extensions of those components.
  Typically, this means scheduling additional time for learning.
* *Look for upcoming technical gaps*: Some codebases have a high degree of technical sprawl. This means that an off-boarding could
  lead to a situation where you have code implemented in a programming language that none of the teams master.
  As such, you want to compare the off-boarding data with CodeScene’s analysis of Technical Sprawl.
  The outcome of this analysis should influence training, hiring, and rewrite decisions.

In particular, look for components that are entirely in the heads of former contributors. That’s where the largest risk is.
