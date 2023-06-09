---
sidebar_position: 1
title: 1. Continuos Integration
---

# Continuos Integration

@Eugenio Tesio

The continuous integration process also known by the acronym __CI/CD (continuous integration / continuous development)__ is a mechanism used to run automatic jobs in relation to the portion of code that is being uploaded to our code repository through a git push. These jobs include code audits (formatting, identation, maximum number of characters per line, etc), test execution and/or execution of actions (sending an email, a Slack message, sending a request to an API, etc).

The sequence of tasks, __pipeline__, varies a lot according to the programming language and the environment to which the code is uploaded. It is not the same to upload a code to the development repository than to the production repository, the latter needs much more controls and even to have automated the deployment of the code to the production servers or the generation of the compiled application to be able to upload it to the stores (Google Play, App Store, Microsoft Apps) where it will be published.

Currently there are many options for continuous integration, and each programming language has its favorites. Among the best known are [Jenkins](https://www.jenkins.io/), [Bamboo](https://www.atlassian.com/software/bamboo) from Atlassian, [TeamCity](https://www.jetbrains.com/teamcity/) from Jetbrains, etc. We can also find integration tools within each cloud; [Amazon Pipeline](https://aws.amazon.com/es/codepipeline/), [Google Build](https://cloud.google.com/build), [Azure Pipelines](https://azure.microsoft.com/es-es/products/devops/pipelines/), etc.

We could say that almost all companies that offer a code repository also offer a continuous integration tool. Unfortunately, there is no standard language for the creation of these jobs, so each solution has its own programming language and this is why the developer must choose the best solution that suits his needs and focus on it...

In the case of Flutter and this course, which has its repository on GitHub, we consider that the best integration option is [GitHub Actions](https://docs.github.com/en/actions), a very recent tool (October 2018) compared to the age and maturity of its repository, but with tremendous potential.

We hope you like doing this section as much as we do! 🥳
