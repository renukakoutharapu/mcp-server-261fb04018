# Building a Python MCP Server with VS Code and GitHub Copilot

A step-by-step implementation of a Python Model Context Protocol (MCP) server integrated with VS Code and GitHub Copilot (Agent Mode).

## Project Overview

- **Project Name:** `hello-mcp`
- **Language:** Python (3.11+)
- **Environment:** VS Code
- **AI Client:** GitHub Copilot (Agent Mode)
- **SDK:** Model Context Protocol Python SDK (`mcp[cli]`)
- **Transport:** Standard I/O (`stdio`)

## Implemented Tools

1. **`get_greeting(name: str) -> str`**: Returns a personalized greeting for a student (`Hello, {name}! Your first MCP tool works.`).
2. **`add_numbers(a: int, b: int) -> int`**: Takes two integers and returns their sum (`a + b`).

## Project Structure

```
hello-mcp/
├── server.py              # MCP server definition with get_greeting & add_numbers tools
├── requirements.txt       # Dependencies (mcp[cli])
├── .venv/                 # Python virtual environment (ignored in git)
└── .vscode/
    └── mcp.json           # VS Code MCP server configuration
```

## Setup & Running

### 1. Create and Activate Virtual Environment
```powershell
py -m venv .venv
```

### 2. Install Dependencies
```powershell
.\.venv\Scripts\python.exe -m pip install "mcp[cli]" --default-timeout=120
```

### 3. VS Code Configuration (`.vscode/mcp.json`)
```json
{
  "servers": {
    "helloMcp": {
      "type": "stdio",
      "command": "${workspaceFolder}\\.venv\\Scripts\\python.exe",
      "args": ["server.py"]
    }
  }
}
```

### 4. Start Server in VS Code
1. Press `Ctrl + Shift + P`.
2. Select **MCP: List Servers**.
3. Select `helloMcp` and choose **Start / Restart**.
4. Verify the output displays:
   - `helloMcp`
   - `Connection state: Running`
   - `Discovered 2 tools`

### 5. Testing with GitHub Copilot (Agent Mode)
- Prompt 1: `"Use the get_greeting MCP tool from helloMcp with the name Students. Show me the result."`
  - Expected: `Hello, Students! Your first MCP tool works.`
- Prompt 2: `"Use the add_numbers MCP tool from helloMcp with a = 10 and b = 20. Show me the result."`
  - Expected: `30`
