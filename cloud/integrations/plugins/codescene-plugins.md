# CodeScene’s Plugin System: integrate static analysis tools and code coverage metrics

Deprecated Feature Alert

The plugin system is deprecated and will soon be removed. Code Coverage data for analysis can instead be uploaded to CodeScene using the new [Code Coverage](../code-coverage.md) integration.

The CodeScene platform covers a broad range of software analyses, including technical and organizational aspects.
CodeScene’s plugin system lets you augment that information by integrate third party information in the CodeScene analysis views.
This lets you get a holistic picture of your codebase in one place.

The goal for the CodeScene team is to open up the plugin API and let the community – and you – provide custom
plugins. That means you could integrate *any* kind of information in the analysis views, for example performance
profiling, security scan audits, or any proprietary data you use for decisions today.

In the short term, the CodeScene team is developing plugins for the most frequently requested integrations:

* **SonarQube and SonarCloud**: Integrate static code analysis results into CodeScene’s views. Prioritize static analysis
  results via CodeScene’s hotspots and virtual code review, or integrate security specific findings in the hotspot views.

![CodeScene's plugins let you integrate other data sources to get a holistic overview of your codebase.](../shared/integrations/plugins/metrics-in-context-overview.png)

These plugins are available for you automatically. This document explains how to configure them as well as
capturing the main uses cases.

The main advantage of the integration is that CodeScene a) aggregates data from multiple sources, b) puts the metrics
into context via CodeScene prioritized hotspots, and c) visualizes large data sets which makes the data actionable.

## Integrate SonarQube as a CodeScene plugin

**Motivation**: There is an overlap between CodeScene’s technical metrics (e.g. code health and virtual code review) and
static analysis. The code health metrics are more at the design level while static analysis can be a complement as a low-level
feedback loop during development. At the system level, static analysis is often verbose. Via
CodeScene’s SonarQube plugin, all static analysis details are put into the context of CodeScene’s prioritized hotspots. The
combination gives you the best of two worlds and help making the static analysis results actionable through the
lens of prioritized hotspots.

SonarQube is a static analysis tool. The main differences compared to CodeScene are:

* Static analysis works on a snapshot of the codebase while CodeScene considers the temporal dimension and evolution of the whole system.
* CodeScene priorities based on the likely business and delivery impact, not just what’s visible in the code.
* CodeScene measures organizational factors like key personnel risks and team coordination. These factors increase
  in importance with the size of the organization.
* CodeScene focuses on the maintainability, readability, and sustainability of the development, while Sonar provides
  detailed code-level findings.

As such, static analysis is often a good complement to CodeScene.

### CodeScene integrates the Sonar data into the Interactive Maps and Code Review

CodeScene’s Sonar plugin integrates any SonarQube data into the interactive hotspot map as well as in the virtual code review:

![CodeScene integrates SonarQube metrics in its interactive views. Here's an example of visualizing Cognitive Complexity.](../shared/integrations/plugins/sonar-codescene-view.png)

CodeScene lets you extract any metrics from Sonar. You specify the metrics of interest in your CodeScene project:

![Configure the Sonar metrics of interest. Each metric gets its own perspective in CodeScene's interactive map.](../shared/integrations/plugins/sonar-plugin-configuration.png)

You can specify any number of metrics, and each one of them will get its own perspective inside CodeScene’s hotspot map.

CodeScene also augments its virtual code review with a summary of the Sonar findings. Clicking on the “Read More” link takes you
to the detailed Sonar data:

![CodeScene aggregates the Sonar findings per file in its virtual code review.](../shared/integrations/plugins/sonar-virtual-code-review-integration.png)

### Configure the SonarQube Plugin

The SonarQube plugin needs credentials that let CodeScene access the Sonar instance. You specify these credentials once in the
global setting so that they can be reused for all CodeScene projects:

![Specify the Sonar access token globally so that it can be reused for all CodeScene projects.](../shared/integrations/plugins/sonar-global-configuration.png)

The global configuration is typically done once by a CodeScene admin. Each project can now specify the Sonar metrics of interest:

![Configure the Sonar metrics of interest inside your CodeScene projects.](../shared/integrations/plugins/sonar-plugin-configuration.png)
