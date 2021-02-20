# Maven GAV Extractor *GitHub Action*

This action extracts GAV from `pom.xml`, i.e.:
 
 * `groupId`
 * `artifactId`
 * `version`

Why should I need this? For example, to **name** and **tag** a Docker image built upon your artifact or **pass as parameters** to a dispatched workflow.

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

## Example usage

```yml
name: Sample workflow

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    name: Should extract GAV
    steps:
    - uses: actions/checkout@v2
    - name: Set up JDK 11
      uses: actions/setup-java@v1
      with:
        java-version: 11
    - name: Extract GAV
      id: extract
      uses: andreacomo/maven-gav-extractor@v1
    - name: Log GAV
      run: |
        echo ${{ steps.extract.outputs.group-id }}
        echo ${{ steps.extract.outputs.artifact-id }}
        echo ${{ steps.extract.outputs.version }}
      shell: bash
```
