# Organizational Accounts

CodeScene allows the owner of your organization to create a CodeScene account connected to your git provider’s “group account”:
- GitHub Organization
- Bitbucket workspace
- Azure DevOps account
- GitLab Group (only top level Groups are considered an organization)

You will pay for only one CodeScene subscription. Other users can join your CodeScene org for free.

In other words, any member of your provider organization can be invited by the account owner.
Members don’t need to subscribe to paid CodeScene accounts to analyze private repositories owned by the organization.
Organizational accounts let you share all analysis configurations and results with members of your organization.

See also [How do Organizational Accounts compare to Project Collaborators?](#collaborators).

<a id="create-an-organizational-account"></a>

## Create an Organizational Account

When you sign up in CodeScene you get an individual account. To connect an organization, you go to your account settings:

![Access your account](organizations/access-account.png)
<br/>

On your account, you’ll see a link that lets you create an organizational account:

![Create your organizational account](organizations/my-account.png)
<br/>

Click on the link to create a new organizational account.
CodeScene will present a dropdown with all GitHub organizations you own.

![Create a new organizational account.](organizations/new-org-account.png)

Select the organization you’re interested in, and press Create Org Account. Your account page will now show both your
individual account as well as the freshly created organizational account:

![Organizational account overview.](organizations/org-account-overview.png)

You current account will be set to the new organizational account automatically.
You can switch between your personal account and the organizational account using the preceding dialog.

<a id="invite-members-to-your-organization"></a>

## Invite Members to your Organization

### Prerequisites

The users you want to add to your CodeScene account must be proper members of the git provider “group account”
(GitHub organization, Bitbucket workspace, etc.).

- For example, GitHub *collaborators* cannot be added as CodeScene org members - in that case, use the [collaborators feature](#collaborators).
- Tip: if you invited a new member to your git provider’s account but you still cannot see them in the [list of available members](/configuration/org/members/add) then check whether they already *accepted* your invitation.

Once you have an organizational account you can go the the Configuration section via the main menu to
see the current members of your organization.

![See the members of your organization.](organizations/org-members.png)

Then you can invite other CodeScene users to give them shared access to your
CodeScene analyses. This screen also allows you to see who you have already invited and revoke that invitation by unchecking
the checkbox next to their name.

![Invite members to your organization.](organizations/org-members-add.png)
<br/>

Once the invited user clicks on the invite link provided in the second step of the invitation wizard
and logs in they will be automatically granted access to the given organization and switched to its
organizational account. They will also be informed that they can switch between accounts in the My Account menu.

![Invite link that should be shared with the invited people](organizations/org-members-invitelink.png)
<br/>

Members can be invited as “admins” or plain “members”:

- *Members* can view existing analyses results as well as run new analyses. They can’t update projects configurations.
- *Admins* can create new projects, update projects configurations, delete existing projects and *invite other organization members*. Hence, any admin (not just the owner) can invite other members to keep the operational costs low by distributing the responsibilities to a group of people.

  <a id="collaborators"></a>

## How do Organizational Accounts compare to Project Collaborators?

CodeScene also supports a “Collaborators” feature, which  is different from organizational accounts because it
is a per project mechanism. That is, if you have an individual account, you can invite people to join on specific CodeScene projects.
The collaborators feature is described in [Project Access Management - Collaborators](../guides/access-management/collaborators.md).
