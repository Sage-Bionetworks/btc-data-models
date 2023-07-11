# BTC Data Model

## Overview

This repository contains the data model for Break Through Cancer (BTC).

## Development Setup

### Requirements

- [Docker Engine] OR [GitHub Codespace]
- [Visual Studio Code]

### Open this repo in VS Code

Click on the button shown below to open this repo in its [development container]
with VS Code. This option is suitable if you want to explore the content of
repo.

[![Open in Dev Containers](https://img.shields.io/static/v1?label=Dev%20Containers&message=Open&color=blue&logo=visualstudiocode&style=for-the-badge)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/Sage-Bionetworks/btc-data-models 'Open in VS Code Dev Containers')

### Open this repo in GitHub Codespace

TODO

## Update the Data Model

### Create a new git branch

First, create a new branch in your local repo from the `main` branch. This
branch will be used to open a PR that update the data model files.

> **Note** Make sure that your `main` branch is up-to-date with the local repo
> by running the command `git pull origin main`.

```console
git checkout -b <branch_name> origin/main
```

### Generate the data model in CSV format

Update the data model in Google Sheet before exporting it to CSV format.

1. Open the [BTC Data Model (Google Sheet)]
2. Update the data model
3. Export the data model to CSV
    - Click on `File` > `Download` > `Comma Separated Value (.csv)`
    - Name the file `btc.model.csv`
    - Download the CSV file
4. Replace the existing file `btc.model.csv` with the new one.
5. Commit and push the changes.
    ```console
    git add -u
    git commit -m 'Brief description of the change'
    git push -u origin <branch_name>
    ```

### Install Schematic and the Synapse client for Python

Install the Schematic package for Python. This step may takes a few minutes but
only need to be done once.

```console
python -m pip install schematicpy
```

The Synapse client is installed along with Schematic. 

### Login into Synapse

Use this Synapse client for Python to login into Synapse.

```
synapse login --rememberMe
```

Enter your Synapse Personal Access Token (PAT) when prompted. The token must
have at least the `View`, `Download` and `Modify` permissions (TODO: confirm the
scopes needed).

### Initialize Schematic

```console
schematic init --config config.yml
```

### Generate the data model in JSON-LD format

The command shown below converts the data model from CSV to JSON-LD:

```console
schematic schema convert btc.model.csv
```

Commit and push the changes:

```console
git add -u
git commit -m 'Brief description of the change'
git push -u origin <branch_name>
```

### Open a Pull Request

Open your browser and create a Pull Request with the following branches:

- Base: `main`
- Compare: `<branch_name>`

Upon review, merging the branch `<branch_name>` into `main` will effectively
update the data model files in CSV and JSON-LD format.

### Specify the new Data Model to DCA

TODO

<!-- Links -->

[docker engine]: https://docs.docker.com/get-docker/
[visual studio code]: https://code.visualstudio.com/
[GitHub Codespace]: https://github.com/features/codespaces
[development container]: https://containers.dev/
[BTC Data Model (Google Sheet)]: https://docs.google.com/spreadsheets/d/1CkNVuWSR3g1XEqWUP2taJfl9PZZIsnFu148tOIM0VRA/