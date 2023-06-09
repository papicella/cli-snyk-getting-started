# Getting Started with Snyk CLI

This guide is provided as a quick reference to getting started with Snyk CLI. We will use an existing repository during a set of tests we run showing how to perform common tasks with the Snyk CLI

_Note: This does not attempt to replace the Snyk Docs which go into far more details but instead aid in a quick start with the snyk CLI_ 

## Step 1 - Installing the CLI

- Install the Snyk CLI using the instructions here https://docs.snyk.io/snyk-cli/install-the-snyk-cli
- AUTH with Snyk CLI https://docs.snyk.io/snyk-cli/commands/auth

Verify you are ready to use the CLI as shown below. Ensure you are runing version "**1.1177.0**" or later

```shell
$ snyk --version
1.1177.0
```

## Step 2 - Obtain your ORG ID and name from snyk settings 

- Click on the Settings tab for your organization as shown below
- Make a note of your organization ID or name 

![alt tag](https://i.ibb.co/KVFfFSG/getting-started-1.png)

In these examples the ORG = "**getting-started-cli**"

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

- Run the "**snyk test**" command as shown below. You will need to install maven and install the dependancies using "mvn install" prior to running this scan. You can use any repo such as a NodeJS repository which would mean the commands would still work just some steps can't be followed further on

Example repo you could use if you don't wish to use a java project

[Goof NodeJS Repository](https://github.com/papicella/goof)

```shell
$ snyk test

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

### Send results to Snyk App UI

To send results to Snyk App we use the monitor command as showb below:

[Snyk Monitor CLI Command](https://docs.snyk.io/snyk-cli/commands/monitor)

Run a command as follows this time we will use an ORG name to target the org we wish to send the results to

- Run "**snyk monitor --all-projects --org=getting-started-cli**"

```shell
$ snyk monitor --all-projects --org=getting-started-cli

Monitoring /Users/pasapicella/snyk/SE/getting-started/snyk-boot-web (com.example:snyk-boot-web)...

Explore this snapshot at https://app.snyk.io/org/getting-started-cli/project/3ec9514f-878c-496f-8458-0c459779bd25/history/e520c99b-8d11-4c3d-8856-afa8388ee0d7

Notifications about newly disclosed issues related to these dependencies will be emailed to you.
```

![alt tag](https://i.ibb.co/XpZKZdr/getting-started-3.png)

### Ignore all H2 vulnerabilities

At some point you will need to ignore vulnerabilities in this example lets ignore mall H2 vulnerabilities.

- First lets just show the h2 vulnerabilities as per a command as follows "**snyk test --org=getting-started-cli | grep h2**" 

```shell
$ snyk test --org=getting-started-cli | grep h2
  Upgrade com.h2database:h2@1.4.200 to com.h2database:h2@2.1.210 to fix
  ✗ Remote Code Execution (RCE) [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-COMH2DATABASE-2331071] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200
  ✗ XML External Entity (XXE) Injection [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-COMH2DATABASE-1769238] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200
  ✗ Remote Code Execution (RCE) [Critical Severity][https://security.snyk.io/vuln/SNYK-JAVA-COMH2DATABASE-2348247] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200
  ✗ Information Exposure [Medium Severity][https://security.snyk.io/vuln/SNYK-JAVA-COMH2DATABASE-3146851] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200
  ✗ Remote Code Execution (RCE) [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-COMH2DATABASE-31685] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200
  ✗ Dual license: MPL-2.0, EPL-1.0 (new) [Medium Severity][https://snyk.io/vuln/snyk:lic:maven:com.h2database:h2:(MPL-2.0_OR_EPL-1.0)] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200
```

Now we see we have 5 H2 library vulnerabilities and 1 license issue. Let's go ahead and create a local "**.snyk**" file that will ignore all 5 H2 library vulnerabilities

- Create a file in the root folder called "**.snyk**" with contents as follows

```shell
# Snyk (https://snyk.io) policy file, patches or ignores known vulnerabilities.
version: v1.25.0
# ignores vulnerabilities until expiry date; change duration by modifying expiry date
ignore:
  SNYK-JAVA-COMH2DATABASE-2331071:
    - '*':
        reason: testing cli ignores
        expires: 2028-04-01T00:00:00.000Z
        created: 2023-03-06T05:15:14.233Z
  SNYK-JAVA-COMH2DATABASE-1769238:
    - '*':
        reason: testing cli ignores
        expires: 2028-04-01T00:00:00.000Z
        created: 2023-03-06T05:20:11.968Z
  SNYK-JAVA-COMH2DATABASE-2348247:
    - '*':
        reason: testing cli ignores
        expires: 2028-04-01T00:00:00.000Z
        created: 2023-03-06T05:20:31.046Z
  SNYK-JAVA-COMH2DATABASE-3146851:
    - '*':
        reason: testing cli ignores
        expires: 2028-04-01T00:00:00.000Z
        created: 2023-03-06T05:21:13.757Z
  SNYK-JAVA-COMH2DATABASE-31685:
    - '*':
        reason: testing cli ignores
        expires: 2028-04-01T00:00:00.000Z
        created: 2023-03-06T05:21:35.203Z
patch: {}
```

_Note: You can generate this file using "**snyk ignore**" CLI option as described below_

[Ignore vulnerabilities using Snyk CLI](https://docs.snyk.io/snyk-cli/test-for-vulnerabilities/ignore-vulnerabilities-using-snyk-cli)

- This time let's run the same command and see those H2 issues have been ignored and are not displayed this time and only the license issue is shown.

_Note: You can also apply a policy file by path as follows "**snyk test --org=getting-started-cli --policy-path=./.snyk | grep h2**" but by default if a ".snyk" file exists in current directory it's not needed_

```shell
snyk test --org=getting-started-cli | grep h2
  Upgrade com.h2database:h2@1.4.200 to com.h2database:h2@2.0.202 to fix
  ✗ Dual license: MPL-2.0, EPL-1.0 (new) [Medium Severity][https://snyk.io/vuln/snyk:lic:maven:com.h2database:h2:(MPL-2.0_OR_EPL-1.0)] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200
```

- Finally, lets send the results to Snyk App UI and confirm our H2 vulnerabilities have been ignored as we requested

```shell
$ snyk monitor --project-name="snyk-boot-web-h2-ignores" --org=getting-started-cli --policy-path=./.snyk

Monitoring /Users/pasapicella/snyk/SE/getting-started/snyk-boot-web (com.example:snyk-boot-web)...

Explore this snapshot at https://app.snyk.io/org/getting-started-cli/project/b17a3ad0-9bd1-4ead-8b2d-82a7949669a7/history/0ba99ab0-6510-49df-8009-ac1d7c070a89

Notifications about newly disclosed issues related to these dependencies will be emailed to you.
```

![alt tag](https://i.ibb.co/qgTcQz5/getting-started-5.png)

![alt tag](https://i.ibb.co/XkRV6q6/getting-started-4.png)

Note: You can also add key/value pairs to a monitor command to add tags to your monitored projects using something as follows

--project-tags=<TAG>[,<TAG>]...> ie: **--project-tags="app=snyk-boot-web"**

[Project Tags](https://docs.snyk.io/manage-issues/introduction-to-snyk-projects/project-tags)

### Separate results by branch/version

Your project may have multiple states which you want to monitor separately, for example, branches, releases, or deployments. You can use the --target-reference option to separate projects into these specific groupings.
--target-reference takes any text so you can combine it with a command to automatically set it to a value.

[Group projects for monitoring](https://docs.snyk.io/snyk-cli/test-for-vulnerabilities/grouping-projects-by-branch-or-version)

- Run a command as follows "**snyk monitor --target-reference="$(git branch --show-current)" --all-projects --org=getting-started-cli --remote-repo-url='MY_WEB_APP'**"

```shell
$ snyk monitor --target-reference="$(git branch --show-current)" --all-projects --org=getting-started-cli --remote-repo-url='MY_WEB_APP'

Monitoring /Users/pasapicella/snyk/SE/getting-started/snyk-boot-web (com.example:snyk-boot-web)...

Explore this snapshot at https://app.snyk.io/org/getting-started-cli/project/9da2a85c-daf4-4ca0-b69e-d0cf83937778/history/9cfed54f-5957-40c7-a8b0-aaadf0de98e5

Notifications about newly disclosed issues related to these dependencies will be emailed to you.
```

- Now run a command and for the demo only lets hard code the new branch name for now to see how this is displayed in the UI, "**snyk monitor --target-reference="release2.0" --all-projects --org=getting-started-cli --remote-repo-url='MY_WEB_APP'**"

```shell
$ snyk monitor --target-reference="release2.0" --all-projects --org=getting-started-cli --remote-repo-url='MY_WEB_APP'

Monitoring /Users/pasapicella/snyk/SE/getting-started/snyk-boot-web (com.example:snyk-boot-web)...

Explore this snapshot at https://app.snyk.io/org/getting-started-cli/project/19532c2e-8396-48f3-b951-42058b4d55c7/history/d65ad0cc-566a-4597-b21c-50f5a67e0143

Notifications about newly disclosed issues related to these dependencies will be emailed to you.
```

Snyk App should show the following using your **--target-reference** names

![alt tag](https://i.ibb.co/RggrPMR/getting-started-6.png)

### Finding Log4J issue by Package Name using a JQ filter

- If we wanted to know if Log4J vulnerabilities existed we can simply run a scan as follows

```shell
$ snyk test | grep log4j
  Upgrade org.apache.logging.log4j:log4j-core@2.15.0 to org.apache.logging.log4j:log4j-core@2.17.1 to fix
  ✗ Arbitrary Code Execution [Medium Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2327339] in org.apache.logging.log4j:log4j-core@2.15.0
    introduced by org.apache.logging.log4j:log4j-core@2.15.0
  ✗ Denial of Service (DoS) [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2321524] in org.apache.logging.log4j:log4j-core@2.15.0
    introduced by org.apache.logging.log4j:log4j-core@2.15.0
  ✗ Remote Code Execution (RCE) [Critical Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2320014] in org.apache.logging.log4j:log4j-core@2.15.0
    introduced by org.apache.logging.log4j:log4j-core@2.15.0
```

Every open-source vulnerability is tagged with a CVE and CWE plus other useful data so here is how we would get the full JSON output and look for Log4j issues driving off the Package Name for example. 

Let's go ahead and find this "CVE-2021-45046: which is one of the vulnerabilities in out output of the scan - [CVE-2021-45046](https://www.cve.org/CVERecord?id=CVE-2021-45046)

This belongs in the current open-source dependancy package named "**org.apache.logging.log4j:log4j-core**"

- To look for this vulnerability in the JSON output we would run a command as follows "**snyk test --json | jq '.vulnerabilities[] | select(.packageName=="org.apache.logging.log4j:log4j-core")'**"

```shell
$ snyk test --json | jq '.vulnerabilities[] | select(.packageName=="org.apache.logging.log4j:log4j-core")'
{
  "id": "SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2320014",
  "title": "Remote Code Execution (RCE)",
  "CVSSv3": "CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:C/C:H/I:H/A:H/E:P/RL:O/RC:C",
  "credit": [
    "Unknown"
  ],
  "semver": {
    "vulnerable": [
      "[2.0-beta9,2.3.1)",
      "[2.4,2.12.2)",
      "[2.13.0,2.16.0)"
    ]
  },
  "exploit": "Proof of Concept",
  "fixedIn": [
    "2.3.1",
    "2.12.2",
    "2.16.0"
  ],
  "patches": [],
  "insights": {
    "triageAdvice": null
  },
  "language": "java",
  "severity": "critical",
  "cvssScore": 9,
  "functions": [],
  "malicious": false,
  
  ...
  
  "description": "## Overview\n[org.apache.logging.log4j:log4j-core](http://logging.apache.org/log4j/1.2/) is a logging library for Java.\nAffected versions of this package are vulnerable to Arbitrary Code Execution. <br /> **Note:** Even though this vulnerability appears to be related to the [log4Shell vulnerability](https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2314720), this vulnerability requires an attacker to have access to modify configurations to be exploitable, which is rarely possible.\r\n\r\nAn attacker with access to modification of logging configuration is able to configure `JDBCAppender` with a data source referencing a JNDI URI - which can execute malicious code.\r\n\r\nIn the fixed versions, `JDBCAppender` is using `JndiManager` and disables JNDI lookups by default (via `log4j2.enableJndiJdbc=false`).\r\n\r\n## Alternative Remediation\r\nIf you have reason to believe your application may be vulnerable and upgrading is not an option, you can either:\r\n\r\n* Disable/remove `JDBCAppender`\r\n* If `JDBCAppender` is used, make sure that it is not configured to use any protocol other than Java\n## Remediation\nUpgrade `org.apache.logging.log4j:log4j-core` to version 2.3.2, 2.12.4, 2.17.1 or higher.\n## References\n- [Apache Security Page](https://logging.apache.org/log4j/2.x/security.html)\n- [GitHub Commit](https://github.com/apache/logging-log4j2/commit/05db5f9527254632b59aed2a1d78a32c5ab74f16)\n- [Jira Issue](https://issues.apache.org/jira/browse/LOG4J2-3293)\n- [Openwall Mail](https://www.openwall.com/lists/oss-security/2021/12/28/1)\n",
  "epssDetails": {
    "percentile": "0.92752",
    "probability": "0.06697",
    "modelVersion": "v2023.03.01"
  },
  "identifiers": {
    "CVE": [
      "CVE-2021-44832"
    ],
    "CWE": [
      "CWE-94"
    ]
  },
  "packageName": "org.apache.logging.log4j:log4j-core",
  "proprietary": false,
  "creationTime": "2021-12-28T19:42:55.818691Z",
  "functions_new": [],
  "alternativeIds": [],
  "disclosureTime": "2021-12-28T19:42:53Z",
  "packageManager": "maven",
  "mavenModuleName": {
    "groupId": "org.apache.logging.log4j",
    "artifactId": "log4j-core"
  },
  "publicationTime": "2021-12-28T20:17:52Z",
  "modificationTime": "2022-10-27T01:37:00.538891Z",
  "socialTrendAlert": false,
  "severityWithCritical": "medium",
  "from": [
    "com.example:snyk-boot-web@0.0.1-SNAPSHOT",
    "org.apache.logging.log4j:log4j-core@2.15.0"
  ],
  "upgradePath": [
    false,
    "org.apache.logging.log4j:log4j-core@2.17.1"
  ],
  "isUpgradable": true,
  "isPatchable": false,
  "name": "org.apache.logging.log4j:log4j-core",
  "version": "2.15.0"
}
```

### Generating an SBOM from a snyk scan

The snyk sbom command generates an SBOM for a local software project in an ecosystem supported by Snyk. Supported formats include CycloneDX v1.4 (JSON or XML) and SPDX v2.3 (JSON). An SBOM can be generated for all supported Open Source package managers as well as unmanaged software projects.

- Run a command as follows

```shell
$ snyk sbom --format=spdx2.3+json --file=pom.xml | jq
{
  "spdxVersion": "SPDX-2.3",
  "dataLicense": "CC0-1.0",
  "SPDXID": "SPDXRef-DOCUMENT",
  "name": "com.example:snyk-boot-web@0.0.1-SNAPSHOT",
  "documentNamespace": "https://snyk.io/spdx/sbom-",
  "creationInfo": {
    "licenseListVersion": "3.19",
    "creators": [
      "Tool: Snyk Open Source",
      "Organization: Snyk"
    ],
    "created": "2023-06-12T10:17:56Z"
  },
  "packages": [
    {
      "name": "com.example:snyk-boot-web",
      "SPDXID": "SPDXRef-1-com.example-snyk-boot-web-0.0.1-SNAPSHOT",
      "versionInfo": "0.0.1-SNAPSHOT",
      "downloadLocation": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:maven/com.example/snyk-boot-web@0.0.1-SNAPSHOT"
        }
      ]
    },
    {
      "name": "com.h2database:h2",
      "SPDXID": "SPDXRef-2-com.h2database-h2-1.4.200",
      "versionInfo": "1.4.200",
      "downloadLocation": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:maven/com.h2database/h2@1.4.200"
        }
      ]
    },
    {
      "name": "org.apache.logging.log4j:log4j-api",
      "SPDXID": "SPDXRef-3-org.apache.logging.log4j-log4j-api-2.13.3",
      "versionInfo": "2.13.3",
      "downloadLocation": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:maven/org.apache.logging.log4j/log4j-api@2.13.3"
        }
      ]
    },
    
....

    {
      "spdxElementId": "SPDXRef-35-org.springframework.boot-spring-boot-starter-tomcat-2.3.10.RELEASE",
      "relatedSpdxElement": "SPDXRef-41-org.springframework.boot-spring-boot-starter-web-2.3.10.RELEASE",
      "relationshipType": "DEPENDENCY_OF"
    },
    {
      "spdxElementId": "SPDXRef-37-org.springframework-spring-web-5.2.14.RELEASE",
      "relatedSpdxElement": "SPDXRef-41-org.springframework.boot-spring-boot-starter-web-2.3.10.RELEASE",
      "relationshipType": "DEPENDENCY_OF"
    },
    {
      "spdxElementId": "SPDXRef-40-org.springframework-spring-webmvc-5.2.14.RELEASE",
      "relatedSpdxElement": "SPDXRef-41-org.springframework.boot-spring-boot-starter-web-2.3.10.RELEASE",
      "relationshipType": "DEPENDENCY_OF"
    }
  ]
}

```

## Dockerfile scanning

### Scanning a Dockerfile from the CLI

The CLI unlike the SCM integration will not sacn a Dockerfile so to do exactly what the SCM integration does, we would run a command as follows "**snyk container test $(cat Dockerfile | head -n 1 | sed -e 's/FROM\ //')**". The aim is is to extract the FROM clause from the Dockerfile. Keep in mind that multi-stage Dockerfiles would require some tweaking to obtain the right FROM clause

```shell
$ snyk container test $(cat Dockerfile | head -n 1 | sed -e 's/FROM\ //')

Testing openjdk:11.0.13-slim-buster...

✗ Low severity vulnerability found in util-linux/libuuid1
  Description: Integer Overflow or Wraparound
  Info: https://security.snyk.io/vuln/SNYK-DEBIAN10-UTILLINUX-1534833
  Introduced through: util-linux/libuuid1@2.33.1-0.1, e2fsprogs@1.44.5-1+deb10u3, util-linux/mount@2.33.1-0.1, util-linux/fdisk@2.33.1-0.1, util-linux/libblkid1@2.33.1-0.1, util-linux@2.33.1-0.1, sysvinit/sysvinit-utils@2.93-8, util-linux/bsdutils@1:2.33.1-0.1, util-linux/libfdisk1@2.33.1-0.1, util-linux/libmount1@2.33.1-0.1, util-linux/libsmartcols1@2.33.1-0.1
  From: util-linux/libuuid1@2.33.1-0.1
  From: e2fsprogs@1.44.5-1+deb10u3 > util-linux/libuuid1@2.33.1-0.1
  From: e2fsprogs@1.44.5-1+deb10u3 > util-linux/libblkid1@2.33.1-0.1 > util-linux/libuuid1@2.33.1-0.1
  and 25 more...
  Image layer: Introduced by your base image (openjdk:11.0.13-slim-buster)

✗ Low severity vulnerability found in util-linux/libuuid1
  Description: Information Exposure
  Info: https://security.snyk.io/vuln/SNYK-DEBIAN10-UTILLINUX-2401082
  Introduced through: util-linux/libuuid1@2.33.1-0.1, e2fsprogs@1.44.5-1+deb10u3, util-linux/mount@2.33.1-0.1, util-linux/fdisk@2.33.1-0.1, util-linux/libblkid1@2.33.1-0.1, util-linux@2.33.1-0.1, sysvinit/sysvinit-utils@2.93-8, util-linux/bsdutils@1:2.33.1-0.1, util-linux/libfdisk1@2.33.1-0.1, util-linux/libmount1@2.33.1-0.1, util-linux/libsmartcols1@2.33.1-0.1
  From: util-linux/libuuid1@2.33.1-0.1
  From: e2fsprogs@1.44.5-1+deb10u3 > util-linux/libuuid1@2.33.1-0.1
  From: e2fsprogs@1.44.5-1+deb10u3 > util-linux/libblkid1@2.33.1-0.1 > util-linux/libuuid1@2.33.1-0.1
  and 25 more...
  Image layer: Introduced by your base image (openjdk:11.0.13-slim-buster)
  
  ...
  
-------------------------------------------------------

Testing openjdk:11.0.13-slim-buster...

Organization:      apples-demo
Package manager:   maven
Target file:       /usr/local/openjdk-11/lib
Project name:      openjdk:11.0.13-slim-buster:/usr/local/openjdk-11/lib
Docker image:      openjdk:11.0.13-slim-buster
Licenses:          enabled

✔ Tested openjdk:11.0.13-slim-buster for known issues, no vulnerable paths found.


Tested 13 projects, 1 contained vulnerable paths.
  
```

### Uploading the results of a Dockerfile scan to Snyk App

To send these results to Snyk App simply replace "test" with "monitor" using a command as follows "**snyk container monitor --org=getting-started-cli --project-name="openjdk:11.0.13-slim-buster"  $(cat Dockerfile | head -n 1 | sed -e 's/FROM\ //')**".

```shell
$ snyk container monitor --org=getting-started-cli --project-name="openjdk:11.0.13-slim-buster"  $(cat Dockerfile | head -n 1 | sed -e 's/FROM\ //')

Monitoring openjdk:11.0.13-slim-buster (openjdk:11.0.13-slim-buster)...

Explore this snapshot at https://app.snyk.io/org/getting-started-cli/project/be8c0743-21ba-4fd1-ad76-55a417ef1287/history/4146cbcd-5295-46be-add2-3c589d9df523

Notifications about newly disclosed issues related to these dependencies will be emailed to you.
```

![alt tag](https://i.ibb.co/tZZ5QDF/getting-started-7.png)

## Snyk Container demos

The next two examples show how to run a container test and monitor. You can add ignores, add projects tags, output to sarif/html/JSON, as well as set severity-threshold much like open-source scans as detailed below

[Snyk Container test options](https://docs.snyk.io/snyk-cli/commands/container-test)

### Running a container test

- Run a test using a command as follows "**snyk container test pasapples/snyk-boot-web:v1**"

```shell

$ snyk container test pasapples/snyk-boot-web:v1

Testing pasapples/snyk-boot-web:v1...

✗ Low severity vulnerability found in util-linux/libuuid1
  Description: Integer Overflow or Wraparound
  Info: https://security.snyk.io/vuln/SNYK-DEBIAN10-UTILLINUX-1534833
  Introduced through: util-linux/libuuid1@2.33.1-0.1, e2fsprogs@1.44.5-1+deb10u3, util-linux/mount@2.33.1-0.1, util-linux/fdisk@2.33.1-0.1, util-linux/libblkid1@2.33.1-0.1, util-linux@2.33.1-0.1, sysvinit/sysvinit-utils@2.93-8, util-linux/bsdutils@1:2.33.1-0.1, util-linux/libfdisk1@2.33.1-0.1, util-linux/libmount1@2.33.1-0.1, util-linux/libsmartcols1@2.33.1-0.1
  From: util-linux/libuuid1@2.33.1-0.1
  From: e2fsprogs@1.44.5-1+deb10u3 > util-linux/libuuid1@2.33.1-0.1
  From: e2fsprogs@1.44.5-1+deb10u3 > util-linux/libblkid1@2.33.1-0.1 > util-linux/libuuid1@2.33.1-0.1
  and 25 more...
  
...

✗ Critical severity vulnerability found in dpkg
  Description: Directory Traversal
  Info: https://security.snyk.io/vuln/SNYK-DEBIAN10-DPKG-2847944
  Introduced through: meta-common-packages@meta
  From: meta-common-packages@meta > dpkg@1.19.7
  Fixed in: 1.19.8



Organization:      apples-demo
Package manager:   deb
Project name:      docker-image|pasapples/snyk-boot-web
Docker image:      pasapples/snyk-boot-web:v1
Platform:          linux/amd64
Base image:        openjdk:11.0.13-slim-buster
Licenses:          enabled

Tested 91 dependencies for known issues, found 101 issues.

Base Image                   Vulnerabilities  Severity
openjdk:11.0.13-slim-buster  101              9 critical, 18 high, 10 medium, 64 low

Recommendations for base image upgrade:

Minor upgrades
Base Image                   Vulnerabilities  Severity
openjdk:11.0.16-slim-buster  91               6 critical, 13 high, 8 medium, 64 low

Alternative image types
Base Image                      Vulnerabilities  Severity
openjdk:21-slim-bullseye        48               0 critical, 0 high, 0 medium, 48 low
openjdk:21-ea-16-slim-bullseye  48               0 critical, 0 high, 0 medium, 48 low
openjdk:21-ea-14-slim-bullseye  48               0 critical, 0 high, 0 medium, 48 low
openjdk:21-ea-15-slim-bullseye  48               0 critical, 0 high, 0 medium, 48 low


Learn more: https://docs.snyk.io/products/snyk-container/getting-around-the-snyk-container-ui/base-image-detection

-------------------------------------------------------

Testing pasapples/snyk-boot-web:v1...

Tested 41 dependencies for known issues, found 35 issues.


Issues to fix by upgrading:

  Upgrade ch.qos.logback:logback-core@1.2.3 to ch.qos.logback:logback-core@1.2.7 to fix
  ✗ Insufficient Hostname Verification [Medium Severity][https://security.snyk.io/vuln/SNYK-JAVA-CHQOSLOGBACK-1726923] in ch.qos.logback:logback-core@1.2.3
    introduced by ch.qos.logback:logback-core@1.2.3

...

License issues:

  ✗ Dual license: MPL-2.0, EPL-1.0 (new) [Medium Severity][https://snyk.io/vuln/snyk:lic:maven:com.h2database:h2:(MPL-2.0_OR_EPL-1.0)] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200

  ✗ EPL-1.0 OR LGPL-2.1 license (new) [Medium Severity][https://snyk.io/vuln/snyk:lic:maven:ch.qos.logback:logback-core:EPL-1.0_OR_LGPL-2.1] in ch.qos.logback:logback-core@1.2.3
    introduced by ch.qos.logback:logback-core@1.2.3

  ✗ EPL-1.0 OR LGPL-2.1 license (new) [Medium Severity][https://snyk.io/vuln/snyk:lic:maven:ch.qos.logback:logback-classic:EPL-1.0_OR_LGPL-2.1] in ch.qos.logback:logback-classic@1.2.3
    introduced by ch.qos.logback:logback-classic@1.2.3



Organization:      apples-demo
Package manager:   maven
Target file:       /app
Project name:      pasapples/snyk-boot-web:v1:/app
Docker image:      pasapples/snyk-boot-web:v1
Licenses:          enabled

....

```

To ignore issues using a "**.snyk**" file you can use the CLI to generate the ignores as described here

[Ignore vulnerabilities using Snyk CLI](https://docs.snyk.io/snyk-cli/test-for-vulnerabilities/ignore-vulnerabilities-using-snyk-cli)

### Uploading container test result

- Run a monitor with a command as follows "**snyk container monitor --org=getting-started-cli pasapples/snyk-boot-web:v1**"

```shell
$ snyk container monitor --org=getting-started-cli pasapples/snyk-boot-web:v1

Monitoring pasapples/snyk-boot-web:v1 (docker-image|pasapples/snyk-boot-web)...

Explore this snapshot at https://app.snyk.io/org/getting-started-cli/project/e4e052ee-2126-4cae-9013-2a2dfe7db1f8/history/e98c3e77-ee78-4201-a8b5-4ab795e554f7

Notifications about newly disclosed issues related to these dependencies will be emailed to you.


-------------------------------------------------------

Monitoring pasapples/snyk-boot-web:v1 (docker-image|pasapples/snyk-boot-web:/app)...

Explore this snapshot at https://app.snyk.io/org/getting-started-cli/project/14cb57a6-fcc5-463f-8b34-34ae7c6a873a/history/af202d53-ed2c-450b-8d43-03b75bba9aae

Notifications about newly disclosed issues related to these dependencies will be emailed to you.

```

![alt tag](https://i.ibb.co/CzvVq2v/getting-started-8.png)

_Note: sarif, JSON and HTML output is also available with container scanning like open-source scans allow_

## Snyk Code demos

### Running a code scan

Running a SAST code scan is don eusing a command as follows "**snyk code test**" make sure your organization you connect to has Snyk Code enabled.

_Note: The ability to upload results from the CLI is currently not available but is coming soon_

```shell
$ snyk code test

Testing /Users/pasapicella/snyk/SE/getting-started/snyk-boot-web ...

 ✗ [High] Use of Hardcoded, Security-relevant Constants
   Path: src/main/java/com/example/snykbootweb/DatabaseService.java, line 8
   Info: Avoid hardcoding values that are meant to be secret. Found hardcoded secret.

 ✗ [High] SQL Injection
   Path: src/main/java/com/example/snykbootweb/jdbc/CustomerRest.java, line 29
   Info: Unsanitized input from the request URL flows into query, where it is used in an SQL query. This may result in an SQL Injection vulnerability.


✔ Test completed

Organization:      apples-demo
Test type:         Static code analysis
Project path:      /Users/pasapicella/snyk/SE/getting-started/snyk-boot-web

Summary:

  2 Code issues found
  2 [High]
```

_Note: sarif, JSON and HTML output is also available with code SAST scanning like open-source scans allow_

To ignore files / directories from code SAST scans follow this guide

[Excluding directories and files from the Snyk Code CLI test](https://docs.snyk.io/scan-application-code/snyk-code/cli-for-snyk-code/excluding-directories-and-files-from-the-snyk-code-cli-test)

### Converting a code scan to HTML

- Run the following commands to generate a HTML file for the code scan results

```shell
$ snyk code test --json | snyk-to-html -o snyk-boot-web-sast-result.html
Vulnerability snapshot saved at snyk-boot-web-sast-result.html
```

### Publishing CLI results to a Snyk Project

Note: This is a closed BETA so please let your SE know if you want this enabled

- Run the following command to publish CLI results to Snyk App

```shell
$ snyk code test --report --project-name="snyk-boot-web-code-monitor" --org=getting-started-cli --remote-repo-url="https://github.com/papicella/snyk-boot-web"

Testing /Users/pasapicella/snyk/customers/anz/woolworths/training-sessions/demo/snyk-boot-web ...

 ✗ [High] SQL Injection
   ID: 90c0854c-9a27-4e78-9ece-9b6f0f44786e
   Path: src/main/java/com/example/snykbootweb/jdbc/CustomerRest.java, line 29
   Info: Unsanitized input from the request URL flows into query, where it is used in an SQL query. This may result in an SQL Injection vulnerability.

 ✗ [High] Use of Hardcoded, Security-relevant Constants
   ID: 041b735c-46ad-432b-bf75-421b9a78f260
   Path: src/main/java/com/example/snykbootweb/DatabaseService.java, line 8
   Info: Avoid hardcoding values that are meant to be secret. Found hardcoded secret.


✔ Test completed

Organization:      getting-started-cli
Test type:         Static code analysis
Project path:      /Users/pasapicella/snyk/customers/anz/woolworths/training-sessions/demo/snyk-boot-web

Summary:

  2 Code issues found
  2 [High]

Code Report Complete

Your test results are available at:
https://app.snyk.io/org/getting-started-cli/project/...../history/....
```

More information is here [Publishing CLI results to a Snyk Project](https://docs.snyk.io/scan-application-code/snyk-code/cli-for-snyk-code/publishing-cli-results-to-a-snyk-project-and-ignoring-cli-results)

![alt tag](https://i.ibb.co/Qb6vH4Z/getting-started-11.png)

## Snyk IaC demos

### Run an IaC scan of a terraform template

- Let's start by running an IaC scan using a command as follows "**snyk iac test ./terraform/main.tf**"

```shell
$ snyk iac test ./terraform/main.tf

Snyk Infrastructure as Code

✔ Test completed.

Issues

Low Severity Issues: 3

  [Low] S3 bucket versioning disabled
  Info:    S3 bucket versioning is disabled. Changes or deletion of objects will
           not be reversible
  Rule:    https://snyk.io/security-rules/SNYK-CC-TF-124
  Path:    resource > aws_s3_bucket[s3_bucket_myapp] > versioning > enabled
  File:    ./terraform/main.tf
  Resolve: For AWS provider < v4.0.0, set `versioning.enabled` attribute to
           `true`. For AWS provider >= v4.0.0, add aws_s3_bucket_versioning
           resource.

  [Low] S3 bucket MFA delete control disabled
  Info:    S3 bucket will not enforce MFA login on delete requests. Object could
           be deleted without stronger MFA authorization
  Rule:    https://snyk.io/security-rules/SNYK-CC-TF-127
  Path:    resource > aws_s3_bucket[s3_bucket_myapp] > versioning > mfa_delete
  File:    ./terraform/main.tf
  Resolve: Follow instructions in `https://docs.aws.amazon.com/AmazonS3/latest/u
           serguide/MultiFactorAuthenticationDelete.html` to manually configure
           the MFA setting. For AWS provider < v4.0.0 set
           `versioning.mfa_delete` attribute to `true` in aws_s3_bucket
           resource. For AWS provider >= v4.0.0 set
           'versioning_configuration.mfa_delete` attribute to `Enabled`. The
           terraform change is required to reflect the setting in the state file

  [Low] S3 server access logging is disabled
  Info:    The s3 access logs will not be collected. There will be no audit
           trail of access to s3 objects
  Rule:    https://snyk.io/security-rules/SNYK-CC-TF-45
  Path:    input > resource > aws_s3_bucket[s3_bucket_myapp] > logging
  File:    ./terraform/main.tf
  Resolve: For AWS provider < v4.0.0, add `logging` block attribute. For AWS
           provider >= v4.0.0, add aws_s3_bucket_logging resource.

Medium Severity Issues: 1

  [Medium] Non-encrypted S3 Bucket
  Info:    Non-encrypted S3 Bucket. A non-encrypted S3 bucket increases the
           likelihood of unintentional data exposure
  Rule:    https://snyk.io/security-rules/SNYK-CC-TF-4
  Path:    input > resource > aws_s3_bucket[s3_bucket_myapp]
  File:    ./terraform/main.tf
  Resolve: For AWS provider < v4.0.0, set `server_side_encryption_configuration`
           block attribute. For AWS provider >= v4.0.0 add
           aws_s3_bucket_server_side_encryption_configuration resource.

High Severity Issues: 1

  [High] S3 block public ACLs control is disabled
  Info:    Bucket does not prevent creation of public ACLs. Anyone who can
           manage bucket's ACLs will be able to grant public access to the
           bucket
  Rule:    https://snyk.io/security-rules/SNYK-CC-TF-95
  Path:    resource > aws_s3_bucket[s3_bucket_myapp]
  File:    ./terraform/main.tf
  Resolve: Set the `aws_s3_bucket_public_access_block` `block_public_acls` field
           to true.

-------------------------------------------------------

Test Summary

  Organization: apples-demo
  Project name: papicella/snyk-boot-web

✔ Files without issues: 0
✗ Files with issues: 1
  Ignored issues: 0
  Total issues: 5 [ 0 critical, 1 high, 1 medium, 3 low ]

-------------------------------------------------------

Tip

  New: Share your test results in the Snyk Web UI with the option --report
```

### Send a report of an IaC scan of a terraform template to Snyk App UI

- Run a command as follows "snyk iac test ./terraform/main.tf --report --org=getting-started-cli"

```shell
$ snyk iac test ./terraform/main.tf --report --org=getting-started-cli

Snyk Infrastructure as Code

✔ Test completed.

...

-------------------------------------------------------

Test Summary

  Organization: getting-started-cli
  Project name: papicella/snyk-boot-web

✔ Files without issues: 0
✗ Files with issues: 1
  Ignored issues: 0
  Total issues: 5 [ 0 critical, 1 high, 1 medium, 3 low ]

-------------------------------------------------------

Report Complete

  Your test results are available at: https://snyk.io/org/getting-started-cli/projects
  under the name: papicella/snyk-boot-web
```

![alt tag](https://i.ibb.co/zst1cCH/getting-started-10.png)

_Note: sarif, JSON and HTML output is also available with IaC scanning like open-source scans allow_

To ignore issues using a "**.snyk**" file you can use the CLI to generate the ignores as described here

[Ignore vulnerabilities using Snyk CLI](https://docs.snyk.io/snyk-cli/test-for-vulnerabilities/ignore-vulnerabilities-using-snyk-cli)

<hr />
Pas Apicella [pas at snyk.io] is a Principal Solution Engineer at Snyk APJ
