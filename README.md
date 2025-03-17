# Documentation: Concordant.app
How to use and configure [Concordant.app](https://concordant.app) in your workflows.

**Quick start**
1. **[Download Concordant.app](https://web.crabnebula.cloud/concordant/concordant/releases)**
2. Open your local repository in Concordant
3. Make a code change
4. Reload to get a testing plan
5. Configure `test.plan.json` to suit your needs





---
## The `Effects` of Your `Code Changes` as a `Testing Plan`

![Screenshot of an example testing round from Concordant with testing details visible.](./testing%20round%20details%20screenshot.png)


---

**Table of Contents**
1. What are `Effects`?
2. What is a `Code Change`?
3. What is a `Testing Plan`?
4. How do I configure Concordant?
5. Which technologies does Concordant support?

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

See how some **changes** become multiplied as **effects**. This is why Concordant was created.  

> Note: Using files as the module representation is an optimisation on multiple levels. More on this topic in the Testing Plan guide. (TODO 3)

  
<br clear="right"/>


- [ ] TODO 1: Add link to supported technologies guide configuration guide.
- [ ] TODO 2: Add link to dependency configuration guide.
- [ ] TODO 3: Add link to testing plan guide configuration guide.


---

### What is a `Code Change`?

- [ ] TODO: Describe how changes are are extracted based on changes files using git diff configurations

### What is a `Testing Plan`?

- [ ] TODO: Describe how the testing plan is formed based on feature rules and effects
- [ ] TODO: Describe how the tests are categorised to user flow and technical details and further down to different types of technical components
- [ ] TODO: Describe how to approach the testing using the plan, the categorised test cases, the `level` shown, and files as features

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
- [ ] TODO: `tsconfig.json? (TypeScript compiler)
- [ ] TODO: `package.json` (JavaScript variants )

---

> Note: This documentation is provided with an open source license, whereas the app itself is closed source and commercial.
