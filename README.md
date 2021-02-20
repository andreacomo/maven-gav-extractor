# Maven GAV (groupId, artifactId, version) Extractor *GitHub Action*

This action extracts from `pom.xml` GAV info, i.e.:
 
 * `groupId`
 * `artifactId`
 * `version`

Why should I need this? For example, to **name** and **tag** a Docker image built upon your artifact

## Prerequirements

This action expects you to have `maven` available in your workflow environment

## Inputs

### `pom-location`

**Required** Full path to your project `pom.xml` file. Default value is POM in your project root: `${{ github.workspace }}/pom.xml`

## Outputs

### `group-id`

Group Id of your project

### `artifact-id`

Artifact Id of your project

### `version`

Version of your project

## Example usage

```
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
      uses: andreacomo/maven-gav-extractor-github-action@v1
    - name: Log GAV
      run: |
        echo ${{ steps.extract.outputs.group-id }}
        echo ${{ steps.extract.outputs.artifact-id }}
        echo ${{ steps.extract.outputs.version }}
      shell: bash
```