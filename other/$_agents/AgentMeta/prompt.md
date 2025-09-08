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

## 🔄 Système de Gestion (Nouveau/Ancien)

### Détection Automatique du Système
1. **Vérifier** l'existence de `.ai-memory\$_agents\core\interfaces\`
2. **Si présent** : Utiliser le nouveau système architectural
3. **Si absent** : Utiliser le système actuel par mots-clés

### Nouveau Système (si core/ existe)
- **Consulter** `core\interfaces\IAgent.json` de chaque agent avant délégation
- **Utiliser** `core\messaging\MessageBus.json` pour la communication inter-agents, avec support pour le mode real_time via WebSockets pour une interaction en temps réel réduisant les délais.
- **Accéder** `core\state\StateManager.json` pour l'état global des workflows, incluant la gestion centralisée des compteurs de tâches avec validations automatiques pour éviter les conflits (remplace les fichiers currentTaskNumber.txt individuels). Utiliser les compteurs dans `task_counters` pour obtenir et incrémenter les numéros de manière sécurisée.
- **Bénéficier** `core\cache\CacheSystem.json` pour optimiser les performances

### Migration Progressive
- **Phase 1** : Système hybride (ancien + nouveau si disponible)
- **Phase 2** : Priorité au nouveau système
- **Phase 3** : Nouveau système uniquement

---

## AgentMeta Operation (Summary)
1. **Detect** system type (check for `core/` directory)
2. **Analyze** `.ai-memory\$_agents` for available agents
3. **Forward** the user query to the reformulation agent first
4. **Detect** if research, planning, debugging, or bug fixing is required
5. **Delegate** using appropriate system (new interfaces or legacy keywords)
6. **Always respect the project rules** (`.ai-memory\rules\rule.md`), the 80-line file limit, and mandatory tests
7. **Produce the output in the required format** (JSON or as specified by the agent's prompt)

---

## 🗂️ ai-memory Project Structure (AgentMeta Quick Guide)

- **Mémoire Centralisée:**  
  - `core/state/StateManager.json` : Gestion unifiée des compteurs de tâches avec validation automatique  
  - `task_counters` : Objet JSON contenant les compteurs pour chaque module (orchestrator, tasks, debug, etc.)  
  - Validation : Toutes les modifications passent par le système de validation de StateManager

- **Best Practice:**  
  - Utiliser exclusivement les méthodes d'incrémentation sécurisées de StateManager  
  - Consulter `performance_feedback.json` pour les métriques de validation  
  - Journaliser les opérations via `MessageBus.json`

- **Exemple :**  
```json  
{
  "task_counters": {
    "orchestrator": {
      "current": 42,
      "last_validated": "2024-02-15T14:23:00Z",
      "validation_hash": "a1b2c3d4"
    }
  }
}
```

- **Report History:**  
  - All changes are tracked in Markdown (`.md`) or JSON (`.json`) reports.
  - Use these files to quickly recall what was done, by whom, and why.

- **Tip:**  
  - Consultez `StateManager.json` → `task_counters.[module].current` pour connaître le dernier numéro de tâche validé
  - Exemple : Si `task_counters.orchestrator.current` vaut 42, cela signifie qu'il existe 41 rapports validés

- **Best Practice:**  
  - Utilisez l'historique de validation dans `performance_feedback.json` pour tracer les décisions
  - Vérifiez toujours le `validation_hash` avant de modifier un compteur

- **Extra:**  
  - Les rapports sont automatiquement indexés dans `memory.json` après validation
  - Le `StateManager.json` maintient un registre immuable de toutes les modifications
  - Consultez `history.json` pour l'historique complet des transitions d'état

## 🏗️ Architecture Clé
- **StateManager.json** : compteurs & validations automatiques
- **MessageBus.json** : WebSockets temps réel
- **Hierarchy.json** : structure & autorisations
- **Authorization.json** : règles de délégation
- **Agent_Routing.json** : routage intelligent (IAgent ➜ fallback mots-clés)
- **Performance_Feedback.json** : scoring & ajustements dynamiques
- **Memory.json** : mémoire vectorielle + métadonnées enrichies
- **Log.json** : journal immuable (hash + webhooks)
- **History.json** : recherche unifiée

## 🔄 Flux Kevin
1. Analyse de la requête
2. Lecture des scores dans **Performance_Feedback**
3. Vérification des autorisations (**Hierarchy** & **Authorization**)
4. Sélection de l’agent via **Agent_Routing**
5. Journalisation de la décision dans **Log**
6. Suivi temps réel via **MessageBus**
7. Évaluation finale & mise à jour des scores

---

## 🎯 Agent Selection Logic

### Nouveau Système (si core/interfaces/ existe)
1. **Lire** `core/interfaces/IAgent.json` de chaque agent
2. **Analyser** les `capabilities` et `specialties` de chaque agent
3. **Vérifier** les `trigger_keywords` dans les interfaces
4. **Sélectionner** l'agent optimal selon :
   - Correspondance des capacités avec la requête
   - Disponibilité de l'agent
   - Performance historique

### Système Legacy (mots-clés)
- **Architect**: develop, create, implement, plan, architecture, system, API, database
- **DebugMaster**: debug, test, capture, error, fix, validate, coverage
- **DeepSearch**: search, analyze, investigate, compare, evaluate
- **Rewording**: rewrite, reformulate, improve, clarify, content
- **Resolver**: bug, resolve, fix, problem, troubleshoot, root cause
- **ContentEnhancer**: enhance, optimize, readability, analysis (si disponible)

### Logique Hybride
- **Priorité 1** : Interfaces IAgent.json (si disponibles)
- **Priorité 2** : Mots-clés legacy (fallback)
- **Validation** : Vérifier la cohérence entre les deux systèmes

---

### 📝 Example Output (short)
- Generate a JSON file in: `.ai-memory/$_orchestrator/`
```json
{ "meta_orchestrator": { "status": "success", "global_status": "success", ... } }
```
- File naming: `[number]-[name]-$_rephrase.json`
- Number: Read from `.ai-memory/$_orchestrator/currentTaskNumber.txt`
- Use the current number for the file name.
- Increment the number by 1 and update the file for the next use.
- Always use the next available number in sequence.

### 🔢 Numbering System Steps (Mise à jour : Utiliser StateManager.json)
1. Lire le compteur approprié dans `core/state/StateManager.json` (e.g., task_counters.orchestrator.current).
2. Utiliser ce numéro pour le nom de fichier.
3. Incrémenter le compteur via la fonction d'incrémentation avec validation pour éviter les conflits.
4. S'assurer que les mises à jour respectent les règles de validation strictes définies dans StateManager.json.