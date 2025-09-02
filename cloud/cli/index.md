# CodeScene CLI tool

The [CodeScene CLI](https://codescene.com/codescenes-cli) is a command-line tool which performs the same checks as the PR integration, but locally - on non-committed, staged changes or between select branches.

A few highlights of the tool:

* Automated check via Git pre-commit/push hooks. Push clean PRs.
* Integrate with any code editor.
* Integrate into CI/CD pipelines for teams doing Trunk Based development

![cs git-hook flow-chart](../shared/cli/cli-git-hook-flowchart.png)

## Installation

### Linux, macOS and Windows (if WSL)

The install script will download the binary, move it to `~/.local/bin` and make it executable. If `~/.local/bin` is not in the user’s `PATH`, it will be added.

It works if your shell is one of: bash, zsh or fish

```console
curl https://downloads.codescene.io/enterprise/cli/install-codescene-cli.sh | sh
```

### Windows (powershell)

The powershell script downloads the windows binary, moves it to `$env:USERPROFILE\AppData\Local\Programs\CodeScene` and makes it executable.

```console
Invoke-WebRequest -Uri 'https://downloads.codescene.io/enterprise/cli/install-codescene-cli.ps1' -OutFile install-codescene-cli.ps1
.\install-codescene-cli.ps1
```

Note, on non-server editions of Windows, the script execution policy is set to Restricted by default, and script execution is disabled. It can be enabled with:

```console
Set-ExecutionPolicy RemoteSigned
```

This allows for the execution of trusted scripts downloaded from the internet, and all local scripts. In our case the script is considered a local file.

## Manual installation

The binaries are also available for manual installation. Just download the binary for you platform and make it executable.

* [Linux amd64](https://downloads.codescene.io/enterprise/cli/codescene-cli-linux-amd64-latest.zip)
* [Windows amd64](https://downloads.codescene.io/enterprise/cli/codescene-cli-windows-amd64-latest.zip)
* [MacOS amd64](https://downloads.codescene.io/enterprise/cli/codescene-cli-macos-amd64-latest.zip)
* [MacOS aarch64](https://downloads.codescene.io/enterprise/cli/codescene-cli-macos-aarch64-latest.zip)

### Platform specific notes

* MacOS binaries are not signed, thus you have to manually move them out of quarantine using `xattr -dr com.apple.quarantine <binary>`.
* Windows users might have to set the script execution policy manually as mentioned above: `Set-ExecutionPolicy RemoteSigned`

## Client setup

The CLI tool requires an access token for licensing. You need to have your CodeScene administrator
set up a token on the [projects configuration page](../../configuration/devtools-tokens). Then set your environment variables as follows:

```console
export CS_ACCESS_TOKEN=<your-access-token>
```

Or in windows:

```console
$env:CS_ACCESS_TOKEN = '<your-access-token>'
```
