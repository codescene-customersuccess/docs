# Getting Started

Welcome to CodeScene - we’re happy to have you here! This guide will help you get started. Before we go there,
let’s have a look at what CodeScene does for you.

## The history of your code predicts its future

CodeScene is a tool that your software project improve their efficiency by identifying and prioritizing technical debt.
We take a different approach to software analysis since we base the results on behavioral and social data.

Our main data source is version-control repositories, which CodeScene views as a behavioral log of how the developers interact with the codebase.
This means we can prioritize based on how the system grows and also include a social dimension of code that lets our customers discover team productivity bottlenecks and save on- and off-boarding costs.

## Log in with GitHub, Bitbucket, Azure DevOps or GitLab

To analyze your code you need to connect CodeScene with your source code hosted on [GitHub](../providers/README.md#github), [Bitbucket](../providers/README.md#bitbucket), [Azure](../providers/README.md#azure), or [GitLab](../providers/README.md#gitlab).

If you don’t have a GitHub, Bitbucket, Azure DevOps or GitLab account we recommend that you check-out our [on-premises version of CodeScene](https://codescene.com/pricing/).

### Log in with [GitHub](../providers/README.md#github)

When you click on the Login button on CodeScene’s front page you’ll be redirected to GitHub for authentication and authorization. Type your GitHub credentials
as shown in [Fig. 1](#sign-into-github).

![Sign into GitHub](getting-started/sign-into-github.png)

Because of how the GitHub API works, CodeScene is forced to request read and write access.
We do, however, never write any data to your Git repositories, and we never will.

### Log in with [Bitbucket](../providers/README.md#bitbucket)

Click Log in with Bitbucket on the front page.
You’ll be redirected to the Bitbucket’s consent page:

![Bitbucket's consent page](getting-started/bitbucket-consent-page.png)

### Log in with [Azure](../providers/README.md#azure)

Click Log in with Azure on the front page.
You’ll be redirected to the Azure’s consent page:

![Azure's consent page](getting-started/azure-consent-page.png)

### Log in with [GitLab](../providers/README.md#gitlab)

Click Log in with GitLab on the front page.
You’ll be redirected to the GitLab’s consent page:

![GitLab's consent page](getting-started/gitlab-consent-page.png)

## How do Organizational Accounts compare to Individual Accounts?

CodeScene supports both Individual and Organizational Accounts. An Individual Account is for personal use, while an Organizational Account is built for teams and businesses to manage and collaborate on their code across multiple projects.

### Organizational Account [recommended option]

Organizational Account is geared toward teams, development organizations, or companies that need to collaborate and manage multiple users and projects at once.

It is intended for multiple users (this account is designed for larger teams or entire organizations, with roles and permissions for different users).

Perfect for companies or teams working on large projects who need detailed analytics and reporting for code health across various departments or teams. Based on these considerations, CodeScene advises moving forward with this option.

#### Setting Up Your CodeScene Organization

CodeScene allows the owner of your organization to create a CodeScene account connected to your git provider’s “group account”:

* GitHub Organization
* Bitbucket workspace
* Azure DevOps Organization
* GitLab Group (only top level Groups are considered an organization)

![Setting up CodeScene Organization](getting-started/setting-up-cs-org.png)

You will pay for only one CodeScene subscription. Other users can join your CodeScene org for free.
In other words, any member of your provider organization can be invited by the account owner. Members don’t need to subscribe to paid CodeScene accounts to analyze private repositories owned by the organization. Organizational accounts let you share all analysis configurations and results with members of your organization.

Instruction on how to invite organization members can be found [here](../organizations/README.md#invite-members-to-your-organization).

### Individual Account

Individual Account is good option for a single user (the individual who created the account). It is limited to personal use, without access to team-level collaboration or organizational tools.

This type of an account is ideal for freelancers, independent developers, or hobbyists who want to improve their code quality and understand code complexity on a personal level.

#### Limitations to the usage of Individual Account

The Individual Account has several limitations that should be considered:

* It does not allow for the invitation of additional members to collaborate on projects.
* Any projects or configurations created under an Individual Account cannot be transferred to an Organization account. This means that if you decide to upgrade to an Organization plan in the future, you would need to recreate or manually migrate any work done under the Individual plan.

These restrictions may impact the scalability and flexibility of your work as your team or project grows.

Note: When you create an Organizational Account on CodeScene, you’re also given an Individual Account because CodeScene’s platform is designed to associate individual users with organizations in order to manage access, permissions, and activity at both levels.

#### Creating an Organizational Account when an Individual Account is already created

If you have already created an Individual Account and wish to set up an Organizational Account, please refer to the instructions provided [here](../organizations/README.md#create-an-organizational-account).

## Additional scopes required

Users give CodeScene access to their provider’s (GitHub, etc..) identifying information such as username and email.
For some users this is sufficient, because they only view analysis results.

If you want to create projects, run analysis, configure projects, and run Pull Request integration, we require more
access, such as access to your repositories and pull requests.

See providers pages for explanation of why we require the particular level of access: [GitHub](../providers/README.md#github), [Bitbucket](../providers/README.md#bitbucket), [Azure](../providers/README.md#azure), [GitLab](../providers/README.md#gitlab).

## Run your first analysis

After you log in, you’re ready to analyze your project.

Click *Create New Project* to configure an analysis project.
You will be prompted to grant additional access to your provider. CodeScene fetches a list of all your repositories from GitHub (or other provider) and lets you specify
the projects to analyse as shown in [Fig. 3](#create-project).

![Create an analysis project](getting-started/create-project.png)

CodeScene’s free plan lets you analyse open source projects. The [paid plans](https://codescene.io/plans) also
let you analyse private repositories as well as repositories that belong to an organization you’re a member of.

CodeScene also supports projects where the code is split across multiple repositories. In that case you just selects all those
repositories and CodeScene will take care of the rest.

If you’re using Azure provider all the repositories selected must be from the same account.

Once you’ve selected the repository to analyse, CodeScene prompts you with the initial configuration as shown in [Fig. 4](#exclusions).

![Configure your analysis project](getting-started/exclusions.png)

That’s it! No further setup is necessary. Just press the button in CodeScene to launch your first analysis. The analysis may take some time to
complete so we recommend that you use that time to check-out our [Focus Areas](../guides/README.md). They’ll make sure you get the most out of your analysis.

## Set an automatic analysis schedule

If you’re on CodeScene’s paid plan you can enable automatic analysis runs on your project.

Open the project configuration page and go to *Analysis Schedule* tab shown in [Fig. 5](#analysis-schedule).

![Add schedule for automatic analysis](getting-started/analysis-schedule.png)

You can choose an interval and click *Save*. An analysis will be run once every interval.
The specific time within that interval will be shown to you.

It is recommended that you enable scheduled analyses for projects in active development.

A scheduled analysis will be skipped if you’ve recently manually triggered an analysis run.

## What’s an Active Author?

CodeScene’s subscription model uses the number of active contributors as one the main criteria.
An active author is anyone who has committed code over the past three months to the codebase you want to analyse.
This time period is a sliding window that always starts at the date of the most recent commit in your repositories.
CodeScene applies the following additional rules:

* *Each author is only counted once*. That is, if you analyze multiple codebases, the same persons only count once no matter
  how many projects they contribute to.
* *Historic contributors are free*. People who haven’t committed code within the last three months are included for free and
  don’t add to the license fee.

You can get a rough estimate on the number of active authors (the past 3 months) in a Git repository through the following command:

```default
git shortlog -sne --all --since "3 months ago"
```

To get all the authors after specific date:

```default
git shortlog -sne --all --after=2022-07-01
```
