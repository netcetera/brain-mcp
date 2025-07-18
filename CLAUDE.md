# Brain MCP - Remote MCP Server

## Project Overview

This is a remote Model Context Protocol (MCP) server called "brain-mcp" that provides calculator functionality through a Cloudflare Worker. The server implements the MCP specification and can be accessed remotely via SSE (Server-Sent Events) or standard HTTP endpoints.

## Key Features

- **Remote MCP Server**: Deployed on Cloudflare Workers for global accessibility
- **Calculator Tools**: Provides basic arithmetic operations (add, subtract, multiply, divide)
- **Dual Tool Interface**: Includes both a simple `add` tool and a comprehensive `calculate` tool
- **Multiple Connection Types**: Supports both SSE and HTTP MCP protocols
- **Durable Objects**: Uses Cloudflare Durable Objects for state management

## Architecture

The application is built using:
- **Cloudflare Workers**: Serverless runtime environment
- **Durable Objects**: For persistent state and MCP agent instances
- **TypeScript**: Type-safe development
- **MCP SDK**: Official Model Context Protocol implementation

## Codebase Structure

```
/root/repo/
├── src/
│   └── index.ts              # Main MCP server implementation
├── package.json              # Dependencies and scripts
├── tsconfig.json             # TypeScript configuration
├── wrangler.jsonc            # Cloudflare Worker configuration
├── biome.json                # Code formatting and linting rules
├── worker-configuration.d.ts # Generated type definitions
└── README.md                 # Deployment and usage instructions
```

## Core Components

### MyMCP Class (`src/index.ts`)
- **Base Class**: Extends `McpAgent` from the `agents` package
- **MCP Server**: Implements calculator tools using the MCP SDK
- **Tool Definitions**:
  - `add`: Simple addition of two numbers
  - `calculate`: Multi-operation calculator (add, subtract, multiply, divide)

### Request Handler
- **SSE Endpoint**: `/sse` - Server-Sent Events for real-time communication
- **MCP Endpoint**: `/mcp` - Standard MCP protocol endpoint
- **404 Handler**: Returns 404 for unmatched routes

## Dependencies

### Production Dependencies
- `@modelcontextprotocol/sdk` (^1.13.0): Official MCP SDK for protocol implementation
- `agents` (^0.0.95): MCP agent framework
- `zod` (^3.25.67): Schema validation library

### Development Dependencies
- `@biomejs/biome` (^2.0.4): Code formatter and linter
- `typescript` (^5.8.3): TypeScript compiler
- `wrangler` (^4.20.5): Cloudflare Workers CLI and deployment tool

## Configuration

### TypeScript Configuration
- **Target**: ES2021
- **Module**: ES2022 with bundler resolution
- **Strict**: Enabled for type safety
- **JSX**: React JSX support

### Cloudflare Worker Configuration
- **Runtime**: Node.js compatibility enabled
- **Durable Objects**: MyMCP class bound as MCP_OBJECT
- **Observability**: Enabled for monitoring

### Code Quality
- **Biome**: Configured for formatting (4-space indentation, 100 character line width)
- **Linting**: Enabled with recommended rules and custom style preferences

## Available Scripts

- `npm run dev`: Start development server
- `npm run deploy`: Deploy to Cloudflare Workers
- `npm run format`: Format code with Biome
- `npm run lint:fix`: Fix linting issues
- `npm run type-check`: Run TypeScript type checking
- `npm run cf-typegen`: Generate Cloudflare Worker types

## Usage

The MCP server can be accessed at:
- SSE endpoint: `https://brain-mcp.<account>.workers.dev/sse`
- MCP endpoint: `https://brain-mcp.<account>.workers.dev/mcp`

Connect to the server using MCP clients like Claude Desktop or the Cloudflare AI Playground.

## Development Notes

- The codebase follows strict TypeScript practices
- All arithmetic operations include proper error handling (e.g., division by zero)
- The server is designed to be stateless and scalable
- Observability is enabled for monitoring production usage