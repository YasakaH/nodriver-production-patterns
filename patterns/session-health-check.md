# Session Health Check

## Problem

A profile can exist, cookies can exist, Chrome can launch — and authentication can still be dead. Sessions expire, tokens rotate, sites invalidate access.

## Rules

1. **Validate before working.** Check session health before starting the real job, not after it fails.
2. **Redirects are the signal.** A logged-in-only page redirecting to a login URL means the session is dead.
3. **Re-authentication is normal.** Treat it as part of the lifecycle, not a surprise.

## Example

```python
async def session_is_valid(browser, check_url: str) -> bool:
    page = await browser.get(check_url)
    return page.url != LOGIN_URL      # redirected → session is dead
```

## Related

- `browser-profile-management.md`
- `production-readiness.md`
