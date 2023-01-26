## Overview

Given that we are a small functional team that is meant to maintain :wrench:, support ::phone::, care for :heart:, and cultivate :sunflower: our amazing Octokit :octocat: and Terraform community we often have to make decisions that are best for the entire community.
We don't take this act of prioritization lightly nor are we haphazard about it. We want to honor the time and thought that everyone has put into all of the SDKs that we have come to know and :heart:.

Add that to the number of repos that we need to maintain (70+) and weekly interactions (500-1000 +/-) that we end up having with everyone I am sure it's clear why we have to define how we **prioritize** and our commitment to respond (think of an **SLA** of sorts) to those priorities.

### What are the Priorities?

In each of the repositories we own you'll see the same [labels](https://github.com/octokit/octokit.net/labels) for priority.  

**They are:**  
`Priority: Critical`, `Priority: High`, `Priority: Normal`, `Priority: Low`

Incidentally, these map directly to the priorities set in our [Octokit Active community board](https://github.com/orgs/octokit/projects/10/views/4).

| [Repo label](https://github.com/octokit/octokit.net/labels)   |      [Community board](https://github.com/orgs/octokit/projects/10/views/4) | Example |
|----------|:-------------:|:-----------|
| Priority: Critical | Urgent | Any security issues - Data leaks - Broken or non functioning SDK that has been published - Any stop work scenarios for users (where rollback is not possible)|
| Priority: High | High | Any broken SDK methods - Deprecated or broken features - Critical dependency updates - Pull Requests that have been completed, are active, and are passing CI - Any issues that have been reported multiple times / impacting multiple users |
| Priority: Normal | Normal | Any non-prioritized features - Issues impacting a low number of users - Schema changes and additions - Normal dependency updates |
| Priority: Low | Low | Basic workflow changes - Draft issues/PRs - Stale issues/PRs - non-critical dependency updates - Any incomplete design work |

### What are our response commitments?

Note: This does not represent a commitment to resolution, just how quickly we'll respond and begin working on it

| Priority  | Response expectation | 
|----------|:-----------|
| Urgent | 0 to **24hrs**:  A security advisory will be posted if needed and updates publically posted to the corresponding repository |
| High | =< **1 Week** : Typically, we'll respond in issue/pr and will have a plan of action within the response expectation time window. | 
| Normal | >= **1 Week** : We'll acknowledge and make administrative assignments to the issue or PR.  They might get labeled "up-for-grabs". |
| Low | > **1 Week**: Typically, little to no action will take place on these items. They will often get labeled "up-for-grabs". |


### How do we Prioritize?

Remembering that we as a team have to prioritize not at the individual SDK or community level but across many repositories and communities our, methods need to consider several variables.
Our process, while not exactly scientific, is aimed at protecting the interests of our communities first - we use a modified version of [RICE](https://www.productplan.com/glossary/rice-scoring-model/).

Here are some data points, empathetic aspects, and questions we use to help us prioritize.

* Does the issue compromise data integrity, user security, or the integrity of GitHub?
* How serious is the need? 
* What's the overall impact on the SDK community?
* What's the overall impact on the package communities
* What's the overall impact on the language communities	
* How active is the SDK community?
* How many open issues are there?
* How many open PRs are there?
* What is the throughput of the given SDK where the issue is?
* What is the overall usage footprint?
* What’s the difficulty of the change set/fix?
* How much friction is the issue causing?
* What's the overall time/effort cost of addressing the issue/need?
etc...


