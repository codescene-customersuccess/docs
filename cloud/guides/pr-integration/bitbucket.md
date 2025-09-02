<a id="bitbucket-presentation"></a>

# Bitbucket result presentation

Analysis results will be presented in a Pull Request comment. You can also choose to add Code Insights Report and/or
: a Build status, all options being enabled by default.
  <br/>
  In Bitbucket Build Status can be made a requirement for merging the Pull Request, acting as a Quality
  Gate. Alternatively you can get a Code Insights Report, which will not prevent merges if you have configured successful builds
  to be a requirement.

![Bitbucket PR comment](../shared/integrations/pr-integration/bitbucket-pr-comment.png)![Bitbucket PR report](../shared/integrations/pr-integration/bitbucket-pr-report.png)

If Code Insights Report is enabled, CodeScene can add annotations to specific lines of files where code degradations and improvements occurred.

![Bitbucket PR report file annotations](../shared/integrations/pr-integration/bitbucket-pr-report-annotations.png)![Bitbucket PR report](../shared/integrations/pr-integration/bitbucket-pr-build.png)
