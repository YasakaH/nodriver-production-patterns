# nodriver Production Patterns

A collection of patterns for building reliable Python browser automation with [nodriver](https://github.com/ultrafunkamsterdam/nodriver).

Covers:

- ✓ persistent browser profiles
- ✓ session validation
- ✓ retry strategies
- ✓ browser recovery
- ✓ profile isolation

## Structure

```
patterns/
├── browser-profile-management.md
├── session-health-check.md
├── retry-with-backoff.md

checklists/
└── production-readiness.md
```

## Getting started

```python
import nodriver

browser = await nodriver.start(user_data_dir="./profiles/job-1")
```

## Articles

Full explanations of the patterns behind the failures these recipes prevent:

- Why browser profiles break (and how to fix them):
  https://versatilesparks.qzz.io/blog/why-browser-profiles-break
- 5 mistakes new nodriver users make (and how to avoid them):
  https://versatilesparks.qzz.io/blog/5-mistakes-nodriver-beginners

## License

MIT

## Related

The complete production implementation is available in:

Python Browser Automation Cookbook
https://gum.co/python-browser-automation-cookbook
