# Documentation: Concordant.app

**Concordant: To be in harmony within one's intentions and actions.**

<br />

How to use and configure [Concordant.app](https://concordant.app) in your workflows.

**Quick start**
1. **[Download Concordant.app](https://web.crabnebula.cloud/concordant/concordant/releases)**
2. Open your local repository in Concordant
3. Make a code change
4. Reload to get a testing plan
5. Configure `test.plan.json` to suit your needs

<br />


## The `Effects` of Your `Code Changes` as a `Testing Plan`

<br />

![Screenshot of an example testing round from Concordant with testing details visible.](./testing%20round%20details%20screenshot.png)


---

**Table of Contents**
1. What are `Effects`?
2. What is a `Code Change`?
3. What is a `Testing Plan`?
4. How do I configure Concordant?
5. Which technologies does Concordant support?

- [ ] TODO 5: Add links to the sections

### What are `Effects`?


Effects are modules, files, features or test cases that have been affected by changes within the currently configured diff.

There are two types of effects:
- **Changed**: a file that has been changed is also an effect
- **Affected**: a file that has a dependency to another file that has been affected or changed

Concordant uses files to represent modules, modules are be mapped into features, and affected features become test cases within the test round. All the effects of the current diff are calculated using file-based module dependencies, such as:
```
import { Something } from './another-file'
```
These dependencies are extracted from the code using language specific import clauses (TODO 1). More dependencies can also be added by hand (TODO 2). See more in the Configuration guide. 

<img align="right" width="50%" height="50%" src="./change%20effects%20screenshot.png">

<br />
<br />

> See how some **changes** become multiplied as **effects**. This is why Concordant was created.  
> 
> Note: Using files as the module representation is an optimisation on multiple levels. More on this topic in the Testing Plan guide. (TODO 3)
> 

  
<br clear="right"/>


- [ ] TODO 1: Add link to supported technologies guide configuration guide.
- [ ] TODO 2: Add link to dependency configuration guide.
- [ ] TODO 3: Add link to testing plan guide configuration guide.

<br />

### What is a `Code Change`?

Changes are files that have been changed based on a Git diff. 

There are two types of changes:
- **Uncommitted**: a file that has been changed locally - essentially uncommitted changes 
- **Committed**: a file that has been changed when comparing the current state of the code to a target older commit

Concordant considers changes always on a file level, just as effects. The list of changes is always created as a combination of the local uncommitted changes and the committed changes based on the change configuration. If no change configuration is provided, the default is the current branch vs the latest upstream state of the branch. Read more in the configuration guide. (TODO 4)


- [ ] TODO 4: Add link to diff configuration guide.

<br />

### What is a `Testing Plan`?

<br />

A testing plan is a fusion of features, effects, configuration and tasks. Based on configured feature rules, effects activate features into test cases on the next test round. The test round represents a partial test plan, focused and filtered down to only show the test cases that have been activated by effects. The Test Round itself is a list of tasks where you can drill down to get more details on which parts of a feature have been affected and why.

<img align="right" width="50%" height="50%" src="./testing%20round%20screenshot.png">

<br />
<br />

Effects activate parts of the testing plan and produce a test round.

  
<br clear="right"/>

<img align="left" width="50%" height="50%" src="./feature%20rules%20screenshot.png">

<br />
<br />

The test plan, and therefore the test round, is created with feature configurations. The feature configurations are glob matchers to files, which means your naming conventions and project structures are meaningful. 

  
<br clear="left"/>

<img align="right" width="50%" height="50%" src="./testing%20round%20details%20screenshot.png">

<br />
<br />

Affected files become test cases inside test suites. They may be further categorised based on configurations and technology assumptions. 
<br />
  
<br clear="right"/>
<br />
<br />

**About the design**
<br />
The `Level` indicates how deep the listed component is in the dependency hierarchy from the feature. For example, `level: 1` means the component is a direct descendant. `Level: 3` means the component is a grand-grand-child of the feature. This is intended to help you in determining what to focus on. The design assumes the deeper the component goes, the more it becomes an implementation detail. However, sometimes the implementation details are the most important. This is why all affected components are visible. 
<br />
Furthermore, with some technology stacks and naming conventions the cases are divided into `User flow` and `Technical details`. As an example, if the codebase contains JSX (*.jsx, *.tsx) files, these are assumed to be user facing components. The testing rounds focus first on the components a user can directly use. As sometimes even JSX files are actually very technical in nature, they may be categorised as utility or state modules, for example. In such situations the modules are automatically moved to the Technical Details grouping.


### How do I configure Concordant?


- [ ] TODO: Describe how to set additional dependencies manually

Here's a configuration template using <img src="https://github.githubassets.com/assets/GitHub-Mark-ea2971cee799.png" valign="middle" width="20" height="20">[Sentry's codebase](https://github.com/getsentry/sentry) as an example.
```
{
  "name": "Sentry Fair Source codebase",
  "purpose": {
    "primary": "Code breaks, fix it faster",
    "secondary": "with application monitoring"

  },
  "config": {
    "changes": {
      "old": "HEAD",
      "new": "HEAD@{upstream}"
    },
    "features": [

      {
        "alias": "App Homepage 👋 ",
        "matchers": ["static/app/views/app/index.tsx"]
      },

      {
        "alias": "Performance 🚀 ",
        "matchers": ["static/app/views/performance/**/*.tsx"]
      },
      {
        "alias": "Profiling 🔬 ",
        "matchers": ["static/app/views/profiling/**/*.tsx"]
      },
      {
        "alias": "Views 📺",
        "matchers": ["static/app/views/**/index.tsx"]
      }
      ,
      {
        "alias": "Subscriptions & Billing 🏦",
        "matchers": ["**/*subscription*/**/*.tsx", "**/*{subscription}*.tsx"]
      }
    ]
  }
}

```

#### Purpose
Use the purpose configuration to set the intention of the project. This helps you align the configurations and testing actions. 

#### Changes
Use Git's commit hashes, branch notation and shortcuts to define the start and end of diffing. If it works on with `git diff <old>..<new>`, it should work here. 

**Examples**

Diff between current state of the current brach vs current state of this branch on the remote (e.g. PR vs target branch)
```
"changes": {
      "old": "HEAD",
      "new": "HEAD@{upstream}"
    }
```

Diff between specific commits (e.g. Previous release vs Upcoming release)
```
"changes": {
      "old": "abcdefg",
      "new": "hijklmn"
    }
```

Diff between branches
```
"changes": {
      "old": "main",
      "new": "hotfix/critical-production-bug"
    }
```

<br />

Note: The diffing system uses your local git repository, meaning you may have to fetch it to get the most accurate diff to remote origins.

#### Features


Features are defined as sets of glob matchers to filenames and paths from your repository's root. The intention is to set define that are important with rules that make testing easier. Think in terms of what are the major view, pages or components of your application. These become your test suites, which in turn contain all the affected components automatically. Thus, you don't necessarily need to have rules for all features, as long as they are part of some bigger feature. 

If you want to be sure, you can set your index page as an entrypoint. This way you always catch everything underneath. However, this doesn't work for architectures where the index isn't actually depending on the other pages. An example could be a system where the routes are generated from directory structures and the pages themselves link to these paths rather than to other UI components.

It is possible to set a catch-all wildcard too. The more rules, and the more files they match, the more time it takes to analyse the codebase. Rules matching to several thousand components can be analysed in less than half a minute. See more about performance and deeper insights into how to configure in useful ways in our example case studies. (TODO 6)


**Examples**

Defining a specific file
```
"features": [

  {
    "alias": "App Homepage 👋 ",
    "matchers": ["static/app/views/app/index.tsx"]
  },
]
```

Multiple matchers for the feature
```
"features": [

  {
    "alias": "View & Pages",
    "matchers": ["**/views/**/*.tsx", "**/views/**/*.tsx",]
  },
]
```

Being specific with the filename (i.e. don't match to just the first appearance of 'view')
```
"features": [

  {
    "alias": "View & Pages",
    "matchers": ["**/views/**/*{View}.tsx",]
  },
]
```

Catching every JSX component
```
"features": [

  {
    "alias": "Catch-all (Legacy code safety net)",
    "matchers": ["**/*.jsx", "**/*.tsx"]
  },
]
```

**Note: The globs are treated as case-insensitive.**


#### Additional Dependencies

One of the main inspirations for creating Concordant was the mysterious nature of breaking some faraway features with a seemingly unintentional change. This is naturally solved by implementing a dependency analysis of the codebase. However, sometimes there is no dependency in the code. You can use `dependencies.json` in the root of your project to inject additional dependencies to the analysis. This is how we can overcome the missing dependencies between, for example, a JavaScript frontend and a Python backend.

The file content needs to be a valid json array as shown below.

**Examples**

Dependency format
```
[
  {
    "source": "some/file",
    "target": "the/other/file"
  }
]
```

UI => API fetch calls
```
[
  {
    "source": "src/ui/pages/SomeController.ts",
    "target": "src/backend/api/SomeApi.ts"
  },
  {
    "source": "src/ui/hooks/AppStateProvider.tsx",
    "target": "src/backend/api/state/index.ts"
  }
]
```

- TODO 6: Add a link to example case studies.

### Which technologies does Concordant support?

- [ ] TODO: Describe how different supported technologies are taken into account
- [ ] TODO: Describe how supported technologies are assured for quality
**Programming Languages**
- [ ] TODO: Typescript/JavaScript (*.ts, *.js)

**Frameworks**
- [ ] TODO: React (*.tsx, *.jsx)
- [ ] TODO: SolidJS (*.tsx, *.jsx)
- [ ] TODO: VueJS (.vue)

**Project & Build Configurations**
- [ ] TODO: `tsconfig.json` (TypeScript compiler)
- [ ] TODO: `package.json` (JavaScript variants )

---

> Note: This documentation is provided with an open source license, whereas the app itself is closed source and commercial.
