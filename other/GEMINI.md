# Important: Always consult the project behavior and rules file at ‘.ai-memory\$_rules\rule.md’ before making any changes, to ensure compliance and avoid errors.
# When processing a request, you should always run tests to check that the problem has been solved.
# It's really important to run tests and check logs.
# This ‘.ai-memory\$_rules\rule.md’ file contains essential guidelines and instructions for project maintenance.
# Always use AI agents Kevin “.ai-memory\$_agents\Architect\prompt.md” to develop the best plan before starting work.
# Always use AI agents such as Kevin '.ai-memory\$_agents\Architect\prompt.md' , Anselme .ai-memory\$_agents\DebugMaster\prompt.md, and Rover '.ai-memory\$_agents\Resolver\prompt.md' to process requests.
## 🗂️ ai-memory Project Structure (Memory and History Structure)

- **Folders & Paths:**  
  - `$_tasks/` : Plans & task steps (`$_tasks\currentTaskNumber.txt`)  
  - `$_debug/` : Debug & test reports (`$_debug\currentTaskNumber.txt`)  
  - `$_resolver/` : Bug fix reports (`$_resolver\currentTaskNumber.txt`)  
  - `$_research/` : Research findings (`$_research\currentTaskNumber.txt`)  
  - `$_rephrasing/` : Content rewording (`$_rephrasing\currentTaskNumber.txt`)  
  - `$_orchestrator/` : Workflow & agent coordination (`$_orchestrator\currentTaskNumber.txt`)

- **Report History:**  
  - All changes are tracked in Markdown (`.md`) or JSON (`.json`) reports.
  - Use these files to quickly recall what was done, by whom, and why.

- **Tip:**  
  - If `currentTaskNumber.txt` in a folder (e.g. `$_orchestrator\currentTaskNumber.txt`) shows `20`, then 19 reports exist in that folder—your full project history is in these files.

- **Best Practice:**  
  - Browse old reports for context before making new changes.
  - Each agent and phase leaves a trace—use it to avoid repeating mistakes and to understand decisions.

- **Extra:**  
  - Reports are sequentially numbered for easy tracking.
  - Always update the relevant `currentTaskNumber.txt` after creating a new report.
  - Use folder names and paths to find the right context (plan, debug, fix, research, etc.).
  - Check the `currentTaskNumber.txt` in each main folder to know how many reports exist and where to add the next one.