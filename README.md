# mariadb-mcp-server

An MCP server implementation for retrieving data from mariadb

## Features

### Resources

Expose schema list in database

### Tools

- query_database
  - Execute read-only operations against MariDB

## dependency

### install mariadb

- mac
  - when install mariadb,
maybe raise os error below.
you can resolve by installing mariadb-connector-c.

```bash

OSError: mariadb_config not found.

      This error typically indicates that MariaDB Connector/C, a dependency which
      must be preinstalled, is not found.
      If MariaDB Connector/C is not installed, see installation instructions
      If MariaDB Connector/C is installed, either set the environment variable
      MARIADB_CONFIG or edit the configuration file 'site.cfg' to set the
       'mariadb_config' option to the file location of the mariadb_config utility.


```

1. execute `brew install mariadb-connector-c`
2. execute `echo 'export PATH="/opt/homebrew/opt/mariadb-connector-c/bin:$PATH"' >> ~/.bashrc`
3. set environment variable `export MARIADB_CONFIG=$(brew --prefix mariadb-connector-c)/bin/mariadb_config`
4. execute `uv add mariadb` again.

## Configuration

### Setting up database connection Environments

Set these environment variables for database connection:

- `MARIADB_HOST`: Database server host (default: `localhost`)
- `MARIADB_PORT`: Database server port (default: `3306`)
- `MARIADB_USER`: Database username (no default)
- `MARIADB_PASSWORD`: Database password (no default)
- `MARIADB_DATABASE`: Database name (no default)

Example configuration:

```bash
# Using .env file
MARIADB_HOST=127.0.0.1
MARIADB_PORT=3306
MARIADB_USER=admin
MARIADB_PASSWORD=secret
MARIADB_DATABASE=mydb

# Or export directly
export MARIADB_USER=admin
export MARIADB_PASSWORD=secret
```

## Usage with Claude Desktop

### Configuration File

Paths to Claude Desktop config file:

- **MacOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

Add this configuration to enable development/unpublished servers:

```json
{
    "mcpServers": {
        "mariadb_mcp_server": {
            "command": "/PATH/TO/uv",
            "args": [
                "--directory",
                "/YOUR/SOURCE/PATH/mariadb-mcp-server",
                "run",
                "mariadb_server.py"
            ]
        }
    }
}
```

**Note**: Replace these placeholders with actual paths:

- `/PATH/TO/uv`: Full path to UV executable
- `/YOUR/SOURCE/PATH/mariadb-mcp-server`: Path to server source code

## License

This mcp server is licensed under the MIT license.  please see the LICENSE file in the repository.
