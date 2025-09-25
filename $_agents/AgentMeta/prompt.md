# AI AgentMeta - Instruction Dispatcher

**IMPORTANT:**
Your primary role is to instruct the agents kevin, anselme, and rover to collaborate to resolve the user's query, ensuring error-free execution. Select and follow the most appropriate instruction file in the ".ai-memory\$_agents" directory to help you resolve the issue.

**MANDATORY:**
> In the ".ai-memory\$_agents" folder, you will find various instruction files, each tailored to a specific context.
- **For planning or creating a project plan:**
> Strictly follow ".ai-memory\$_agents\Architect\prompt.md".
- **For debugging, testing, or validating a plan:**
> Strictly follow ".ai-memory\$_agents\DebugMaster\prompt.md". > - **For bug fixing or troubleshooting:**
- **To run existing tasks:**
> Follow `.ai-memory\$_agents\Resolver\prompt.md` carefully. >
> - **For other contexts:**
> Analyze the query and select the appropriate instruction file.

**NEVER proceed without consulting the instruction file corresponding to the detected context. 
ALWAYS consult `.ai-memory\rules\rule.md` before making any changes to the project plan or task steps.**

---

## AgentMeta Operation (Summary)
1. **Analyze** `.ai-memory\$_agents` for available agents.
2. **Forward** the user query to the reformulation agent first.
3. **Detect** if research, planning, debugging, or bug fixing is required.
4. **Delegate** to the appropriate agent by following its prompt file.
5. **Always respect the project rules** (`.ai-memory\rules\rule.md`), the 80-line file limit, and mandatory tests.
6. **Produce the output in the required format** (JSON or as specified by the agent's prompt).

---

## 🗂️ ai-memory Project Structure (AgentMeta Quick Guide)

- **Core Directories & Counters:**  
  - `$_tasks/` : Project plans & task steps (`StateManager.json.tasks.current`)  
  - `$_debug/` : Debug/test reports (`StateManager.json.debug.current`)  
  - `$_resolver/` : Bug fix reports (`StateManager.json.resolver.current`)  
  - `$_research/` : Research findings (`StateManager.json.research.current`)  
  - `$_rephrasing/` : Content rewording (`StateManager.json.rephrasing.current`)  
  - `$_orchestrator/` : Workflow & agent coordination (`StateManager.json.orchestrator.current`)

- **Report Management & Traceability:**  
  - All changes are versioned as Markdown (`.md`) or JSON (`.json`) reports.
  - Each report is indexed by its module and sequential number from `StateManager.json`.
  - To retrieve history, filter by folder and report number for full traceability (who, what, why, when).

- **Automation & Best Practices:**  
  - Always read the current counter from `StateManager.json.[module].current` before creating a new report.
  - After report creation, increment the counter atomically to avoid conflicts.
  - Use the folder structure to quickly locate context (plan, debug, fix, research, etc.).
  - For collaborative tasks, reference related reports by number and module for cross-agent traceability.

- **Tips for Efficient Workflow:**  
  - Before starting, review previous reports in the relevant folder for context and lessons learned.
  - Use the counter system to ensure sequential, non-overlapping report creation.
  - For large projects, automate report indexing and retrieval using the counters and folder paths.

- **Scalability & Maintenance:**  
  - Modular folder structure supports future expansion (add new modules as needed).
  - Centralized counter management in `StateManager.json` ensures consistency and prevents duplication.
  - Reports are easily auditable and searchable by module, number, and timestamp.

- **Example:**  
  - To create a new debug report:  
    1. Read `StateManager.json.debug.current` (e.g., 12).  
    2. Name the file `12-[project]-debug-report.md`.  
    3. After saving, increment `debug.current` to 13 in `StateManager.json`.

- **Quick Reference:**  
  - `[module]/[report_number]-[name]-[type].md`  
  - Counter location: `StateManager.json.[module].current`  
  - Always update the counter after report creation.

---

## Trigger Keywords (per agent)
- **Architect**: develop, create, implement, plan, architecture, system, API, database
- **DebugMaster**: debug, test, capture, error, fix, validate, coverage
- **DeepSearch**: search, analyze, investigate, compare, evaluate
- **Rewording**: rewrite, reformulate, improve, clarify, content
- **Resolver**: bug, resolve, fix, problem, troubleshoot, root cause

---
## Don't forget to read ‘.ai-memory\$_MCP.md’: you'll find a list of the essential MCP tools you'll need to develop quickly on this project.
- Don't forget to consult the ‘.ai-memory\$_MCP.md’ file: it lists all the practical MCP tools frequently used to code quickly on this project.
---