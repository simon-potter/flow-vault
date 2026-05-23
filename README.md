# flow-vault

Obsidian-format vault, auto-managed by `hermes-flow`.

- Seeded by Ansible role `hermes_native` on 2026-05-23.
- The `vault-autocommit.timer` on the VM pushes changes every
  *:0/5.
- The `gbrain-sync.service` on the VM indexes notes for RAG recall.

Do not edit on GitHub directly during active hermes sessions —
the timer pulls before committing but conflict resolution is
best-effort.
