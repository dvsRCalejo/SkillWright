# SkillWright

SkillWright is a Copilot Studio agent package focused on installing and managing skills using `skills-for-copilot-studio` patterns.

## Prerequisites

Before importing or running the agent, ensure the following requirements are met:

1. Copilot Studio environment is available and accessible.
2. A **Managed Environment** is enabled for your target Power Platform environment.
3. **Dataverse Intelligence** capabilities are enabled in the environment.
4. Required permissions are granted to import connectors, solutions, and agent assets.
5. `skills-for-copilot-studio` extension/tooling is installed in VS Code (or equivalent authoring workflow).

## Installation Order (Important)

Install assets in this order to avoid dependency issues:

1. **Install the custom connector first** (GitHub Search connector).
2. Validate connector connection references and authentication.
3. Import or deploy the agent assets.
4. Bind/update connection references.
5. Test starter topics and action calls.

## Notes

- The custom connector is a hard dependency for action invocations.
- If connector references are missing, topic actions that call GitHub APIs will fail.
- For best results, deploy in a managed environment aligned with Dataverse Intelligence requirements.
