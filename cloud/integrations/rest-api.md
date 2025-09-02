# Public API

We are expanding the API with every release to make more analysis information available.
Contact Codescene, and we are happy to share our detailed plans and get your feedback.

You can get the following information from the API:

* [Projects list](#projects-list)
* [New Project](#new-project)
* [Analysis List of a project](#analysis-list-of-a-project)
* [Single analysis details](#single-analysis-details)
* [Files list from an analysis](#files-list-from-an-analysis)
* [Components list from an analysis](#components-list-from-an-analysis)
* [Single components details from an analysis](#single-components-details-from-an-analysis)
* [Component file list from an analysis](#component-file-list-from-an-analysis)
* [Delta Analyses List of a project](#delta-analysis-list-of-a-project)
* [Single delta analysis details](#single-delta-analysis-details)
* [Commit activity trend from an analysis](#commit-activity-trend-from-an-analysis)
* [Author statistics from an analysis](#author-statistics-from-an-analysis)
* [Branch statistics from an analysis](#branch-statistics-from-an-analysis)
* [Developer Settings list](#developer-settings-list)
* [Teams list](#teams-list)
* [Create team](#create-team)
* [Update team](#update-team)
* [Delete team](#delete-team)
* [Developer list](#developer-list)
* [Update developer](#update-developer)
* [Delete developer](#delete-developer)
* [Remove Developer from Team](#remove-developer-from-team)
* [Get Project Badge Status](#get-project-badge-status)
* [Update Project Badge Status](#update-project-badge-status)
* [KPI trends endpoints](#kpi-trends-endpoints)

## Using CodeScene’s REST API

### The REST API documentation URL

You can browse the REST API functions here [CodeScene RestAPI Functions](https://api.codescene.io/v2/docs). Before trying any functionality, use the Authorize button then fill in the value with ‘Bearer <your_token>’ to authenticate.
<br/>
The version in use is **v2**.
<br/>

### The REST API token

CodeScene lets you create a token intended to consume the API. Login then create a new token as illustrated in [Fig. 182](#apitokenlist) and [Fig. 183](#apitokenadd).
<br/>
![List Api tokens](integrations/ApiTokenList.png)![Add Api token](integrations/ApiTokenAdd.png)![Api token](integrations/ApiTokenCreated.png)
To consume the REST API, you need to authenticate by adding the http header `'Authorization: Bearer <your token>'`.
<br/>

### Filter queries

The API endpoints that returns file lists support an optional filter parameter. This makes it possible
to specify queries for returning objects in a flexible manner.

#### Query structure and terminology

A query clause consists of a field followed by an operator followed by a value, optionally quoted:

| clause   | `owner:"Igor Lavrov"`   |
|----------|-------------------------|
| field    | `email`                 |
| operator | `:`                     |
| value    | `Igor Lavrov`           |

You can combine multiple query clauses in a search by separating them with a space.
When multiple query clauses are specified, the API combines them with AND logic.
Quotation marks around values are optional, but must be used for values containing spaces.

#### Query Clause Syntax

The following table lists the operators that you can use to construct a query clause.

| OPERATOR      | USAGE         | DESCRIPTION                                                          |
|---------------|---------------|----------------------------------------------------------------------|
| `:`           | `field:value` | Exact match operator (case insensitive)                              |
| `~`           | `field~value` | Substring match operator (case insensitive)                          |
| `>`, `<`, `=` | `field<value` | Greater than/less than/equals operators. Supported only for numbers. |

Any field present on the returned items can be used in a clause. Nested fields are specified using dot notation, as in code_health.current_score.
For fields that are lists, the clause will be true if it is fulfilled by any item in the list.

### Project endpoints

<a id="projects-list"></a>

#### Projects list

```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects'
```

<a id="new-project"></a>

#### New Project

```bash
 curl -X POST --header 'Content-Type: application/json' --header 'Authorization: Bearer <token>' \
 --data "@./project.json" 'https://api.codescene.io/v2/projects/new'
```

- Replace `./project.json` with a valid a path to your project configuration.
- Example of `./project.json`

```json
{
   "config": {
   "name" : "test",
   "repo-paths" : ["https://yourprovider.com/mycompany/myproject.git"],
   "developer-configuration" : 99
   }
}
```

- `name` is optional, if missing CodeScene will use the project name from the first repository
- the repo paths must contain only urls accessible by the user which created the token
- `developer-configuration` is optional, replace `99` with a valid id taken from the developer settings list results.

<a id="analysis-list-of-a-project"></a>

#### Analysis List of a project

```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects/{project-id}/analyses'
```

- Replace `{project-id}` with a valid id taken from the project list results.

<a id="single-analysis-details"></a>

#### Single analysis details

Single analysis details using its id
<br/>
```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects/{project-id}/analyses/{analysis-id}'
```

- Replace `{project-id}` with a valid id taken from the project list results.
- Replace `{analysis-id}` with a valid id taken from the analysis list results.

Latest analysis details
<br/>
```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects/{project-id}/analyses/latest'
```

- Replace `{project-id}` with a valid id taken from the project list results.

<a id="files-list-from-an-analysis"></a>

#### Files list from an analysis

File list in descending order based on order_by value for given analysis id
<br/>
```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects/{project-id}/analyses/{analysis-id}/files?page={page}&page_size={page_size}&order_by={order_by}'
```

- Replace `{project-id}` with a valid id taken from the project list results.
- Replace `{analysis-id}` with a valid id taken from the analysis list results.
- Replace `{page}` with required page to return. If page parameter is omitted the default value is 1.
- Replace `{page_size}` with the number of files to return for a page. If page_size parameter is omitted the default value is 100.
- Replace `{order_by}` with one of the following values: “lines_of_code”, “change_frequency”, “number_of_defects”, “code_health” or “cost”. If order_by parameter is omitted the default value is “change_frequency”.

Files list in descending order based on order_by value for latest analysis
<br/>
```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects/{project-id}/analyses/latest/files?page={page}&page_size={page_size}&order_by={order_by}'
```

- Replace `{project-id}` with a valid id taken from the project list results.
- Replace `{page}` with required page to return. If page parameter is omitted the default value is 1.
- Replace `{page_size}` with the number of files to return for a page. If page_size parameter is omitted the default value is 100.
- Replace `{order_by}` with one of the following values: “lines_of_code”, “change_frequency”, “number_of_defects”, “code_health” or “cost”. If order_by parameter is omitted the default value is “change_frequency”.

<a id="components-list-from-an-analysis"></a>

#### Components list from an analysis

Components list using analysis id
<br/>
```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects/{project-id}/analyses/{analysis-id}/components'
```

- Replace `{project-id}` with a valid id taken from the project list results.
- Replace `{analysis-id}` with a valid id taken from the analysis list results.

Latest analysis components list
<br/>
```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects/{project-id}/analyses/latest/components'
```

- Replace `{project-id}` with a valid id taken from the project list results.

<a id="single-components-details-from-an-analysis"></a>

#### Single components details from an analysis

Component details using analysis id
<br/>
```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects/{project-id}/analyses/{analysis-id}/components/{component-name}'
```

- Replace `{project-id}` with a valid id taken from the project list results.
- Replace `{analysis-id}` with a valid id taken from the analysis list results.
- Replace `{component-name}` with a valid name taken from the components list results.

Latest analysis component detail
<br/>
```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects/{project-id}/analyses/latest/components/{component-name}'
```

- Replace `{project-id}` with a valid id taken from the project list results.
- Replace `{component-name}` with a valid name taken from the components list results.

<a id="component-file-list-from-an-analysis"></a>

#### Component file list from an analysis

Component file list in descending order based on order_by value for given analysis id
<br/>
```bash
curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
'https://api.codescene.io/v2/projects/{project-id}/analyses/{analysis-id}/components/{component-name}/files?page={page}&page_size={page_size}&order_by={order_by}'
```

- Replace `{project-id}` with a valid id taken from the project list results.
- Replace `{analysis-id}` with a valid id taken from the analysis list results.
- Replace `{component-name}` with a valid id taken from the component list results.
- Replace `{page}` with required page to return. If page parameter is omitted the default value is 1.
- Replace `{page_size}` with the number of files to return for a page. If page_size parameter is omitted the default value is 100.
- Replace `{order_by}` with one of the following values: “lines_of_code”, “change_frequency”, “number_of_defects”, “code_health” or “cost”. If order_by parameter is omitted the default value is “change_frequency”.

Component files list in descending order based on order_by value for latest analysis
<br/>
```bash
curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
'https://api.codescene.io/v2/projects/{project-id}/analyses/latest/components/{component-name}/files?page={page}&page_size={page_size}&order_by={order_by}'
```

- Replace `{project-id}` with a valid id taken from the project list results.
- Replace `{component-name}` with a valid id taken from the component list results.
- Replace `{page}` with required page to return. If page parameter is omitted the default value is 1.
- Replace `{page_size}` with the number of files to return for a page. If page_size parameter is omitted the default value is 100.
- Replace `{order_by}` with one of the following values: “lines_of_code”, “change_frequency”, “number_of_defects”, “code_health” or “cost”. If order_by parameter is omitted the default value is “change_frequency”.

<a id="delta-analysis-list-of-a-project"></a>

#### Delta Analyses List of a project

```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects/{project-id}/delta-analyses'
```

- Replace `{project-id}` with a valid id taken from the project list results.

<a id="single-delta-analysis-details"></a>

#### Single delta analysis details

Single delta analysis details using its id
<br/>
```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects/{project-id}/delta-analyses/{delta-analysis-id}'
```

- Replace `{project-id}` with a valid id taken from the project list results.
- Replace `{delta-analysis-id}` with a valid id taken from the delta analysis list results.

<a id="commit-activity-trend-from-an-analysis"></a>

#### Commit activity trend from an analysis

Commit activity trend for given analysis id
<br/>
```bash
curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
'https://api.codescene.io/v2/projects/{project-id}/analyses/{analysis-id}/commit-activity'
```

- Replace `{project-id}` with a valid id taken from the project list results.
- Replace `{analysis-id}` with a valid id taken from the analysis list results.

Commit activity trend for latest analysis
<br/>
```bash
curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
'https://api.codescene.io/v2/projects/{project-id}/analyses/latest/commit-activity'
```

- Replace `{project-id}` with a valid id taken from the project list results.

<a id="author-statistics-from-an-analysis"></a>

#### Author statistics from an analysis

Author statistics for given analysis id
<br/>
```bash
curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
'https://api.codescene.io/v2/projects/{project-id}/analyses/{analysis-id}/author-statistics'
```

- Replace `{project-id}` with a valid id taken from the project list results.
- Replace `{analysis-id}` with a valid id taken from the analysis list results.

Author statistics for latest analysis
<br/>
```bash
curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
'https://api.codescene.io/v2/projects/{project-id}/analyses/latest/author-statistics'
```

- Replace `{project-id}` with a valid id taken from the project list results.

<a id="branch-statistics-from-an-analysis"></a>

#### Branch statistics from an analysis

Branch statistics for given analysis id
<br/>
```bash
curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
'https://api.codescene.io/v2/projects/{project-id}/analyses/{analysis-id}/branch-statistics'
```

- Replace `{project-id}` with a valid id taken from the project list results.
- Replace `{analysis-id}` with a valid id taken from the analysis list results.

Branch statistics for latest analysis
<br/>
```bash
curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
'https://api.codescene.io/v2/projects/{project-id}/analyses/latest/branch-statistics'
```

- Replace `{project-id}` with a valid id taken from the project list results.

<a id="get-project-badge-status"></a>

#### Get Project Badge Status

CodeScene support the following badges: code-health, missed-goals, system-mastery

```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects/{project_id}/badges'
```

- Replace `{project_id}` with a valid id taken from the project list results.

<a id="update-project-badge-status"></a>

#### Update Project Badge Status

```bash
 curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' \
 --header 'Authorization: Bearer <token>' -d '{"code-health":true, "missed-goals": true ,"system-mastery": false}' \
 'https://api.codescene.io/v2/projects/{project_id}/badges'
```

- Replace `{project_id}` with a valid id taken from the project list results.

<a id="run-analysis"></a>

#### Run Analysis

```bash
 curl -X POST --header 'Content-Type: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/projects//{project_id}/run-analysis'
```

- Replace `{project_id}` with a valid id taken from the project list results.
- Note that it is **strongly recommended** that analysis scheduling be turned off if this endpoint is used as a continuous trigger of analysis.

### Teams and Developers endpoints

<a id="developer-settings-list"></a>

#### Developer Settings list

```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/developer-settings'
```

<a id="teams-list"></a>

#### Teams list

```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/developer-settings/{developer_setting_id}/teams'
```

- Replace `{developer_setting_id}` with a valid id taken from the developer settings list results.

<a id="create-team"></a>

#### Create team

```bash
 curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' \
 --header 'Authorization: Bearer <token>' -d '{ "team_name": "my-new-team"}' \
 'https://api.codescene.io/v2/developer-settings/{developer_setting_id}/teams/new'
```

- Replace `{developer_setting_id}` with a valid id taken from the developer settings list results.

<a id="update-team"></a>

#### Update team

```bash
 curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' \
 --header 'Authorization: Bearer <token>' -d '{ "team_name": "my-updated-team"}' \
 'https://api.codescene.io/v2/developer-settings/{developer_setting_id}/teams/{team_id}'
```

- Replace `{developer_setting_id}` with a valid id taken from the developer settings list results.
- Replace `{team_id}` with a valid id taken from the teams list results.

<a id="delete-team"></a>

#### Delete team

```bash
 curl -X DELETE --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/developer-settings/{developer_setting_id}/teams/{team_id}'
```

- Replace `{developer_setting_id}` with a valid id taken from the developer settings list results.
- Replace `{team_id}` with a valid id taken from the teams list results.

<a id="developer-list"></a>

#### Developer list

```bash
 curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/developer-settings/{developer_setting_id}/developers'
```

- Replace `{developer_setting_id}` with a valid id taken from the developer settings list results.

<a id="update-developer"></a>

#### Update developer

```bash
 curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' \
 --header 'Authorization: Bearer <token>' -d '{ "team_id": 12, "former_contributor": true, "exclude_from_all_analyses": true}' \
 'https://api.codescene.io/v2/developer-settings/{developer_setting_id}/developers/{developer_id}'
```

- Replace `{developer_setting_id}` with a valid id taken from the developer settings list results.
- Replace `{developer_id}` with a valid id taken from the developers list results.
- Set the team_id to a valid id taken from teams list if you need to assign the current developer to that team.
- The only updateable attributes of a developer are the team_id, former_contributor and exclude_from_all_analyses
- The payload can contain any of the attributes or only some of them.

<a id="delete-developer"></a>

#### Delete developer

```bash
 curl -X DELETE --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/developer-settings/{developer_setting_id}/developers/{developer_id}'
```

- Replace `{developer_setting_id}` with a valid id taken from the developer settings list results.
- Replace `{developer_id}` with a valid id taken from the developers list results.

<a id="remove-developer-from-team"></a>

#### Remove Developer from Team

```bash
 curl -X DELETE --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/developer-settings/{developer_setting_id}/developers/{developer_id}/team'
```

- Replace `{developer_setting_id}` with a valid id taken from the developer settings list results.
- Replace `{developer_id}` with a valid id taken from the developers list results.

<!-- the "Remove Developer Settings" must be last in the file, for on-prem we have some extra text which must follow after this -->

<a id="remove-developer-settings"></a>

#### Remove Developer Settings

```bash
 curl -X DELETE --header 'Accept: application/json' --header 'Authorization: Bearer <token>' \
 'https://api.codescene.io/v2/developer-settings/{developer_setting_id}'
```

- Replace `{developer_setting_id}` with a valid id taken from the developer settings list results.

<a id="kpi-trends-endpoints"></a>

### KPI trends endpoints

The KPI trends endpoints lets you get the data behind the graphs and metrics found on CodeScenes 4-factors dashboards,
as described in [From Code to Delivery: the 4 factors model](../4f-dashboard/4-factors-dashboard.md).

A full and current documentation of the endpoints can be found at the REST API documentation URL,
see above for usage and authorization.

<a id="code-coverage-endpoints"></a>

### Code Coverage endpoints

The Code Coverage endpoints lets you upload code coverage data for use during analysis.

<a id="upload-code-coverage-data"></a>

#### Upload Data

The code coverage data upload uses two endpoints, one for requesting an upload and specifying some metadata necessary for analysis and one for doing the actual upload.

- Given that you have code coverage data on disc, first request an upload:

```bash
 curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' \
 --header 'Authorization: Bearer <token>' -d "{\"commit-sha\": \"$(git rev-parse HEAD)\", \"repo-url\": \"$(git config --get remote.origin.url)\", \"repo-path\": \"$(pwd)\", \"format\": \"open-clover\", \"metric\": \"statement-coverage\"}"
 'https://api.codescene.io/v2/code-coverage/upload'

 => {"ok":"upload request accepted","ref":"/api/v2/code-coverage/upload/65","id":65}
```

- And then use the returned ref in a subsequent call to do the actual upload of the data (compressed in gz format)

```bash
 curl -X PUT --header "Content-Type: text/plain" --header 'Accept: application/json' \
 --header 'Authorization: Bearer <token>' --data-binary @coverage/clover.xml.gz
 'https://api.codescene.io/v2/code-coverage/upload/{id}'

 => {"ok":"Successfully parsed open-clover data for 829 files."}
```

<a id="delete-code-coverage-data"></a>

#### Delete Data

All code coverage data for a specific repository can be deleted like this:

```bash
 curl -X DELETE --header 'Content-Type: application/json' --header 'Accept: application/json' \
 --header 'Authorization: Bearer <token>' -d "{\"repo-url\": \"$(git config --get remote.origin.url)\"}"
 'https://api.codescene.io/v2/code-coverage'

 => {"ok":"Deleted 2 coverage data entries."}
```
