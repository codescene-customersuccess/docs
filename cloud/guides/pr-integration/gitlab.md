<a id="gitlab-presentation"></a>

# GitLab result presentation

Results are presented as Discussion comment in the Merge Request:

![GitLab MR Comment](../shared/integrations/pr-integration/gitlab-pr-comment.png)

If PR check is successful then the comment is resolved, otherwise it’s unresolved. Status is shown
with a green checkmark (red arrow points to it).

This is useful if you set the restriction to prevent merge if there are unresolved comments.

Instead of posting one comment, CodeScene can add discussions to specific lines of files where code degradations and improvements occurred.

![GitLab MR Discussion in changed file](../shared/integrations/pr-integration/gitlab-pr-annotations.png)
