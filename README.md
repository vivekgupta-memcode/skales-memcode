# MemCode Memory for Skales

An opt-in page for saving selected facts and recalling them through the user's MemCode account. It uses Skales' remote MCP connection and OAuth sign-in. The page never asks for or stores an API key.

## Setup

1. Enable Skales' MCP Servers add-on.
2. In **Settings → Extensions → MCP servers**, add an enabled HTTP server named `memcode` at `https://mcp.memcode.in/mcp` with OAuth on. Leave request headers empty.
3. Complete the sign-in prompted by Skales and test the connection.
4. Install this plugin from its repository in Skales. The page offers explicit **Save**, **Check save status**, **Search**, and **Get a grounded answer** actions.

The exact server name matters because Skales prefixes discovered tools with `mcp_<server>_`. If the server is unavailable, the page shows a connection error. You can also use the MemCode MCP tools directly in Skales chat after connecting the server.

## Data and permissions

- **No automatic capture.** Only text entered into this page and submitted with **Save this text** is sent to MemCode. The plugin does not inspect chat history, files, Skales' shared memory, or other apps.
- **Network:** the user-configured MemCode MCP server reaches MemCode's hosted service. OAuth credentials stay in Skales' MCP connection; the page receives tool results, not tokens.
- **Filesystem:** none. **Skales memory:** own, with no shared-memory access. The page itself does not write to the plugin store.
- **Tools:** `mcp_memcode_save_memory`, `mcp_memcode_get_memory_ingest_status`, `mcp_memcode_search_memories`, and `mcp_memcode_retrieve_answer` only.
- **Asynchronous saves:** a save returns a job ID. Use **Check save status** until the job completes before expecting recall. The page never retries a write automatically.
- **Removal:** disable/uninstall the plugin in Skales to stop using it. Manage or delete hosted memories in your MemCode account; uninstalling the plugin does not delete remote data.

MemCode has a [free tier and paid plans](https://memcode.in/memory). See the [Memory and MCP documentation](https://memcode.in/docs).

## Development status

This is a draft community submission linked to [skalesapp/skales#312](https://github.com/skalesapp/skales/issues/312). The bridge behavior and minimum compatible app version still need an in-app check against Skales 12.9.45; this environment could not download the macOS installer. The manifest's `minAppVersion` is provisional until that check is completed. The plugin should not be installed from the draft as a verified release.

The page is a standalone HTML file with no imports, CDN, background tasks, or telemetry. Maintained by Vivek Gupta at MemCode. Issues and compatibility reports belong in this repository.
