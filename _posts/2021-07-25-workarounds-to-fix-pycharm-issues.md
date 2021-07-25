---
layout: single
title: "Workarounds to fix PyCharm issues"
date: 2021-07-12
last_modified_at: 2021-07-13
tags:
  - PyCharm
lang: en
---

A collection of issues I ran into when using PyCharm and ways to resolve them.

## Ignore breakpoints

For some projects, I got this issue when trying to enable the Debug mode for tests with pytest. Some people who ran into the same issue suggested [some solutions](https://intellij-support.jetbrains.com/hc/en-us/community/posts/360008107400-PyCharm-2020-1-not-stopping-on-breakpoints-anymore).

What [works with me](https://youtrack.jetbrains.com/issue/PY-42679) till now is to disable the Cython by adding the `PYDEVD_USE_CYTHON=NO` environment variable to the run configuration.
