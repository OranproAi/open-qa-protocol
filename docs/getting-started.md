# Getting Started with OQP

Welcome to the Open QA Protocol (OQP). This guide will help you understand how to implement an OQP server or build an agent that consumes the OQP standard.

## For Server Implementers

If you are building a QA tool, testing framework, or Knowledge Graph (like OrangePro), you should implement the OQP server specification.

### Step 1: Expose the Discovery Endpoint
Your server must expose `GET /.well-known/oqp`. This endpoint returns a JSON manifest declaring the capabilities your server supports.

```json
{
  "protocol_version": "1.0.0",
  "capabilities": [
    "context.read",
    "verification.execute"
  ],
  "extensions": {}
}
```

### Step 2: Implement the Core Capabilities
Depending on what you advertised in the discovery endpoint, you must implement the corresponding routes defined in the OpenAPI specification.
* If you advertise `context.read`, you must implement `GET /context/workflows/{workflow_id}`.
* If you advertise `verification.execute`, you must implement `POST /verification/execute`.

## For Agent Developers

If you are building a coding agent (like a Cursor plugin, Claude Code extension, or custom CLI tool), you can use OQP to give your agent semantic awareness.

### Step 1: Discover Capabilities
When your agent initializes in a repository, it should query the configured OQP server's `/.well-known/oqp` endpoint to see what testing capabilities are available.

### Step 2: Query Context Before Coding
Before your agent writes code for a specific feature, it should query the OQP server for the semantic business rules.

```bash
curl -X GET https://api.your-oqp-server.com/v1/oqp/context/workflows/checkout_flow \
  -H "Authorization: Bearer YOUR_TOKEN"
```

The response will provide your agent with the necessary business rules and historical edge cases to ensure the generated code is semantically correct.

## Next Steps
* Read the [Core Concepts](core-concepts.md) to understand the philosophy behind OQP.
* Learn how to extend the protocol in [Extensions](extensions.md).
