Here is a workaround without having to install a fork

1. Register the client:

```bash
curl -X POST https://api.figma.com/v1/oauth/mcp/register \
  -H "Content-Type: application/json" \
  -d '{
    "client_name": "Claude Code (figma)",
    "redirect_uris": ["http://127.0.0.1:19876/mcp/oauth/callback"],
    "grant_types": ["authorization_code", "refresh_token"],
    "response_types": ["code"],
    "token_endpoint_auth_method": "none"
  }'
```

Adjust redirect_uris to match your MCP client's OAuth callback. The above is OpenCode's default.

2. Configure the returned credentials in opencode.jsonc:

```json
"figma": {
  "enabled": true,
  "type": "remote",
  "url": "https://mcp.figma.com/mcp",
  "oauth": {
    "clientId": "<client_id from response>",
    "clientSecret": "<client_secret from response>"
  }
}
```

3. Remove the figma entry from `~/.local/share/opencode/mcp-auth.json` and then run `opencode mcp auth figma` and accept browser prompts

<img width="281" height="141" alt="Image" src="https://github.com/user-attachments/assets/d07090d4-3dc4-45ba-bb1d-cdc47f9b8cc0" />

Enjoy your freedom
