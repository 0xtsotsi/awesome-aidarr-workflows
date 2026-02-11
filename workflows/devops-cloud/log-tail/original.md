



# Log Tail

Stream recent logs from the systemd journal. View logs by service unit, control line count, and optionally follow in real time.

## Commands

```bash
# Show recent journal logs (default: 50 lines)
log-tail [--unit <service>] [--lines 50]

# Follow logs for a specific service in real time
log-tail --follow <service>
```

## Install

No installation needed. `journalctl` is always present on systemd-based systems like Bazzite/Fedora.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
