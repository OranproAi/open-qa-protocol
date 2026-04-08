# Extending OQP

The Open QA Protocol is designed to be an "open bazaar." The core specification provides the foundation for agentic verification, but it cannot possibly anticipate every testing methodology, security scanner, or performance monitoring tool.

To solve this, OQP uses an **Extension Model**.

## How Extensions Work

An extension is a custom capability that an OQP server implements. It is not part of the core OpenAPI specification. Instead, the server advertises the extension in its `/.well-known/oqp` manifest, and agents that understand the extension can use it.

### 1. Reverse-Domain Naming
To prevent naming collisions, all extensions must use reverse-domain naming. 
* If OrangePro creates a custom Wind Tunnel simulation capability, it should be named `com.orangepro.simulation.wind_tunnel`.
* If Sentry creates an incident context capability, it should be named `com.sentry.incident_context`.

### 2. Advertising Extensions
When an agent queries `GET /.well-known/oqp`, the server returns the extensions it supports in the `extensions` object:

```json
{
  "protocol_version": "1.0.0",
  "capabilities": [
    "context.read",
    "verification.execute"
  ],
  "extensions": {
    "com.orangepro.simulation.wind_tunnel": true,
    "com.sentry.incident_context": true
  }
}
```

### 3. Agent Negotiation
When an agent (like Claude Code) connects to the OQP server, it checks the `extensions` object. 

If the agent knows how to use `com.orangepro.simulation.wind_tunnel`, it can send custom payloads or query custom endpoints defined by OrangePro's documentation. 

If the agent does not recognize `com.sentry.incident_context`, it safely ignores it and falls back to the core OQP capabilities.

## Proposing Extensions for the Core Spec
If an extension becomes widely adopted by the community (e.g., multiple vendors implement `com.example.accessibility_scan`), the community can propose pulling that capability into the core OQP specification via a Pull Request.
