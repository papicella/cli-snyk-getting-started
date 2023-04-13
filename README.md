# Getting Started with Snyk CLI

This guide is provided as a quick reference to getting started with Snyk CLI. We will use an existing repository during a set of tests we run showing how to perform common tasks with Snyk

## Step 1 - Installing the CLI

- Install the Snyk CLI using the instructions here https://docs.snyk.io/snyk-cli/install-the-snyk-cli
- AUTH with Snyk CLI https://docs.snyk.io/snyk-cli/commands/auth

Verify you are ready to use the CLI as shown below

```shell
$ snyk --version
1.1114.0
```

## Step 2 - Obtain your ORG ID and name from snyk settings 

- Click on the Settings tab for your organization as shown below
- Make a note of your organization ID or name 

![alt tag](https://i.ibb.co/wYT04Z1/getting-started-1.png)

## Snyk Open Source Demos

First let's clone the following repo we will use this repo in the examples. You can use your own code if you like. be sure to perform a build of the code, in this example it's a java maven project so you would run "mvn package" for example. Snyk Open Source supports the following programming languages, build tools, and package managers

https://docs.snyk.io/scan-application-code/snyk-open-source/snyk-open-source-supported-languages-and-package-managers

- Clone the repo as shown below

```shell
$ git clone https://github.com/papicella/snyk-boot-web
Cloning into 'snyk-boot-web'...
remote: Enumerating objects: 217, done.
remote: Counting objects: 100% (34/34), done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 217 (delta 10), reused 25 (delta 5), pack-reused 183
Receiving objects: 100% (217/217), 95.16 KiB | 2.38 MiB/s, done.
Resolving deltas: 100% (84/84), done.
```

Display all issues

Filter issues based on severity threshold

Output results to HTML

Output Results to JSON or SARIF



<hr />
Pas Apicella [pas at snyk.io] is a Principal Solution Engineer at Snyk APJ
