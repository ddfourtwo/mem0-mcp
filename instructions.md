  1. Clone the repository and navigate to the project directory:
  ```bash
  git clone https://github.com/whysosaket/mem0-mcp.git
  cd mem0-mcp
  ```

  2. Install dependencies and build the Node.js component:
  ```bash
  cd node/mem0
  npm install
  npm run build
  cd ../..
  ```

  3. Create or update your .mcp.json file with mem0 configuration:
  ```bash
  # First check if .mcp.json exists
  if [ -f .mcp.json ]; then
    # Use jq to add/update the mem0-mcp configuration
    jq '.tools."mem0-mcp" = {
      "autoApprove": ["add-memory", "search-memories"],
      "disabled": false,
      "timeout": 60,
      "command": "node",
      "args": ["./node/mem0/build/index.js"],
      "env": {
        "MEM0_API_KEY": "your-mem0-api-key-here",
        "DEFAULT_USER_ID": "default-user-id"
      },
      "transportType": "stdio"
    }' .mcp.json > .mcp.json.new && mv .mcp.json.new .mcp.json
  else
    # Create a new .mcp.json file
    cat > .mcp.json << EOF
  {
    "tools": {
      "mem0-mcp": {
        "autoApprove": ["add-memory", "search-memories"],
        "disabled": false,
        "timeout": 60,
        "command": "node",
        "args": ["./node/mem0/build/index.js"],
        "env": {
          "MEM0_API_KEY": "your-mem0-api-key-here",
          "DEFAULT_USER_ID": "default-user-id"
        },
        "transportType": "stdio"
      }
    }
  }
  EOF
  fi
  ```

  4. Replace placeholder values with actual API key and preferred user ID in the .mcp.json file.