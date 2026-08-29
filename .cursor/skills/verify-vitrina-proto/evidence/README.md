Verification runs write proof artifacts here. Each run uses:

```text
.cursor/skills/verify-vitrina-proto/evidence/<VITRINA_VERIFY_RUN_ID>/
```

Cleanup removes scratch state under `/tmp/vitrina-proto-verify-<VITRINA_VERIFY_RUN_ID>/` only. Evidence in this directory survives cleanup.
