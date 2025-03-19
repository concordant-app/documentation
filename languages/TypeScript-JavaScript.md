# Typescript & JavaScript support

We support various import statements, including require.

## Import statements
Here's a non-exhaustive list of the variations we support.


```
// Various "import from" statements

import * from 'module';

import { Something } from 'module';

import { 
Something,
SomethingElse,
AnotherThing
} from 'module';

import 'module';
  
// Various "import()" statements

const SomeModule = import('module')

// Various "require()" statements

const point = require('module')
```

## Supported project configurations


### `tsconfig.json`

Used fields
- `compilerOptions.paths` for resolving extracted module import paths
- `extends` for merging `compilerOptions.paths` from multiple files


### `package.json`
- `dependencies` and `devDependencies` are read and used to filter 3rd party library dependencies out of the extracted imports, optimising the analysis

## Known problems ❌

1. ❌ Import statements that are using variables in the path of the module cannot be resolved as the code is never executed.

```
let runtime_module_path = (process.env.NODE_ENV === 'development') ? "./mocks/" : "./api/external/";
const module = import(`${runtime_module_path}/service-module`);
```

Workaround: Use `dependencies.json` to mitigate critical blindspots.

2. ❌ Package.json import aliases are not supported. Workaround: Use `dependencies.json` to mitigate critical blindspots.
3. ❌ `fetch()` and similar calls to APIs or URLs are not automatically mapped to modules. Workaround: Use `dependencies.json` to mitigate critical blindspots.

## Supported frameworks

`.tsx` and `.jsx` files are by default assumed to be TypeScript/JavaScript files and are included in the processing. They are further considered as `User flow test cases` by default. If a framework is specified here, it means at least one project built with that framework is part of the quality assurance activities of that language, and has been deemed correctly extracted.

### React 

`.tsx` and `.jsx` support

### SolidJS

`.tsx` and `.jsx` support

### VueJS
`.vue` files are treated as TypeScript/JavaScript files and go through the same extraction. `.vue` files are also considered as `User flow test cases` by default.
