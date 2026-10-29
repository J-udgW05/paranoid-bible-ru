# Antigravity Tool Mapping for Superpowers

When skills describe actions, in Antigravity they map to these native tools:

| Action in Skill | Antigravity Native Tool | Description |
|-----------------|-------------------------|-------------|
| Read a file | `read_file` | Read contents of file with line numbers |
| Create a new file | `write_file` | Write content to a new or existing file |
| Edit an existing file | `edit_file` | Precise search and replace |
| Run shell command | `run_command` | Execute PowerShell command in workspace |
| Ask the user | `ask_question` | Present options or question modal |
| Dispatch subagent | `invoke_subagent` | Launch background subagent (`TypeName: "self"` or `"research"`) |
| Manage subagent | `manage_subagents` / `send_message` | List, kill, or message active subagents |
| Search the web | `search_web` | Query web search |
| Task tracking | Artifacts in `<appDataDir>/brain/<id>` | Create structured plans and progress checklists |
