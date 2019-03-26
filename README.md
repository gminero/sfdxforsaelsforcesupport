## Joe Coffee Project

![JoeCoffeeLogo](JoesLogo.png)

Joes Coffee is a sample application that is used by Coveo for onboarding partners. It allows partners to demonstrate their development & resourcefullness skills while learning to do a basic Coveo implementation. Joes Coffee is a fictitious Coffee Shop with a striving community that helps Joe manage his online community for FAQ's and offers them a rich user experience while using Coveo as their main community Search.

## Table of contents

-   Installation Instructions

    -   [Setting up Joe Coffee using Salesforce DX](#setting-up-JoeCoffee-using-salesforce-dx)


-   [Project Walkthrough](#project-walkthrough)

## Installation Instructions

-   [Seting up your Environment for JoeCoffee using Salesforce DX](#setting-up-JoeCoffee-using-salesforce-dx): This is the recommended setup. Use this option if you are a developer.
-   [Seting up your Environment for JoeCoffee using a Developer Org](#setting-up-JoeCoffee-using-a-developer-org): This option allows anybody to go through the project.

## Pre-requisites
1. This project assumes you are familair with version control, Git and Github.
    -   In order to get familiar with the basics, follow the steps in the [Git and GitHub Basics](https://trailhead.salesforce.com/en/content/learn/modules/git-and-git-hub-basics) Trailhead module.

## Seting up your Environment for Joes Coffee using Salesforce DX

0. Get Started with Visual Studio Code. Follow the steps in the [Quick Start: Visual Studio Code for Salesforce Development](https://trailhead.salesforce.com/content/learn/projects/quickstart-vscode-salesforce) Trailhead project. The steps include:

-  Install Visual Studio Code
-  Install the Salesforce CLI
-  Use VS Code for Salesforce DEvelopment  

1. Set up your environment. Follow the steps in the [Quick Start: App Development with Salesforce DX](https://trailhead.salesforce.com/en/content/learn/modules/sfdx_app_dev) Trailhead module. The steps include:

-   Salesforce DX
-   Create an App
-   Build an App Using the Salesfsorce CLI
-   Convert and Deploy an Existing App

2. Authenticate with your hub org and provide it with an alias (**myDevHub** in the command below):

```
sfdx force:auth:web:login -d -a myDevHub
```

3. Clone the repository:

```
git clone https://github.com/gminero/joe-coffee.git
cd joe-cofee
```

4. Create a scratch org and provide it with an alias (**joescoffee** in the command below):

```
sfdx force:org:create -s -f config/project-scratch-def.json -a joescoffee
```

5. Under the siteAdmin force-app/main/default/sites/Joes_Coffee.site-meta.xml, Assign your scratchorg's user to the **siteAdmin** XML node 

```
<siteAdmin>SratchOrgUserName</siteAdmin>
```

6. Push the app to your scratch org:

```
sfdx force:source:push
```

7. In **Setup**, under **User**, activate the **Knowledge User** setting.

8. Ensure that the Sys admin Profile has read/write access to the cusotm fields (origin_url__c, long_summary__c, topic__c)

9. Load sample Knowledge Articles:

```
sfdx force:data:tree:import --plan ./data/sample-data-plan.json
```

10. Open the scratch org:

```
sfdx force:org:open
```

## Seting up your Environment for Joes Coffee using a Developer Org

1. [Sign up](https://developer.salesforce.com/signup) for a Developer Edition (DE) org.

2. Enable MyDomain in your DE org. Instructions to do this are [here](https://trailhead.salesforce.com/modules/identity_login/units/identity_login_my_domain).

3. In **Setup**, under **User**, activate the **Knowledge User** setting..

4. In **Setup**, under **Knowledge**, Enable Lightning Knowledge and create the fields as specified in the project guide.

5. Import Knowledge data Using Salesforce's API:

-   Use the Knowledge__cs JSON file from the data folder. 
-   Using Salesforce's API, Uploade the data [Lightning Platform API Basics](https://trailhead.salesforce.com/en/content/learn/modules/api_basics).
-   After having uploaded the content, th articles will still need to be published, this can be easily achieved using APEX.


## Optional Installation Instructions

This repository contains several files that are relevant if you want to integrate modern web development tooling to your development processes, or to your continuous integration/continuous deployment processes.

### Code formatting

[Prettier](https://prettier.io/) is a code formatter used to ensure consistent formatting across your code base. To use Prettier with Visual Studio Code, install [this extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) from the Visual Studio Code Marketplace. The [.prettierignore](/.prettierignore) and [.prettierrc](/.prettierrc) files are provided as part of this repository to control the behavior of the Prettier formatter.

### Code linting

[ESLint](https://eslint.org/) is a popular JavaScript linting tool used to identify stylistic errors and erroneous constructs. To use ESLint with Visual Studio Code, install [this extension](https://marketplace.visualstudio.com/items?itemName=salesforce.salesforcedx-vscode-lwc) from the Visual Studio Code Marketplace. The [.eslintignore](/.eslintignore) file is provided as part of this repository to exclude specific files from the linting process in the context of Lighning Web Components development.

### Pre-commit hook

This repository also comes with a [package.json](./package.json) file that makes it easy to set up a pre-commit hook that enforces code formatting and linting by running Prettier and ESLint every time you `git commit` changes.

To set up the formatting and linting pre-commit hook:

1. Install [Node.js](https://nodejs.org) if you haven't already done so
2. Run `npm install` in your project's root folder to install the ESLint and Prettier modules (Note: Mac users should verify that Xcode command line tools are installed before running this command.)

Prettier and ESLint will now run automatically every time you commit changes. The commit will fail if linting errors are detected. You can also run the formatting and linting from the command line using the following commands (check out [package.json](./package.json) for the full list):

```
npm run lint:lwc
npm run prettier
```
