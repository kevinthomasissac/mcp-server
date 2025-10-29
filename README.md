# 🌦️ MCP Server – Weather

A Model Context Protocol (MCP) server providing U.S. weather forecasts and severe weather alerts using data from the [National Weather Service (NWS)](https://www.weather.gov/).

---

## 🧩 Features

- `get-alerts`: Fetch current weather alerts for a U.S. state  
- `get-forecast`: Get a short-term forecast for a U.S. location (latitude/longitude)

---

## 📦 Project Setup

### 1. Clone and install dependencies

```bash
git clone <your-repo-url>
cd mcp-server-weather
npm install
```

---

### 2. Build the TypeScript code

```bash
npm run build
```

This compiles the source from `src/` to `dist/`.

---

### 3. Run the server directly

```bash
node dist/index.js
```

You should see:

```
Weather MCP Server running on stdio
```

---

## 🧰 Testing with the MCP Inspector CLI

The official CLI tool for interacting with MCP servers is [`@modelcontextprotocol/inspector`](https://www.npmjs.com/package/@modelcontextprotocol/inspector).

---

### 4. List available tools

```bash
npx @modelcontextprotocol/inspector --cli node dist/index.js --method tools/list
```

**Expected output:**
```json
{
  "tools": [
    { "name": "get-alerts", "description": "Get weather alerts for a US state" },
    { "name": "get-forecast", "description": "Get weather forecast for a location in the US" }
  ]
}
```

---

### 5. Get weather alerts

```bash
npx @modelcontextprotocol/inspector --cli node dist/index.js \
  --method tools/call \
  --params '{"name":"get-alerts","arguments":{"state":"CA"}}'
```

---

### 6. Get forecast

```bash
npx @modelcontextprotocol/inspector --cli node dist/index.js \
  --method tools/call \
  --params '{"name":"get-forecast","arguments":{"latitude":37.7749,"longitude":-122.4194}}'
```

---

## ⚙️ Publishing to npm

To publish this MCP server as an npm CLI tool:

1. Update the `name`, `version`, and `repository` fields in your `package.json`.
2. Ensure the executable mapping is correct:
   ```json
   "bin": {
     "mcp-server-weather": "dist/index.js"
   }
   ```
3. Build the project:
   ```bash
   npm run build
   ```
4. Make sure the binary file is executable:
   ```bash
   chmod +x dist/index.js
   ```
5. Log in to npm:
   ```bash
   npm login
   ```
6. Publish:
   ```bash
   npm publish --access public
   ```

After publishing, anyone can install and run your server globally:

```bash
npm install -g mcp-server-weather
mcp-server-weather
```

---

## ⚙️ Node.js Version

- Minimum required: **Node.js 18**
- Recommended: **Node.js ≥ 22.7.5** (to match the latest `@modelcontextprotocol/inspector`)
- Update using:
  ```bash
  brew upgrade node@22
  ```

---

## 🧱 Project Structure

```
mcp-server-weather/
├── src/
│   └── index.ts
├── dist/
│   └── index.js
├── package.json
├── tsconfig.json
└── README.md
```

---

## 🧩 Development Commands

| Command | Description |
|----------|-------------|
| `npm run build` | Compile TypeScript into `dist/` |
| `npm run watch` | Watch for changes and rebuild automatically |
| `npm run clean` | Clean build artifacts |
| `npm run do-publish` | Clean, install, and publish package to npm |
| `npm run publish-dry-run` | Test npm publish process without uploading |

---

## ⚙️ Notes

- The server uses **STDIO** transport and must **not** write to `stdout` (use `console.error()` for logs).
- MCP clients (like OpenAI ChatGPT or the MCP Inspector) communicate via JSON-RPC.
- Works only for **U.S. coordinates**, as the NWS API doesn’t cover other countries.

---

## 📜 License

MIT License © 2025  