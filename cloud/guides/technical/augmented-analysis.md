# Manage Hotspots and Technical Debt with Goals

CodeScene lets you add contextual information to the analysis data as specific \_goals_.
In combination with the hotspot analyses, CodeScene’s goal-oriented workflow serves as a framework for managing
technical debt and code quality issues, from detection to action.

## Specify Contextual Information

Context matters:

* What features do you plan to implement next and what parts of the system will they affect? If you know a particular module requires an extension, you might want to start by a set of pro-active refactorings to make the new feature cheaper and less risky to implement.
* There’s always a trade-off between adding new features versus improving existing code. So how much can you spend on re-work and improvements?
* Finally, there’s a decision to be made on when is a piece of code is good enough.

By planning a goal, you specify such contextual information which is then processed as part of the analysis.
This means that the analyses are aware of your goals and can measure the progress towards them. Let’s get started with an example.

### Plan a Goal for a Hotspot

CodeScene supports the following goals and categorizations of code:

1. *Planned Refactoring*: Choose this category when you have investigated the code, perhaps with CodeScene’s virtual code reviewer or its X-Ray analysis and see the need to pay-off some technical debt in the short term.
2. *Supervise*: Choose this category for code that might be acceptable for now, but that shouldn’t grow worse. Supervise lets you put a quality bar on existing code, which is particularly useful in legacy codebases.
3. *No Problem*: Choose this category to let CodeScene know that you don’t consider the code a problem. Perhaps you plan a replacement of the hotspot code, or you consider the report a false positive.
4. *Critical Code*: Categorize a module as Critical Code to have it indicated in Pull Requests when modified, included in the PDF reports, and supervised for risky changes. Typical use cases involve tracking code that’s business critical or has security impact.

You can specify the goals and categories in the  Code Health view.
Goals can also be specified on any file via the virtual code reviewer in CodeScene.

![Add a goal in the biomarkers view](guides/technical/act-on-hotspots.png)

Once a goal has been added, CodeScene will start to track it in every sub-sequent analysis.
How CodeScene tracks a file depends on the category you have assigned.
Let’s look at the differences between the categories in the next sections.

### Analysis Of Planned Refactorings

When you specify a *Planned Refactoring* goal, CodeScene will do the following, depending on how the code evolves over time:

* *Code Degrades*: This will trigger a warning on the analysis dashboard since it violates the refactoring goal.
* *Code Improves*: This gives you a thumbs-up as the goal was met and the code is now in measureably better state.
* *No Change*: CodeScene understands that complex refactorings take time. However, if there’s no clear improvement over the next months, CodeScene will warn you about it. Perhaps you want to re-consider your goal or prioritize the refactoring?

### Analysis Of Supervised Hotspots

Specifying a Supervise goal puts a quality bar on that module. If it declines in code health, the goal will fail and you get an alert.

Note that project specific thresholds for code health alerts apply to goals as well; a supervise goal won’t fail as long as the module
is above your manually configured minimum code health level (the default is code health 9).

### Analysis Of Code Marked As “No Problem”

No Problem is typically used on false positives or code that is planned to be removed in the near future.

Specifying a No Problem goal on a hotspot suppresses that module in the analysis. It won’t show up in the UI or reports.

There’s always a danger of suppressing warning signs or problems. Hence, CodeScene keeps analyzing No Problem modules in the
background. Should that code degrade in code health, then CodeScene will point your attention to it by failing the goal so that you
can re-consider the goals for that hotspot.

### Analysis Of Code Marked As “Critical”

All files marked as “critical code” are listed in a dedicated view where you can inspect their evolution.

Files marked as “critical code” are highlighted in CodeScene’s code review recommendations given on Pull Requests.
This is important since critical code often has security implications and a detailed code review is recommended:

![CodeScene notifies reviewers when critical code is modified.](guides/technical/code-review-critical-code-warning.png)

During an analysis, critical code acts like the “Supervise” goal. That is, any code health decline leads to a
failed goal and is reported as such. Just as for Supervise, Critical Code respects the project specific thresholds for code health alerts.

## Manage Your Goals From The Dashboard

Most of the time you will interact with the goals via the virtual code reviewer or the Code Health view.
But you can also get an overview of all goals and administrate them on a separate dashboard as shown in [Fig. 45](#au-notes-dashboard).

![Manage your goals on their dashboard.](guides/technical/au-notes-dashboard.png)

The dashboard is particularly interesting for the hotspots classified as *No Problem* as they won’t show up in the
other analyses unless CodeScene found a growing problem in them.

## Know The Edge Cases When Tracking Hotspots

CodeScene does its best to track the goals you have attached to hotspots even if you move or rename the hotspot files.
However, in some situations this isn’t possible. The reasons are due to the way Git works.

When CodeScene cannot find the file referenced by a goal, that goal
appears in the list of “Lost Notes” in the Hotspot Goals Dashboard.

The interface for lost goals lets you to decide what to do:

* A file has been removed from the project. If this is the case, it’s time to remove
  the note as well. Just click on the Pen icon and select “Delete”.
* A file (or an ancestor directory) has been renamed or moved. You
  should create a new note through the usual procedure, then delete
  the lost note.

The following situations are known to cause a *lost goal*:

* Deleted content: The most common reason for a lost goal is that the original hotspot has been deleted.
* Two-step renaming of content: Normal file renames work fine, but if the deletion step and the adding of the new
  file are performed in separate commits then CodeScene won’t be able to maintain the link from note to content.
