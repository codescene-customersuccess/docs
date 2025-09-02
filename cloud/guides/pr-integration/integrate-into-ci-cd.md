# Integrate CodeScene with Pull Requests

CodeScene offers an automated integration with GitHub, BitBucket, Azure DevOps or GitLab pull requests to incorporate the *Delta Analysis* results into existing delivery workflows.

Integration is different per provider:

* Github via Checks with option of annotations
* Bitbucket via either Builds or Code Insights Reports
* Azure Status Check and Pull Request comment
* GitLab via Merge Request Discussion comment

See [GitHub](github.md#github-presentation), [Bitbucket](bitbucket.md#bitbucket-presentation), [Azure](integrate-codescene-with-pull-requests.md#azure-presentation), [GitLab](gitlab.md#gitlab-presentation) presentation.

## CodeScene and Pull Requests: Use Cases

The purposes of CodeScene’s pull request integration is to:

* Specify quality gates that trigger in case the Code Health of a hotspot declines.
* Serve as a quality gate and provide feedback on user-defined hotspot goals (e.g. Supervise, Planned Refactoring).
* Prioritize code reviews based on the risk of the commits.
* Get early warnings on new and complex code, and detect the absence of expected change coupling to catch omissions.

**Note**: some of these checks can be accomplished locally using the [CodeScene CLI tool](../../cli/README.md).

![CodeScene's quality gate triggers in a GitHub check on code health decline.](../shared/integrations/pr-integration/codescene-quality-gates.png)
<br/>
![Example on the review recommendations: CodeScene notifies reviewers when critical code with potential security implications is modified.](../shared/integrations/pr-integration/code-review-critical-code-warning.png)
<br/>

This topic is split into two documents. This document is about the PR Integration itself, configuring CodeScene with the Git Providers and the result presentation.

For the actual **Delta Analysis** itself, its use cases and value proposition look at [PR Integration with CodeScene’s Delta Analysis](integrate-codescene-with-pull-requests.md).

## Enable the Pull Request Integration

Navigate to your project’s configuration in CodeScene, navigate to Pull Request Integration settings.

If you’re using GitHub the first step is to install the GitHub app for the integration.
CodeScene will inform you of this step, if needed:

![Install the GitHub integration for pull request integrations.](guides/pr-integration/config-install-the-app.png)
<br/>

With the app installed, all you need to do is to check a box and you are up and running with a single click:

![Enable the pull request integration with a single click.](guides/pr-integration/config-enable-pr-integration.png)
<br/>

If you are using Bitbucket you’ll need to install an Atlassian Connect App on the Workspaces of repositories
of the CodeScene project, there is a link on the configuration page to install it.

## Pull Request Analysis Results Presentation

> * [GitHub result presentation](github.md)
> * [Bitbucket result presentation](bitbucket.md)
> * [Azure result presentation](azure.md)
> * [GitLab result presentation](gitlab.md)

<a id="pr-suppressions"></a>

## Suppress Pull Request Findings

You can suppress individual findings in a PR check. The suppression affects the PR check and subsequent checks on the same pull request.

The option is available on the results page in CodeScene. You can get to this page from PR check via the results link.

![Add a suppression of a finding](../shared/integrations/pr-integration/suppression.png)

## Set Up an Automatic Analysis Schedule

To get the best results for the Pull Request Integration checks,
it’s a good idea to set up an automatic full analysis for your project.

You can do this in the Analysis schedule section of the project configuration.
See the [Getting Started](../../getting-started/README.md) section to learn more about this feature.

<a id="pr-stats"></a>

## Pull Requests: Statistics, Actions, and Impact

**Available in Analysis Results, System menu, PR Statistics**

No matter what baseline we start from, we never want our
code to become harder to read, understand, or maintain. CodeScene’s pull request integration lets you stay on top of your development so that you can prioritize and act upon any negative trends. For that
purpose, CodeScene visualizes the impact of pull requests over time:

![View the impact and developer action due to the pull request integration.](../shared/integrations/pr-integration/pr-statistics-and-impact.png)

The presented statistics are:

* *Checks performed*: This is the total number of pull request analyses run by CodeScene.
* *Findings Detected*: A finding is either a violated goal (e.g. a planned refactoring never happened), a reported code health decline, or new code with code health findings.
* *Findings Fixed*: A number of detected findings that are acted upon and mitigated.
* *Findings Ignored*: This is the number of detected findings that were merged as-is, without remediation, to the main branch. Ignored findings lead to a failed goal and/or a code health decline.
* *Findings Suppressed*: This is the number of findings that are suppressed

You can also inspect the details of individual pull requests if you need to drill down even further:

![CodeScene presents detailed statistics per pull request, allowing a deeper drill down.](../shared/integrations/pr-integration/pr-impact-by-pr.png)
<br/>

You can find the pull request statistics on your project’s analysis dashboard:

![The dashboard includes pull request statistics and a link to view more details.](../shared/integrations/pr-integration/pr-statistics-on-dashboard.png)

## Enable CodeScene’s Status Badges

Available in Project Configuration, Status Badges.

Status badges allow your teams to keep an eye on the health of their projects at a glance:

![Keep track of knowledge loss when developers leave the project, as well as average code health.](../shared/integrations/pr-integration/codescene-status-badges.png)

The status badges are intended for embedding in your GitHub README file.
Sample GitHub markup is provided on the “Status Badges” configuration tab.

## Constraints and Limitations

* Pull requests created from **forked repositories** are supported with a caveat:
  If the fork’s branch (from which the PR has been created) is not up to date with the corresponding
  upstream repository’s main branch then it’s possible that CodeScene fails to detect
  a code health decline (or an improvement) due to obsolete versions of changed files
  in the fork. This should only happen when the files modified by the PR has been changed, in the meantime,
  in the upstream repository .
  A recommended remedy is to **keep forks synchronized with upstream repositories**.
