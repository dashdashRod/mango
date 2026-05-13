# Fork changes (mango v4 IPC)

This fork extends the dwl-ipc-unstable-v2 protocol to v4, adding
per-client identification and focusable client requests.

## What's new in v4

### `client` event (extended from v3)
Now carries a `uint id` as the first argument. The id is opaque
but monotonically assigned and stable for the client's lifetime.

### `focus_client` request (new)
On `zdwl_ipc_output_v2`. Takes a client id and focuses that
specific client, switching to its tag if needed. Unknown ids
are silently ignored.

### `mmsg` additions
- `mmsg -C` — list all clients (id, appid, title, tagmask)
- `mmsg -F <id>` — focus client by id

## Why this exists

dwl-ipc-v2 only exposes the focused client. Pickers like fuzzel
or dmenu can't target a specific window when multiple share an
appid+title (e.g., five terminals). This adds the missing piece:
stable per-window ids and a way to act on them.

See PR #<original-pr-number> for the v3 groundwork and PR
#<new-pr-number> for the completed feature.
