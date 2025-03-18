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

- [ ] TODO: Describe how the tests are categorised to user flow and technical details and further down to different types of technical components
- [ ] TODO: Describe how to approach the testing using the plan, the categorised test cases, the `level` shown, and files as features

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
**About the design**
The `Level` indicates how deep the listed component is in the call stack from the feature. For example, `level: 1` means the component is a direct descendant. `Level: 3` means the component is a grand-grand-child of the feature. This is intended to help you in determining what to focus on. The design assumes the deeper the component goes, the more it becomes an implementation detail. However, sometimes the implementation details are the most important. This is why all affected components are highlighted. Furthermore, with some technology stacks and naming conventions the cases are divided into `User flow` and `Technical details`. As an example, if the codebase contains JSX (*.jsx, *.tsx) files, these are assumed to be user facing components. The testing rounds focus first on the components that a user can directly use. As sometimes even JSX files are actually very technical in nature, they may be categorised as utility or state modules, for example. In such situations the modules are automatically moved to the Technical Details grouping.

  
<br clear="right"/>

- [ ] TODO 6: 

### How do I configure Concordant?

- [ ] TODO: Describe how to create feature rules and diff configurations
- [ ] TODO: Describe how to set the project purpose

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
