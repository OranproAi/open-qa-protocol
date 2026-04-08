# Core Concepts of OQP

The Open QA Protocol (OQP) is built on a few fundamental concepts that shift the paradigm of software testing from "human-driven execution" to "agentic verification."

## 1. The Verification Surface
In traditional testing, the "surface" is a web UI (e.g., a dashboard showing green and red checkmarks). In the agentic era, the surface is an API protocol. OQP acts as the central Verification Surface where agents can declare intent ("Verify this PR") and other agents can execute the work.

## 2. Semantic vs. Syntactic Testing
Most testing tools today are syntactic: they understand code structure, ASTs, and PR diffs. OQP is designed to be **semantic**: it understands business logic. 

When an agent queries OQP for context on a "Checkout" workflow, OQP doesn't return the `checkout.js` file. It returns the business rules ("Orders over $500 require manual review") and historical edge cases ("Guest checkout fails if email has a plus sign"). This is what allows coding agents to write correct code the first time.

## 3. The Green Contract
The "Green Contract" is an agreement between the developer (or coding agent) and the verification agent. It defines the required level of confidence before a change can be shipped.

OQP defines four levels of the Green Contract:
*   `TARGETED_TESTS`: The specific change is covered by unit tests.
*   `PACKAGE`: The entire package/module containing the change is verified.
*   `WORKSPACE`: The entire monorepo/workspace is verified.
*   `MERGE_READY`: All business workflows impacted by the change have been verified end-to-end, and no semantic regressions were found.

## 4. Capability Negotiation
Not all OQP servers are created equal. A basic open-source implementation might only support `context.read`. An enterprise implementation (like OrangePro) might support `verification.execute` and custom extensions like `com.orangepro.wind_tunnel`.

Agents use the `/.well-known/oqp` endpoint to discover what the server is capable of, allowing for graceful degradation if a feature is missing.
