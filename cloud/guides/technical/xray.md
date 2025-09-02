# X-Ray

## X-Ray gives you Deep Insights into your Code

Hotspots are code with high change frequencies.
We know that any improvements we do to a hotspot are likely to pay-off immediately. However, sometimes those
improvements aren’t straightforward; Some of the worst hotspots we’ve seen are files with several thousands
lines of code. Given that amount of code, where do we start? Are all parts of that file equally important? Are there
any functions or methods that contribute more to the code being a hotspot than others?

Until recently, this is where the CodeScene analyses stopped.
After all, we’ve significantly reduced the amount of code we need to consider as we narrowed down a whole codebase to
a single file where improvements matter. However, we need to do even better and CodeScene’s X-Ray feature fills this gap.

X-Ray is a language-dependent analysis. X-Ray is available for the following programming languages:

| Language                                 | X-Ray   | McCabe Complexity   | Biomarkers   |
|------------------------------------------|---------|---------------------|--------------|
| C                                        | Yes     | Yes                 | Yes          |
| C++                                      | Yes     | Yes                 | Yes          |
| C#                                       | Yes     | Yes                 | Yes          |
| Java                                     | Yes     | Yes                 | Yes          |
| Groovy                                   | Yes     | Yes                 | Yes          |
| JavaScript                               | Yes     | Yes                 | Yes          |
| TypeScript                               | Yes     | Yes                 | Yes          |
| React (jsx, tsx)                         | Yes     | Yes                 | Yes          |
| Vue.js                                   | Yes     | Yes                 | Yes          |
| Objective-C 2.0                          | Yes     | Yes                 | Yes          |
| Scala                                    | Yes     | Yes                 | Yes          |
| Python                                   | Yes     | Yes                 | Yes          |
| Swift                                    | Yes     | Yes                 | Yes          |
| Go                                       | Yes     | Yes                 | Yes          |
| Visual Basic .Net                        | Yes     | Yes                 | Yes          |
| PHP                                      | Yes     | Yes                 | Yes          |
| Ruby                                     | Yes     | Yes                 | Yes          |
| Rational Software Architect models (C++) | Yes     | Yes                 | Yes          |
| Kotlin                                   | Yes     | Yes                 | No           |
| Clojure                                  | Yes     | No                  | No           |
| Erlang                                   | Yes     | No                  | No           |
| Apex                                     | Yes     | No                  | No           |

We’ll continue to add X-Ray and biomarkers support for more programming languages over time. As always: if you lack support for
a language, let us know and we are likely to make it happen.

## An Overview of X-Ray

X-Ray is an analysis that operates on the function/method level of your code. Thus, X-Ray is able to provide deep
and detailed information on what’s happening *inside* a Hotspot.

There are three main use cases for the X-Ray functionality:

1. X-Ray lets you make sense of large files and get specific recommendations on the parts to improve.
2. X-Ray provides detailed information on why a cluster of files are temporally coupled.
3. X-Ray recommends re-structuring opportunities on the methods in your Hotspots in order to make the code easier to understand and maintain.

In the following guide we’ll cover all of these cases. Let’s start with how you can make sense of large files.

## X-Ray calculates Hotspots on a Method Level

A Hotspot analysis is orthogonal to the data it operates on. That is, CodeScene presents hotspots as
individual files, but also on an architectural level as entire components and sub-systems. With X-Ray, we climb down
the abstraction ladder and run a Hotspot analysis on a method level.

A large file is like a system in itself. Some parts remain stable, while other parts of the file keeping changing
as new features are added and bugs get resolved. With X-Ray, you’ll get a prioritized list of the methods you want
to refactor and improve first. This is important since re-designing a large module is both high-risk and expensive. So
instead you want to take an iterative approach to your improvements and base those improvements on data.

To run X-Ray, go to your Hotspot map, click on the Hotspot and select ‘X-Ray’ from the context menu as
shown in [Fig. 55](#x-ray-context-menu).

![Run X-Ray from the context menu](../shared/guides/technical/XrayRunXray.png)

X-Ray is run on demand. That is, the first time you execute it on a Hotspot it may take a few seconds to get the results.
Sub-sequent accesses are cheap since we cache the results.

Once you get the results you’ll see that you typically spend more time on some methods than others. So let’s walk
through the X-Ray results and look at the individual pieces. Have a look [Fig. 56](#x-ray-results) as a starting-point.

![An overview of the X-Ray results.](../shared/guides/technical/XrayResults.png)

[Fig. 56](#x-ray-results) shows the results of an X-Ray analysis. We see that our hotspot is a method named getGridCoverageReader, which
consists of 134 lines of code. You also see that getGridCoverageReader has a Function Complexity of 26, which is a fairly high number. Thus,
the method represents complicated code that you also have to work with often.
You can also see which issues have been identified in the Code Review column. You can find detailed information about each issue
by hovering over it.

Methods like this are exactly where you’d like to focus your refactoring efforts; The high change
frequency of the method indicates that improvements are likely to pay-off immediately. And the lines of code and complexity numbers
gives you a sense of the effort you need to invest to make the necessary improvements.

But X-Ray gives you more information. As you see in the table above, CodeScene also lets you run a Complexity Trend analysis.
In this case, the trend analysis
will show the complexity growth of an individual method. Look at the results of those trends to determine if the X-Ray
hotspot represents a method that we’ve already started to refactor or, the more common case, represents code that
continues to degrade in quality.

### A Note on Overloaded Methods

Some languages like C++, C#, and Java let you use the same function name for different implementations.

CodeScene *combines overloaded methods* - that is, it presents the statistics for all of the overloads as a single entry.
For instance, if you have functions with the signature f(int) and f(string) they will be combined in the analysis.
This approach typically gives you better results since the overloaded functions are part of the same logical unit of design
and you want to analyze them as such.

CodeScene includes a count on the total number of methods to highlight such overloads, as shown in [Fig. 57](#x-ray-overloads).

![Overloaded methods in X-Ray](../shared/guides/technical/xray-overloads.png)

## Interpret Cyclomatic Complexity as part of the Evolutionary Metrics

The cyclomatic complexity measure included in X-Ray doesn’t stand on its own. Just because some code is complex doesn’t
mean it’s a problem. However, when we combine a complexity measure with change frequencies – like X-Ray does – we get
information we can act upon since the code complexity is put into context.

CodeScene includes its cyclomatic complexity metric as a supplement to the other information as a decent approximation of
code quality. As a rule of thumb, any cyclomatic complexity value above 10 is
likely to be problematic. A cyclomatic complexity beyond 25 is likely to hint at a true maintenance nightmare. But again, use
the complexity value as a guide, not as an absolute truth.

Cyclomatic complexity also helps you make refactoring decisions in the sense that you get a rough idea on how hard the
code will be to test. Each branch in your functions add to their complexity value and, as a direct consequence, to the testing efforts.

CodeScene currently supports cyclomatic complexity calculations for the following languages:

* Java, Kotlin, Groovy
* C#
* C, C++
* Objective-C

## X-Ray calculates Change Coupling between Methods

As you X-Ray a Hotspot, CodeScene also looks for change coupling *between* individual methods in that file. This is information that
helps you identify unexpected change patterns. Let’s look the example in [Fig. 58](#x-ray-internal-coupling).

![X-Ray calculates change coupling between the methods in your Hotspot.](../shared/guides/technical/XrayInternalCoupling.png)

[Fig. 58](#x-ray-internal-coupling) shows that two methods, getGridCoverageReader and getWebMapServer changes together in
42% of all changes. That is, every third time you change one of these methods there’s a predictable change to the other one.

You use the Change Coupling results as input to your refactoring efforts. For example, in the example above, you probably
want to have a close look at both methods to see why they are so strongly coupled in time. Often, there’s either a leaky
abstraction or a fair chunk of duplicated logic in either part of the code.

One of the most common reasons for unexpected change coupling is a dear old friend: copy-paste. In fact, copy-paste is
so common that we’ve included an analysis of code similarity in X-Ray as
illustrated in [Fig. 59](#x-ray-code-similarity).

![An example on the code similarity analysis in X-Ray](../shared/guides/technical/XrayCodeSimilarity.png)

In [Fig. 59](#x-ray-code-similarity) you see that there are two methods – with names that indicate they’re related –
and a code similarity of 86%. You want to use this data as a starting point. If you could encapsulate that shared logic in
a separate method your change coupling will go away and your application will become a little bit easier to maintain.

## X-Ray lets you look into Change Coupling Clusters

Change Coupling is one of the most powerful software analyses in our arsenal. A change coupling analysis often
highlights unexpected change patterns in our codebase and provides us with important information that we cannot
deduce from the code alone. However, change coupling has also been one of the hardest results to act upon.

Think about it for a minute. Let’s say that you investigate some change coupling results and identify a cluster of
10 files that tend to change together. Now, how do you uncover the reason for this coupling in time? Well, in more
complex cases you need to compare the code and walk through the historic revisions to know which parts of the files
that are responsible for the coupling. This can be painful, particularly for large files that are low on cohesion.
Enter X-Ray for change coupling.

With X-Ray, all of these steps are completely automated. You just click on a file in the change coupling visualization and
select ‘X-Ray’ from the context menu as illustrated in [Fig. 60](#x-ray-temporal-cluster).

![Invoke X-Ray by using the context menu in a change coupling visualization.](../shared/guides/technical/XrayTemporalCluster.png)

Once X-Ray is done, you’re presented with a dependency wheel on method level. Have a look the dependency
wheel in [Fig. 61](#x-ray-external-coupling) and I’ll walk you though the details.

![The X-Ray of external change coupling](../shared/guides/technical/XrayExternalTemporalCoupling.png)

The dependency wheel in [Fig. 61](#x-ray-external-coupling) is an interactive visualization. As you see in the example above, when we
hover over the part that represents the method testGlobalCapabilities, we see that the method is
coupled in time to two other methods located in the same class. This information is powerful: now we’ve limited the
amount of code you need to inspect in order to improve the design and break this expensive change pattern.

## A word on Software Clone Detection

Copy-paste detection isn’t exactly a new technique. However, it’s still far from mainstream in the software industry.
One reason that copy-paste detectors haven’t caught on is because they fail to prioritize their findings in a
sensible way.

If you look at studies of large codebases, you’ll learn that around 5-20% of all large codebases represents duplicated
logic to some degree. That’s quite a lot. There’s simply no way you can start to refactor that amount of code and hope
to get a return on that investment. In fact, most of that duplicated code doesn’t matter. So how can we find the software
clones that limit out ability to maintain the system?

CodeScene’s X-Ray solves this dilemma. By combining copy-paste detection with change coupling we *know* that the
identified software clones matter. For example, if you look at the example above, you’ll see that the two methods
with a code similarity of 98% are changed together in one third of all cases. That is, with X-Ray you’ll find the software
clones that actually matter. This lets you prioritize the improvements that you do while still ensuring that you get a
real return on those refactoring investments.

<a id="proximity"></a>

## Follow the Restructuring Recommendations

CodeScene is the first ever software analysis tool that implements a *proximity analysis*. The X-Ray findings present the proximity results as a set of
recommendations on how to re-structure the methods in a Hotspot in order to make the code more readable. Let’s start by understanding
the concept of proximity and why it matters to our ability to maintain code.

The proximity principle focuses on how well organized your code is with respect to readability and change. You use proximity both as a design principle and as a heuristic to evaluate the cohesion and structure of existing code.

The principle of proximity is a concept from Gestalt psychology. The Gestalt movement pioneered principles on how we make sense of all chaotic input from our sensory systems. We need to understand the Gestalt principles if we want to optimize our code for readability. Remember, we use the same brain to interpret code as we use to make sense of the physical world.

![The principle of proximity](../shared/guides/technical/XrayProximityGestalt.png)

Within Gestalt psychology, the principle of proximity specifies that objects or shapes that are close to one another appear to form groups as illustrated in [Fig. 62](#x-ray-proximity-gestalt). If we translate this to software, it means that readable code is structured in a way that lets our brain understand parts of the source code file as a whole. The main reason is because we want our code to support our change patterns: code that is expected to be changed together should be close. Such a code structure serves as a powerful reminder to both the programmer and, more important, the code reader that a set of functions belong together.

CodeScene measures proximity based on your change patterns (aka internal change coupling). You see an example on a proximity analysis in [Fig. 63](#x-ray-proximity).

![An example on a proximity analysis in X-Ray](../shared/guides/technical/XrayProximity.png)

The highlighted recommendation in [Fig. 63](#x-ray-proximity) shows two functions, handleLayers and handleLayerGroup, that are frequently changed together.
That is, they are temporally coupled. However, if you look at the implementation in the project you’ll see that there are thousands of lines of code
between handleLayers and handleLayerGroup. This is bad news for a maintenance programmer because it’s so easy to miss an update to one of the functions.
A simple, low-risk refactoring is to just move those two functions next to each other. That simple change lets the code signal that the functions belong together.
In addition it dramatically increases the chances that a bug fix to one of the functions is applied to the other function too.

So what metric do we use for proximity? If you look at [Fig. 63](#x-ray-proximity) you see that there’s a *Total Proximity* column in the analysis results.
The proximity values specify the distance between the related functions. The unit of measure is the number of intermediate functions between the related parts.
In our example with handleLayers and handleLayerGroup [Fig. 63](#x-ray-proximity) shows that there’s a total proximity of 17. That means that there are 17 (!)
functions separating the implementation of handleLayers from its related temporally coupled handleLayerGroup.

## Know the limitations of Method-level analyses

CodeScene tracks renamed content. That is, if you move or rename a file, we make sure to fetch its past
history even if you’ve renamed the file multiple times. We implement a similar mechanism for X-Ray too.
X-Ray will track and analyze the history of renamed methods/functions…except when it won’t. Let’s elaborate on that
so that you know the possible corner cases.

First of all we have a philosophical question here. Let’s say you decide to refactor parts of your code. You simplify
some parts of it and rename a few functions. Now, when is a function renamed and when is it actually a new function that
replaces an old one? This distinction isn’t clear.

X-Ray resolves this dilemma by introducing a set of heuristics for its rename detection and, in general, X-Ray tries to
do the most sensible thing to avoid false positives in
your analysis results.

## Limitation of Analysis Depth

X-Ray looks at a maximum of 200 revisions. In most codebases that’s more than enough. So why put a limit on it?
Well, there are projects that have been around for a long time and their top Hotspots may well have over thousands of commits. To
X-Ray that data will take quite some time. In addition, the most interesting patterns are likely to be in the recent evolution of
the Hotspot.

Most of the time this is the behavior that you want. However, in some case you want to dive deeper and X-Ray the complete evolution of
a Hotspot. Future versions of CodeScene will support a configuration option for this.
