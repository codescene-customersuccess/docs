# Integrate CodeScene with Pull Requests

CodeScene offers an automated integration with GitHub, BitBucket, Azure DevOps or GitLab pull requests to incorporate the _Delta Analysis_ results into existing delivery workflows.

Integration is different per provider:

* Github via Checks with option of annotations
* Bitbucket via either Builds or Code Insights Reports
* Azure Status Check and Pull Request comment
* GitLab via Merge Request Discussion comment

See [GitHub](about:blank/github.html#github-presentation), [Bitbucket](about:blank/bitbucket.html#bitbucket-presentation), [Azure](about:blank/integrate-codescene-with-pull-requests.html#azure-presentation), [GitLab](about:blank/gitlab.html#gitlab-presentation) presentation.

### CodeScene and Pull Requests: Use Cases[¶](broken-reference)

The purposes of CodeScene’s pull request integration is to:

* Specify quality gates that trigger in case the Code Health of a hotspot declines.
* Serve as a quality gate and provide feedback on user-defined hotspot goals (e.g. Supervise, Planned Refactoring).
* Prioritize code reviews based on the risk of the commits.
* Get early warnings on new and complex code, and detect the absence of expected change coupling to catch omissions.

**Note**: some of these checks can be accomplished locally using the [CodeScene CLI tool](broken-reference).

This topic is split into two documents. This document is about the PR Integration itself, configuring CodeScene with the Git Providers and the result presentation.

For the actual **Delta Analysis** itself, its use cases and value proposition look at PR Integration with CodeScene’s Delta Analysis.

### Enable the Pull Request Integration[¶](broken-reference)

Navigate to your project’s configuration in CodeScene, navigate to Pull Request Integration settings.

If you’re using GitHub the first step is to install the GitHub app for the integration. CodeScene will inform you of this step, if needed:

With the app installed, all you need to do is to check a box and you are up and running with a single click:

If you are using Bitbucket you’ll need to install an Atlassian Connect App on the Workspaces of repositories of the CodeScene project, there is a link on the configuration page to install it.

### Pull Request Analysis Results Presentation[¶](broken-reference)

> * GitHub result presentation
> * Bitbucket result presentation
> * Azure result presentation
> * GitLab result presentation

### Suppress Pull Request Findings[¶](broken-reference)

You can suppress individual findings in a PR check. The suppression affects the PR check and subsequent checks on the same pull request.

The option is available on the results page in CodeScene. You can get to this page from PR check via the results link.

### Set Up an Automatic Analysis Schedule[¶](broken-reference)

To get the best results for the Pull Request Integration checks, it’s a good idea to set up an automatic full analysis for your project.

You can do this in the _Analysis schedule_ section of the project configuration. See the [Getting Started](broken-reference) section to learn more about this feature.

### Pull Requests: Statistics, Actions, and Impact[¶](broken-reference)

**Available in Analysis Results, System menu, PR Statistics**

No matter what baseline we start from, we never want our code to become harder to read, understand, or maintain. CodeScene’s pull request integration lets you stay on top of your development so that you can prioritize and act upon any negative trends. For that purpose, CodeScene visualizes the impact of pull requests over time:



The presented statistics are:

* _Checks performed_: This is the total number of pull request analyses run by CodeScene.
* _Findings Detected_: A finding is either a violated goal (e.g. a planned refactoring never happened), a reported code health decline, or new code with code health findings.
* _Findings Fixed_: A number of detected findings that are acted upon and mitigated.
* _Findings Ignored_: This is the number of detected findings that were merged as-is, without remediation, to the main branch. Ignored findings lead to a failed goal and/or a code health decline.
* _Findings Suppressed_: This is the number of findings that are suppressed

You can also inspect the details of individual pull requests if you need to drill down even further:

You can find the pull request statistics on your project’s analysis dashboard:



### Enable CodeScene’s Status Badges[¶](broken-reference)

Available in Project Configuration, Status Badges.

Status badges allow your teams to keep an eye on the health of their projects at a glance:

The status badges are intended for embedding in your GitHub _README_ file. Sample GitHub markup is provided on the “Status Badges” configuration tab.

### Constraints and Limitations[¶](broken-reference)

* Pull requests created from **forked repositories** are supported with a caveat: If the fork’s branch (from which the PR has been created) is not up to date with the corresponding upstream repository’s main branch then it’s possible that CodeScene fails to detect a code health decline (or an improvement) due to obsolete versions of changed files in the fork. This should only happen when the files modified by the PR has been changed, in the meantime, in the upstream repository . A recommended remedy is to **keep forks synchronized with upstream repositories**.
