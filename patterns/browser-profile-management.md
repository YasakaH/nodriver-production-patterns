# Browser Profile Management

## Problem

Browser profiles are state, not folders. They contain cookies, local storage, IndexedDB, preferences, and session data — and Chrome locks the directory while a browser is running.

## Rules

1. **One profile directory per instance.** Never share a `user_data_dir` between browsers.
2. **Derive profile paths from task IDs** so jobs are isolated and failures don't cascade.
3. **Check for stale locks.** `SingletonLock` may remain after a crash; clean it before launch.

## Example

```python
from pathlib import Path

def profile_for(task_id: str) -> str:
    profile_dir = Path(f"./profiles/task-{task_id}")
    profile_dir.mkdir(parents=True, exist_ok=True)
    return str(profile_dir)

browser = await nodriver.start(user_data_dir=profile_for(task.id))
```

## Lock check

```python
import os
from pathlib import Path

def profile_is_locked(profile_dir: Path) -> bool:
    lock = profile_dir / "SingletonLock"
    if not lock.exists():
        return False
    try:
        pid = int(lock.read_text().strip())
        os.kill(pid, 0)          # signal 0 = "does the process exist?"
    except (ValueError, ProcessLookupError):
        return False             # stale lock from a dead process
    return True
```

## Related

- `session-health-check.md` — validate a session before doing real work
- `production-readiness.md` — full deployment checklist
- Full article: "Why Your nodriver Browser Profiles Break (and How to Fix Them)" - https://versatilesparks.pages.dev/blog/why-browser-profiles-break
- Python Browser Automation Cookbook - https://gum.co/python-browser-automation-cookbook
