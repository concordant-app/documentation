# Typescript & JavaScript support

We support various import statements, including require.

## Import statements
TODO: List known import statement styles

TODO: List tsconfig.json fields that are used

## Known problems ❌

1. ❌ Import statements that are using variables in the path of the module cannot be resolved as the code is never executed.

```
let runtime_module_path = (process.env.NODE_ENV === 'development') ? "./mocks/" : "./api/external/"
const module = import(`${runtime_module_path}/service-module`
```

**Workaround: Use `dependencies.json` to mitigate critical blindspots.** 
