# Architectural Analyses

CodeScene’s architectural analyses let you run Hotspots, Change Coupling
and more at the *architectural level* of your project. The
results give you the power to evaluate how well your architecture
supports the evolution of your system.

With CodeScene, you get the same information on an architectural level as the file level analyses, as
illustrated in [Fig. 116](#conway). Note that this is information that isn’t available in your code.

![High level architectural analyses](guides/architectural/conway.png)

This section of the guide walks you through the necessary configuration and gives you some ideas
on how to interpret and act upon the architectural analysis results.

## What is an Architectural Component?

An *Architectural Component* is a logical building block in your system.
For example, if you build a Microservices architecture, each
microservice could be considered a logical block. Similarly, if you
organize your code in layers (MVC-, MVP-, MVVM-patterns, etc), each
layer would be a logical block.

![An example of architectural components](guides/architectural/ArchitecturalComponentsExample.png)

An Architectural Component could also be much more coarse. For
example, let’s say that you’re interested in the co-evolution of your
application code versus the test code. Perhaps you suspect that you
spend way too much effort on keeping your automated tests up to
date. In that case, you could define two Architectural Components:
*Application Code* and *Automated Tests*.

You’ll learn to define your components in the next section. Before we go there, let’s have a look at the end result.

As you see in  [Fig. 118](#hotspots-architecture), CodeScene presents a hotspot analysis on the architectural level. This
gives you a high-level view of how your development activity is focused.  You also have access to social knowledge
metrics on an architectural level. Later in this guide we will go into more detail about using
them to analyse complex architectures like Microservices.

![High level architectural hotspot analysis](guides/architectural/hotspots-architecture.png)

## Defining architectural components

To enable these analyses, first you need to configure your
Architectural Components. The Architectural Components you specify
should take into account your project’s architectural style and on the
type of questions you have about your codebase. For example, do the
change patterns in the code match the intent of the architecture?
Often, the potential for large maintenance savings are found in these
architectural analyses once you spot patterns that violate your
architectural principles.

To get started, first go to the “Architectural Components” tab of your
project’s configuration. This tab displays any existing Architectural
Components:

![A project's default Architectural Components](guides/architectural/ArchitecturalTabDefault.png)

By default, when a new project is created, CodeScene automatically
creates a new component for each Github repository included in the
project. This way, in a multi-repository project, there are already
meaningful architectural components, though of course you are free to
redefine them afterwards. In this example, the project only has one
repository, so the default component includes the entire project,
which of course is not particularly interesting.

To define your own components, click on the link to the “Architectural
Component Editor”.

![The Architectural Component Editor](guides/architectural/ArchitecturalComponentEditorBaseview.png)

To define a new component, use the System Map on the left to zoom in on a folder:

![Zooming in on a directory in the architectural component editor.](guides/architectural/ArchitecturalComponentRailsTest.png)

When a folder is selected, the corresponding path appears in the
sidebar on the left. As you can see in the image above, it actually
appears twice, once with a predefined glob pattern and once as an
editable field.

If we want our architectural component to include the complete
contents of this subfolder, we can select the predefined pattern. When
we click on “Select a component”, a menu appears:

![The "Select a component" menu](guides/architectural/ArchitecturalComponentCreatePatternSelectMenu.png)

In this case we will need to create a new component. (We plan on
deleting the “Rails” component so we won’t use that one.) If you
choose “Create a new component”, the editor will prompt for a
component name:

![The "Create component" popup](guides/architectural/ArchitecturalComponentNewComponentModal.png)

The name can be anything you want. Spaces are allowed. Once validated,
if there are other test-related folders we want to add to the
component, we can repeat the process by simply selecting “Test” in the
“Select component” dropdown menu.

Components that are created in the editor are not permanently saved
until you scroll down and click on the “Update” button at the bottom
of the page. Before we do that, though, we will delete the
automatically generated “Rails” component by clicking on “Delete
pattern” here:

![Delete a component by deleting its pattern](guides/architectural/ArchitecturalComponentDeleteComponent.png)

To delete a component, simply delete all the patterns it contains. A
component with no patterns is automatically deleted.

Click on “Update” to save your changes. The changes should now appear
in the “Architectural Components” tab:

![The architectural components tab reflects the changes made](guides/architectural/ArchitecturalComponentConfirmChanges.png)

On the next analysis run, the new component will be used.

Let’s consider the example above to learn more about how CodeScene’s
glob patterns work. The configuration in
[Fig. 122](#architectural-editor-select-component) specifies the pattern
rails/activerecord/test/\*\*. That means that all content under the
folder rails/activerecord/test will be considered as the
architectural/logical component *Test*.

In many cases, your architectural components can correspond to the
primary sub-folders of your codebase. However, the pattern
definitions, with the power of glob patterns, can be as granular as
you like and even match individual files.  If you need finer
granularity, the “Edit a custom pattern” field allows you to type your
own glob pattern based on the currently selected folder.

Multiple folders can be mapped to the same architectural component. In
the Rails project in this example, the high-level folders generally
contain test subfolders. Our *Test* component could include a
pattern for each subfolder.

When patterns are nested, it’s important to remember that only the
higher-level component will be used in the analysis results. For
example, if we also defined an *ActiveRecord* component with this
pattern rails/activerecord/\*\*, the rails/activerecord/test/\*\*
pattern would no longer match any files. To avoid this, define
components with a finer granularity. In this example, using
rails/activerecord/lib/\*\* for the *ActiveRecord* component and
rails/activerecord/test/\*\* for *Tests* would provide the desired
behavior.

## System Complexity Trend

CodeScene calculates a trend of how your system, as a whole, has evolved over time.

Note that you need to enable this analysis yourself as it’s expensive in terms of analysis time. [Fig. 126](#architectural-trends-config) shows how to enable the trends.

![Enable Architectural Trends](guides/architectural/EnableArchTrends.png)

Once you’ve enabled the architectural trends, CodeScene calculates an overall view of the evolution of your system as
illustrated in [Fig. 127](#id1).

![The system complexity trend](guides/architectural/SystemComplexityTrend.png)

You use this information to see if the system has stabilized and entered a maintenance phase or if it still evolves rapidly. You can
also correlate the growth patterns to how the staffing has looked over time - did more people really resulted in a faster growth?

CodeScene also presents a breakdown of the system complexity per architectural component as illustrated in [Fig. 128](#architectural-stacked-trends).

![The architectural trends](guides/architectural/ArchitecturalStackedTrends.png)

## Know the Biases in System Complexity Trends

The system/architectural complexity trends don’t take all your historic development into consideration. The trends are
based upon the active amount of code. That is, only the code that’s included in your repositories today will be considered.
More specific, this means that:

* If you have deleted whole files and folders in your codebase it won’t reflect in the trends.

We also want you to be careful when interpreting the results of an analysis that use a shorter time span than that of the whole repository lifetime.
In such a shorter analysis period, only the files with active development activity are included in the codebase. You’ll still
be able to see a trend and reason about possible complexity growth in your code. However, the absolute numbers are likely to
be lower than the total amount of code; Only files that you have modified are included in the trends.

## Interpret the Architectural Analysis Results

The Architectural Analyses lets you focus on logical building blocks
rather than individual files. This allows you to identify architectural
Hotspots, as shown in [Fig. 129](#architectural-hotspots).

![Architectural hotspots](guides/architectural/ArchitecturalHotspots.png)

The architectural analyses also lets you inspect the complexity trends of architectural hotspots. Note that
you need to enable the architectural trends in your project configuration as noted above.

Finally, the architectural analyses also let you identify expensive modification
patterns where code changes ripple through multiple logical components,
as seen in in [Fig. 130](#architectural-change-coupling).

![Architectural change coupling](guides/architectural/ArchitecturalTemporalCoupling.png)

## Evaluate Conway’s Law

CodeScene measures the knowledge distribution on an architectural level too. This gives you a powerful tool to
evaluate how well your architecture aligns with your organization, aka *Conway’s Law* as illustrated in [Fig. 131](#conway-law).

![High level architectural analyses](guides/architectural/conway.png)

The same analysis also lets you measure the coordination needs on an architectural level. This is useful to detect
sub-systems that become coordination bottlenecks or lack a clear ownership, as illustrated in [Fig. 132](#architectural-coordination).

![High level architectural analyses](guides/architectural/architectural-coordination.png)

You use this information to find parts of the code that may have to be split into smaller parts to facilitate parallel development, or,
to introduce a new team into your organization that takes on a shared responsibility.

The high-level analyses are particularly useful if you work on a (micro) service oriented architecture. In that case you
also want to investigate *Technical Sprawl*, which we discuss next.

## Measure Technical Sprawl

One of the big selling points behind Microservice architectures is the freedom of choice when it comes to implementation technologies. Using a
Microservice architecture, each team is free to chose the programming language they think makes the best fit for the problem at hand.

In practice, however, this freedom may lead to a sprawl in programming languages that makes it hard to rotate teams. It also puts you – as
an organization – at risk when the only people who master a particular technology leaves. Thus, CodeScene provides analyses to measure
your technical sprawl, as illustrated in [Fig. 133](#technical-sprawl).

![The technical sprawl architectural analyses](guides/architectural/technical-sprawl.png)

The technical sprawl analysis is particularly useful for off-boarding. Let’s say that we want to move a developer to another project or, worse,
someone decides to leave the organization. In that case we run a pro-active simulation of knowledge loss (see [Knowledge Distribution](../social/knowledge-distribution.md))
and ensure that we still have the technical competencies we need within the organization, as illustrated in [Fig. 134](#knowledge-gap).

![The technical sprawl with knowledge loss architectural analyses](guides/architectural/knowledge-gap.png)
