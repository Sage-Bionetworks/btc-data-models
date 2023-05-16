# BTC Data Models

## Overview

This repository contains the data model for Break Through Cancer (BTC).

## Main files

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
