# Branch Analyses

Many organizations are transitioning to short-lived feature branches and employ practices like continuous integration/delivery.
To work in practice, branches have to be kept short-lived.

CodeScene introduces a new suite of analyses that measure branching activity, different lead times, and risks.
This is information you can use to get insights into your CI/CD process, or to reason about delivery and development risks.

## Meet the Branch Measures

CodeScene presents a summary of the branch statistics on its dashboard as shown in [Fig. 150](#dashboard).

![An overview of the branch measures](../shared/guides/branches/dashboard.png)

Branch Duration
: The calendar time from the first commit of a branch to the latest commit of the branch.
  For example, if the first commit on the feature branch task-52-support-cherenkov-drive-mode
  is made at 7am on Dec 1st, and the second commit is done at 10am on the same day, the
  branch duration at that point is three hours.
  High values indicate long-lived branches, which can indicate high risk.

Lead Time to Merge
: The calendar time between when the last commit of the branch is made, and when the
  branch is merged.
  It can be caused by waiting for code reviews or other tasks required before merging.

Contributing Authors
: The number of unique authors that have contributed to a branch.
  A high number could indicate a complicated feature, or that it contains many features
  from different authors.

By default, CodeScene calculates statistics for all branches that have been worked on during the past two months.

> *Note*: you can configure the time span for active branches as well as filter out specific branch names (e.g. long-lived
> release branches) in the project configuration.

Use this high-level overview to ensure you have a short *Branch Duration* and a short *Lead Time to Merge* for each branch. When
a branch lives for too long, it puts your delivery at risk of merge conflicts and unexpected feature interactions.

If you click on the link “View branch delivery risks” below the branch statistics summary,
CodeScene displays a detailed view of each branch as shown in [Fig. 151](#branch-details).

![A detailed analysis of the work on each branch](guides/branches/detailed-branches.png)

This information lets you identify early signs of trouble, such as long-lived branches, or branches that become congested
by attracting contributions from several different authors.

Note that the thresholds used to trigger the early warnings are automatically deduced from your normal branching strategy; CodeScene warns
when a branch deviates from your normal ways of working. As such, the warnings are relative to the patterns in your codebase.

The information on long-lived branches can be used to:

* Re-plan the scope: Sometimes it’s just too much work in a single feature. Identifying a smaller feature set that you can deliver faster is one way to shorten the lead times and minimize risk.
* Prioritize verification activities: Use the early warning to focus extra code reviews and tests on the highlighted branches.

Another example of such deviations from normal ways of working is the number of contributing authors. A warning for an unusually high
number might put you at risk for parallel development. It’s also a sign that there’s too much development activity on that branch, so you could
use this information to investigate the scope.

## Detect Delivery Risks

CodeScene predicts the delivery risk of each active branch (i.e. unmerged work) as shown in [Fig. 151](#branch-details).

This *risk classification* predicts the risk for defects, and is given on the scale 1-10 where 10 is the highest risk.

Use this information to plan preventive measures such as extra code reviews and tests. You can also setup a separate CodeScene
analysis and just focus on the work being done on the branch. In extreme cases you may chose to postpone the merge of such
high-risk branches if you’re close to a critical deadline.
