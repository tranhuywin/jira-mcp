# Jira MCP

A Go-based MCP (Model Control Protocol) connector for Jira that enables AI assistants like Claude to interact with Atlassian Jira. This tool provides a seamless interface for AI models to perform common Jira operations.

## Features

- Get issue details
- Search issues with JQL
- List and manage sprints
- Create and update issues
- List available statuses
- Transition issues through workflows

## Installation

There are several ways to install the Script Tool:

### Option 1: Download from GitHub Releases

1. Visit the [GitHub Releases](https://github.com/nguyenvanduocit/jira-mcp/releases) page
2. Download the binary for your platform:
   - jira-mcp_linux_amd64` for Linux
   - `jira-mcp_darwin_amd64` for macOS
   - `jira-mcp_windows_amd64.exe` for Windows
3. Make the binary executable (Linux/macOS):
   ```bash
   chmod +x jira-mcp_*
   ```
4. Move it to your PATH (Linux/macOS):
   ```bash
   sudo mv jira-mcp_* /usr/local/bin/jira-mcp
   ```

### Option 2: Go install

```
go install github.com/nguyenvanduocit/jira-mcp
```

### Option 3: Docker

#### Using Docker directly

1. Build the Docker image:
   ```bash
   docker build -t jira-mcp .
   ```

2. Run the container with environment variables (recommended):
   ```bash
   docker run --rm -i \
     -e ATLASSIAN_HOST=your_atlassian_host \
     -e ATLASSIAN_EMAIL=your_email \
     -e ATLASSIAN_TOKEN=your_token \
     jira-mcp
   ```
   
   For SSE server mode:
   ```bash
   docker run --rm -i -p 8080:8080 \
     -e ATLASSIAN_HOST=your_atlassian_host \
     -e ATLASSIAN_EMAIL=your_email \
     -e ATLASSIAN_TOKEN=your_token \
     jira-mcp -sse_port 8080
   ```

## Config

### Environment Variables

The following environment variables are required for authentication:
```
ATLASSIAN_HOST=your_atlassian_host
ATLASSIAN_EMAIL=your_email
ATLASSIAN_TOKEN=your_token
# Optional
READ_ONLY=true  # When set to "true", only read operations are allowed.
```

You can set these:
1. Directly in the Docker run command (recommended, as shown above)
2. Through a .env file (optional for local development)

### Claude, cursor

For local binary with .env file:
```
{
  "mcpServers": {
    "jira": {
      "command": "/path-to/jira-mcp",
      "args": ["-env", "path-to-env-file"]
    }
  }
}
```

For Docker (recommended):
```
{
  "mcpServers": {
    "jira": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-i",
        "-e", "ATLASSIAN_HOST=your_atlassian_host",
        "-e", "ATLASSIAN_EMAIL=your_email",
        "-e", "ATLASSIAN_TOKEN=your_token",
        "jira-mcp"
      ]
    }
  }
}
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.
