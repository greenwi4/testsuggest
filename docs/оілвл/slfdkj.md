---
title: slfdkj
deprecated: false
hidden: false
metadata:
  robots: index
---
# Connect to N-able MCP in 2 Simple Steps

<Glossary>N-able MCP</Glossary> lets you connect such <Glossary>AI tools</Glossary> as Claude, GitHub Copilot, Gemini and **many more** - directly to your N-able environment. Built on the <Glossary>N-able GraphQL</Glossary> API, it gives AI assistants **real-time access** to N-central device data, N-sight RMM data, and more via the <Anchor label="<Glossary>N-able GraphQL API</Glossary>" target="_blank" href="https://developer.n-able.com/gql/page/api-reference"><Glossary>N-able GraphQL API</Glossary></Anchor>.

Ask questions in **<Glossary>natural language</Glossary>**, run compliance checks, and query your fleet **without writing code** or navigating separate product APIs.

View the full list of <Anchor label="default and custom tools" target="_blank" href="/gql/docs/mcp-capabilities">default and custom tools</Anchor> currently available.

<ApexCards  
  gridColsMd={3}  
  layout="centered"  
  items={[  
    {  
      adornment: { type: "icon", iconClass: "fa-solid fa-circle-info text-info" },  
      title: "Choose endpoint",  
      description: "Pick the endpoint that matches your use case and risk profile before configuring any tool.",  
      button: { text: "Go to endpoint setup", href: "#1-choose-your-endpoint", target: "_self" }  
    },  
    {  
      adornment: { type: "icon", iconClass: "fa-solid fa-key text-warning" },  
      title: "Connect your tool",  
      description: "Set token auth and configure Claude, Gemini, or Copilot with the same MCP pattern.",  
      button: { text: "Go to tool setup", href: "#2-connect-your-ai-tool-or-ide-non-exhaustive-examples", target: "_self" }  
    },  
    {  
      adornment: { type: "icon", iconClass: "fa-solid fa-circle-check text-success" },  
      title: "Verify quickly",  
      description: "Run two practical checks to confirm auth, schema access, and real query execution.",  
      button: { text: "Go to verification", href: "#5-verify-its-working-expected-behavior", target: "_self" }  
    }  
  ]}  
/>

***

# 1. Choose your endpoint

<Glossary>N-able MCP</Glossary> provides three distinct endpoints for different purposes. Choose the endpoint that matches your use case before configuring your <Glossary>AI tool</Glossary> or <Glossary>IDE</Glossary>.

<ApexAlert type="warning" title="Live data access and modification" message="Both `/mcp` and `/mcp-preview` can read and modify live production data across all connected N-able products. This includes executing scripts on devices and will extend to billing and other data as the platform grows. Understand the implications before connecting to a production endpoint. Use with caution - changes affect real customer environments." />

If you open the MCP endpoint in a web browser you may see an `RBAC: access denied` message. This is expected because N-able MCP only accepts POST requests.

<ApexCards  
  gridColsMd={1}  
  items={[  
    {  
      adornment: { type: "icon", iconClass: "fa-solid fa-server text-warning" },  
      title: "Production",  
      description: "`https://api.n-able.com/mcp`",  
      copyText: "https://api.n-able.com/mcp",  
      dataAccess: "**Full read and write access** across all connected N-able products. Can query data, execute scripts, and modify devices.",  
      useCase: "Use this for production automations once you have fully tested your setup. Treat it with the same care as direct access to your N-able platform."  
    },  
    {  
      adornment: { type: "icon", iconClass: "fa-solid fa-shield-halved text-success" },  
      title: "Read-only",  
      description: "`https://api.n-able.com/mcp-read-only`",  
      copyText: "https://api.n-able.com/mcp-read-only",  
      dataAccess: "**Read-only.** Queries and reporting only - cannot execute scripts or modify anything across any connected product.",  
      useCase: "Recommended starting point for most use cases. Use this for dashboards, compliance reports, and any AI tool that needs visibility without write access."  
    },  
    {  
      adornment: { type: "icon", iconClass: "fa-solid fa-flask text-info" },  
      title: "Preview",  
      description: "`https://api.n-able.com/mcp-preview`",  
      copyText: "https://api.n-able.com/mcp-preview",  
      dataAccess: "**Preview.** Early access to new tools and data sources before they reach production API. Also has full read and write access across connected products.",  
      useCase: "Use this to try new capabilities as they are developed. Not recommended for production automations - tools and available data may change without notice."  
    }  
  ]}  
/>

***

# 2. Connect your AI Tool or IDE (Non-Exhaustive Examples)

## Before you start: Get your API Token

To connect <Glossary>N-able MCP</Glossary> to an <Glossary>AI tool</Glossary> or <Glossary>IDE</Glossary>, you need a valid <Glossary>API token</Glossary>. Tokens are tied to the <Glossary>N-able</Glossary> SSO user account that creates them, so the token only returns data that account has permission to see.

<ApexCards  
  gridColsMd={1}  
  items={[  
    {  
      adornment: { type: "icon", iconClass: "fa-solid fa-lightbulb text-success" },  
      title: "Get your API Token",  
      description: <>Create your token at <a href="https://n-able.app/api-token-management" target="_blank">https://n-able.app/api-token-management</a>. Copy it somewhere safe because you will not be able to view it again after creation.</>,  
      button: { text: "Get your token", href: "https://n-able.app/api-token-management", target:"_blank" }  
    }  
  ]}  
/>

To communicate with <Glossary>N-able MCP</Glossary>, clients must provide a valid authorization token via the HTTP header:

```
Authorization: Bearer <YOUR_API_TOKEN>
```

<ApexAlert type="info" title="Simpler setup is coming" message="We are working on dynamic client registration, which is planned for Q3 2026. This will let supported AI tools connect to N-able MCP without manually configuring a token. For now, use the token-based setup below." />

### Permissions

<Glossary>API tokens</Glossary> inherit permissions from the N-able SSO user who created them, so authorization depends on that user account's access.

If a token **does not** have adequate permissions:

- Queries may fail with a 401 Unauthorized error
- Fields your user account cannot access may return `null` rather than an error
- Device lists will only include customers your account has permission to see

_Example: if your token was created by a user with access to 3 of your 10 customer accounts, a query for all devices will only return devices from those 3 accounts._

<Glossary>N-able MCP</Glossary> works with any MCP-compatible <Glossary>AI tool</Glossary> or <Glossary>IDE</Glossary>. Find your tool below, copy the configuration, and restart the application. If your tool is **not listed**, the same pattern applies: use the server URL and pass your <Glossary>API token</Glossary> in the Authorization header.

***

## Pick your tool

<ApexAlert
  type="warning"
  title="Node.js/NPX path may differ by machine"
  message="Some MCP clients (especially desktop apps) do not inherit your shell PATH. If setup fails with errors like `spawn npx ENOENT` or `command not found`, use the full absolute path to `npx` in your MCP config instead of just `npx`."
/>

Quick checks:

- Confirm `npx` is installed and available in your terminal with `npx --version`
- Find the executable path:
  - Windows: `where npx`
  - macOS/Linux: `which npx`
- If your MCP client still fails, set the full path in config (examples below)

```json
{
  "mcpServers": {
    "n-able": {
      "command": "C:/Program Files/nodejs/npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://api.n-able.com/mcp-read-only",
        "--header",
        "Authorization: Bearer <YOUR_API_TOKEN>"
      ]
    }
  }
}
```

Common `npx` locations:

- Windows: `C:/Program Files/nodejs/npx` or `C:/Program Files/nodejs/npx.cmd`
- macOS (Homebrew): `/opt/homebrew/bin/npx` (Apple Silicon) or `/usr/local/bin/npx` (Intel)
- Linux: usually `/usr/bin/npx` or `/usr/local/bin/npx`

Slash hygiene (common copy/paste issue):

- Use single forward slashes in local paths and endpoint paths
- Avoid accidental double slashes like `C://...` or `/mcp/preview`

```json
{
  "bad": {
    "command": "C://Program Files/nodejs/npx",
    "url": "https://api.n-able.com/mcp/preview"
  },
  "good": {
    "command": "C:/Program Files/nodejs/npx",
    "url": "https://api.n-able.com/mcp-preview"
  }
}
```

<ApexCards  
  gridColsMd={1}  
  items={\[  
    {  
      adornment: { type: "icon", iconClass: "fa-solid fa-desktop text-primary" },  
      title: "Claude Desktop",  
      description: "Anthropic desktop client using **mcp-remote** and the read-only endpoint `https://api.n-able.com/mcp-read-only`.",  
      codeBlock: {  
        language: "json",  
        label: "Claude Desktop config",  
        code: `{
  "mcpServers": {
    "n-able": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://api.n-able.com/mcp-read-only",
        "--header",
        "Authorization: Bearer <YOUR_API_TOKEN>"
      ]
    }
  }
}`  
      }  
    },  
    {  
      adornment: { type: "icon", iconClass: "fa-solid fa-terminal text-info" },  
      title: "Claude Code",  
      description: "Terminal-based setup using HTTP transport with `Authorization` header.",  
      codeBlock: {  
        language: "json",  
        label: "Claude Code config",  
        code: `{
  "mcpServers": {
    "n-able": {
      "type": "http",
      "url": "https://api.n-able.com/mcp-read-only",
      "headers": {
        "Authorization": "Bearer <YOUR_API_TOKEN>"
      }
    }
  }
}`  
      }  
    },  
    {  
      adornment: { type: "icon", iconClass: "fa-solid fa-gem text-accent" },  
      title: "Gemini CLI",  
      description: "Google Workspace/CLI flow using `httpUrl` and token header.",  
      codeBlock: {  
        language: "json",  
        label: "Gemini CLI config",  
        code: `{
  "mcpServers": {
    "n-able": {
      "httpUrl": "https://api.n-able.com/mcp-read-only",
      "headers": {
        "Authorization": "Bearer <YOUR_API_TOKEN>"
      }
    }
  }
}`  
      }  
    },  
    {  
      adornment: { type: "icon", iconClass: "fa-solid fa-code text-success" },  
      title: "Copilot VS Code",  
      description: "VS Code agent-mode MCP setup using `servers` and explicit token header.",  
      codeBlock: {  
        language: "json",  
        label: "VS Code settings.json",  
        code: `{
  "servers": {
    "n-able": {
      "url": "https://api.n-able.com/mcp-read-only",
      "type": "http",
      "headers": {
        "Authorization": "Bearer <YOUR_API_TOKEN>"
      }
    }
  },
  "inputs": []
}`  
      }  
    },  
    {  
      adornment: { type: "icon", iconClass: "fa-solid fa-wand-magic-sparkles text-primary" },  
      title: "Copilot Studio",  
      description: "Step-by-step setup for adding N-able MCP inside a Copilot Studio agent, including connection and re-auth flow.",  
      button: { text: "Open Copilot Studio setup guide", href: "/gql/docs/copilot-setup", target: "\_self" }  
    }  
  ]}  
/>

<ApexAlert type="info" title="Choose your endpoint" message="Replace the URL in each config block below with the endpoint that matches your use case (from the Endpoints section above). The examples use `/mcp-preview` for safety, but you can swap in `/mcp` for production or `/mcp-preview`." />

***

# 5. Verify it's working (Expected Behavior)

<ApexAlert type="success" title="Verification goal" message="Confirm that your MCP server is visible, token auth is valid, and your AI assistant can execute real GraphQL-backed queries." />

Once <Glossary>N-able MCP</Glossary> is configured properly:

✔️ There should be no console errors

- No connection failures
- No token-related errors
- N-able MCP tools visible to the agent

✔ <Glossary>N-able MCP</Glossary> server visible to the agent  
✔ Requests authenticated using an <Glossary>API token</Glossary>  
✔ Agent can resolve the schema and execute queries

***

## Step 1: Quick connection check

After verification, you can test the connection by asking:

<ApexCards  
  gridColsMd={1}  
  items={\[  
    {  
      variant: "qa",  
      adornment: { type: "icon", iconClass: "fa-solid fa-server text-info" },  
      title: "Q&A · Quick connection check",  
      question: "How many devices are you managing?",  
      response: "You are currently managing 42 devices across all your customers.",  
      codeBlocks: \[  
        {  
          language: "graphql",  
          label: "See GraphQL query executed",  
          code: \`# Query may differ between AI models

query GetAssetCount {  
  assetSearch(first: 1) {  
    totalCount  
  }  
}`        },
        {
          language: "json",
          label: "Raw output",
          code:`{  
  "data": {  
    "assetSearch": {  
      "totalCount": 42  
    }  
  }  
}\`  
        }  
      ]  
    }  
  ]}  
/>

***

The agent should have used the default MCP tools to run a <Glossary>GraphQL operation</Glossary> and return an expected output like:

The number will reflect the actual device count in your tenant.

This proves that:

- Authentication is correct
- Default tools are available
- The <Glossary>N-able GraphQL API</Glossary> is reachable

***

### Step 2: Real MSP example

After the quick connection check, try a query that demonstrates an operational use case for <Glossary>MSP automation</Glossary>:

<ApexCards  
  gridColsMd={1}  
  items={\[  
    {  
      variant: "qa",  
      adornment: { type: "icon", iconClass: "fa-solid fa-shield-halved text-warning" },  
      title: "Q&A · Real MSP example",  
      question: "Show me all Windows devices that don't have full BitLocker encryption, grouped by customer.",  
      response: "You have 28 Windows devices without full BitLocker encryption across your customers. Acme Ltd has the most unprotected devices. Would you like me to list them all or break it down by customer?",  
      codeBlocks: \[  
        {  
          language: "graphql",  
          label: "See GraphQL query executed",  
          code: \`# Query may differ between AI models

query UnencryptedWindowsDevices {  
  assetSearch(  
    first: 50  
    where: {  
      bitlocker: { protectionStatus: { notEquals: FULL } }  
      operatingSystem: { type: { equals: WINDOWS } }  
    }  
    orderBy: [{ field: CUSTOMER_NAME, direction: ASC }]  
  ) {  
    totalCount  
    nodes {  
      name  
      bitlocker {  
        protectionStatus  
      }  
      customer {  
        name  
      }  
      operatingSystem {  
        name  
        version  
      }  
    }  
  }  
}`        },
        {
          language: "json",
          label: "Raw output",
          code:`{  
  "data": {  
    "assetSearch": {  
      "totalCount": 28,  
      "nodes": [  
        {  
          "name": "DESKTOP-04",  
          "bitlocker": {  
            "protectionStatus": "NONE"  
          },  
          "customer": {  
            "name": "Acme Ltd"  
          },  
          "operatingSystem": {  
            "name": "Microsoft Windows 11 Pro",  
            "version": "10.0.22621"  
          }  
        },  
        {  
          "name": "LAPTOP-12",  
          "bitlocker": {  
            "protectionStatus": "PARTIAL"  
          },  
          "customer": {  
            "name": "Acme Ltd"  
          },  
          "operatingSystem": {  
            "name": "Microsoft Windows 11 Pro",  
            "version": "10.0.22621"  
          }  
        }  
      ]  
    }  
  }  
}\`  
        }  
      ]  
    }  
  ]}  
/>

***

### Current tools

View the full list of <Anchor label="default and custom tools" target="_blank" href="/gql/docs/mcp-capabilities">default and custom tools</Anchor> currently available.

***

# Error Handling & Troubleshooting

<ApexAlert type="info" title="Fast triage" message="Match the exact symptom first, apply only the paired fix, then retest before changing anything else." />

| Problem                                                 | Likely cause                                                                                                           | Fix                                                                                                                                                                                           |
| ------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 401 Unauthorized                                        | Token is missing, malformed, or has been revoked.                                                                      | Generate a new token at <https://n-able.app/api-token-management> and update your AI tool or IDE configuration.                                                                               |
| 404 Not Found                                           | The endpoint URL is wrong.                                                                                             | Confirm the URL is `https://api.n-able.com/mcp-preview` with no trailing slash.                                                                                                               |
| `spawn npx ENOENT` or `command not found`               | Your MCP client cannot resolve `npx` from PATH (common in desktop apps or service contexts).                           | Set `command` to the absolute `npx` path (for example `C:/Program Files/nodejs/npx`), then restart the client. Verify the path using `where npx` (Windows) or `which npx` (macOS/Linux).      |
| Config contains `C://...` or `/mcp/preview`             | Path/URL uses an incorrect slash pattern from copy/paste.                                                              | Normalize to single-slash Windows paths (`C:/Program Files/nodejs/npx`) and use the correct endpoint format (`https://api.n-able.com/mcp-preview` or `https://api.n-able.com/mcp-read-only`). |
| N-able MCP tools not visible in your AI tool            | The client is misconfigured or was not restarted after setup.                                                          | Re-check your configuration file, save it, and fully restart the IDE or AI tool.                                                                                                              |
| Query returns no results or fewer devices than expected | The token was created by a user who does not have access to all customers in N-able.                                   | Create a new token using an account with the appropriate customer access. See the Permissions section above.                                                                                  |
| `execute` returns an error but other tools work         | `execute` is not enabled in your MCP client configuration.                                                             | Check your MCP configuration and ensure `execute` is explicitly permitted. It is the only tool that requires this.                                                                            |
| Security fields such as BitLocker return `null`         | BitLocker data is only available for Windows devices. Non-Windows devices and some server editions will return `null`. | Filter your query to Windows assets using `operatingSystem: { type: { equals: WINDOWS } }` before checking BitLocker status.                                                                  |
| Your AI assistant reports an unknown field              | The field name may have changed in a recent schema update, or the field does not exist.                                | Use the `search` tool to find the correct field name, or check the schema changelog in the references below for recent changes.                                                               |

***

# Additional References

- CAT-MIP MCP Standard - <https://cat-mip.org/> - External CAT-MIP project documentation related to MCP interoperability.
- CAT-MIP Releases - <https://github.com/cat-mip/cat-mip/releases> - Release history for the CAT-MIP project.

## Share your feedback

<Glossary>N-able MCP</Glossary> is in active development and the tools added next will be shaped by what <Glossary>MSP automation</Glossary> workflows actually need. If something is missing, broken, or could work better, let us know.

***

# Quiz Time

<ApexCards  
  gridColsMd={1}  
  items={[  
  {  
    title: "Ready for a quick challenge?",  
    description:  
      "Take the N-able MCP Quiz to check your understanding and reinforce key concepts.",  
    adornment: {  
      type: "icon",  
      iconClass: "fa-solid fa-graduation-cap",  
    },  
    button: {  
      text: "Take the Quiz",  
      href: "https://developer.n-able.com/gql/docs/n-able-mcp-quiz-time",  
      target: "_self",  
    },  
  },  
]}  
/>