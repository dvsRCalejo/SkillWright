# SkillWright

SkillWright is a Copilot Studio agent package focused on installing and managing skills using `skills-for-copilot-studio` patterns.

## What This Repo Requires

Before importing or running the agent, make sure all requirements below are satisfied.

1. Copilot Studio environment is available and you can open the target agent.
2. The Power Platform environment is a **Managed Environment**.
3. **Dataverse Intelligence** is enabled for the environment.
4. You have permissions to import connectors, manage connections, and import agent assets.
5. The `skills-for-copilot-studio` VS Code tooling is installed for local authoring and validation.

## Environment Requirements

### Managed Environment

SkillWright should be deployed to a managed environment to ensure governance, policy, and enterprise controls are in place.

Recommended checks:

1. Confirm the target environment is marked as Managed Environment in Power Platform admin center.
2. Confirm DLP and connector governance policies allow the GitHub custom connector.
3. Confirm solution import and connector creation are not blocked by tenant policy.

### Dataverse Intelligence

SkillWright assumes Dataverse Intelligence capabilities are enabled for intelligent behaviors and advanced orchestration patterns.

Recommended checks:

1. Confirm Dataverse Intelligence is enabled in the target environment.
2. Confirm the environment has required capacity and licensing for Dataverse-backed features.
3. Confirm users running the agent can access required Dataverse resources.

### Why Dataverse Intelligence Matters For Business Skills

Dataverse Intelligence helps the agent move from simple Q&A into business-aware automation.

It enables richer enterprise scenarios by allowing skills to:

1. Use business context from Dataverse data, not just prompt text.
2. Route actions based on business entities, relationships, and rules.
3. Produce more reliable and relevant responses in line with organizational data.
4. Support repeatable workflows where skills can be reused across departments and use cases.

Without this layer, skills can still run, but they are typically less contextual and less aligned with real business processes.

## What Are Business Skills?

Business skills are reusable, task-focused capabilities an agent can invoke to complete a business outcome.

In practice, a business skill usually combines:

1. A clear intent (what the user wants done).
2. A connector or API action (how the action is executed).
3. Optional business data context (who/what/where in business terms).
4. A safe response pattern (how results and errors are returned to the user).

For SkillWright, examples of business skills include:

1. Finding skill collections in GitHub repositories for a specific capability.
2. Discovering agent skill definitions and returning install-ready references.
3. Listing repository files recursively to evaluate skill package structure.
4. Pulling file content to inspect installation metadata or manifests.

## Example Ways To Use This Agent

After setup is complete, use SkillWright for scenarios like:

1. "Find me skill collections for IT service management in GitHub."
2. "Search for agent skills related to employee onboarding."
3. "List all files in this repo so I can verify skill packaging."
4. "Get the default branch and inspect installation files before import."
5. "Retrieve this skill definition file content and summarize what it installs."

### Example Workflow: Discover Then Validate A Skill

1. Ask the agent to search GitHub for relevant skills.
2. Ask it to list repository contents.
3. Ask it to fetch target files (metadata, docs, manifests).
4. Review compatibility with your managed environment and governance policies.
5. Import the custom connector and complete the installation sequence.

## Required Installation Order

Install in this order to avoid broken references:

1. **Install the custom connector first** (`Github-Search.swagger.json`).
2. Create/authorize connector connections.
3. Import agent files and solution assets.
4. Map all connection references.
5. Validate actions and topic triggers.

If you import the agent first, action steps may fail because connection references to the GitHub connector do not yet exist.

## Setup Steps

1. Clone this repository.
2. Open the workspace in VS Code.
3. Install `skills-for-copilot-studio` tooling if not already installed.
4. Import the custom connector from `Custom Connector/Github-Search.swagger.json`.
5. Complete connector authentication and test a connector operation.
6. Import the agent package from the `Skills Agent` folder.
7. Bind connection references in `connectionreferences.mcs.yml` to the created connector connection.
8. Validate key topics, especially `Search.mcs.yml`, and run a test conversation.

## Post-Install Validation

Run this quick validation checklist after import:

1. Connector operations run successfully from the connector test panel.
2. Agent opens without unresolved dependency warnings.
3. Topic `Search` invokes GitHub actions and returns results.
4. No missing connection references remain.
5. `OnError` topic gracefully handles connector/API failures.

## Troubleshooting

### Action Fails With Connection Error

Likely cause: connector installed but connection reference was not mapped.

Fix:

1. Open `Skills Agent/connectionreferences.mcs.yml`.
2. Rebind to the valid connector connection.
3. Re-run action test.

### Topic Runs But Returns No GitHub Data

Likely cause: connector auth is incomplete or token scope is insufficient.

Fix:

1. Re-open connector connection settings.
2. Re-authorize the connection.
3. Test the `SearchGitHubforAgentSkills` action directly.

### Import Succeeds But Agent Behaves Inconsistently

Likely cause: environment requirements are partially met.

Fix:

1. Re-check Managed Environment status.
2. Re-check Dataverse Intelligence configuration.
3. Validate DLP and connector policy alignment.

## Notes

- The custom connector is a hard dependency for action invocations.
- Importing the connector first is mandatory for a reliable setup.
- Managed Environment plus Dataverse Intelligence should be treated as baseline platform requirements.
