# Configure Developers and Teams

Your knowledge maps are based on colors to give you an accessible high-level
overview. The system will automatically assign a distinct color to each top
contributor in your codebase on the first analysis. Similarly, you can define
teams of developers and the system will assign a distinct color to each.

![Sample on colored knowledge maps](configuration/TeamGuideKnowledgeSample.png)

The rest of this guide will walk you through the configuration.

## Important: Run an Initial Analysis Before You Configure Authors

CodeScene mines a list of all contributing developers. Note
that this list is mined and updated during each analysis. That means you
need to run one initial analysis *before* the tool gives you the option
to configure developer properties!

## Define Your Development Teams

Click the *Teams* tab in your project configuration to proceed to the
teams configuration, as shown in [Fig. 191](#teams-configuration).

![Configure teams for a project in the Teams tab.](configuration/teams-configuration.png)

For each team in your organization, specify the following properties:

- *Team name:* This will be used to identify the team. Later, when you
  configure developers, you’ll assign them to the team names you chose
  here.

Add a team for each team in the organization that works on your codebase.

![Configure the teams that reflect your organization.](configuration/configure-team-properties.png)

*Tip:* Some organizations just use one development team. In that case,
introduce virtual teams that depend upon the responsibilities of the
different developers. For example, you might want to define a Feature
team, a Maintenance team and an Infrastructure team. Using this
strategy, you’d be able to identify code at risk for incompatible
parallel changes since different forces lead to the changes.

### Even Open-Source Software Has Teams

The team definition is straightforward if you analyze a codebase that’s
owned by a traditional organization; Just use the information from your
organizational chart. However, we find it interesting to apply teams to
open-source codebases as well.

So if you happen to analyze an open-source project, consider introducing
the following teams to get additional social information:

- Define a teams for the organization that owns the code. For example,
  if you analyze the Clojure codebase, you’d define *Cognitect* as one
  team. If you analyze one of Microsoft’s open-source codebases, you’d
  use *Microsoft* as one team.
- Define a team for third party developers that contribute to the
  codebase
- Consider defining a team of the core maintainers too.

## Configure Developer Properties

The developer properties are a bit more tricky than the team
configuration, so please let us walk you through them one by one as
illustrated in [Fig. 193](#assign-dev-properties).

![Clone developer information](configuration/GuideAssignDeveloperProperties.png)

CodeScene automatically updates the list of contributing
developers; If a new developer starts to contribute code, they’ll be
present in the list and the tool lets you configure their properties.

Here are the properties you need to specify:

1. *Active/Former Contributor:* By default, all developers are considered
   active. If some of them leaves your project, mark them as *Former
   Contributors* and CodeScene will include them in the *Knowledge Loss
   Analysis*.
2. *Team:* The third column lets you assign the developer to a team.
   That will include them in the *Team Knowledge Distribution Analysis*.
3. *Exclude author from analysis:* If you check this option, the author
   will be excluded from *all* social analyses (although their
   contributions will still be included in the technical analyses like
   Hotspots and Code Churn). This is an option you use in case you have
   roles like System Integrators that only merge code, but never
   actually make their own contributions.

Once you’ve defined all developer properties you just need to run a new
analysis and you’ll get a smorgasbord of interesting social analysis
results.

## Authors and their Aliases: Mapping Version-Control Names to People

Often, over the lifetime of a project, some developers will sign their
commits with different names. This can be a source of inaccuracies for
CodeScene’s social analysis tools.

To deal with this, CodeScene provides an interface that allows you to
specify the version-control names that correspond with real people. In
CodeScene, when we talk about an *Author*, we mean the real person.
Team membership, author exclusion and former contributor status belong to
the developer. Each developer has at least one *Alias*, which is how
they are identified in version control.

For example, an *author* named **Jane Doe** might have several
*aliases* in version control commits: **Doe, Jane**, **janedoe**,
**J. Doe**, etc. This interface allows theses aliases all to refer to
the same person, which provides more meaningful results in social
analyses and unifies the information we have about the author in
question.

### Workflow

To access the interface, click on the *Developer identity mapping* tab
in the *Teams/Developers* configuration corresponding to the project you are interested in.

On the left, the interface displays a list of the current authors.

![The developer list](configuration/DeveloperAliasMappingDevList.png)

Choose an author you want to work on. This is the name that you want
to *keep*.

On the right, a new list will appear.

![Developer list with alias list](configuration/DeveloperAliasMappingAliasListTop.png)

To find the alias you want to merge, you can use the
“Filter aliases” box to search for matching aliases.
Regular expressions are allowed, with whitespace counting as a logical OR.

![Use the filter box to search for aliases](configuration/DeveloperAliasMappingFilterBox.png)

When you have found the alias or aliases you are looking for, select
them on the right and click on *Stage changes*.

![Developer list with alias list, getting ready to select.](configuration/DeveloperAliasMappingAliasList.png)

In this example, we want to merge the aliases “Calvin” with  “Calvin Buckley”.
This will update the list of authors on theleft. Now we can either make other modifications or click on “Submit”
at the top of the window to finalize the operation.

### Separating aliases from their authors

If we change our minds, we can later **separate** these aliases from
the author that we assigned them to. To do this, we select the
corresponding checkbox and click on *Stage changes* again.

![Selecting an alias to unmerge](configuration/DeveloperAliasMappingUnmerge.png)

After clicking on *Submit*, the aliases we chose to separate will
become full-fledged authors. Because these are new
identities, group membership, former contributor status, and exclusion
status will be lost. Merging and unmerging an alias is *lossy*.

### Renaming authors

Because an **Author** is separate from the version control
**alias**, authors can be renamed without changing how they are
detected by CodeScene’s analyses. To change a name, click
on that author in the left column. You will notice an “Edit name”
link next to their name in the box on the right.

![The rename field](configuration/DeveloperAliasMappingRename.png)

When you run a new analysis, the new name will appear in the analysis
results.
