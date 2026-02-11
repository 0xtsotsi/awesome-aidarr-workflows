



# signal-cli (Signal Messaging)

Use the local `signal-cli` binary.

## Preconditions

- `signal-cli` is installed and already linked/registered.
- For safety: confirm recipient + final message text with the user before sending.

## Quick patterns

### Discover available accounts

```bash
signal-cli listAccounts
```

### List contacts (JSON)

```bash
signal-cli -o json -u "+386..." listContacts
```

### Find a contact by name/nickname/number

Prefer the bundled script (handles fuzzy-ish matching + multiple matches):

```bash
python3 scripts/find_contact.py --account "+386..." --query "Name"
```

### Send a message

Prefer the bundled script (resolves contact names to numbers):

```bash
python3 scripts/send_message.py --account "+386..." --to "Name" --text "Heyo ..."
```

If `--to` is already a phone number in E.164 (e.g. `+386...`), it sends directly.

## Safety checklist (always)

- If resolving by name returns multiple matches, present options and ask the user which one.
- If message contains sensitive info, ask explicitly before sending via Signal.
- Default to `--service-environment live` (signal-cli default) and normal trust behavior.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
