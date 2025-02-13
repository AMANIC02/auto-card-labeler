# Auto card labeler

[![CI Status](https://github.com/technote-space/auto-card-labeler/workflows/CI/badge.svg)](https://github.com/technote-space/auto-card-labeler/actions)
[![codecov](https://codecov.io/gh/technote-space/auto-card-labeler/branch/master/graph/badge.svg)](https://codecov.io/gh/technote-space/auto-card-labeler)
[![CodeFactor](https://www.codefactor.io/repository/github/technote-space/auto-card-labeler/badge)](https://www.codefactor.io/repository/github/technote-space/auto-card-labeler)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/technote-space/auto-card-labeler/blob/master/LICENSE)

*Read this in other languages: [English](README.md), [日本語](README.ja.md).*

This is a `GitHub Action` that automatically labels Issues or PullRequests based on project card moves.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Screenshot](#screenshot)
- [Installation](#installation)
- [Behavior](#behavior)
- [Options](#options)
  - [CONFIG_FILENAME](#config_filename)
- [Action event details](#action-event-details)
  - [Target event](#target-event)
- [GitHub Actions using this Action](#github-actions-using-this-action)
- [Author](#author)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Screenshot
![GitHub Action](https://raw.githubusercontent.com/technote-space/auto-card-labeler/images/screenshot.gif)

## Installation
1. Setup workflow  
   e.g. `.github/workflows/project_card_moved.yml`
   ```yaml
   on:
     project_card:
       types: [moved]
   name: Project Card Event
   jobs:
     triage:
       name: Auto card labeler
       runs-on: ubuntu-latest
       steps:
         - name: Auto card labeler
           uses: technote-space/auto-card-labeler@v1
           with:
             GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
   ```
1. Add action setting  
   e.g. `.github/card-labeler.yml`
   ```yaml
   Project name1:
     Column name1:
       - 'Status: test1'
     Column name2:
       - 'Status: test2-1'
       - 'Status: test2-2'
   Project name2:
     Column name3:
       - 'Status: test1'
   ```

## Behavior
e.g.
```yaml
Project name1:
  Column name1:
    - 'Status: test1'
  Column name2:
    - 'Status: test2-1'
    - 'Status: test2-2'
```
1. Card created (`Column name1`)
   - Add
     - `Status: test1`
   - Remove
     - None
   - Current Labels
     - `Status: test1`
1. Card moved to `Column name2`
   - Add
     - `Status: test2-1`
     - `Status: test2-2`
   - Remove
     - `Status: test1`
   - Current Labels
     - `Status: test2-1`
     - `Status: test2-2`
1. Card moved to `Column name3`
   - Add
     - None
   - Remove
     - `Status: test2-1`
     - `Status: test2-2`
   - Current Labels
     - None
1. Card moved to `Column name1`
   - Add
     - `Status: test1`
   - Remove
     - None
   - Current Labels
     - `Status: test1`

## Options
### CONFIG_FILENAME
Config file name.  
default: `'card-labeler.yml'`

## Action event details
### Target event
| eventName | action |
|:---:|:---:|
|project_card|moved|
|project_card|rerequested|

## GitHub Actions using this Action
- [Release GitHub Actions](https://github.com/technote-space/release-github-actions)
  - [project_card_moved.yml](https://github.com/technote-space/release-github-actions/blob/master/.github/workflows/project_card_moved.yml)
- [Auto card labeler](https://github.com/technote-space/auto-card-labeler)
  - [project_card_moved.yml](https://github.com/technote-space/auto-card-labeler/blob/master/.github/workflows/project_card_moved.yml)
- [Assign Author](https://github.com/technote-space/assign-author)
  - [project_card_moved.yml](https://github.com/technote-space/assign-author/blob/master/.github/workflows/project_card_moved.yml)
- [TOC Generator](https://github.com/technote-space/toc-generator)
  - [project_card_moved.yml](https://github.com/technote-space/toc-generator/blob/master/.github/workflows/project_card_moved.yml)
- [Package Version Check Action](https://github.com/technote-space/package-version-check-action)
  - [project_card_moved.yml](https://github.com/technote-space/package-version-check-action/blob/master/.github/workflows/project_card_moved.yml)

## Author
[GitHub (Technote)](https://github.com/technote-space)  
[Blog](https://technote.space)
