# Supported Git Hosting Providers

You can use your GitHub, Bitbucket or Azure DevOps account to sign up with CodeScene and analyse your repositories.

### GitHub[¶](broken-reference)

CodeScene provides full integration with GitHub and all codescene.io functionality has been thoroughly tested using our own GitHub accounts.

#### Required access[¶](broken-reference)

CodeScene needs access to your organizations to facilitate creating an organizational account. It needs repository (code) access to analyse your code. **Unfortunately GitHub OAuth apps cannot request read-only access to repositories. CodeScene will never do any write operations, except for PR Integration creating and editing Check Runs in your Pull Requests.**

### Bitbucket[¶](broken-reference)

CodeScene provides integration with Bitbucket and all codescene.io functionality has been thoroughly tested. Pull Request Integration requires that our Atlassian Connect App is installed in participating workspaces.

Our Delta Analysis app - used to [Integrate CodeScene with Pull Requests](broken-reference) - has been published on [Atlassian’s Marketplace ](https://marketplace.atlassian.com/apps/1223491/codescene-delta-analysis?hosting=cloud\&tab=overview).

#### Required access[¶](broken-reference)



CodeScene needs read-only access to your code and the ability to post pull request comments.

### Azure[¶](broken-reference)

CodeScene provides full integration with Azure DevOps, including Project management analyses of Work Items. Pull Request Integration is done using Service Hooks, expect them in your projects if you’re using the feature.

#### Required access[¶](broken-reference)



These are the features that require a specific access:

* Creating organization accounts, finding user projects: _Project and team (read), Graph (read)_
* Analysis of code: _Code (read)_
* PR Integration comments: _PR threads_
* PR Integration Status Checks: _Code (status)_
* Project Management Analyses: _Work items (read)_

CodeScene will add PR comments and Status Checks to your pull requests and it will add Service Hooks to receive PR related events. Otherwise CodeScene won’t perform write operations.

Unfortunately it is not possible to register OAuth consumer with Azure DevOps that would have all _potential_ scopes and then request reduced scope of access based on your actual feature use. Azure OAuth server will throw an error if requested scopes and OAuth App’s scopes don’t match exactly.

#### Resolving login issues[¶](broken-reference)

In some cases, when Azure DevOps organization was connected or disconnected from another Active Directory, there is a bug where Azure cannot map user’s VSID to descriptor (and therefore organization member). To address this issue you need to create a fresh new Organization (or have someone else create it and invite you to it), then you need to enable _3rd party app access_ in Organization Settings:



Select Policies and enable Third-party application access via OAuth, then try to log in. You can delete the organization used for this workaround after users have successfully logged in.

### GitLab[¶](broken-reference)

CodeScene provides full integration with GitLab. Merge Request Integration is done using Webhooks Hooks, expect them in your projects if you’re using the feature.

#### Required access[¶](broken-reference)



The access requested by our OAuth App is extensive. The reason is that the only way to clone a private GitLab project with an OAuth token is when the token has _api_ access, which is read/write access to almost everything. As with GitHub, we never do any write operations except the Merge Request comments to post results of analysis.
