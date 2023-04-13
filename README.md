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

[Snyk Open Source - supported languages and package managers](https://github.com/papicella/cli-snyk-getting-started)

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

_Note: change into the "**snyk-boot-web**" folder before running the next series of commands_ 

### Display all issues

- Run the "**snyk test**" command as shown below

```shell
snyk test

Testing /Users/pasapicella/snyk/SE/getting-started/snyk-boot-web...

Tested 40 dependencies for known issues, found 34 issues, 34 vulnerable paths.


Issues to fix by upgrading:

  Upgrade com.h2database:h2@1.4.200 to com.h2database:h2@2.0.202 to fix


  Upgrade org.apache.logging.log4j:log4j-core@2.15.0 to org.apache.logging.log4j:log4j-core@2.17.1 to fix
  ✗ Arbitrary Code Execution [Medium Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2327339] in org.apache.logging.log4j:log4j-core@2.15.0
    introduced by org.apache.logging.log4j:log4j-core@2.15.0
  ✗ Denial of Service (DoS) [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2321524] in org.apache.logging.log4j:log4j-core@2.15.0
    introduced by org.apache.logging.log4j:log4j-core@2.15.0
  ✗ Remote Code Execution (RCE) [Critical Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2320014] in org.apache.logging.log4j:log4j-core@2.15.0
    introduced by org.apache.logging.log4j:log4j-core@2.15.0
  
  ...
  
  Issues with no direct upgrade or patch:
  ✗ Arbitrary Code Execution [Medium Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGYAML-3152153] in org.yaml:snakeyaml@1.26
    introduced by org.springframework.boot:spring-boot-starter-web@2.3.10.RELEASE > org.springframework.boot:spring-boot-starter@2.3.10.RELEASE > org.yaml:snakeyaml@1.26
  This issue was fixed in versions: 2.0


License issues:

  ✗ Dual license: MPL-2.0, EPL-1.0 (new) [Medium Severity][https://snyk.io/vuln/snyk:lic:maven:com.h2database:h2:(MPL-2.0_OR_EPL-1.0)] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200

  ✗ EPL-1.0 OR LGPL-2.1 license (new) [Medium Severity][https://snyk.io/vuln/snyk:lic:maven:ch.qos.logback:logback-core:EPL-1.0_OR_LGPL-2.1] in ch.qos.logback:logback-core@1.2.3
    introduced by org.springframework.boot:spring-boot-starter-web@2.3.10.RELEASE > org.springframework.boot:spring-boot-starter@2.3.10.RELEASE > org.springframework.boot:spring-boot-starter-logging@2.3.10.RELEASE > ch.qos.logback:logback-classic@1.2.3 > ch.qos.logback:logback-core@1.2.3

  ✗ EPL-1.0 OR LGPL-2.1 license (new) [Medium Severity][https://snyk.io/vuln/snyk:lic:maven:ch.qos.logback:logback-classic:EPL-1.0_OR_LGPL-2.1] in ch.qos.logback:logback-classic@1.2.3
    introduced by org.springframework.boot:spring-boot-starter-web@2.3.10.RELEASE > org.springframework.boot:spring-boot-starter@2.3.10.RELEASE > org.springframework.boot:spring-boot-starter-logging@2.3.10.RELEASE > ch.qos.logback:logback-classic@1.2.3



Organization:      apples-demo
Package manager:   maven
Target file:       pom.xml
Project name:      com.example:snyk-boot-web
Open source:       no
Project path:      /Users/pasapicella/snyk/SE/getting-started/snyk-boot-web
Licenses:          enabled
```

### Filter issues based on severity threshold

To improve control over your tests, you can use the --severity-threshold option for the snyk test command with one of the supported levels: low|medium|high|critical. With this option, only vulnerabilities of the specified level or higher are reported

[Severity thresholds for CLI tests](https://docs.snyk.io/snyk-cli/test-for-vulnerabilities/set-severity-thresholds-for-cli-tests)

- Run the "**snyk test --severity-threshold=critical**" command as shown below

```shell
$ snyk test --severity-threshold=critical

Testing /Users/pasapicella/snyk/demos/languages-code-demos/JavaScript/goof...

Tested 564 dependencies for known issues, found 2 issues, 2 vulnerable paths.


Issues to fix by upgrading:

  Upgrade adm-zip@0.4.7 to adm-zip@0.4.11 to fix
  ✗ Arbitrary File Write via Archive Extraction (Zip Slip) [Critical Severity][https://security.snyk.io/vuln/npm:adm-zip:20180415] in adm-zip@0.4.7
    introduced by adm-zip@0.4.7


Issues with no direct upgrade or patch:
  ✗ Prototype Pollution [Critical Severity][https://security.snyk.io/vuln/SNYK-JS-HANDLEBARS-534988] in handlebars@4.0.11
    introduced by tap@11.1.5 > nyc@11.9.0 > istanbul-reports@1.4.0 > handlebars@4.0.11
  This issue was fixed in versions: 3.0.8, 4.5.3



Organization:      apples-demo
Package manager:   npm
Target file:       package-lock.json
Project name:      goof
Open source:       no
Project path:      /Users/pasapicella/snyk/demos/languages-code-demos/JavaScript/goof
Local Snyk policy: found
Licenses:          enabled
```

### Output results to HTML

First, Install the Snyk JSON to HTML Mapper using npm:

[Snyk JSON to HTML Mapper](https://github.com/snyk/snyk-to-html)

- Run a command as follows and then open the resulting html file "**snyk test --json | snyk-to-html -o results.html**"

```shell
$ snyk test --json | snyk-to-html -o results.html
Vulnerability snapshot saved at results.html
```

![alt tag](https://i.ibb.co/vJF8Grg/getting-started-2.png)

### Output Results to JSON or SARIF

Run either of the following commands:

```shell
$ snyk test --json

$ snyk test --sarif
```

Send results to Snyk App UI


Ignore all H2 vulnerabilities

Separate results by branch/version

Finding Log4J issue by CVE using JQ filter

## Dockerfile scanning

Scanning a Dockerfile from the CLI

Uploading the results of a Dockerfile scann  to Snyk App

TODO://


<hr />
Pas Apicella [pas at snyk.io] is a Principal Solution Engineer at Snyk APJ
