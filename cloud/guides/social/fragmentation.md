# Parallel Development and Code Fragmentation

Large scale software development is a social activity. However, the technical nature of our work tends to obscure
that fact and we often mistake organizational issues for technical problems.

One such example is excess parallel development. Excess parallel development is something that happens when
your architecture cannot support the way you’re organized. You may have 20-30 developers that need to modify
the same file, but for different reasons. The symptoms you see are often technical, for example expensive merges,
code that’s hard to understand since it’s changed by different people all the time, or unexpected feature interactions.
CodeScene’s *Parallel Development* analysis helps you uncover and prioritize these problems.

Before you read on, please note that CodeScene uses the name of each committer to calculate the fragmentation
metrics. So *make sure* you understand the possible biases
discussed in the guide [Know the possible Biases in the Data](bias.md).

## The Coordination Needs View Uncovers Excess Parallel Development

Excess parallel development means the modules have a high *fragmentation
value*. A high fragmentation value means that the development effort is
shared between multiple programmers. This is a risk you want to be aware
off - the number of programmers is one of the best predictors of the
number of post-release defects in a module. The more programmers, the
more quality issues in that code.

CodeScene runs the fragmentation analyses on both individual authors and teams. You may want to focus on the
team view in case you have cohesive teams with well-defined responsibilities.

If your organization doesn’t have any team structure, start with
investigating the fragmentation by authors  as illustrated in [Fig. 113](#fragmentation-map).

![An example of a fragmentation map](guides/social/fragmentationmap.png)

The fragmentation map in [Fig. 113](#fragmentation-map) shows the *fractal value* of each file. A fractal value is the
degree of parallel work:

1. Fragmentation 0 (zero): This means that the file has had a single
   developer working on it.
2. Fragmentation closer to 1.0 (one): The closer to 1.0 the
   fragmentation gets, the more developers behind the code and the
   smaller the contribution of each developer.

Once you’ve found a part of your codebase with excess parallel work you want to get more detailed information.
The Fractal Figures described in the next section gives you all the details you need.

## Get more Detailed Information with Fractal Figures

The fragmentation map in [Fig. 113](#fragmentation-map) is interactive. That means you can click on each file and
inspect the amount of fragmentation as illustrated in [Fig. 114](#fragmentation).

![An example of a developer fragmentation](guides/social/social-developer-fragmentation.png)
