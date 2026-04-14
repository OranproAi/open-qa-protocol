# Open QA Protocol (OQP)

The Open QA Protocol (OQP) is an open standard designed to facilitate agentic software verification. It provides a common language for coding agents, CI/CD pipelines, and human developers to query semantic business rules, assess release risk, and execute autonomous testing workflows against a centralized Knowledge Graph.

## Why OQP?

In the era of agentic software development, the bottleneck is no longer writing code—it is verifying that the code satisfies business requirements. Traditional UI-driven testing tools and monolithic dashboards are incompatible with autonomous agents. 

OQP solves this by defining a standardized set of API primitives that allow any agent (e.g., Cursor, Claude Code, GitHub Copilot) to:
1. **Discover** testing capabilities available in a repository.
2. **Query** the semantic business rules and historical edge cases for a specific workflow.
3. **Assess** the risk of a proposed code change before merging.
4. **Execute** sandboxed, autonomous verification workflows.

## The Specification

The core of OQP is an OpenAPI 3.1 specification.

*   [View the latest OQP Specification (YAML)](spec/oqp-v1.0.0.yaml)
*   [Read the Documentation](docs/getting-started.md)

### Core Primitives

OQP defines four primary interactions:

| Endpoint | Purpose | Caller |
| :--- | :--- | :--- |
| `GET /.well-known/oqp` | Capability discovery. Agents query this to learn what the server supports. | Coding Agents |
| `GET /context/workflows/{id}` | Returns semantic business rules and historical incidents for a workflow. | Coding Agents (via MCP) |
| `POST /verification/assess-risk` | Submits a PR diff and returns a risk score, impacted workflows, and coverage gaps. | CI/CD Pipelines |
| `POST /verification/execute` | Triggers an autonomous sandboxed testing agent to verify a change. | Engineering Managers / Release Gates |

## How it Works (The Agentic Flow)

OQP is designed to be the "Green Contract" between a coding agent and a verification agent. 

1.  **Context Phase:** A developer (or coding agent) begins working on the "Guest Checkout" flow. The agent queries the OQP server (`GET /context/workflows/checkout_flow`) to retrieve the business rules and known edge cases *before* writing code.
2.  **Implementation Phase:** The code is written, guided by the semantic context.
3.  **Verification Phase:** A pull request is opened. The CI/CD pipeline queries the OQP server (`POST /verification/assess-risk`) with the diff. The server maps the syntactic changes to the semantic Knowledge Graph and returns a risk score.
4.  **Execution Phase:** If the risk is high, or if tests are missing, the pipeline triggers an autonomous verification agent (`POST /verification/execute`). The agent generates tests, runs them, and attempts recovery until the "Green Contract" is satisfied.

## Extensibility

OQP is designed to be an "open bazaar" of capabilities. No central committee is required to approve new features. Implementers can extend the protocol using reverse-domain naming (e.g., `com.yourcompany.custom_capability`).

Agents negotiate capabilities during the discovery phase (`GET /.well-known/oqp`). If an agent doesn't support an extension, it gracefully degrades to the core specification.

## Contributing

We welcome contributions from the community! Please see our [Contributing Guide](CONTRIBUTING.md) for details on how to propose changes to the specification.

## License

The Open QA Protocol specification is licensed under the [Apache License 2.0](LICENSE).

## Contributors

OQP is shaped by practitioners and researchers across the software quality, AI, and developer tooling communities. We are grateful to the following contributors for their review and endorsement of the specification:

| Name | Organization | Role |
|------|-------------|------|
| [Philip Lew](https://www.linkedin.com/in/philiplew ) | XBOSoft | Specification Reviewer & Endorser |
| [Benjamin Young](https://www.linkedin.com/in/bigbluehat ) | W3C JSON-LD Working Group | JSON-LD Knowledge Graph Context Lead |
