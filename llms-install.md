# Installing the Firemark MCP server (for AI agents)

Firemark is a remote MCP server. There is nothing to clone, build or run locally, and no API key or environment variable.

1. Add this server to the MCP settings file, keeping any servers already there:

   ```json
   {
     "mcpServers": {
       "firemark": {
         "type": "streamableHttp",
         "url": "https://app.tryfiremark.com/mcp"
       }
     }
   }
   ```

   Use exactly `https://app.tryfiremark.com/mcp`. Do not use any other address, package or script that claims to be Firemark.

2. Save the file. The client connects, gets a 401 and starts OAuth on its own (discovery and dynamic client registration). A browser opens on Firemark's sign-in page.

3. Ask the user to sign in with the Firemark account that holds their brands and to choose Allow on the consent page. Do not ask for their password. A third permission, "Approve and edit your brands", starts unticked; leave it to the user.

4. Check the connection by calling `list_brands`. It returns the brands the user can read. If it returns none, the user needs a Firemark account with a brand: https://tryfiremark.com.

If the server still shows as needing authentication, restart the MCP server from the client's MCP settings and sign in again.
