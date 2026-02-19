# mcp-server-s3

[![npm version](https://img.shields.io/npm/v/mcp-server-s3.svg)](https://www.npmjs.com/package/mcp-server-s3)
[![npm downloads](https://img.shields.io/npm/dm/mcp-server-s3.svg)](https://www.npmjs.com/package/mcp-server-s3)
[![CI](https://github.com/ofershap/mcp-server-s3/actions/workflows/ci.yml/badge.svg)](https://github.com/ofershap/mcp-server-s3/actions/workflows/ci.yml)
[![TypeScript](https://img.shields.io/badge/TypeScript-strict-blue.svg)](https://www.typescriptlang.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Manage AWS S3 buckets and objects directly from your AI assistant — browse files, upload/download content, and generate presigned URLs.

```bash
npx mcp-server-s3
```

> Works with Claude Desktop, Cursor, VS Code Copilot, and any MCP client. Uses your AWS credentials (~/.aws/credentials or environment variables).

![Demo](assets/demo.gif)

## Tools

| Tool            | What it does                                           |
| --------------- | ------------------------------------------------------ |
| `list_buckets`  | List all S3 buckets in your AWS account.               |
| `list_objects`  | List objects in a bucket, with optional prefix filter. |
| `get_object`    | Download and read an object's content as text.         |
| `put_object`    | Upload text content to an S3 object.                   |
| `delete_object` | Delete an object from a bucket.                        |
| `presigned_url` | Generate a temporary presigned URL for an object.      |
| `bucket_info`   | Check if a bucket exists and get basic info.           |

## Quick Start

### Cursor

Add to `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "s3": {
      "command": "npx",
      "args": ["mcp-server-s3"],
      "env": {
        "AWS_REGION": "us-east-1",
        "AWS_ACCESS_KEY_ID": "your-access-key",
        "AWS_SECRET_ACCESS_KEY": "your-secret-key"
      }
    }
  }
}
```

### Claude Desktop

Add to `claude_desktop_config.json` (macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "s3": {
      "command": "npx",
      "args": ["mcp-server-s3"],
      "env": {
        "AWS_REGION": "us-east-1",
        "AWS_ACCESS_KEY_ID": "your-access-key",
        "AWS_SECRET_ACCESS_KEY": "your-secret-key"
      }
    }
  }
}
```

### VS Code (Copilot / MCP extension)

Configure the MCP server to run `npx mcp-server-s3` with `AWS_REGION`, `AWS_ACCESS_KEY_ID`, and `AWS_SECRET_ACCESS_KEY` in the environment.

## Authentication

The server uses the standard AWS credential chain:

1. **Environment variables** — `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_REGION`
2. **Shared credentials file** — `~/.aws/credentials`
3. **IAM roles** — When running on EC2, ECS, Lambda, or similar

Set `AWS_REGION` (defaults to `us-east-1`) and ensure your credentials have the necessary S3 permissions: `s3:ListBuckets`, `s3:ListBucket`, `s3:GetObject`, `s3:PutObject`, `s3:DeleteObject`, `s3:HeadBucket`.

## Example prompts

- "List all my S3 buckets"
- "Show me the files in my-bucket/uploads/"
- "Download the config.json from my-bucket"
- "Upload this content to my-bucket/notes.txt"
- "Generate a presigned URL for this file that expires in 1 hour"

## Development

```bash
npm install
npm run typecheck
npm run build
npm test
npm run format
npm run lint
```

## Author

Ofer Shapira · [GitHub](https://github.com/ofershap)

## License

MIT
