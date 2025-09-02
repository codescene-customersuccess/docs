# Azure result presentation

Results are presented as status check and a PR comment.

![Azure Status Check](../shared/integrations/pr-integration/azure-status-check.png)

You can make the check mandatory for merging into a specific branch:

* go to Azure’s Project Settings
* Repositories
* select a repository
* Policies tab
* select “master” or similar main branch in Branch Policies
* Status Checks, click + button to add one

On this same page you can also enable: Check for comment resolution.
Since CodeScene’s PR comments on failed checks are *Unresolved*, this setting forms a Quality Gate that
prevents PR merging, unless PR comment is manually marked as resolved. This gives a nice flexibility
where CodeScene’s failed PR check can be manually overridden.

Instead of posting one comment, CodeScene can add discussions to specific lines of files where code degradations and improvements occurred.

![Azure PR Thread in changed file](../shared/integrations/pr-integration/azure-pr-annotations.png)
