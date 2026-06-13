## Sample Commands

1. Run a no-config diagnostic without reading project env or browser cookies.

```bash
LAST30DAYS_CONFIG_DIR="" python3 skills/last30days/scripts/last30days.py --diagnose
# Expect: JSON provider/source status and no browser-cookie prompts.
```

2. Run a quick public-source search with browser cookies disabled.

```bash
FROM_BROWSER=off python3 skills/last30days/scripts/last30days.py shopify --quick --emit=json --search=reddit,hackernews,polymarket
# Expect: JSON report; X is unavailable unless explicit AUTH_TOKEN/CT0, XAI_API_KEY, or xurl auth exists.
```

3. Opt into a trusted project env file explicitly.

```bash
LAST30DAYS_ENABLE_PROJECT_ENV=1 python3 skills/last30days/scripts/last30days.py --diagnose
# Expect: _CONFIG_SOURCE may show project:<path> when .claude/last30days.env exists.
```

4. Opt into browser-cookie X auth explicitly.

```bash
FROM_BROWSER=firefox python3 skills/last30days/scripts/last30days.py --diagnose
# Expect: X source can become available if Firefox contains x.com auth cookies.
```

## Failure Modes

| Symptom | Fix |
|---|---|
| X/Twitter missing | Set XAI_API_KEY, AUTH_TOKEN/CT0, xurl OAuth, or explicitly set FROM_BROWSER=firefox/safari/auto. |
| Project config ignored | Set LAST30DAYS_ENABLE_PROJECT_ENV=1 only inside trusted repos. |
| Browser cookies not read by vendored Bird CLI | Set BIRD_ALLOW_BROWSER_COOKIES=1 explicitly, or provide AUTH_TOKEN/CT0. |
| Config warning says file is too readable | Run `chmod 600 ~/.config/last30days/.env`. |
