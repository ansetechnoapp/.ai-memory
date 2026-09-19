# Project Structure Documentation

## Directory Layout
```
.ai-memory/
├── $_agents/               # Agent-specific logic and configuration
│   ├── AgentMeta/         # Central orchestrator
│   ├── Architect/         # Planning specialist
│   ├── Rephrasing/       # Query optimization
│   └── [other agents]/   # Additional specialist agents
├── $_rules/               # Project rules and standards
│   ├── rule.md           # Core project rules
│   └── rule2.md          # Documentation standards
├── $_tasks/              # Generated task plans and reports
├── core/                 # Core system components
│   ├── state/            # State management
│   └── interfaces/       # Agent interfaces
├── architecture/         # Architecture documentation
└── other/               # Additional resources
```

## Key Files
- `StateManager.json`: Central state and counter management
- `$_agents/*/config.json`: Agent-specific configuration
- `$_agents/*/prompt.md`: Agent instruction sets

## Integration Points
1. **Agent Integration**
   - Use $_agents directory structure
   - Follow agent interface definitions
   - Implement required hooks

2. **State Management**
   - Use StateManager.json for counters
   - Follow validation protocols
   - Maintain audit trails

3. **Testing Requirements**
   - Create test scripts for all changes
   - Follow 80-line limit
   - Implement incremental testing
