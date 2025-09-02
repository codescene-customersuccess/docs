# Organizational Accounts

CodeScene allows the owner of your organization to create a CodeScene account connected to your git provider’s “group account”: - GitHub Organization - Bitbucket workspace - Azure DevOps account - GitLab Group (only top level Groups are considered an organization)

You will pay for only one CodeScene subscription. Other users can join your CodeScene org for free.

In other words, any member of your provider organization can be invited by the account owner. Members don’t need to subscribe to paid CodeScene accounts to analyze private repositories owned by the organization. Organizational accounts let you share all analysis configurations and results with members of your organization.

See also [How do Organizational Accounts compare to Project Collaborators?](broken-reference).

### Create an Organizational Account[¶](broken-reference)

When you sign up in CodeScene you get an individual account. To connect an organization, you go to your account settings:

On your account, you’ll see a link that lets you create an organizational account:

Click on the link to _create a new organizational account_. CodeScene will present a dropdown with all GitHub organizations you own.

Select the organization you’re interested in, and press _Create Org Account_. Your account page will now show both your individual account as well as the freshly created organizational account:

You current account will be set to the new organizational account automatically. You can switch between your personal account and the organizational account using the preceding dialog.

### Invite Members to your Organization[¶](broken-reference)

#### Prerequisites[¶](broken-reference)

The users you want to add to your CodeScene account must be proper members of the git provider “group account” (GitHub organization, Bitbucket workspace, etc.).

* For example, GitHub _collaborators_ cannot be added as CodeScene org members - in that case, use the [collaborators feature](broken-reference).
* Tip: if you invited a new member to your git provider’s account but you still cannot see them in the list of available members then check whether they already _accepted_ your invitation.

Once you have an organizational account you can go the the Configuration section via the main menu to see the current members of your organization.

Then you can invite other CodeScene users to give them shared access to your CodeScene analyses. This screen also allows you to see who you have already invited and revoke that invitation by unchecking the checkbox next to their name.

Once the invited user clicks on the invite link provided in the second step of the invitation wizard and logs in they will be automatically granted access to the given organization and switched to its organizational account. They will also be informed that they can switch between accounts in the My Account menu.

Members can be invited as “admins” or plain “members”:

* _Members_ can view existing analyses results as well as run new analyses. They can’t update projects configurations.
* _Admins_ can create new projects, update projects configurations, delete existing projects and _invite other organization members_. Hence, any admin (not just the owner) can invite other members to keep the operational costs low by distributing the responsibilities to a group of people.

### How do Organizational Accounts compare to Project Collaborators?[¶](broken-reference)

CodeScene also supports a “Collaborators” feature, which is different from organizational accounts because it is a per project mechanism. That is, if you have an individual account, you can invite people to join on specific CodeScene projects. The collaborators feature is described in Project Access Management - Collaborators.
