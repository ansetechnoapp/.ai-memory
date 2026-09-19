# AI Memory Project Structure

## Overview
This project serves as a foundation for an autonomous agent ecosystem, with AgentMeta (kevin) as the central orchestrator.

## Core Components
### 1. Agent System
- **AgentMeta (kevin)**: Central orchestrator
- **Specialist Agents**:
  - Architect: Project planning and architecture
  - Rephrasing (kita): Request analysis and optimization
  - DebugMaster: Testing and validation
  - Resolver: Task execution
  - DeepSearch: Research and analysis

### 2. Core Architecture
- **State Management**: `.ai-memory/StateManager.json`
  - Task counters
  - Validation system
  - Audit trails

- **Rules & Standards**: `.ai-memory/$_rules/`
  - Project rules (rule.md)
  - Documentation standards (rule2.md)
  - Code quality guidelines

### 3. Agent Directories
`.ai-memory/$_agents/`
- **Architect/**: Planning and architecture design
- **Rephrasing/**: Query optimization and analysis
- **DebugMaster/**: Testing and validation
- **Resolver/**: Task execution
- **DeepSearch/**: Research capabilities

## Key Features
- Message broker-based communication
- Event-driven architecture
- Centralized state management
- Automated testing and validation
- Documentation-first approach
- 80-line file size limit
- Incremental development process

## Integration Points
- Designed for easy integration with other projects
- Standardized interfaces and protocols
- Centralized memory and state management