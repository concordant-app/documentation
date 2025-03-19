# Sentry example

<img src="https://github.githubassets.com/assets/GitHub-Mark-ea2971cee799.png" valign="middle" width="20" height="20">[Sentry's codebase](https://github.com/getsentry/sentry)

## Performance

**State**
- _Concordant 1.0.0_
- _Sentry codebase state in March 2025_
- _Macbook Air M3_

**Result**
On a Macbook Air M3 the example configurations runs a full reload in about 10s. Without configuration from 30s-60s depending on the amount of effects in the codebase. In general, smaller changesets run faster.

Memory usage varies between 1GB-10GB depending on the amount of components. 

At the time of the latest benchmark, the example configuration produced nearly 700 components, and a run without a configuration produced nearly 7000 components.


| Resource      | Example result | Cold start result |
| ------------- | -------------- | ----------------- |
| Time          | 10s            | 30s-60s           |
| Memory        | 1GB            | 10GB              |
| Components    | 700            | 7000              |
| Dependencies  | 52 000         | 52 000            |


## Example `test.plan.json` configuration:

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
    "excludes": ["**/resources/templates/**"],
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
      },
      {
        "alias": "Alerts 🚨",
        "matchers": ["**/*alert*/**/*.tsx", "**/*{alert}*.tsx"]

      }
    ]
  }
}
```
