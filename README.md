# Maven GAV Extractor

![Maven GAV Extractor](https://github.com/andreacomo/maven-gav-extractor/actions/workflows/test.yml/badge.svg)

This *GitHub Action* extracts GAV from `pom.xml`, i.e.:
 
 * `groupId`
 * `artifactId`
 * `version`
 * `name` (as Maven default, get the same value of `artifactId` if not specified)

Why should I need this? For example, to **name** and **tag** a Docker image built upon your artifact or **pass as parameters** to a dispatched workflow.

## Versioning
This project follows *Semantic Versioning* according to [GitHub Actions versioning practice](https://github.com/actions/toolkit/blob/main/docs/action-versioning.md)

>Current stable version is `v2`

## Prerequirements

This action expects you to have `maven` available in your workflow environment

## Inputs

| Name | Description | Default | Required |
| --- | --- | --- | --- |
| `pom-location` | Full path to your project `pom.xml` file | `${{ github.workspace }}/pom.xml` | `true` |

## Outputs

| Name | Description |
| --- | --- |
| `group-id` | Group Id of your project |
| `artifact-id` | Artifact Id of your project |
| `version` | Version of your project |
| `name` | Name of your project, artifact Id if not specified |

## Example usage

```yml
name: Sample workflow

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    name: Should extract GAV
    steps:
    - uses: actions/checkout@v3
    - name: Set up JDK 11
      uses: actions/setup-java@v2
      with:
        java-version: 11
        distribution: temurin
    - name: Extract GAV
      id: extract
      uses: andreacomo/maven-gav-extractor@v2
    - name: Log GAV
      run: |
        echo ${{ steps.extract.outputs.group-id }}
        echo ${{ steps.extract.outputs.artifact-id }}
        echo ${{ steps.extract.outputs.version }}
        echo ${{ steps.extract.outputs.name }}
      shell: bash
```
