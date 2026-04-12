---
title: "Obsidian Bases"
type: concept
tags: [obsidian, databases, data-structures, views, notion-like]
created: 2026-04-12
updated: 2026-04-12
sources: ["raw/Obsidian 必装 Skills.md", "raw/Obsidian 官方 CLI 命令全景速查表.md"]
confidence: high
---

## Definition

Obsidian Bases is a native database feature in [[entities/obsidian]] (v1.12+) that creates Notion-like dynamic views of notes as structured data tables, cards, lists, or maps. Bases are defined by `.base` YAML configuration files that specify filters, formulas, and display options.

## How It Works

**Architecture**:
- `.base` files are YAML configurations stored in vault
- Reference note properties (frontmatter YAML) or file metadata
- Generate dynamic views without duplicating note content
- Support formulas for calculated fields

**File Structure**:
```yaml
# example-projects.base
source: "Projects/"
filters:
  - tag: "#project"
  - property: status
    value: active
views:
  - type: table
    columns: [name, deadline, progress]
formulas:
  daysRemaining: "deadline - today()"
```

**View Types**:
1. **Table**: Spreadsheet-like rows and columns
2. **Cards**: Kanban-style cards (grouped by property)
3. **List**: Simple bullet list with metadata
4. **Map**: Geographic visualization (requires Maps plugin)

**Formula System**: Can read:
- Frontmatter properties (status, tags, custom fields)
- File metadata (creation date, modification time, word count)
- Perform calculations (date arithmetic, string operations, conditionals)

## Key Features

**Dynamic Filtering**:
```yaml
filters:
  - folder: "Projects"
  - property: status
    operator: not_equals
    value: "archived"
  - property: deadline
    operator: less_than
    value: "2026-12-31"
```

**Computed Fields**:
```yaml
formulas:
  progress: "tasksCompleted / tasksTotal * 100"
  daysLate: "today() - deadline"
  priority: "if(deadline < today() + 7, 'urgent', 'normal')"
```

**Aggregation**:
```yaml
summaries:
  - type: count
    field: status
  - type: sum
    field: budget
  - type: average
    field: completion
```

**CLI Integration**:
```bash
# List all Bases
obsidian bases

# List views in a Base
obsidian base:views file=Projects

# Create new record
obsidian base:create file=Contacts name="John Doe" email="john@example.com"

# Query and export
obsidian base:query file=Projects view=Active format=json > active-projects.json
obsidian base:query file=Projects view=Active format=csv > export.csv
```

## When To Use

**Ideal for**:
- **Project management**: Track tasks, deadlines, status across many projects
- **Contact management**: People database with tags, relationships, context
- **Content calendar**: Blog posts, videos with publication dates and status
- **Habit tracking**: Daily habits with completion checkboxes and streaks
- **Finance**: Expenses, income, budgets with calculations
- **Research**: Papers database with citations, reading status, notes links

**Better than traditional Dataview when**:
- Need GUI for non-technical users
- Want pre-built views that are easy to share
- Require complex formulas beyond Dataview's query language
- Need export to CSV/JSON for external tools

**Worse than Dataview when**:
- Need maximum query flexibility (Dataview's JavaScript)
- Already invested in Dataview query syntax
- Prefer inline queries embedded in notes

## Risks & Pitfalls

**Learning Curve**: Formula syntax is powerful but requires learning. Start with simple filters before complex calculations.

**Performance**: Large Bases (1,000+ notes) with complex formulas can slow down Obsidian. Use folder/tag filters to limit scope.

**Breaking Changes**: `.base` files are relatively new (2026). Syntax may evolve, requiring migration.

**Property Consistency**: Bases rely on consistent frontmatter. Typos in property names (`status` vs `Status`) break filters.

**Maps Dependency**: Map view requires additional Maps plugin installation.

**AI Generation**: While [[concepts/agent-skills]] can generate `.base` files, complex formulas may need human review. AI can create invalid syntax.

## Formula Examples

**Date Calculations**:
```yaml
daysUntilDeadline: "deadline - today()"
overdueBy: "if(deadline < today(), today() - deadline, 0)"
weekNumber: "week(deadline)"
```

**String Operations**:
```yaml
fullName: "firstName + ' ' + lastName"
initials: "left(firstName, 1) + left(lastName, 1)"
```

**Conditional Logic**:
```yaml
priority: "if(deadline < today() + 3, 'critical', if(deadline < today() + 7, 'high', 'normal'))"
status: "if(tasksCompleted == tasksTotal, 'done', 'in progress')"
```

**Aggregations**:
```yaml
totalBudget: "sum(budget)"
avgProgress: "average(progress)"
completedCount: "count(status == 'done')"
```

## Related Concepts

- [[concepts/obsidian-cli]] — CLI commands for Base operations
- [[concepts/agent-skills]] — obsidian-bases Skill generates `.base` files
- [[concepts/automation-workflows]] — Workflow 5 uses Bases for external data

## Related Entities

- [[entities/obsidian]] — Application providing Bases feature
- [[entities/steph-ango]] — Maintains obsidian-bases Skill

## Sources

- [[summaries/obsidian-essential-skills]] — obsidian-bases Skill description
- [[summaries/obsidian-cli-command-reference]] — Base-related CLI commands
