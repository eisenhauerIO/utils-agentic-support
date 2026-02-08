---
name: sync-general-skills
description: Sync shared external skills from GitHub into .claude/skills/ as symlinks.
allowed-tools: Bash
---

# Sync General Skills

Fetch the latest shared skills from the `eisenhauerIO/utils-agentic-support` GitHub repo and symlink them into `.claude/skills/`.

## Steps

1. Clone or update the cache:

```bash
cache_dir=".claude/.cache/utils-agentic-support"
if [ -d "$cache_dir/.git" ]; then
  git -C "$cache_dir" pull --ff-only
else
  mkdir -p .claude/.cache
  git clone --depth 1 https://github.com/eisenhauerIO/utils-agentic-support.git "$cache_dir"
fi
```

2. Symlink each skill:

```bash
cache_dir=".claude/.cache/utils-agentic-support"
for d in "$cache_dir"/claude/skills/*/; do
  name="$(basename "$d")"
  target=".claude/skills/$name"
  if [ ! -e "$target" ]; then
    ln -s "../.cache/utils-agentic-support/claude/skills/$name" "$target"
    echo "Linked: $name"
  else
    echo "Skipped (exists): $name"
  fi
done
```

Report which skills were linked and which were skipped.
