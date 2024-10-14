# Introduction

This is a series of scripts that represents what I often do manually to
test changes to pip's resolution algorithm.

# Prerequisites

These scripts rely on uv so that any python version can be downloaded to
run any particular version of Python. First you will need to install uv:
https://github.com/astral-sh/uv?tab=readme-ov-file#installation

# Running the scripts

The script is PEP 723 compliant, so you can use any tool that can run
PEP 723 scipts. Here are examples using uv:

    uv run scenarios.py --pip-version 24.2
    uv run scenarios.py --github-repo "notatallshaw/pip" --git-commit c4157d8dfb2823fc967549ccca08c150ab3df98b
    uv run compare.py --pip-version-1 24.2 --github-repo-2 "notatallshaw/pip" --git-commit-2 c4157d8dfb2823fc967549ccca08c150ab3df98b

# What is it measuring?

The idea is to measure the resolution in terms of what requirements and
packages did pip have to visit. As pip's resolution algorithm is is at
least an O(n^2) algorithm then the number of packages pip has to visit
goes up it domainates the amount of time it takes pip to resolve a given
set of requirements.

# What is it not measuring?

The script it not measuring wall clock time. While it may be added in the
future there are a number of problems to solve:

 * Replace `pypi-timemachine` with something faster that uses Simple API 1.1+
 * Only compare times from runs on the same machine

# Why not use `pip-resolver-benchmarks`?

[pip-resolver-benchmarks](https://github.com/pradyunsg/pip-resolver-benchmarks) is
a great tool but currently is unmaintained and is focused on wall clock time.

# To Dos

 * Rich logging, that shows progress of long pip installs
 * More metrics around what counts as a "better" install and resolution