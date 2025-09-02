# Project Access Management - Collaborators

## Adding/Removing Collaborators

To manage collaborators for a project, go to project configuration and click on Access Management.

![Add collaborators in project Access Management configuration](guides/access-management/project-config_access-management_collaborators.png)

Clicking `Add Collaborator` will bring up a page where you enter the collaborator’s **email address** (used by their CodeScene.io account),
and choose the appropriate privilege level:

![Add a collaborator by providing his email address and access level.](guides/access-management/project-config_access-management_add-collaborator.png)

A “Readonly” collaborator can run analyses and X-Rays, but cannot modify the project configuration.
A “Configuration” collaborator can run analyses and X-Rays,
and also make changes to most project configuration items, with the exception of Git repositories.

The email address associated with the collaborator’s CodeScene account is needed to add a user as a collaborator.
This is available in the top bar, and also under My Account.

![Find CodeScene account email address in My Account.](guides/access-management/account-email.png)

After adding a collaborator, they can be removed by the project owner or collaborators with the `Admin` role.
The user can also always remove themself:

![Remove a collaborator by clicking ``Remove`` button](guides/access-management/project-config_access-management_remove-collaborator.png)

After a user is added as a collaborator to a project,
the project will appear on the collaborator’s projects dashboard.

## Collaborator Permission Roles

This collaborator has `Readonly` privileges, so they can run an  analysis,
but the project configuration cannot be changed:

![A Readonly collaborator can only view project config but they cannot change it.](guides/access-management/project-config_readonly-collaborator-view.png)

However, a collaborator with the **\`\`Admin\`\` role can update any part of the project’s configuration
except the list of repositories**.

Furthermore, unlike organization’s admins, **collaborator with an admin role cannot delete a project**.
Only the individual account owner can do that.

## Free-Plan Collaborators

Collaborators on a free plan can be added to a private project owned by a paid CodeScene account.
Project analysis is always run using the project owner’s OAuth token.
