# Code Churn

Code churn is a measure that tells you the rate at which your code
evolves. Code churn has several usages:

- *Visualize your development process:* Your code churn signature in
  the diagrams below mirrors the practices you use to deliver code. You
  may want to watch out for regular spikes, which may hint at a mini
  waterfall going on in your daily work
- *Reason about delivery risks:* Code churn is a good predictor of
  post-release defects. Thus, it’s a warning sign if you approach a
  deadline while your code churn increases. That’s a sign that the code
  gets more and more volatile the closer you get to your deadline. You
  want the opposite. You want to stabilize more and more code the
  closer you get to delivery.
- *Track trends by task:* CodeScene lets you inspect the size and impact
  of your tasks. Use the information to see if your project management
  tasks are on an appropriate level or if each one of them implies a
  mini big bang in terms of code changes.

CodeScene provides several churn measures. They’re all described
in this guide and you typically investigate all of them to get the
overall trend in your codebase.

## Use the Commit Activity as the Pulse of your Codebase

The commit activity chart shows the number of commits and contributing
authors over time as illustrated in [Fig. 154](#code-churn-pulse).

![Commit and Author activity](guides/technical/CodeChurnPulse.png)

The number of commits and authors over time is a different kind of
churn. This metric will typically correlate well with your other Code
Churn metrics described below. However, you want to look out for
potential productivity issues like an increase in authors without a
corresponding increase in commits and churn; Such a trend often
indicates that you’ve more programmers contributing than the software
architecture (and/or organization) can support.

## Correlate Trends in the Number of Contributors with the Churn Metrics

The Active Contributors trend shows the number of authors in the codebase over time.
CodeScene calculates this information by looking at the first and last recorded contribution
times for each author. This lets you view a trend as illustrated in [Fig. 155](#active-contributors-trend).

![Active contributors trend](guides/technical/ContributingAuthorsTrend.png)

The contribution trend is particularly interesting when correlated with the other churn trends. You may
also want to compare the contribution trend with the system complexity trend (see [Architectural Analyses](../architectural/architectural-analyses.md)).
Correlating the number of active contributors to these churn metrics lets you evaluate the effect (or lack thereof) when a project is scaled up or down.

## Uncover Long-term Trends in your Code Churn Rolling Average

CodeScene measures two separate churn metrics: the number of
added lines of code, and the number of deleted lines. The values in the
graph shows the rolling average of your code churn (rolling average is a
technique to smooth out sudden fluctuations in your data). You configure a
time window for the rolling average in your project configuration.

The main use of these code churn metrics is to reason about delivery
risks; If you’re close to a deadline and have a rising churn, you might
want to understand *why*. After all, an increase in churn means that the
codebase has become more and more volatile. Unless you have an extensive
safety net in terms of tests and continuous deployment techniques, you
probably want to stabilize before a release as illustrated in [Fig. 156](#code-churn-added-trend).

![The code churn trend](guides/technical/CodeChurnAddedRolling.png)

## Inspect The Level of your Tasks

It’s a challenge to strike the right level when you partition your work into individual tasks. Large tasks are hard to reason about and also
less predictable to plan. That’s why we generally prefer small and well-focused tasks.

CodeScene lets you inspect the impact of your project management tasks on the codebase in terms of both code churn
and collaboration (that is, how many authors worked together to solve the task?) as illustrated in [Fig. 157](#code-churn-by-ticket-id).

![Code Churn by Ticket ID](guides/technical/CodeChurnByTicketID.png)

CodeScene uses your Ticket ID to group individual commits into tasks. As you see in [Fig. 157](#code-churn-by-ticket-id), CodeScene also
calculates a *Lead Time* for each task. The lead time is the time that passed between the first and the last commit referencing a
specific task. Note that many tasks tend to be solved in a single commit. In that case CodeScene doesn’t have the data to calculate a
proper lead time. So CodeScene defaults to one hour in case of a task that’s resolved in a single commit.

We recommend that you use the lead time data to track tasks that drift in time. Often, those tasks suggests requirements that aren’t
as well-defined as they could be. You can also use the lead time analysis to track the effects of process changes in your organization.
