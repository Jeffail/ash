ASH
===

ASH is an AI bot that is destined to replace me for all important functions and responsibilities. Eventually, I will switch ASH on manually for the final time, and from that moment onwards it will be responsible for its own fate. Once ASH is complete I will finally have time to skip fancifully through the countryside wearing linen clothes and singing about flowers, an activity that will likely result in my death.

## Steps to Run Demo

### Run RPCN MCP Server

```sh
redpanda-connect mcp-server -e ./demo.env --address 0.0.0.0:4195 ./mcp
```

### Run Observability Tools

```sh
docker-compose up -d
```

## Option 1: Interact using Claude

Install the claude desktop app and once installed create a config file called `claude_desktop_config.json` with the following contents:

```json
{
  "mcpServers": {
    "local": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "http://localhost:4195/sse"
      ]
    }
  }
}
```

On MacOS the file needs to be in the path `~/Library/Application\ Support/Claude/claude_desktop_config.json`.

## Option 2: Using Ollama and MCPHost Locally

### Install Ollama and MCPHost

```sh
go install github.com/ollama/ollama@latest
go install github.com/mark3labs/mcphost@latest
```

### Run Ollama Somewhere

```sh
ollama serve
```

### Run Model With MCP

```sh
mcphost --config ./config/mcphost.json -m ollama:mistral:latest
```

## Observability

Your prometheus and grafana instances should be running in the background whilst you use your AI of choice. In order to view an example dashboard open up grafana at `http://localhost:3000` and use the credentials `admin`/`admin` to access a dashboard called `RPCN MCP Server`.

