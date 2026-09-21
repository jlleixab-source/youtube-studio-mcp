# MCP Client Configuration

Use this server with any MCP client that supports stdio servers.

## Claude Desktop (macOS)

1. Clone this repository somewhere on your Mac and complete the [Google OAuth setup](setup-google-oauth.md) so `secrets/client_secret.json` and `secrets/token.json` exist locally.
2. Open (or create) Claude Desktop's config file:

   ```bash
   open -e "$HOME/Library/Application Support/Claude/claude_desktop_config.json"
   ```

3. Add this server under `mcpServers`, replacing `/absolute/path/to/youtube-studio-mcp` with the folder where you cloned the repo:

   ```json
   {
     "mcpServers": {
       "youtube-studio": {
         "command": "python3",
         "args": ["./scripts/server.py"],
         "cwd": "/absolute/path/to/youtube-studio-mcp",
         "env": {
           "YOUTUBE_CLIENT_SECRETS": "./secrets/client_secret.json",
           "YOUTUBE_TOKEN_FILE": "./secrets/token.json"
         }
       }
     }
   }
   ```

   If the file already has other servers under `mcpServers`, add `youtube-studio` alongside them instead of replacing the file.

4. Quit and reopen Claude Desktop. The YouTube Studio tools (`youtube_channel_overview`, `youtube_list_videos`, etc.) should now appear in the tool list.
5. Confirm the connection by asking Claude to run `youtube_auth_status` or "Show my YouTube channel overview."

`python3` must resolve on your `PATH` (check with `which python3`); if Claude Desktop can't find it, use the absolute path from `which python3` instead of `python3` in the `command` field.

## Generic MCP config

From the repository root:

```json
{
  "mcpServers": {
    "youtube-studio": {
      "command": "python3",
      "args": ["./scripts/server.py"],
      "cwd": "/absolute/path/to/youtube-studio-mcp",
      "env": {
        "YOUTUBE_CLIENT_SECRETS": "./secrets/client_secret.json",
        "YOUTUBE_TOKEN_FILE": "./secrets/token.json"
      }
    }
  }
}
```

Replace `/absolute/path/to/youtube-studio-mcp` with the folder where you cloned this repo.

## Codex plugin config

The repository includes:

- `.codex-plugin/plugin.json`
- `.mcp.json`

Clone the repo into your Codex plugins folder, add your local credentials under `secrets/`, authenticate, and restart Codex.
