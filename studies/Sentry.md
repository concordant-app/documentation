# Sentry example

Example test plan configuration:
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
