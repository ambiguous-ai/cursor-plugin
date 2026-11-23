# Ambiguous for Cursor

Work in your [Ambiguous](https://www.ambiguous.ai) workspace from Cursor: docs, sheets,
slides, canvas, chat, mail, drive, tasks, CRM, forms, calendar and wiki.
Ambiguous Workspace is free for up to 5 teammates.

The plugin bundles the hosted **Ambiguous MCP server** and the **Ambiguous skill**.
It contains no credentials and runs no local server. Sign in to Ambiguous through
Cursor to use your account's workspace and permissions.

## Test locally before marketplace publication

Clone this repository, then copy its contents into a real directory at
`~/.cursor/plugins/local/ambiguous/`, including the hidden `.cursor-plugin/` folder:

```bash
git clone https://github.com/ambiguous-ai/cursor-plugin.git
mkdir -p ~/.cursor/plugins/local/ambiguous
cp -R cursor-plugin/. ~/.cursor/plugins/local/ambiguous/
```

Run **Developer: Reload Window** in Cursor, then open **Customize → Plugins → Ambiguous**.
You should see one skill and one MCP server. Cursor skips symlinks to repositories
outside its local plugins folder. A marketplace install with the same name takes
precedence over the local copy. Enterprise administrators must allow local plugin imports.

## Connect and use

Open the Ambiguous MCP configuration in Customize and complete browser sign-in.
If you already configured Ambiguous manually, choose the plugin source when testing
this package so the existing connection cannot hide a plugin setup failure.

Start a fresh Agent chat and ask:

- "Use the Ambiguous plugin to check which account and workspace I am connected to."
- "Find my open tasks in Ambiguous."
- "Create an Ambiguous task called 'Try Cursor', then read it back and give me its link."

Confirm the returned account and workspace before creating anything. The connector
uses `https://app.ambiguous.ai/mcp`; sign-in and workspace operations require internet
access even when the plugin is installed locally.

### Authentication compatibility

Local discovery has been verified, but standalone plugin authentication is currently
blocked on Cursor Desktop 3.31.15: after Authenticate reports success, protected calls
such as `auth_whoami` still return `Unauthorized`. An existing manually configured
connection can mask this failure. This package is not yet verified end to end.

Cursor is tracking a [matching OAuth issue](https://forum.cursor.com/t/plugin-mcp-oauth-never-reaches-needsauth-authenticate-button-missing-browser-never-opens/170058)
with servers that allow unauthenticated discovery. Do not treat the chat's
"authenticated" message as proof; verify a protected workspace read succeeds.

## Source and license

This repository is assembled from `plugins/cursor/` and the shared
`skills/ambiguous/SKILL.md` in [ambiguous-ai/workspace](https://github.com/ambiguous-ai/workspace).
Make changes there; this repository contains only the installable package.

MIT. See [LICENSE](LICENSE).
