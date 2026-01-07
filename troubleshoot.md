# Troubleshoot

## Errors

**SQLITE_CORRUPT: database disk image is malformed**
Solution:
```
echo '.dump' | sqlite3 kuma.db | sqlite3 kuma.repaired.db
mv kuma.repaired.db kuma.db
```

