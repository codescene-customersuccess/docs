# Integrate Costs and Issues into CodeScene

CodeScene provides an optional integration to Project Management tools like Jira. The integration has the following pre-requisites:

* Issue numbers are included/referenced in the commit messages or pull requests/branch names.
* You use labels and/or issue types to distinguish different kinds of work (e.g. Bugs, Features).

When present, CodeScene’s Project managment s integrations let you measure:

* Accumulated costs per hotspot and sub-system.
* Trends by work type, such as “Planned” versus “Unplanned” work.

> CodeScene’s cost analyses let you reason about the technical and organizational findings from a financial perspective.
> For example, how much time do you spend on defects in your top hotspots? What amount of work is unplanned? And what happens over time?

CodeScene supports multiple cost models depending on the data you have available such as cycle times, story points, or time spent.
CodeScene can deduce costs automatically based on your development history, so you don’t even need to have developers
reporting their time to be able to get a detailed view of your development costs. We cover all options and provide our recommended
setup in this guide. Let’s start by looking at the overall model.

## CodeScene’s Cost Model

CodeScene offers a breakdown of the development costs on three separate levels: file-, architecture-, and system-level.
The file level corresponds to the hotspots, the architecture level accumulates costs on a component/service/module level,
whereas the system level presents the cost trend as aggregated for all application code.

![CodeScene calculates cost trends on a file-, architecture-, and system-level.](integrations/costs-trend-example.png)

Using CodeScene’s cost model, you get the specific development costs on each hotspot. Use this data to inform re-work decisions and
to communicate the costs of technical debt to the business:

![CodeScene calculates cost per hotspot, including both feature and defect data.](integrations/jira-hotspot-costs.png)

## Filtering: view the code associated with issues

The System Maps include a filtering feature that enables visualization of modified areas in the codebase based on ticket data.
A “Filter by Issue ID” option is available at the System Maps page, which offers two filter tabs: “All Issues” and “Selected.”
Multiple tickets can be selected for filtering system maps (up to 50).

This feature empowers users to explore and analyze the relationship between tickets and codebase changes,
offering valuable insights for various use cases:

* Trace high-risk tickets like security issues all the way down to their code changes.
* Map regulatory requirements to their impacted code areas. Visualize and communicate that impact to non-technical stakeholders like auditors.

![Filter System Maps by Issue ID.](integrations/system-map-issue-filter.png)

## Calculating Development Costs: the four options

There are four strategies, and you need to select one of them depending on what data you have in your project management tool:

* *Estimated development time*: calculate a cycle time for the number of hours from the time an issue entered a specific state until the last commit is done on this issue.
  The cycle time is then adjusted for the number of hours in a typical work day. That is, a cycle time of 3 days has a cost of 3 \* 8 hours.
  In addition, CodeScene distributes the total costs proportional to the change impact when multiple modules/files are modified for the same issue.
  This cost model lets CodeScene calculate costs as opposed to rely on time reported in the project management tool, which is
  often incorrect, incomplete, or both.
* *Issues*: the number of issues associated with a given file or architectural component. Use *Issues* to get a summary and inspect general trends, but without assessing actual time spent.
* *Points*: the cost of an Issue in /Story points/. Use this option if you keep track of story points and use them to communicate within the organization.
* *Minutes*: the cost expressed in time. This method requires that time has been reported on the specified cost-field in the project managment tool. Use this option if you have
  accurate data on how much time you have spent on each issue.

## Export Cost Data to Excel/CSV

All cost trends in CodeScene provides a button that lets you export to a CSV file and explore further details in a
spreadsheet application.

**NOTE**: The exported data use the internal cost units. For issues and story points, this unit is always the unit of
presentation in the graphs. However, for time-based cost units like *Estimated development time* or *Minutes*, the exported cost is
in minutes. This typically differs from the values presented in the graphs since CodeScene converts them to more
suitable visual presentations (e.g. hours, days).

![Export CodeScene's cost data to CSV.](integrations/codescene-csv-export.png)

## Configuration

All configuration is done under the PM Data Integration tab in your CodeScene project:

![Select the data source you want to integrate with.](integrations/pm-data-start-config.png)

### Connect CodeScene to Jira

Jira is enabled and configured per project. Navigate to the “PM
Integration” tab in your project’s configuration and select “Jira”:

![Start by selecting "Jira"](integrations/jira-config-step1.png)

Fill in your Jira credentials here. We recommend using a Jira API
token as the password.

You also have to specify a cost model that determines how CodeScene calculates the costs. The cost model options are
described earlier in this document.

Once you press “Save and Continue”, you are presented with the detailed configuration options. See further below in
this document for a detailed walkthrough of the configuration options.

### Connect CodeScene to Trello

Trello is enabled and configured per project. Navigate to the “PM
Integration” tab in your project’s configuration and select “Trello”:

![Start by selecting "Trello"](integrations/trello-detailed-config.png)

You need an API Key and an API token from Trello. You generate those credentials via the [Trello app-key](https://trello.com/app-key).

You also have to specify a cost model that determines how CodeScene calculates the costs. The cost model options are
described earlier in this document.

Once you press “Save and Continue”, you are presented with the detailed configuration options, as specified below.

### Connect CodeScene to GitHub Issues

GitHub issues is only available if the account itself is a GitHub account.

GitHub Issues are enabled and configured per project.
Navigate to the “PM Integration” tab in your project’s configuration and select “GitHub Issues”.

Once you press “Save and Continue”, you are presented with the detailed configuration options, as specified in the next section.
Note that the GitHub Issues integration supports only the *Issues* cost model.

### Connect CodeScene to GitLab Issues

GitLab issues is only available if the account itself is a GitLab account.

GitLab Issues are enabled and configured per project.
Navigate to the “PM Integration” tab in your project’s configuration and select “GitLab Issues”.

Once you press “Save and Continue”, you are presented with the detailed configuration options, as specified in the next section.

### Connect CodeScene to Azure DevOps

Azure DevOps is enabled and configured per project. Navigate to the “PM
Integration” tab in your project’s configuration and select “Azure DevOps”:

![Start by selecting "Azure DevOps"](integrations/azure-config-step1.png)

Integration uses Work Items in the project’s Azure account.

You only need to specify a cost model that determines how CodeScene calculates the costs and mapping options.
The cost model options are described earlier in this document.

Once you press “Save and Continue”, you are presented with the detailed configuration options, as specified below.

### Connect CodeScene to YouTrack

YouTrack is enabled and configured per project. Navigate to the “PM
Integration” tab in your project’s configuration and select “YouTrack”.

You need an permanent token from YouTrack. See [Creating a permanent token](https://www.jetbrains.com/help/youtrack/server/Manage-Permanent-Token.html#obtain-permanent-token).

Once you press “Save and Continue”, you are presented with the detailed configuration options, as specified in the next section.

### Specify the Detailed Configuration Options

![Configure the information you want to retrieve from Jira.](integrations/jira-detailed-config.png)

**External Projects**: Select one or more Jira projects that CodeScene will use as data sources.

**Cost Field**: is used for he cost models *Points* and *Minutes*, Select the Jira field that has
your cost estimates. If you use *Issues* or *Estimated development time* as cost model, then
it is not necessary to configure *Cost Field* and you can leave it as is.

**Work In Progress Transition Name**: Specify the name of the Jira status that indicates that the development work has started.
Often, this is the “In Progress” or “In Development” state.

The *Work In Progress Transition Name* is relevant for two analyses:
1. If you use *Estimated development time* as cost model, then this field is mandatory.
2. Delivery Performance: if you have enabled the delivery performance module, then this config option
is needed to calculate lead times.

**Supported Work Types** should correspond to the different kinds of
issue labels defined in your Jira project.

**Defect Work Types**: specify the JIRA labels or JIRA
Issue Types that will be regarded as defects. This configuration is used to
calculate defect densities and work type trends.

The *Rename Work Types* field allows the work types to be mapped to
different analytical categories that you can define yourself. How you
do this depends on the type of analysis you wish to  perform.

## Tip: Rename Work Types to distinguish Planned and Unplanned work

When looking at cost trends, the most interesting distinction is
typically between Planned- versus Unplanned Work.

By specifying *Rename Work Types* option, the Jira labels are translated to the specified label before being
sent to CodeScene. For example, if your Jira project contains
Feature and Documentation labels, like in the illustration above,
these can be categorized together as Planned Work, while Bug and
Defect are treated as Unplanned Work; the Refactoring label –
which doesn’t have a translation – will be sent as is. Mapping labels
this way can allow you to see more meaningful trends. You are free to
map labels however you like depending on your analytical needs.

## Advanced Information

### Measures to reduce bias in the trends

Let’s face it: Project management data can be noisy. CodeScene reduces as much of this noise as possible via its data cleaning:

* **Cycle time in development**: improve the precision by identifying issues that have a transition to “In progress” \_after_ the
  last commit related to that issue. CodeScene then fall back on using the date of the first commit as starting point to recover part of the cycle time.
* **Issues that lack a cycle time**: even with the previously mentioned fallback mechanisms, some issues might be implemented with just a single commit.
  Hence, there’s no way of measuring the actual time in development. To avoid losing valuable data, CodeScene applies a default cycle time of one
  working day (8 hours).
