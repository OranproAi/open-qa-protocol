# Contributing to the Open QA Protocol (OQP)

First, thank you for your interest in contributing to the Open QA Protocol! We are building the foundational infrastructure for agentic software verification, and community input is essential to making this standard robust and universal.

This document outlines the process for proposing changes, adding extensions, and improving the specification.

## How to Contribute

The OQP specification is hosted in the `spec/` directory of this repository as an OpenAPI 3.1 YAML file.

### 1. Reporting Issues and Requesting Features

If you find a bug in the specification, or if you have an idea for a new core capability, please open an issue in the GitHub issue tracker.

*   **Bug Reports:** Clearly describe the issue, the expected behavior, and the actual behavior. Provide a snippet of the OpenAPI YAML if applicable.
*   **Feature Requests:** Describe the use case and why the current specification is insufficient. Propose a specific change to the OpenAPI schema if possible.

### 2. Proposing Changes to the Core Specification

If you want to propose a change to the core OQP specification (e.g., adding a new endpoint, modifying an existing schema, or clarifying the documentation), please follow these steps:

1.  **Fork** the repository.
2.  **Create a branch** for your feature or bug fix (`git checkout -b feature/my-new-capability`).
3.  **Modify the OpenAPI YAML file** in the `spec/` directory. Ensure your changes are valid OpenAPI 3.1.
4.  **Update the Documentation** in the `docs/` directory or the `README.md` if your change introduces new concepts.
5.  **Commit** your changes with a descriptive commit message.
6.  **Push** to your fork and submit a **Pull Request (PR)** against the `main` branch.

### 3. The Extension Model (No PR Required)

OQP is designed to be an "open bazaar." You do not need to submit a PR to add a custom capability to your own OQP server implementation.

If you are a vendor (e.g., a security scanning tool, a performance monitoring platform, or a specialized testing framework) and you want to expose your capabilities via OQP, you should use the **Extension Model**.

1.  Define your custom capability using reverse-domain naming (e.g., `com.yourcompany.security_scan`).
2.  Advertise this capability in your server's `/.well-known/oqp` manifest.
3.  Agents that understand your extension will negotiate it during discovery. Agents that do not will safely ignore it.

If an extension becomes widely adopted by the community, we may propose pulling it into the core specification in a future version.

## Code of Conduct

By participating in this project, you agree to abide by our Code of Conduct. We expect all contributors to be respectful, inclusive, and constructive in their interactions.

## License Agreement

By contributing to the Open QA Protocol, you agree that your contributions will be licensed under the Apache License 2.0.
