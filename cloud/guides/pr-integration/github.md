<a id="github-presentation"></a>

# GitHub result presentation

CodeScene integrates with pull requests via GitHub’s checks API. If any Quality Gate is triggered, CodeScene will fail the check and
present the results on the Check Run details page:

![GitHub Check Run details](../shared/integrations/pr-integration/github-check-run-details.png)

## GitHub Review

CodeScene can additionally present the results as a GitHub review with comments on specific files. There
are some limitations to Reviews stemming from GitHub API limits on posting comments. If you find
that GitHub Reviews are failing for you, then you can opt for using Annotations, as described in the next section.

The Review will be visible on PR page:

![GitHub review on PR page](../shared/integrations/pr-integration/github-review.png)

The review comments will also be visible when reviewing the modified files:

![GitHub review comments in file view](../shared/integrations/pr-integration/github-review-code.png)

You can enable the review by checking an option in the Pull Request integration settings:

![Enable GitHub Review](../shared/integrations/pr-integration/config-enable-github-review.png)

## GitHub annotations

Alternatively CodeScene can also create annotations for all Code Health changes in a Pull Request.
The annotations will be visible on the Check Run details page:

![GitHub annotations in Check Run details](../shared/integrations/pr-integration/github-annotations.png)

The annotations will link directly to code being modified in the Pull Request, and will also be visible
when reviewing the modified files:

![GitHub annotations in file view](../shared/integrations/pr-integration/github-annotations-code.png)

Annotations will be produced for improvements as well as for degradations. If the Code Health score for the specific biomarker
is not degrading, the annotations will be created as notices rather than warnings.

You can enable the annotations by checking an option in the Pull Request integration settings:

![Enable GitHub annotations](../shared/integrations/pr-integration/config-enable-github-annotations.png)
