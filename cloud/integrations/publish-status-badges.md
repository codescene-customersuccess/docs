# Keep Tabs on the State of your Code with Badges

Status badges allow your teams to keep an eye on the health of their
projects and their individual architectural components at a glance.
They can be integrated into any tool, but are most frequently embedded on GitHub’s README pages.

CodeScene auto-generates the badges and the links for you.

## Types of Badges

CodeScene currently supports badges for the following metrics:

### Average Code Health

The Average Code Health status badge:

![The Code Health status badge](integrations/average-code-health-example.png)

### Hotspot Code Health

The Hotspot Code Health status badge:

![The Code Health status badge](integrations/hotspot-code-health-example.png)

### System Mastery

The System Mastery status badge:

![The System Mastery status badge](integrations/system-mastery-example.png)

### Missed Goals

The Missed Goals status badge:

![The Missed Goals status badge](integrations/missed-goals-example.png)

## Configuration

Status badges can be activated on a per-project and per-metric basis in the “Status Badges” configuration tab.

In addition to project-level badges,  the Average Code Health and System Mastery badges can also be shown for  individual architectural components in the project.
These badges are activated using the same checkbox that activates the project-level badge and their URLs can be obtained by selecting component name from the drop-down menu on the configuration screen.

## Embedding

CodeScene’s status badges can be embedded anywhere, as long as a network connection to the CodeScene service is available.

HTML and Markdown snippets are available on the “Status Badge” configuration page when you select a badge type:

![CodeScene generates markup and HTML for status badges.](integrations/status-badges-generate.png)

<a id="status-badge-security-section"></a>

## Security

When they are activated, CodeScene’s status badges are *public*.
Users who are not logged in to CodeScene will still be able to see be able to see the badges.
This is why badges are *opt-in*.

Activating a badge does not expose any other data besides the SVG image itself.
