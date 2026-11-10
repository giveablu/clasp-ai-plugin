# Clasp agent plugin for Claude and Perplexity

This package bundles a field-service skill and the remote Clasp MCP connector.
It uses the existing Clasp service rather than running a second backend. Each
person signs in to Clasp and grants access to their own workspace. Connection
files contain no credentials. The shared service defines 33 tools; discovery
and execution remain limited by each connection's current permissions.

## Install in Claude

Upload the ZIP through **Customize → Plugins → Add → Upload plugin**. Open its
Connectors tab and connect Clasp. For a private test connection, choose
**Use your own OAuth client** and enter the Clasp client registered for Claude.
For a public directory release, Clasp supplies that client securely through
Anthropic's developer portal instead.

Uploading this package does not create the connection. For public release,
Clasp must submit the plugin bundle and its remote MCP server as two separate
items in Anthropic's developer portal. The repository can remain private during
validation and review, but Anthropic requires it to be public before the
listing goes live.

The same package layout loads in Claude Code with
`claude --plugin-dir /absolute/path/to/clasp-ai-plugin`. The skill is
`/clasp:field-service`. Claude Code's loopback OAuth flow needs its own approved
registration; the hosted Claude callback is not a loopback callback. This
package does not establish Claude Code OAuth compatibility.

## Install in Perplexity

Open **Plugins → Add custom → Upload plugin or skill**, then upload the same
ZIP. Perplexity explicitly supports the Claude manifest location and
`.mcp.json`, so no second copy of the plugin is needed. Confirm that both the
field-service skill and Clasp connector appear, then open the connector to
authenticate. If Perplexity asks for OAuth client credentials, enter the Clasp
client registered for Perplexity in its secure connector form. Never paste
credentials into a chat or put them in this ZIP.

This release targets a personal Perplexity installation, not an organization
or Enterprise connector. If Plugins is unavailable, add the remote connector
through **Customize → Connectors** using `https://mcp.clasp.pro/mcp`, OAuth and
Streamable HTTP; the bundled skill is then a separate installation.

## Verify and disconnect

Ask Clasp for the connection profile, then search for a synthetic no-match
customer. Confirm the intended company and the actual tool call. A Connected
badge is insufficient. Use only an authorized QA workspace for mutation tests;
real customer sends and payments are not installation checks.

Disconnect in the provider and revoke the matching grant in Clasp. Removing a
plugin can leave its connector connected, so verify both independently.

Privacy: https://clasp.pro/privacy. Terms: https://clasp.pro/terms.
Support: https://clasp.pro/support.

Build and release operations are maintained in the Clasp application
repository. This package is proprietary Clasp software; see `LICENSE`.
