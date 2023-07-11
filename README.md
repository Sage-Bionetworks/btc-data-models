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
git checkout -b my-new-branch origin/main
```

Update the data model in Google Sheet before exporting it to CSV format.

1. Open the [BTC Data Model (Google Sheet)]
2. Update the data model
3. Export the data model to CSV
    - Click on `File` > `Download` > `Comma Separated Value (.csv)`
    - Name the file `btc.model.csv`
    - Download the CSV file

4. Make sure the `main` branch 
4. Create a new branch in this repo from the `main` branch
    ```console
    git checkout -b my-branch origin/main
    ```


This repository contains 3 major files:

1. `btc.model.csv`: The CSV representation of the example data model. This file
   is created by the collective effort of data curators and annotators from a
   *community* (e.g. *HTAN*), and will be used to create a JSON-LD
   representation of the data model. This file is generated from the [BTC data
   model Google
   sheet](https://docs.google.com/spreadsheets/d/1PVdQqi8R_pFRYESBcrpZHBPueT7kA2IuCIh8u_xBjyg).


2. `btc.model.jsonld`: The JSON-LD representation of the example data model,
   which is automatically created from the CSV data model using the schematic
   CLI. More details on how to convert the CSV data model to the JSON-LD data
   model can be found
   [here](https://sage-schematic.readthedocs.io/en/develop/cli_reference.html#schematic-schema-convert).
   This is the central schema (data model) which will be used to power the
   generation of metadata manifest templates for various data types (e.g.,
   `scRNA-seq Level 1`) from the schema.


3. `config.yml`: The schematic-compatible configuration file, which allows users
   to specify values for application-specific keys (e.g., path to Synapse
   configuration file) and project-specific keys (e.g., Synapse fileview for
   community project). A description of what the various keys in this file
   represent can be found in the [Fill in Configuration
   File(s)](https://sage-schematic.readthedocs.io/en/develop/README.html#fill-in-configuration-file-s)
   section of the schematic
   [docs](https://sage-schematic.readthedocs.io/en/develop/index.html).

## Usage

### Install Schematic

#### From PyPi

```
python -m pip install schematicpy
```

#### From its source

```console
mkdir tmp
cd tmp

git clone --single-branch --branch main https://github.com/Sage-Bionetworks/schematic.git
cd schematic
poetry build
pip3 install dist/schematicpy-*-py3-none-any.whl
cd ..

~/.local/bin/schematic --help
```

### Login with the Synapse client

The Synapse client is installed along with Schematic.

```
synapse login --rememberMe
```

Enter your Synapse Personal Access Token (PAT) when prompted. The token must
have at least the `View`, `Download` and `Modify` permissions (TODO: to
confirm.)

### Initialize Schematic

```console
schematic init --config config.yml
```

### Generate the data model in JSON-LD format

The following command converts the data model from CSV to JSON-LD:

```console
schematic schema convert btc.model.csv
```

### Generate the data model manifest

As an Excel sheet:

```console
schematic manifest \
  --config config.yml get \
  --data_type BulkRNA-seqLevel1 \
  --title "Test BulkRNA-seq" \
  --output_xlsx btc.model.xlsx
```

As a Google sheet:

```console
schematic manifest \
  --config config.yml get \
  --data_type BulkRNA-seqLevel1 \
  --title "Test BulkRNA-seq" \
  --sheet_url
```


<!-- Links -->

[docker engine]: https://docs.docker.com/get-docker/
[visual studio code]: https://code.visualstudio.com/
[GitHub Codespace]: https://github.com/features/codespaces
[development container]: https://containers.dev/
[BTC Data Model (Google Sheet)]: https://docs.google.com/spreadsheets/d/1CkNVuWSR3g1XEqWUP2taJfl9PZZIsnFu148tOIM0VRA/