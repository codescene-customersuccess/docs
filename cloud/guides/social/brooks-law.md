# Delivery Effectiveness by Organizational Trends

The Delivery Effectiveness measures the development throughput in the context of organizational trends.

The throughput measure is based on the ideas from Brooks’ Law.
Brooks’ Law states that adding more people to a late software project makes it later. The reason for this is communication and
coordination overhead. While we add more people to a project, the total number of available hours increases linearly *but* the
coordination paths increase exponentially. Hence, there’s a point beyond which each additional person’s hours get comsumed by
the increased coordination efforts…and then some.

Hence, use CodeScene’s development output to measure the effects of any changes in staff as shown in [Fig. 135](#development-output-velocity).

![Development output with respect to the number of contributing authors](guides/social/development-output-velocity.png)

The development output graph shows the following data:

* *Development Output*: This is measured by taking all commits during a week and dividing them by the number of contributing authors.
  The resulting normalized output metric gives you an estimate on the organizations’s output.
* *Authors (month)*: This trend shows how many unique authors that have contributed code over a month. This trend is likely to reflect the
  total number of developers on the project.

If your project is at risk of falling victim to Brooks’ Law, then you will see this as an increased distance between the total number
of authors and their normalized output.

Like always when trying to measure things like developer and organizational productivity, the absolute numbers aren’t that interesting; the
interesting thing is the trend. Do you get an increase or decrease in response to changes in staffing?

## Delivery Effectiveness by Team

By configuring teams in CodeScene, you enable a detailed breakdown of the Delivery Effectiveness to a team level:

![Development output by team](guides/social/brooks-by-team.png)

The trends let you detect the frequency of contributions, patterns in each team’s contributions, as well as detecting
when a team stops contributing, perhaps as a shift in responsibility to a different part of the codebase.

## Follow-up with in-depth Analyses of the Team Composition

Should you identify a decrease in development output, then we recommend getting more information via the following analyses:

* *Coordination Needs*: Check if the teams and/or individual developers need to coordinate their work in the hotspots using the [Parallel Development and Code Fragmentation](fragmentation.md) analysis.
* *Decrease in Code Health*: The decrease in development output could also be due to an increased level of technical debt, so inspect the [Code Health – How easy is your code to maintain and evolve?](../technical/code-health.md) analysis.
* *Team Composition*: Measure the on-boarding and experience effects as described in the next section below.

## Measure Team Composition Trends

While Brooks’s Law is one potential reason that a project might hit a wall, there might be other explanations as well.
Sometimes a development effort is appropriately staffed, but it takes time for people to get up to speed with a new codebase; on-boarding
always comes with a cost. Hence, the team composition in terms of experience on your specific codebase is an important factor.

CodeScene measures team experience as shown in [Fig. 137](#team-composition).

![The team composition with respect to experience accumulation and on-boarding.](guides/social/team-composition.png)

The team composition visualization includes the following information based on the actual contribution span of each author:

1. Monthly team composition in terms of experience on this particular product. There are three categories: *onboarded* (0-3 months), *experienced* (6-12 months), and *veterans* (+12 months).
2. Total accumulated experience in terms on months worked on the codebase (black line).
3. “Qualitative” team experience: this is a weighted value where we consider the experience of each developer currently in the team (blue line). On-boarding a developer
   will come at a slight cost for a period of time. The model also takes ramp-up effects into consideration.

Often, the area between the black and blue lines is the interesting part. The wider the gap, the higher the on-boarding costs. On-boarding
can of course also be viewed as an investment. From that perspective, the area between the lines shows the unrealized potential if the
organization manages to keep the team stable and avoid high author churn.

### Highlight the Effects of Author Churn

The team composition analysis is also useful to highlight the effects of *High Author Churn*: Taking people in and out of a project
comes with a cost due to lower system mastery and repeated on-boarding effects. Keeping a team stable allows for learning and is
very likely to have a positive impact on the development output.

[Fig. 138](#team-author-churn) shows the effects on high author churn, where the qualitative team experience fails to accumulate:

![High author churn leads to low system mastery and constant on-boarding costs.](guides/social/team-author-churn.png)

When used together with the Brooks’s Law development output trends, these graphs help visualizing the costs and effects over on-boarding
and staffing changes over time.
